# 01 – Introducción

## Descripción del proyecto

El laboratorio implementa **autenticación, autorización y registro (AAA) centralizados** para el acceso administrativo a equipos de red. Un router (`R1-0697`) y un switch (`SW-0697`), ambos con Cisco IOS 15.2 (imágenes IOSv), actúan como **clientes RADIUS** de un servidor Windows (`SRV-0697`, Windows Server 2019) que ejecuta **Active Directory** (dominio `lab0697.local`) y **Network Policy Server (NPS)**.

Las cuentas administrativas pertenecen a tres grupos de seguridad de Active Directory (**nivel 0, 5 y 10**). NPS identifica el grupo del usuario y entrega al equipo un nivel de privilegio, que limita los comandos disponibles. En cada equipo existe además un usuario local (`admin0697`) como respaldo.

## Problema de seguridad que aborda

Si cada equipo mantiene sus propias cuentas locales, las credenciales son difíciles de gestionar y de auditar, y todos los administradores tienden a recibir los mismos privilegios. Con AAA centralizado, las identidades se administran en Active Directory, los privilegios se asignan por grupo y los intentos de acceso quedan registrados tanto en los equipos como en el servidor (eventos 6272 y 6273 de NPS).

## Propósito del laboratorio

**Estudiar y documentar la autenticación y autorización centralizada mediante RADIUS y NPS, integrados con Active Directory, para el acceso administrativo a los dispositivos de red.**

El alcance de lo realmente demostrado se detalla en [09 – Resultados](09-resultados.md); las limitaciones, en [10 – Problemas, hallazgos y pendientes](10-problemas-y-soluciones.md).

## Tecnologías utilizadas

| Componente | Detalle | Fuente |
|---|---|---|
| Router | Cisco IOS 15.2, imagen IOSv | `running-config` y banner |
| Switch | Cisco IOS 15.2, imagen IOSv | `running-config` y banner |
| Servidor | Windows Server 2019 Standard Evaluation (10.0.17763) | [`Get-ComputerInfo`](../images/servidor/srv-ipconfig-y-version.png) |
| Roles del servidor | AD DS, DNS y NPAS (NPS) | Administrador del servidor (capturas de PuTTY) |
| Protocolos | RADIUS (UDP 1812 autenticación / 1813 *accounting*), SSH v2 | `running-config` |
| Herramientas de prueba | PuTTY, consola de los equipos, Visor de eventos, PowerShell | Capturas |
| Control de versiones | GitHub | — |
| Emulador | **[INFORMACIÓN PENDIENTE]** (la captura de topología parece de GNS3; confirmar) | — |
