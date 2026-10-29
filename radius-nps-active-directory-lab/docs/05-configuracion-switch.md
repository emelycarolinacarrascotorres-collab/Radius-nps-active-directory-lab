# 05 – Configuración del switch SW-0697

Fuente: [`configs/switch/running-config.txt`](../configs/switch/running-config.txt) (sanitizado) y [`show ip ssh` antes](../evidence/ssh/show-ip-ssh-sw-0697-antes.txt) y [después](../evidence/ssh/show-ip-ssh-sw-0697-despues.txt).

> La versión inicial está en [`configs/switch/historial/`](../configs/switch/historial/). El archivo actual es la recaptura final del 29-oct-2026 y su contenido es idéntico al del 28-oct.

| Dato | Valor |
|---|---|
| Hostname / dominio | `SW-0697` / `lab0697.local` |
| Versión IOS | 15.2 |
| SVI | Vlan97 – 20.25.6.2/24, `ip default-gateway 20.25.6.1` |
| Último cambio de configuración (archivo) | 05:06:08 UTC, jue 29-oct-2026 (sin usuario indicado) |

## 1. Usuario local y enable

```text
enable secret 5 <HASH_SECRET_REDACTADO>
username admin0697 privilege 15 secret 5 <HASH_SECRET_REDACTADO>
```

## 2. AAA y RADIUS

Igual que el router (desde su última versión), el switch usa un **grupo de servidores RADIUS nombrado**.

```text
aaa group server radius GRP-NPS
 server name NPS-0697
 ip radius source-interface Vlan97
!
radius server NPS-0697
 address ipv4 20.25.6.97 auth-port 1812 acct-port 1813
 timeout 3
 retransmit 2
 key 7 <RADIUS_SHARED_SECRET_REDACTADO>
```

| Función | Lista | Métodos |
|---|---|---|
| Autenticación login | `default` | `local` |
| Autenticación login | `LOGIN-NPS` | `group GRP-NPS` → `local` |
| Autenticación enable | `default` | `enable` |
| Autorización | consola | habilitada |
| Autorización exec | `default` / `EXEC-NPS` | `local` / `group GRP-NPS` → `local` |
| Accounting exec | `ACCT-NPS` | `start-stop group GRP-NPS` |
| Accounting connection / system | `default` | `start-stop group GRP-NPS` |

El origen RADIUS es `Vlan97` (20.25.6.2), coincidente con el cliente `SW-0697` en NPS ([captura](../images/nps/nps-clientes-radius.png)).

## 3. Líneas de acceso

| Línea | Configuración |
|---|---|
| `con 0` | `LOGIN-NPS`, `EXEC-NPS`, `ACCT-NPS`, `exec-timeout 5 0`, `logging synchronous` |
| `aux 0` | `LOGIN-NPS`, `EXEC-NPS`, `ACCT-NPS`, `exec-timeout 5 0`, `logging synchronous` (**corregido**: antes estaba sin configurar) |
| `vty 0 4` y `vty 5 15` | `LOGIN-NPS`, `EXEC-NPS`, `ACCT-NPS`, `exec-timeout 5 0`, `transport input ssh` |

## 4. SSH

Configurado:

```text
ip domain-name lab0697.local
ip ssh version 2
ip ssh time-out 60
ip ssh server algorithm encryption aes128-ctr aes192-ctr aes256-ctr
ip ssh client algorithm encryption aes128-ctr aes192-ctr aes256-ctr
```

**Estado según `show ip ssh`:**

| Momento | Resultado |
|---|---|
| Antes | `SSH Disabled - version 2.0`, `%Please create RSA keys…`, `IOS Keys … NONE` |
| Después | `SSH Enabled - version 2.0`, clave `ssh-rsa` del host `SW-0697.lab0697.local` |

> ✅ Tras generar las claves RSA, el servicio SSH quedó **habilitado** y hay sesiones SSH a `20.25.6.2` con `usr-nivel0` y `usr-nivel10` ([08](08-pruebas-y-validacion.md#6-switch-sw-0697)). Las claves RSA no aparecen en el `running-config`.

## 5. Registros y protección de acceso

```text
logging buffered 64000 informational
logging console informational
login block-for 120 attempts 3 within 60
login on-failure log
login on-success log
service timestamps log datetime msec
```

`login block-for` (bloqueo de 120 s tras 3 fallos en 60 s) está presente en el switch y **no** en el router.

## 6. Niveles de privilegio

Mismos niveles que el router, con comandos propios de un switch:

| Nivel | Comandos definidos |
|---|---|
| 0 | `show`, `show privilege` |
| 5 | `ping`, `traceroute`, `show ip`, `show ip interface [brief]`, `show mac [address-table]`, `show vlan`, `show version`, `show interfaces` |
| 10 | `configure [terminal]`, `show running-config`, `show logging`; modo `interface` y, dentro, `shutdown`, `switchport`, `description` |

## 7. Servicios deshabilitados

`no ip http server`, `no ip http secure-server`, `no ip domain-lookup`.

## Pruebas

- SSH con `usr-nivel0` (nivel 0; `ping` y `show run` rechazados), nivel 5 (`show privilege` y `ping`) y `usr-nivel10` (`ping`, `configure terminal` y `show running-config` reducido).
- Evidencia de consola con `usr-nivel10` y contadores RADIUS (`show aaa servers`).
- **Falta** el rechazo de `show running-config` y `configure terminal` con el nivel 5. Ver [08](08-pruebas-y-validacion.md#6-switch-sw-0697) y [§10](08-pruebas-y-validacion.md#10-pruebas-no-evidenciadas).
