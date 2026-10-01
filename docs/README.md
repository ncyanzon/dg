# docs — Documentación de los datos

## diccionario_pozos.csv

Diccionario de datos del maestro de pozos: una fila por columna del archivo de origen.

| Dato | Valor |
| --- | --- |
| Archivo que describe | `data/raw/capitulo-iv-pozos.csv` (85.611 filas, 26 columnas, 34.133.626 bytes) |
| Versión de la fuente | Publicada por la Secretaría de Energía, última modificación 08/07/2026 |
| Licencia de la fuente | CC-BY-4.0 (uso libre citando la fuente) |
| Qué representa cada fila | Un **pozo + formación productiva** (`idpozo`). Un pozo físico (`sigla` normalizada) puede tener varias filas |
| Basado en | `notebooks/01_pozos_perfilado.ipynb` (hallazgos H-xx) |
| Versión | **1.3**, aprobada (ver historial) |

### Historial de versiones

| Versión | Fecha | Cambio | Motivo |
| --- | --- | --- | --- |
| 1.0 | 30/09/2026 | Primera versión, revisada y aprobada | Línea base del diccionario |
| 1.1 | 30/09/2026 | Se corrige la definición de `idpozo` (pozo + formación, no pozo físico) y de `sigla` (identifica al pozo físico); se agrega H-23 | Al investigar la decisión D-3 se verificó que la formación cambia en el 97,8% de los grupos con sigla repetida |
| 1.2 | 30/09/2026 | Se agregan `valor_min` y `valor_max` (límites duros); `regla_validez` pasa a tener las reglas de contexto; se corrige la regla de `cota` y se agrega H-24 | La regla anterior de `cota` (-100 a 6.000) salía del dato observado y aceptaba dos valores imposibles. Las reglas tienen que salir del negocio y de la física, no del dato |
| 1.3 | 01/10/2026 | `sigla`, `area`, `empresa`, `yacimiento` y `formacion` suman H-25 (espacios sobrantes); `sigla` suma H-26 y se identifica al pozo físico por la sigla normalizada (78.299) | Al investigar la decisión D-8 aparecieron espacios sobrantes y siglas escritas de más de una forma |

### Por qué se construyó

La fuente no publica un diccionario de campos: ni el portal de la Secretaría de Energía ni datos.gob.ar
describen las columnas de este archivo. Lo único documentado oficialmente es la unidad de la producción
y el sistema de coordenadas del shapefile (EPSG:4326). Por eso cada definición indica de dónde sale.

### Campos del diccionario

| Campo | Qué dice |
| --- | --- |
| `columna` | Nombre exacto en el CSV original |
| `descripcion` | Qué representa, en lenguaje de negocio |
| `tipo_raw` | Tipo con el que pandas lee la columna hoy |
| `tipo_esperado` | Tipo que debería tener después de la limpieza |
| `unidad` | Unidad de medida; "(a confirmar)" si la fuente no la documenta |
| `admite_nulos` | Si puede faltar. "Sí (hoy)" = hoy tiene faltantes, pero la decisión está pendiente |
| `faltante_se_representa_como` | Cómo aparece un dato faltante: celda vacía, 'No informado' o un valor de relleno |
| `valor_min` / `valor_max` | Límites duros, incluidos: fuera de ellos el valor es imposible. En `geojson` se dan para longitud y latitud |
| `regla_validez` | Reglas de contexto (dependen de otra columna) o lista de valores válidos |
| `origen_definicion` | Nivel de confianza de la definición (ver abajo) |
| `hallazgos` | Códigos H-xx del perfilado que afectan a la columna |
| `observaciones` | Cifras y aclaraciones |

### Dos tipos de reglas de validez

| Tipo | Dónde está | Ejemplo | Si no se cumple |
| --- | --- | --- | --- |
| Límite duro | `valor_min` / `valor_max` | Profundidad entre 1 y 10.000 m | Error: el valor pasa a nulo y se marca |
| Regla de contexto | `regla_validez` | Cota 0 válida solo costa afuera | Sospechoso: el valor se conserva y se marca |

Los límites duros solos no alcanzan: una cota de -100 m es posible en la Argentina, pero no en la zona de Mendoza donde está ese pozo.

### Niveles de confianza (`origen_definicion`)

| Nivel | Significa |
| --- | --- |
| Fuente oficial | Lo documenta la Secretaría de Energía |
| Verificado en el dato | Se comprobó con código sobre el archivo |
| Inferido | Deducido del nombre y de los valores; falta confirmarlo |
| Desconocido | No se sabe qué representa; no se inventa una definición |

### Hallazgos detectados al construir y corregir el diccionario

Registrados en `notebooks/01_pozos_perfilado.ipynb` (sección 9, con su evidencia en código).

| Código | Dimensión | Hallazgo | Filas |
| --- | --- | --- | --- |
| H-19 | Validez | Coordenadas con longitud y latitud invertidas (idpozo 10143 y 162058) | 2 |
| H-20 | Completitud | H-05 sobreestima los faltantes: en `sub_tipo_recurso`, 'No informado' significa "no aplica" para los pozos convencionales | 58.319 |
| H-21 | Consistencia | Pozo CONVENCIONAL con `sub_tipo_recurso` = TIGHT | 1 |
| H-22 | Consistencia | Pozos en yacimientos cuyo nombre tiene más de un código (88 nombres) | 17.478 |
| H-23 | Unicidad | Misma sigla y misma formación: posible carga duplicada (159 siglas) | 353 |
| H-24 | Validez | Cota mayor que la altura máxima de su provincia (5.543 m en Neuquén) | 1 |
| H-25 | Consistencia | Textos con espacios sobrantes (al principio, al final o dobles). Esconden parte de H-17 y H-22 | 5.904 |
| H-26 | Consistencia | Sigla escrita de más de una forma (por ejemplo NQ y Nq; 37 siglas) | 85 |
