# 09 – Resultados

Se resumen **solo** los resultados demostrados por las evidencias. El detalle y las capturas están en [08 – Pruebas y validación](08-pruebas-y-validacion.md).

## Resultados demostrados

| Área | Resultado | Evidencia |
|---|---|---|
| Router – niveles | `usr-nivel0`, `usr-nivel5` y `usr-nivel10` obtienen nivel 0, 5 y 10 (`show privilege`) por consola | [Nivel 0](../images/router/consola-r1-usr-nivel0.png) · [Nivel 5](../images/router/consola-r1-usr-nivel5.png) · [Nivel 10](../images/router/consola-r1-usr-nivel10.png) |
| Router – restricción de comandos | Nivel 0: sin `ping` ni `show running-config`. Nivel 5: `ping` correcto (4/5), sin `show running-config` ni `configure terminal`. Nivel 10: `configure terminal` y `show running-config` reducido; sin `reload` ni `debug` | Figuras anteriores, [ping](../images/router/ssh-r1-usr-nivel5-ping.png) y [config](../images/router/ssh-r1-usr-nivel10-config-y-show-run.png) |
| Router – SSH | `show ip ssh`: habilitado v2.0; sesiones PuTTY con los tres usuarios | [`show ip ssh`](../evidence/ssh/show-ip-ssh-r1-0697.txt) · [PuTTY nivel 0](../images/router/ssh-putty-r1-usr-nivel0.png) |
| Switch – SSH | Deshabilitado antes de generar claves RSA; habilitado después | [Antes](../evidence/ssh/show-ip-ssh-sw-0697-antes.txt) · [Después](../evidence/ssh/show-ip-ssh-sw-0697-despues.txt) |
| Switch – niveles | Nivel 0: `ping` y `show run` rechazados. Nivel 5: `show privilege` 5 y `ping` correcto. Nivel 10: `ping`, `configure terminal` y `show running-config` reducido | [Nivel 0](../images/switch/ssh-sw-usr-nivel0-login-y-ping-rechazado.png) · [Nivel 5](../images/switch/sw-nivel5-show-privilege-y-ping.png) · [Nivel 10](../images/switch/sw-nivel10-ping-show-run-y-config-t.png) |
| RADIUS en los equipos | Servidor 20.25.6.97 *UP* en R1 y SW; autenticaciones aceptadas (R1: 9, SW: 2) | [R1](../evidence/radius-logs/show-logging-y-aaa-servers-r1-0697.txt) · [SW](../evidence/radius-logs/show-logging-y-aaa-servers-sw-0697.txt) |
| NPS – auditoría | Eventos 6272 («acceso concedido») para los tres usuarios | [Nivel 0](../images/nps/nps-evento-6272-usr-nivel0.png) · [Nivel 5](../images/nps/nps-evento-6272-usr-nivel5.png) · [Nivel 10](../images/nps/nps-evento-6272-usr-nivel10.png) |
| NPS – directivas | Cada directiva exige un grupo de AD y envía `Cisco-AV-Pair = shell:priv-lvl=N` | [Directivas](07-configuracion-nps.md#directivas-de-red) |
| Active Directory | Tres grupos `Global`/`Security`, cada uno con su usuario | [Membresía](../images/active-directory/ad-miembros-de-grupos.png) · [Ámbito](../images/active-directory/ad-ambito-de-los-grupos.png) |

## Resultados no demostrados o con reservas

- **Switch, nivel 5:** solo `show privilege` y `ping`; el inicio de sesión no es visible y no se probó el rechazo de `show running-config` ni de `configure terminal`.
- **Puerto auxiliar** y **respaldo local** con NPS detenido: sin prueba. Los fallos de `admin0697` en R1 con NPS activo son coherentes con el comportamiento esperado de IOS, pero no prueban el respaldo.
- **Accounting:** R1 y SW muestran 12 timeouts, 8 retransmisiones y 4 transacciones fallidas ([H10](10-problemas-y-soluciones.md)); existe un filtro de puerto UDP 1813 en el servidor, pero no se verificó que su regla esté habilitada.
- **Registros en los equipos:** las salidas de `show logging` están incompletas ([H11](10-problemas-y-soluciones.md)); no hay registros de autorización separados (`Author request 0`).
- **Configuración guardada** (`startup-config`): sin evidencia ([H15](10-problemas-y-soluciones.md)).
