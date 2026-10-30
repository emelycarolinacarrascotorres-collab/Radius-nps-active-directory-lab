# 02 – Objetivos y alcance

## Objetivo general

Implementar y documentar un esquema de AAA centralizado en un router y un switch Cisco IOS, usando RADIUS sobre NPS integrado con Active Directory, de modo que el acceso administrativo se valide con cuentas de dominio y se autorice por niveles de privilegio (0, 5 y 10), con una cuenta local como respaldo.

## Objetivos específicos

1. Configurar el router y el switch como clientes RADIUS.
2. Crear un usuario local en cada equipo.
3. Aplicar autenticación, autorización y *accounting* mediante listas de métodos nombradas en consola, auxiliar y VTY.
4. Habilitar registros de autenticación y de la actividad AAA/RADIUS.
5. Habilitar el servicio SSH (v2) en ambos equipos.
6. Crear en Active Directory un grupo para cada nivel (0, 5 y 10).
7. Configurar NPS con los clientes RADIUS y una directiva de red por nivel.
8. Verificar el comportamiento de cada nivel y documentar la evidencia.

## Alcance

**Incluye** (con evidencia en este repositorio):

- Router `R1-0697`, switch `SW-0697` y servidor `SRV-0697` en la red 20.25.6.0/24.
- Active Directory: dominio `lab0697.local`, tres grupos y tres usuarios de prueba.
- NPS: dos clientes RADIUS y tres directivas de red.
- Pruebas por consola y SSH, eventos de NPS y contadores RADIUS.

**No se documenta** (no hay evidencia en los materiales entregados): scripts de automatización adicionales (según el autor, los scripts del laboratorio son los `running-config`; ver [scripts/](../scripts/README.md)), exportación de la configuración de NPS (ver [07](07-configuracion-nps.md#exportación-de-la-configuración)), redundancia de servidores RADIUS, ni la prueba del puerto auxiliar y del respaldo local.

## Aclaración sobre el requisito «solo consola y auxiliar»

El enunciado pide limitar la autenticación y autorización a consola y auxiliar, y también pide el servicio SSH (que usa las líneas VTY). En la configuración real, **consola, auxiliar y VTY** usan las mismas listas con NPS. Esta diferencia se registra como [H4](10-problemas-y-soluciones.md) y requiere que el autor indique la interpretación correcta.
