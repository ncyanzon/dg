# Datos procesados (clean)

Archivos generados **solo por los notebooks**: no se editan a mano. Para regenerarlos, ejecutar el notebook indicado de principio a fin.

## capitulo-iv-pozos_limpio.csv

Maestro de pozos limpio: una fila por **pozo + formación productiva** (`idpozo`).

| Dato | Valor |
| --- | --- |
| Generado por | `notebooks/02_pozos_limpieza.ipynb` |
| Archivo de origen | `data/raw/capitulo-iv-pozos.csv` (ver `data/raw/README.md`) |
| Huella SHA-256 del origen | `44c466133c7881753d49204bebf8e0ff3d0960c92ec7d7c0c63868946fd78e87` |
| Huella SHA-256 de este archivo | `08afa03010a2f507db3b725bd4a6d866397edaec3b568f706aa3e38c19b7e760` |
| Fecha de generación | 01/10/2026 (pandas 3.0.6) |
| Filas | 85.611 (las mismas que el origen: no se eliminó ninguna) |
| Columnas | 35: las 26 originales, en el mismo orden, más 9 nuevas |
| Diccionario | `docs/diccionario_pozos.csv` (v1.5); el resultado cumple sus límites duros |

La **huella SHA-256** identifica el contenido exacto de un archivo: si cambia un solo carácter, la huella cambia.
Permite comprobar que un archivo es exactamente el que se usó o se generó.

### Columnas nuevas

| Columna | Tipo | Qué indica | Filas | Regla |
| --- | --- | --- | ---: | --- |
| `sigla_normalizada` | texto | Sigla en mayúsculas: identifica al **pozo físico** (78.299) | todas | R-14 |
| `es_multiformacion` | sí/no | El pozo físico tiene más de un registro (produce de varias formaciones) | 13.514 | R-15 |
| `posible_duplicado` | sí/no | Repite sigla y formación con otra fila: posible carga duplicada | 369 | R-16 |
| `ubicacion_compartida` | sí/no | Comparte ubicación con otro pozo físico (plataforma o locación múltiple) | 1.063 | R-17 |
| `profundidad_sospechosa` | sí/no | La profundidad original era mayor a 10.000 m; pasó a nulo | 7 | R-07 |
| `cota_sospechosa` | sí/no | Cota 0 en tierra (se conserva) o imposible (pasó a nulo) | 110 | R-08, R-09 |
| `fechas_inconsistentes` | sí/no | La fecha de fin es anterior a la de inicio | 3 | R-12 |
| `coordenadas_corregidas` | sí/no | Se intercambiaron longitud y latitud (corrección verificada) | 2 | R-13 |
| `recurso_inconsistente` | sí/no | Pozo CONVENCIONAL con subtipo de no convencional | 1 | R-18 |

### Diferencias con el origen

- Textos sin espacios sobrantes.
- Los faltantes disfrazados pasaron a nulo: "No informado", profundidad 0 y fecha 1900-01-01.
- `sub_tipo_recurso` dice "NO APLICA" en los pozos CONVENCIONAL y SIN RESERVORIO.
- Las fechas tienen tipo fecha (`AAAA-MM-DD`).
- Dos pozos tienen las coordenadas corregidas.

El detalle completo, regla por regla y con las filas afectadas, está en la sección 5 del notebook 02.

### Antes de usarlo

- **Para contar pozos físicos** use `sigla_normalizada`, no `idpozo`.
- **Para mapas** tenga en cuenta `ubicacion_compartida`, porque hay varios pozos en un mismo punto.
- **Salvedades** (a confirmar con la fuente): las unidades de `cota` y `profundidad`, la hipótesis de la coma decimal en los valores marcados como sospechosos, y el criterio de jurisdicción "Estado Nacional". Ver las conclusiones del notebook 02.
