# 11 – Conclusiones

Basadas exclusivamente en la evidencia disponible.

1. **Router y switch autentican y autorizan contra NPS.** Con `usr-nivel0`, `usr-nivel5` y `usr-nivel10` se obtienen los niveles 0, 5 y 10 en R1 (consola y SSH) y en SW (SSH; en el nivel 5 el inicio de sesión no es visible en la captura). NPS registra los eventos 6272 y `show aaa servers` muestra el servidor *UP* en ambos equipos.
2. **El nivel se entrega desde NPS.** Cada directiva (`POL-Nivel-10/5/0`) se activa por pertenencia al grupo de AD correspondiente y envía `Cisco-AV-Pair = shell:priv-lvl=N`.
3. **Los niveles restringen comandos.** En R1: el nivel 0 no ejecuta `ping` ni `show running-config`; el nivel 5 ejecuta `ping` pero no `show running-config` ni `configure terminal`; el nivel 10 entra a `configure terminal` y ve `show running-config` en versión reducida, pero no ejecuta `reload` ni `debug`. En SW: el nivel 0 no ejecuta `ping` ni `show run` y el nivel 10 ve una configuración reducida.
4. **Active Directory está verificado:** tres grupos Global/Security, cada uno con su usuario, y el servidor con IP 20.25.6.97/24 en Windows Server 2019.
5. **SSH funciona en ambos equipos** (`show ip ssh` y sesiones PuTTY).
6. **Las correcciones se aplicaron:** `enable secret` y `login block-for` en R1, `line aux 0` con NPS en SW y un grupo de servidores RADIUS nombrado en ambos equipos. Las recapturas finales de los `running-config` confirman que no hubo más cambios.
7. **Quedan puntos por cerrar:** las restricciones del nivel 5 en el switch, el puerto auxiliar, el respaldo local, los *timeouts* de *accounting* y la confirmación de que la configuración está guardada. Detalle en [docs/10](10-problemas-y-soluciones.md).

**Estado global:** el objetivo principal (AAA centralizado con niveles 0/5/10) está demostrado en el router y en el switch; faltan comprobaciones de detalle, no del mecanismo.
