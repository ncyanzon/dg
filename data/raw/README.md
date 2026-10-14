# Datos originales (raw)

Estos archivos NO se modifican. Toda limpieza se hace en los notebooks
y el resultado se guarda en data/clean.

Los CSV quedan solo en la máquina local: están excluidos de GitHub
mediante `.gitignore`. Para reproducir el análisis, descargalos desde
el link de la fuente y guardalos en esta carpeta con estos nombres.

## Fuente
- Dataset: Producción de petróleo y gas por pozo (Capítulo IV)
- Publicado por: Secretaría de Energía de la Nación
- Link: http://datos.energia.gob.ar/dataset/produccion-de-petroleo-y-gas-por-pozo
- Link alternativo: https://datos.gob.ar/ar/dataset/energia-produccion-petroleo-gas-por-pozo-capitulo-iv
- Fecha de descarga: 23/09/2026

## Archivos
| Archivo | Descargado | Tamaño | Uso |
| --- | --- | --- | --- |
| capitulo-iv-pozos.csv | 23/09/2026 | 34,1 MB | Maestro de pozos (notebooks 01 y 02) |
| produccin-de-pozos-de-gas-y-petrleo-2024.csv | 13/10/2026 | 319,9 MB | Producción 2024 (notebook 03 en adelante) |
| produccin-de-pozos-de-gas-y-petrleo-2025.csv | 13/10/2026 | 327,9 MB | Producción 2025 (notebook 03 en adelante) |
| produccin-de-pozos-de-gas-y-petrleo-2026.csv | 23/09/2026 | 211,9 MB | Producción 2026 (notebook 03 en adelante) |
| produccin-de-pozos-de-gas-y-petrleo-no-convencional.csv | 23/09/2026 | 147,1 MB | No se usa: sus filas 2024–2026 ya están en los archivos anuales |

Período de análisis de la producción: 2024–2026.

Salvedad: el archivo 2026 se descargó antes que los de 2024 y 2025. Si la
fuente corrigió algún mes de 2026 después del 23/09/2026, esa corrección
no está incluida.

## Archivos de práctica
Usados para entrenar la carga y la limpieza de datos.
- Fuente: http://datos.energia.gob.ar/dataset/produccion-de-petroleo-y-gas-por-pozo
- produccion_energia.csv — descargado el 07/09/2026 (145 MB)
- pronostico_produccion.csv — descargado el 14/09/2026 (1,8 MB)

## Unidades
- Petróleo: m3
- Gas: miles de m3
