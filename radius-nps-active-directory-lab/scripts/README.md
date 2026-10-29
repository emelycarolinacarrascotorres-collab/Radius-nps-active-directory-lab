# Scripts

## Estado

Por indicación del autor, **los scripts del laboratorio son los archivos de configuración (`running-config`) del router y del switch**. No se entregaron otros scripts (por ejemplo, de PowerShell para el servidor).

| Equipo | Archivo | Versión |
|---|---|---|
| Router `R1-0697` | [`configs/router/running-config.txt`](../configs/router/running-config.txt) | Actual |
| Router `R1-0697` | [`configs/router/historial/running-config_v1-inicial.txt`](../configs/router/historial/running-config_v1-inicial.txt) | Inicial |
| Switch `SW-0697` | [`configs/switch/running-config.txt`](../configs/switch/running-config.txt) | Actual |
| Switch `SW-0697` | [`configs/switch/historial/running-config_v1-inicial.txt`](../configs/switch/historial/running-config_v1-inicial.txt) | Inicial |

Los archivos no se duplican: se mantienen en `configs/`.

## Qué contienen y qué precauciones tomar

- Son la salida de `show running-config`: describen el **estado resultante** de cada equipo, no el orden en que se ejecutaron los comandos.
- Son copias **sanitizadas**: los hashes y la clave compartida RADIUS están sustituidos por `<HASH_SECRET_REDACTADO>` y `<RADIUS_SHARED_SECRET_REDACTADO>`. Para reutilizarlos hay que reemplazar esos marcadores por valores propios.
- Incluyen líneas de la salida del comando (`Building configuration…`, `Current configuration…`) que no son comandos de configuración.
- Las claves RSA de SSH no aparecen en el `running-config`; su evidencia está en [`evidence/ssh/`](../evidence/ssh/).
- La configuración del servidor (Active Directory y NPS) se documenta con capturas: ver [`configs/server/README.md`](../configs/server/README.md).
