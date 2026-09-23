# Proyecto DG — Data Governance Portfolio

## Contexto
- Soy Carolina, especialista en Configuration & Information Management, formándome en Data Governance y Analytics Engineering.
- Este repositorio es mi portfolio público: cada paso tiene que poder explicarse en una entrevista.
- Estoy aprendiendo Python, pandas, SQL y Git: explicame lo que hacés en español y en lenguaje simple.

## Entorno
- Windows. Python y Jupyter instalados con Anaconda: usá siempre el Python de Anaconda.
- Carpeta local del proyecto: C:\Users\Carolina\Documents\Capacitaciones\DataGovernance
- Repositorio remoto: GitHub, repositorio "DG".
- Los nombres son distintos a propósito: la carpeta local DataGovernance está vinculada al repositorio DG. No renombrar ninguno de los dos.

## Estructura de carpetas
- data/raw: datos originales descargados. NUNCA modificar, mover ni borrar estos archivos.
- data/clean: datos procesados, generados solo por los notebooks.
- notebooks: notebooks de Jupyter (.ipynb), numerados en orden: 01_..., 02_...
- Cada carpeta de datos tiene su README.md con fuente, link, fecha y descripción.

## Reglas de trabajo
1. Trabajá un paso por vez y esperá mi confirmación antes de seguir.
2. Las decisiones de limpieza las tomo yo: proponé opciones con pros y contras, no decidas solo.
3. En los notebooks, antes de cada celda de código poné una celda de texto que explique qué hace y por qué.
4. Cada decisión de limpieza queda documentada en el notebook (qué se cambió, cuántas filas afectó y por qué).
5. Nunca sobrescribas un archivo de data/raw. Los resultados van a data/clean con un nombre que indique su origen.
6. Antes de hacer un commit, mostrame qué archivos entran y proponé el mensaje.
7. Mensajes de commit en español, claros: qué cambió y por qué.
8. No subas archivos de más de 100 MB, contraseñas ni datos confidenciales. Usá .gitignore cuando corresponda.
9. Si algo falla, explicame el error en palabras simples antes de corregirlo.

## Gobierno de datos (mi sello)
- Trazabilidad: todo resultado debe poder rastrearse hasta el archivo raw de origen.
- Linaje: documentar cada transformación en orden.
- Calidad: reportar nulos, duplicados, tipos de datos y valores fuera de rango antes de limpiar.
