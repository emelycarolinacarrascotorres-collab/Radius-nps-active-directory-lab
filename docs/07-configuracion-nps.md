# 07 – Configuración de NPS y autenticación RADIUS

El servidor `SRV-0697` ejecuta el rol **Servicios de acceso y directivas de redes (NPAS/NPS)**, visible en el Administrador del servidor de las capturas de PuTTY.

## Servidor

![Configuración IP del servidor](../images/servidor/srv-ipconfig-y-version.png)

| Dato | Valor |
|---|---|
| Hostname / sufijo DNS | `SRV-0697` / `lab0697.local` |
| Sistema operativo | Windows Server 2019 Standard Evaluation (10.0.17763) |
| Adaptador | `Ethernet0 2` – Intel(R) PRO/1000 MT |
| IPv4 | 20.25.6.97 / 255.255.255.0, DHCP deshabilitado |
| Gateway / DNS | 20.25.6.1 / 20.25.6.97 |

## Clientes RADIUS

![Clientes RADIUS en NPS](../images/nps/nps-clientes-radius.png)

| Nombre | IP | Fabricante | Estado |
|---|---|---|---|
| R1-0697 | 20.25.6.1 | RADIUS Standard | Habilitada |
| SW-0697 | 20.25.6.2 | RADIUS Standard | Habilitada |

Puertos usados por los equipos: **1812** (autenticación) y **1813** (*accounting*). El *shared secret* no se publica.

## Directivas de red

![Directivas de red en NPS](../images/nps/nps-directivas-de-red.png)

| Orden | Directiva | Estado | Condición | Atributo estándar | Atributo específico del proveedor |
|---|---|---|---|---|---|
| 1 | `POL-Nivel-10` | Habilitada | Grupos de Windows = `LAB0697\GRP-Nivel-10` | `Service-Type` = `Login` | `Cisco-AV-Pair` = `shell:priv-lvl=10` |
| 2 | `POL-Nivel-5` | Habilitada | Grupos de Windows = `LAB0697\GRP-Nivel-5` | `Service-Type` = `Login` | `Cisco-AV-Pair` = `shell:priv-lvl=5` |
| 3 | `POL-Nivel-0` | Habilitada | Grupos de Windows = `LAB0697\GRP-Nivel-0` | `Service-Type` = `Login` | `Cisco-AV-Pair` = `shell:priv-lvl=0` |

Así se entrega el nivel de privilegio: cada directiva se activa por pertenencia a grupo y envía al equipo el atributo `Cisco-AV-Pair` con el nivel correspondiente. Si un usuario perteneciera a varios grupos, NPS aplicaría la primera directiva que coincida según el orden (10 → 5 → 0).

### POL-Nivel-10

| Condiciones | Atributo estándar | Cisco-AV-Pair |
|---|---|---|
| ![](../images/nps/nps-pol-nivel-10-condiciones.png) | ![](../images/nps/nps-pol-nivel-10-service-type.png) | ![](../images/nps/nps-pol-nivel-10-cisco-av-pair.png) |

### POL-Nivel-5

| Condiciones | Atributo estándar | Cisco-AV-Pair |
|---|---|---|
| ![](../images/nps/nps-pol-nivel-5-condiciones.png) | ![](../images/nps/nps-pol-nivel-5-service-type.png) | ![](../images/nps/nps-pol-nivel-5-cisco-av-pair.png) |

### POL-Nivel-0

| Condiciones | Atributo estándar | Cisco-AV-Pair |
|---|---|---|
| ![](../images/nps/nps-pol-nivel-0-condiciones.png) | ![](../images/nps/nps-pol-nivel-0-service-type.png) | ![](../images/nps/nps-pol-nivel-0-cisco-av-pair.png) |

> **No capturado:** las pestañas «Información general» (tipo de permiso de acceso) y «Restricciones» (métodos de autenticación) de cada directiva, y las directivas de solicitud de conexión. Ver [docs/10](10-problemas-y-soluciones.md#datos-faltantes).

## Flujo AAA

```mermaid
sequenceDiagram
    autonumber
    actor Admin as Administrador usr-nivelX
    participant Dev as R1-0697 / SW-0697 (cliente RADIUS)
    participant NPS as SRV-0697 NPS (UDP 1812 y 1813)
    participant AD as Active Directory lab0697.local
    Admin->>Dev: Inicio de sesión (consola o SSH)
    Dev->>NPS: Access-Request (lista LOGIN-NPS)
    NPS->>AD: Valida credenciales y grupo
    AD-->>NPS: Resultado
    alt Válido y grupo con directiva POL-Nivel-X
        NPS-->>Dev: Access-Accept con Cisco-AV-Pair priv-lvl=X
    else Rechazo
        NPS-->>Dev: Access-Reject
    end
    Dev-->>Admin: Sesión EXEC nivel 0, 5 o 10 / fallo de autenticación
    Dev->>NPS: Accounting start-stop (ACCT-NPS)
```

*Diagrama conceptual basado en configuraciones y capturas.*

## Registros de auditoría de NPS

NPS registra en el Visor de eventos (Seguridad) los eventos **6272** (acceso concedido) y **6273** (acceso denegado). Las evidencias de 6272 para los tres usuarios están en [08](08-pruebas-y-validacion.md#3-eventos-de-nps). Los contadores RADIUS de los equipos están en [08](08-pruebas-y-validacion.md#7-contadores-radius-show-aaa-servers).

