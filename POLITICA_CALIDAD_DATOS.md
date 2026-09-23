# Política de calidad de datos — Proyecto DG

Esta política define cómo se perfilan, limpian y documentan los datos del proyecto, para que todo resultado sea trazable hasta su fuente.

## Principios

- **Source of truth:** los datos originales de `data/raw` son la fuente única de verdad y nunca se modifican, mueven ni borran.
- **Integridad:** toda transformación genera un archivo nuevo en `data/clean`; el original queda intacto como evidencia.
- **Trazabilidad:** todo resultado se puede rastrear hasta el archivo de origen, la regla aplicada y su justificación.
- **Linaje documentado:** el código muestra el *qué*; las celdas de texto del notebook explican el *por qué*.
- **Reproducibilidad:** si el notebook se ejecuta desde cero, da exactamente el mismo resultado.
- **Versionado:** se versiona la documentación de la fuente, no el dato. Todos los archivos de `data/raw` quedan solo en la computadora local, excluidos de GitHub mediante `.gitignore`, excepto su `README.md`. En GitHub se publican el procedimiento (notebooks) y su resultado (`data/clean`).
- **Respaldo:** la copia local de `data/raw` se respalda fuera del repositorio, porque la fuente pública se actualiza y la versión descargada puede dejar de estar disponible.

## Dimensiones de calidad

| Dimensión | Pregunta | Ejemplo en el dataset |
| --- | --- | --- |
| Completitud | ¿Falta algún dato? | Pozo sin valor de producción |
| Unicidad | ¿Hay registros repetidos? | Mismo pozo y mismo mes dos veces |
| Validez | ¿El valor respeta su formato y rango? | Producción negativa, fecha imposible |
| Consistencia | ¿Se escribe siempre igual? | "Neuquén" / "NEUQUEN" / "Nqn" |
| Exactitud | ¿Refleja la realidad? | Valor 1000 veces mayor que el habitual |
| Oportunidad | ¿Está actualizado? | Fecha de corte del dataset |

## Procedimiento de limpieza

1. **Perfilar:** medir cuántos problemas hay de cada dimensión, sin modificar nada.
2. **Definir la regla** para cada problema, antes de aplicarla.
3. **Elegir la acción** (tabla de abajo).
4. **Aplicar y medir el impacto:** filas afectadas y porcentaje del total.
5. **Validar:** volver a perfilar y confirmar que el problema desapareció.
6. **Documentar:** qué se hizo, por qué, a cuántas filas afectó y cómo se verificó.

| Acción | Cuándo usarla | Riesgo |
| --- | --- | --- |
| Marcar | Ante la duda; conserva el dato con una columna de alerta | El más bajo |
| Corregir | Error de formato evidente (mayúsculas, tipos, fechas) | Bajo, si la regla es clara |
| Completar / imputar | Hay un valor defendible para rellenar | Medio: puede introducir sesgo |
| Eliminar | Dato irrecuperable y no clave | Alto: se pierde información |

## Criterios de oro

- **Cero no es nulo.** Un pozo con producción 0 puede estar cerrado: es un dato real. Un nulo es un dato faltante.
- **Un outlier no se borra automáticamente.** Primero se investiga.
- **Ante la duda, marcar antes que eliminar.**
- **Nunca cambiar unidades en silencio.** Si se convierte, el nombre de la columna lo dice (`gas_m3`, no `gas`).
- **Toda regla tiene un porqué de negocio**, no solo técnico.
- **Toda decisión informa su impacto** en filas y porcentaje.

## Registro de reglas del dataset

| ID | Dimensión | Problema detectado | Regla | Acción | Filas afectadas | Notebook |
| --- | --- | --- | --- | --- | --- | --- |
| R-01 | | | | | | |
