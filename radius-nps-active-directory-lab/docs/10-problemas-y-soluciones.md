# 10 – Problemas, hallazgos y pendientes

Resultado de revisar los archivos entregados. **No se modificó ninguna configuración**; las acciones son recomendaciones.

## Hallazgos

| ID | Severidad | Estado | Hallazgo | Acción recomendada |
|---|---|---|---|---|
| H1 | Alta | ✅ Resuelto | SW: SSH estaba deshabilitado por falta de claves RSA. Ahora `show ip ssh` indica *SSH Enabled* y hay sesiones SSH con `usr-nivel0` y `usr-nivel10`. | — |
| H2 | Media | ✅ Resuelto | R1 no tenía `enable secret`. El `running-config` actual sí lo incluye. | — |
| H3 | Media | ✅ Resuelto | SW: `line aux 0` sin configuración. Ahora usa `LOGIN-NPS`, `EXEC-NPS` y `ACCT-NPS`. | — |
| H4 | Decisión | ⏳ Abierto | VTY también usa NPS en R1 y SW. El requisito dice «solo consola y auxiliar», pero exige SSH (que usa VTY) y las pruebas SSH usaron NPS. | Documentar la interpretación elegida en el README. |
| H5 | Baja | ✅ Resuelto | `login block-for` faltaba en R1. Ahora está en ambos equipos. | — |
| H6 | Baja | Abierto | Diferencia de 1 h entre el servidor y los equipos (UTC) al correlacionar logs. | Alinear zona horaria o configurar NTP. |
| H7 | Info | Abierto | Claves RADIUS en tipo 7 (reversible) y hashes `secret 5` en los equipos. Aquí están redactados. | No compartir configuraciones sin sanitizar; rotar claves si ya se compartieron. |
| H8 | Info | Abierto | El direccionamiento 20.25.6.0/24 no pertenece a RFC 1918. Es inocuo en un laboratorio aislado. | Valorar un rango privado si el entorno llegara a conectarse a otras redes. |
| H9 | Info | Abierto | Los eventos 6273 (4:41:08 y 4:43:44) no tienen detalle capturado. | Abrir y capturar el campo «Motivo». |
| H10 | Media | Abierto | *Accounting* con **12 timeouts, 8 retransmisiones y 4 fallos** idénticos en R1 y SW. En el servidor existe un filtro de puerto UDP 1813 ([Fig. 36](../images/servidor/firewall-puerto-udp-1813.png)), pero no se verificó que su regla esté habilitada. | Comprobar la regla (`Get-NetFirewallPortFilter -Protocol UDP \| Where-Object LocalPort -match '1813' \| Get-NetFirewallRule \| Format-List DisplayName,Enabled,Direction,Action`) y repetir `show aaa servers` tras nuevas pruebas. |
| H11 | Baja | Abierto | Las salidas de `show logging` no incluyen éxitos que sí aparecen en otras capturas (R1: 03:42:29 y 03:44:07; SW: `usr-nivel10`). | Capturar `show logging` completo justo después de las pruebas. |
| H12 | Info | Abierto | Cualquier usuario de nivel 0, 5 o 10 puede ejecutar `enable`; solo el `enable secret` impide llegar al nivel 15. | Usar un `enable secret` robusto y no compartirlo. |
| H13 | Info | Abierto | `netsh nps export` exige `exportPSK=YES` y escribe los secretos sin cifrar. | No exportar ni publicar ese XML; documentar con capturas (ya hecho). |
| H14 | Baja | ✅ Resuelto | Recaptura del 29-oct-2026 de SW y R1: el contenido es idéntico al de la versión anterior; solo cambian los encabezados. | — |
| H15 | Media | Abierto | Sin evidencia directa de que las configuraciones estén **guardadas** en `startup-config`. La recaptura de R1 no incluye la línea «Last configuration change». | `copy running-config startup-config` en ambos equipos y capturar `show startup-config \| include NVRAM\|Last`. |

## Cambios detectados entre la versión 1 y la actual de los `running-config`

| Equipo | Cambio |
|---|---|
| R1 | `radius-server host …` → `radius server NPS-0697` + `aaa group server radius GRP-NPS`; listas AAA con `group GRP-NPS` |
| R1 | Añadidos `enable secret`, `login block-for 120 attempts 3 within 60` y `logging console informational` |
| R1 | Descripción `Enlace a SW-0697` en Gi1/0; cambiaron además el hash de `admin0697` y la clave RADIUS (valores redactados) |
| SW | `line aux 0` configurada con `LOGIN-NPS`, `EXEC-NPS`, `ACCT-NPS` |

Las versiones anteriores están en [`configs/router/historial/`](../configs/router/historial/) y [`configs/switch/historial/`](../configs/switch/historial/).

## Datos faltantes

| # | Dato | Dónde debe ir |
|---|---|---|
| 1 | Video Demostrativo : enlace en el README | README (inicio) |
| 2 | Scripts:  los `running-config` | [`scripts/`](../scripts/README.md) |
| 3 | Evidencia de `startup-config` en R1 y SW (H15) | `configs/` |
| 4 | SW con `usr-nivel5`: inicio de sesión visible y rechazo de `show running-config` y `configure terminal` | docs/08 |
| 5 | Pestañas «Información general» y «Restricciones» de las directivas NPS y directivas de solicitud de conexión | docs/06 |
| 6 | Ámbito de GRP-Nivel-0 y GRP-Nivel-5  | docs/06 |
| 7 | Emulador utilizado | docs/01 |
| 8 | Prueba del puerto auxiliar y del respaldo local | docs/07 |
| 9 | show logging completo y registros de *accounting* en NPS | docs/07 |
| 10 | Detalle de los eventos 6273 | docs/07 |
| 11 | Autoría y fecha para el README | README |

### Ya resueltos

Versión de Windows Server e IP del servidor · pertenencia a grupos · condiciones y atributos de las directivas NPS · SSH en el switch · `show aaa servers` · `running-config` actuales de R1 y SW · `ping` con nivel 5 · `configure terminal` con nivel 10 · sesiones SSH al switch con nivel 0 y 10 · scripts (los `running-config`, por indicación del autor) · enlace del video · ámbito de los tres grupos de AD · niveles 0, 5 y 10 en el switch · recaptura de ambos `running-config`.
