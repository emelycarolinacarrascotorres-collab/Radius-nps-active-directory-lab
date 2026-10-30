# Configuración del servidor

No se incluye una exportación de la configuración de NPS ni de Active Directory.

`netsh nps export` exige `exportPSK=YES` y escribe los *shared secrets* sin cifrar en el XML ([captura del error](../../docs/07-configuracion-nps.md#exportación-de-la-configuración)), por lo que no debe publicarse. La configuración se documenta con capturas:

- Active Directory: [`06-active-directory.md`](../../docs/06-active-directory.md)
- NPS y RADIUS: [`07-configuracion-nps.md`](../../docs/07-configuracion-nps.md)
- Datos del servidor (IP, versión): [captura](../../images/servidor/srv-ipconfig-y-version.png)
