# 12 – Estado del proyecto e inventario

## Verificación final

| # | Requisito | Estado | Justificación |
|---|---|---|---|
| 1 | Existe un `README.md` profesional | COMPLETADO | [README](../README.md) con todas las secciones solicitadas |
| 2 | El video aparece al principio del README | COMPLETADO | Enlace de YouTube con miniatura al inicio del README. Solo se comprobaron título, canal y fecha; no se reprodujo ni se verificó su contenido |
| 3 | El propósito está explicado | COMPLETADO | [01](01-introduccion.md) y README |
| 4 | La documentación está organizada | COMPLETADO | Documentos 01–12 en `docs/` |
| 5 | Se incluyen las capturas disponibles | COMPLETADO | 36 capturas incluidas; 3 excluidas con motivo (ver «Material no incluido») |
| 6 | Se incluyen los diagramas disponibles | COMPLETADO | Topología original y 3 diagramas Mermaid conceptuales |
| 7 | La topología original se conserva | COMPLETADO | [`diagrams/topologia-original.png`](../diagrams/topologia-original.png), sin modificar |
| 8 | Los scripts utilizados están incluidos | COMPLETADO | Por indicación del autor, los scripts son los `running-config` de R1 y SW ([scripts/README.md](../scripts/README.md)); no se entregaron otros |
| 9 | Los running-configs del router y del switch están incluidos | COMPLETADO | Versión inicial y recaptura final del 29-oct-2026, sanitizadas |
| 10 | Se documentan AD, grupos 0/5/10 y NPS | COMPLETADO | [06](06-active-directory.md) y [07](07-configuracion-nps.md); faltan pestañas «Restricciones» e «Información general» |
| 11 | Se documentan autenticación, autorización y RADIUS según las evidencias | PARCIALMENTE COMPLETADO | Router completo; switch con niveles 0, 5 y 10 (nivel 5 sin restricciones probadas); *accounting* con timeouts; aux y respaldo local sin prueba |
| 12 | Los enlaces internos funcionan | COMPLETADO | Rutas y anclas verificadas con un script antes de empaquetar |
| 13 | Las imágenes se muestran en GitHub | PARCIALMENTE COMPLETADO | Rutas relativas verificadas; el renderizado en GitHub debe comprobarse tras subirlo |
| 14 | No hay secretos expuestos | COMPLETADO | Hashes y claves RADIUS redactados; búsqueda automática sin coincidencias. Solo hay claves **públicas** de host SSH |
| 15 | Limitaciones y pendientes identificados | COMPLETADO | [10](10-problemas-y-soluciones.md) |
| 16 | Las conclusiones corresponden a los resultados | COMPLETADO | [11](11-conclusiones.md) se basa en [09](09-resultados.md) |

## Aclaraciones necesarias del autor

1. **VTY (H4):** el enunciado limita AAA a consola y auxiliar, pero las líneas VTY (SSH) también usan NPS. ¿Cuál es la interpretación correcta?
2. **Scripts:** el autor indicó que los scripts son los `running-config`. Si existiera algún otro (por ejemplo, de PowerShell para el servidor), debe entregarse.
3. **`running-config` originales:** ¿se publican sanitizados (actual) o se entregan los originales por otra vía?
4. **Licencia:** no se añade ninguna; si se desea, debe decidirla el autor (es una entrega académica).
5. **Autoría, institución, asignatura, fecha y emulador:** marcados como `[INFORMACIÓN PENDIENTE]`. El canal del video figura como «Emely Carrasco»; el autor debe confirmar cómo desea consignar su nombre.
6. **Video:** confirmar que es público o «no listado» y que su contenido coincide con el README.

## Inventario de materiales

| Fig. | Archivo en el repositorio | Archivo original | Componente | Contenido | Observaciones |
|---:|---|---|---|---|---|
| 1 | [`diagrams/topologia-original.png`](../diagrams/topologia-original.png) | `Captura_de_pantalla_2026-10-28_000054.png` | Topología | Topología original R1 – SW – WINDOWSSERVER |  |
| 2 | [`images/active-directory/ad-usuarios-y-grupos.png`](../images/active-directory/ad-usuarios-y-grupos.png) | `Captura_de_pantalla_2026-10-27_234801.png` | AD | OU `Admin-Red`: 3 grupos y 3 usuarios |  |
| 3 | [`images/nps/nps-clientes-radius.png`](../images/nps/nps-clientes-radius.png) | `Captura_de_pantalla_2026-10-27_234821.png` | NPS | Clientes RADIUS R1-0697 y SW-0697 |  |
| 4 | [`images/nps/nps-directivas-de-red.png`](../images/nps/nps-directivas-de-red.png) | `Captura_de_pantalla_2026-10-27_234840.png` | NPS | Lista de directivas de red y orden | Paneles inferiores vacíos |
| 5 | [`images/router/consola-r1-usr-nivel0.png`](../images/router/consola-r1-usr-nivel0.png) | `Captura_de_pantalla_2026-10-27_234208.png` | Router | Consola R1, nivel 0 | Incluye un intento fallido |
| 6 | [`images/router/consola-r1-usr-nivel5.png`](../images/router/consola-r1-usr-nivel5.png) | `Captura_de_pantalla_2026-10-27_234317.png` | Router | Consola R1, nivel 5 | Listado de `?` truncado |
| 7 | [`images/router/consola-r1-usr-nivel10.png`](../images/router/consola-r1-usr-nivel10.png) | `Captura_de_pantalla_2026-10-27_234457.png` | Router | Consola R1, nivel 10 | Parte superior recortada |
| 8 | [`images/router/ssh-putty-r1-usr-nivel0.png`](../images/router/ssh-putty-r1-usr-nivel0.png) | `Captura_de_pantalla_2026-10-27_235013.png` | Router | PuTTY → R1, inicio de sesión nivel 0 | Sin comandos |
| 9 | [`images/router/ssh-putty-r1-usr-nivel5.png`](../images/router/ssh-putty-r1-usr-nivel5.png) | `Captura_de_pantalla_2026-10-27_235049.png` | Router | PuTTY → R1, inicio de sesión nivel 5 | Sin comandos |
| 10 | [`images/router/ssh-putty-r1-usr-nivel10.png`](../images/router/ssh-putty-r1-usr-nivel10.png) | `Captura_de_pantalla_2026-10-27_235121.png` | Router | PuTTY → R1, inicio de sesión nivel 10 | Sin comandos |
| 11 | [`images/nps/nps-evento-6272-usr-nivel0.png`](../images/nps/nps-evento-6272-usr-nivel0.png) | `Captura_de_pantalla_2026-10-27_234723.png` | NPS | Evento 6272 de `usr-nivel0` | Hora del servidor +1 h |
| 12 | [`images/nps/nps-evento-6272-usr-nivel5.png`](../images/nps/nps-evento-6272-usr-nivel5.png) | `Captura_de_pantalla_2026-10-27_234706.png` | NPS | Evento 6272 de `usr-nivel5` |  |
| 13 | [`images/nps/nps-evento-6272-usr-nivel10.png`](../images/nps/nps-evento-6272-usr-nivel10.png) | `Captura_de_pantalla_2026-10-27_234651.png` | NPS | Evento 6272 de `usr-nivel10` |  |
| 14 | [`images/active-directory/ad-miembros-de-grupos.png`](../images/active-directory/ad-miembros-de-grupos.png) | `Captura_de_pantalla_2026-10-28_002156.png` | AD | `Get-ADGroupMember` y `Get-ADGroup` | Ámbito solo de `GRP-Nivel-10` |
| 15 | [`images/servidor/srv-ipconfig-y-version.png`](../images/servidor/srv-ipconfig-y-version.png) | `Captura_de_pantalla_2026-10-28_002202.png` | Servidor | `ipconfig /all` y `Get-ComputerInfo` | Contiene MAC y DUID de la VM |
| 16 | [`images/nps/nps-pol-nivel-10-condiciones.png`](../images/nps/nps-pol-nivel-10-condiciones.png) | `Captura_de_pantalla_2026-10-28_002244.png` | NPS | POL-Nivel-10: condición de grupo |  |
| 17 | [`images/nps/nps-pol-nivel-10-service-type.png`](../images/nps/nps-pol-nivel-10-service-type.png) | `Captura_de_pantalla_2026-10-28_002252.png` | NPS | POL-Nivel-10: `Service-Type` |  |
| 18 | [`images/nps/nps-pol-nivel-10-cisco-av-pair.png`](../images/nps/nps-pol-nivel-10-cisco-av-pair.png) | `Captura_de_pantalla_2026-10-28_002257.png` | NPS | POL-Nivel-10: `Cisco-AV-Pair` |  |
| 19 | [`images/nps/nps-pol-nivel-5-condiciones.png`](../images/nps/nps-pol-nivel-5-condiciones.png) | `Captura_de_pantalla_2026-10-28_002307.png` | NPS | POL-Nivel-5: condición de grupo |  |
| 20 | [`images/nps/nps-pol-nivel-5-service-type.png`](../images/nps/nps-pol-nivel-5-service-type.png) | `Captura_de_pantalla_2026-10-28_002314.png` | NPS | POL-Nivel-5: `Service-Type` |  |
| 21 | [`images/nps/nps-pol-nivel-5-cisco-av-pair.png`](../images/nps/nps-pol-nivel-5-cisco-av-pair.png) | `Captura_de_pantalla_2026-10-28_002320.png` | NPS | POL-Nivel-5: `Cisco-AV-Pair` |  |
| 22 | [`images/nps/nps-pol-nivel-0-condiciones.png`](../images/nps/nps-pol-nivel-0-condiciones.png) | `Captura_de_pantalla_2026-10-28_002329.png` | NPS | POL-Nivel-0: condición de grupo |  |
| 23 | [`images/nps/nps-pol-nivel-0-service-type.png`](../images/nps/nps-pol-nivel-0-service-type.png) | `Captura_de_pantalla_2026-10-28_002335.png` | NPS | POL-Nivel-0: `Service-Type` |  |
| 24 | [`images/nps/nps-pol-nivel-0-cisco-av-pair.png`](../images/nps/nps-pol-nivel-0-cisco-av-pair.png) | `Captura_de_pantalla_2026-10-28_002344.png` | NPS | POL-Nivel-0: `Cisco-AV-Pair` |  |
| 25 | [`images/switch/ssh-sw-usr-nivel0-show-privilege.png`](../images/switch/ssh-sw-usr-nivel0-show-privilege.png) | `Captura_de_pantalla_2026-10-28_012318.png` | Switch | SSH → SW, `usr-nivel0`, `show privilege` |  |
| 26 | [`images/switch/ssh-sw-usr-nivel10-configure-terminal.png`](../images/switch/ssh-sw-usr-nivel10-configure-terminal.png) | `Captura_de_pantalla_2026-10-28_012955.png` | Switch | SSH → SW, `usr-nivel10`, `configure terminal` |  |
| 27 | [`images/switch/sw-usr-nivel10-show-running-config.png`](../images/switch/sw-usr-nivel10-show-running-config.png) | `Captura_de_pantalla_2026-10-28_013006.png` | Switch | `show running-config` reducido de nivel 10 | Sin barra de título |
| 28 | [`images/router/ssh-r1-usr-nivel10-config-y-show-run.png`](../images/router/ssh-r1-usr-nivel10-config-y-show-run.png) | `Captura_de_pantalla_2026-10-28_013936.png` | Router | SSH → R1, nivel 10, `config t` y `show run` |  |
| 29 | [`images/router/ssh-r1-usr-nivel5-ping.png`](../images/router/ssh-r1-usr-nivel5-ping.png) | `Captura_de_pantalla_2026-10-28_014109.png` | Router | SSH → R1, nivel 5, `ping 20.25.6.2` |  |
| 30 | [`images/switch/ssh-sw-usr-nivel0-login-y-ping-rechazado.png`](../images/switch/ssh-sw-usr-nivel0-login-y-ping-rechazado.png) | `Captura_de_pantalla_2026-10-28_233148.png` | Switch | SSH → SW, `usr-nivel0`: `ping` rechazado | |
| 31 | [`images/switch/ssh-sw-usr-nivel0-show-run-rechazado.png`](../images/switch/ssh-sw-usr-nivel0-show-run-rechazado.png) | `Captura_de_pantalla_2026-10-28_233153.png` | Switch | `show run` rechazado y `show privilege` = 0 | Continuación de la Fig. 30 |
| 32 | [`images/switch/sw-nivel5-show-privilege-y-ping.png`](../images/switch/sw-nivel5-show-privilege-y-ping.png) | `Captura_de_pantalla_2026-10-28_233137.png` | Switch | Nivel 5: `show privilege` y `ping` | Login y barra de título no visibles |
| 33 | [`images/switch/ssh-sw-usr-nivel10-login-con-primer-intento-denegado.png`](../images/switch/ssh-sw-usr-nivel10-login-con-primer-intento-denegado.png) | `Captura_de_pantalla_2026-10-28_233336.png` | Switch | SSH → SW, `usr-nivel10`: inicio de sesión | Primer intento *Access denied* |
| 34 | [`images/switch/sw-nivel10-ping-show-run-y-config-t.png`](../images/switch/sw-nivel10-ping-show-run-y-config-t.png) | `Captura_de_pantalla_2026-10-28_233350.png` | Switch | Nivel 10: `ping`, `show run` reducido y `config t` | Sin barra de título |
| 35 | [`images/active-directory/ad-ambito-de-los-grupos.png`](../images/active-directory/ad-ambito-de-los-grupos.png) | `1793251873786_image.png` | AD | `Get-ADGroup` de los tres grupos | |
| 36 | [`images/servidor/firewall-puerto-udp-1813.png`](../images/servidor/firewall-puerto-udp-1813.png) | `1793251895964_image.png` | Servidor | Filtro de puerto UDP 1813 | No muestra si la regla está habilitada |

### Archivos de texto

| Archivo en el repositorio | Archivo original | Contenido | Observaciones |
|---|---|---|---|
| [`configs/router/running-config.txt`](../configs/router/running-config.txt) | `show_running-config_R1-0697_907143.txt` | `running-config` final de R1 (29-oct) | Sanitizado; tratado como script ([scripts/](../scripts/README.md)) |
| [`configs/router/historial/running-config_v1-inicial.txt`](../configs/router/historial/running-config_v1-inicial.txt) | `show_running-config_R1-0697.txt` | Versión inicial de R1 | Sanitizado |
| [`configs/switch/running-config.txt`](../configs/switch/running-config.txt) | `show_running-config_SW-0697_d7be1a.txt` | `running-config` final de SW (29-oct) | Sanitizado; tratado como script |
| [`configs/switch/historial/running-config_v1-inicial.txt`](../configs/switch/historial/running-config_v1-inicial.txt) | `show_running-config_SW-0697.txt` | Versión inicial de SW | Sanitizado |
| [`evidence/ssh/show-ip-ssh-r1-0697.txt`](../evidence/ssh/show-ip-ssh-r1-0697.txt) | `show_ip_ssh_R1.txt` | SSH habilitado en R1 | Clave pública de host |
| [`evidence/ssh/show-ip-ssh-sw-0697-antes.txt`](../evidence/ssh/show-ip-ssh-sw-0697-antes.txt) | `show_ip_ssh_sw1.txt` | SSH deshabilitado en SW | — |
| [`evidence/ssh/show-ip-ssh-sw-0697-despues.txt`](../evidence/ssh/show-ip-ssh-sw-0697-despues.txt) | `show_ip_ssh_sw1_1.txt` | SSH habilitado en SW | Clave pública de host |
| [`evidence/radius-logs/show-logging-y-aaa-servers-r1-0697.txt`](../evidence/radius-logs/show-logging-y-aaa-servers-r1-0697.txt) | `show_logging__include_SEC_LOGIN_r1.txt` | `SEC_LOGIN` y `show aaa servers` de R1 | Salida incompleta (H11) |
| [`evidence/radius-logs/show-logging-y-aaa-servers-sw-0697.txt`](../evidence/radius-logs/show-logging-y-aaa-servers-sw-0697.txt) | `show_logging__include_SEC_LOGIN_sw.txt` | Ídem para SW | Salida incompleta (H11) |

### Material no incluido

| Archivo original | Motivo |
|---|---|
| `Captura_de_pantalla_2026-10-28_002230.png` | Muestra el error de `netsh nps export`; no aporta evidencia del laboratorio (ver [07](07-configuracion-nps.md#exportación-de-la-configuración)) |
| `Captura_de_pantalla_2026-10-28_002341.png` | Duplicado de la Fig. 24 |
| `Captura_de_pantalla_2026-10-28_233015.png` | Sesión de nivel 0 en SW redundante con las Figs. 30 y 31 (mismos comandos y resultados) |
