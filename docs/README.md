# docs — Documentación de los datos

## diccionario_pozos.csv

Diccionario de datos del maestro de pozos: una fila por columna del archivo de origen.

| Dato | Valor |
| --- | --- |
| Archivo que describe | `data/raw/capitulo-iv-pozos.csv` (85.611 filas, 26 columnas, 34.133.626 bytes) |
| Versión de la fuente | Publicada por la Secretaría de Energía, última modificación 08/07/2026 |
| Licencia de la fuente | CC-BY-4.0 (uso libre citando la fuente) |
| Basado en | `notebooks/01_pozos_perfilado.ipynb` (hallazgos H-xx) |
| Estado | **Borrador**, pendiente de revisión |
| Fecha | 28/09/2026 |

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
| `regla_validez` | Rango o lista de valores válidos |
| `origen_definicion` | Nivel de confianza de la definición (ver abajo) |
| `hallazgos` | Códigos H-xx del perfilado que afectan a la columna |
| `observaciones` | Cifras y aclaraciones |

### Niveles de confianza (`origen_definicion`)

| Nivel | Significa |
| --- | --- |
| Fuente oficial | Lo documenta la Secretaría de Energía |
| Verificado en el dato | Se comprobó con código sobre el archivo |
| Inferido | Deducido del nombre y de los valores; falta confirmarlo |
| Desconocido | No se sabe qué representa; no se inventa una definición |

### Hallazgos detectados al construir el diccionario

Registrados en `notebooks/01_pozos_perfilado.ipynb` (sección 9, con su evidencia en código).

| Código | Dimensión | Hallazgo | Filas |
| --- | --- | --- | --- |
| H-19 | Validez | Coordenadas con longitud y latitud invertidas (idpozo 10143 y 162058) | 2 |
| H-20 | Completitud | H-05 sobreestima los faltantes: en `sub_tipo_recurso`, 'No informado' significa "no aplica" para los pozos convencionales | 58.319 |
| H-21 | Consistencia | Pozo CONVENCIONAL con `sub_tipo_recurso` = TIGHT | 1 |
| H-22 | Consistencia | Pozos en yacimientos cuyo nombre tiene más de un código (88 nombres) | 17.478 |
