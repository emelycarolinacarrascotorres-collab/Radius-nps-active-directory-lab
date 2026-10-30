# Configuraciones

| Archivo | Contenido |
|---|---|
| [`router/running-config.txt`](router/running-config.txt) | `show running-config` de `R1-0697`, versión actual (sanitizada) |
| [`router/historial/running-config_v1-inicial.txt`](router/historial/running-config_v1-inicial.txt) | Versión inicial, previa a las correcciones |
| [`switch/running-config.txt`](switch/running-config.txt) | `show running-config` de `SW-0697`, versión actual (sanitizada) |
| [`switch/historial/running-config_v1-inicial.txt`](switch/historial/running-config_v1-inicial.txt) | Versión inicial, previa a las correcciones |
| [`server/README.md`](server/README.md) | Explica por qué no se exporta la configuración del servidor |

## Sanitización

Son copias de los archivos originales con **solo** estas sustituciones:

| Original | Marcador |
|---|---|
| `secret 5 <hash>` (usuario local y `enable secret`) | `<HASH_SECRET_REDACTADO>` |
| `key 7 <clave>` (clave compartida RADIUS) | `<RADIUS_SHARED_SECRET_REDACTADO>` |

Se añade un encabezado de comentarios (`!`) que lo indica. Los originales sin sanitizar **no** forman parte del repositorio público; el autor los conserva.

