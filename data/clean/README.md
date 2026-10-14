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

## produccion_2024-2026_limpio.parquet

Producción mensual por pozo, de enero de 2024 a agosto de 2026: una fila por **pozo + mes** (`idpozo` + `anio` + `mes`).
Une los tres archivos anuales de producción en una sola tabla.

| Dato | Valor |
| --- | --- |
| Generado por | `notebooks/04_produccion_limpieza.ipynb` (diagnóstico en `notebooks/03_produccion_perfilado.ipynb`) |
| Archivos de origen | `data/raw/produccin-de-pozos-de-gas-y-petrleo-2024.csv`, `-2025.csv` y `-2026.csv` (ver `data/raw/README.md`) |
| Huella SHA-256 del origen 2024 | `2c3e2f6ec26840266c92aea509acf7677daf146d52e58bbd794a976b96e29cba` |
| Huella SHA-256 del origen 2025 | `53d7831455a50c73a8f66176238fa7af3599d5695071e8982ecd53b2022580e2` |
| Huella SHA-256 del origen 2026 | `c63017b48aa0723904a9a0db41a360790c99c5dd05fb83ff363dd0e18acfbc97` |
| Referencia | `capitulo-iv-pozos_limpio.csv` (se consulta para dos marcas; sus columnas no se incorporan) |
| Huella SHA-256 de este archivo | `d36d226e79a810492639b807956b0443536bde649fd35d5fa024dd5f2e91b790` |
| Fecha de generación | 14/10/2026 (pandas 3.0.6, pyarrow 24.0.0) |
| Formato | Parquet con compresión zstd, 11,7 MB. Se lee con `pd.read_parquet`; no se abre con Excel |
| Filas | 2.628.689 (las mismas que los tres orígenes juntos: no se eliminó ninguna) |
| Columnas | 28: las 22 leídas del origen (dos renombradas), más `archivo_origen`, `fecha_mes` y 4 marcas |
| Totales | Petróleo 122.566.029 m³ · gas 138.232.359 miles de m³ (idénticos a los del origen) |

Las filas están ordenadas por `idpozo` y `fecha_mes`.

### Columnas nuevas o renombradas

| Columna | Tipo | Qué indica | Filas | Regla |
| --- | --- | --- | ---: | --- |
| `prod_pet_m3` | decimal | Petróleo del mes, en m³ (antes `prod_pet`; mismo valor) | todas | R-21 |
| `prod_gas_miles_m3` | decimal | Gas del mes, en miles de m³ (antes `prod_gas`; mismo valor) | todas | R-21 |
| `archivo_origen` | texto | Archivo raw del que viene la fila (linaje) | todas | — |
| `fecha_mes` | fecha | Primer día del mes informado (por ejemplo, 2025-03-01) | todas | R-22 |
| `tef_fuera_de_rango` | sí/no | `tef` negativo o mayor que los días del mes; el valor se conserva | 2.830 | R-23 |
| `produccion_negativa` | sí/no | Petróleo o gas negativo (ajustes de la empresa); el valor se conserva | 9 | R-24 |
| `fuera_del_maestro` | sí/no | El `idpozo` no está en el maestro de pozos limpio (en su mayoría, pozos nuevos) | 1.270 | R-25 |
| `recurso_inconsistente` | sí/no | El pozo cambia de tipo de recurso en el período o difiere del maestro | 32 | R-26 |

### Antes de usarlo

- **Petróleo y gas no se suman:** tienen unidades distintas.
- **Vaca Muerta no convencional:** `formprod == "VMUT"` y `tipo_de_recurso == "NO CONVENCIONAL"` (hay pozos verticales viejos de Vaca Muerta marcados CONVENCIONAL, y es un dato real).
- **Empresa:** cada mes figura con la empresa que lo operó; muchos pozos cambiaron de operador en 2024–2025 (venta de áreas).
- **`tef`:** si se usa, excluir las filas con `tef_fuera_de_rango`.
- **Salvedad:** el archivo 2026 se descargó el 23/09/2026; los de 2024 y 2025, el 13/10/2026.

El detalle regla por regla está en la sección 5 del notebook 04.
