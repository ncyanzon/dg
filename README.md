# DG — Data Governance aplicado a datos de producción de hidrocarburos

Proyecto de portfolio que aplica prácticas de gobierno de datos (trazabilidad, linaje, calidad y control de cambios) a datos públicos de producción de petróleo y gas de Argentina, incluyendo Vaca Muerta.

> Estado: en construcción. Este repositorio documenta mi formación en Data Governance y Analytics Engineering.

## Objetivo

Recorrer el ciclo completo del dato, desde la fuente hasta el análisis, sin perder el control de calidad y la trazabilidad:

1. Obtener datos públicos y documentar su origen.
2. Perfilar y limpiar los datos, registrando cada decisión.
3. Analizar la producción por pozo y yacimiento.
4. Publicar resultados reproducibles y verificables.

## Enfoque de gobierno de datos

- **Trazabilidad:** todo resultado se puede rastrear hasta el archivo original.
- **Linaje:** cada transformación queda documentada, en orden, en los notebooks.
- **Integridad:** los datos originales (`data/raw`) nunca se modifican.
- **Control de versiones:** cada cambio queda registrado en Git con su justificación.

El detalle de estos criterios está en [POLITICA_CALIDAD_DATOS.md](POLITICA_CALIDAD_DATOS.md).

## Estructura del repositorio

```
DG/
├── README.md        Portada del proyecto (este archivo)
├── CLAUDE.md        Reglas de trabajo para el asistente de IA
├── POLITICA_CALIDAD_DATOS.md   Política de calidad: principios, criterios y registro de reglas
├── .gitignore       Archivos excluidos de GitHub (los datos de data/raw)
├── data/
│   ├── raw/         Datos originales (solo locales, no se suben) + README de la fuente
│   └── clean/       Datos procesados por los notebooks
└── notebooks/       Análisis en Jupyter, numerados en orden de ejecución
```

## Fuente de datos

- **Dataset:** Producción de petróleo y gas por pozo (Capítulo IV)
- **Publicado por:** Secretaría de Energía de la Nación (Argentina)
- **Detalle:** ver `data/raw/README.md` (link, fecha de descarga y descripción de cada archivo)

## Herramientas

Python (pandas) · Jupyter Notebook (Anaconda) · Git y GitHub · Claude Code (asistente de IA para programación)

## Cómo reproducir el análisis

1. Clonar este repositorio.
2. Descargar los archivos indicados en `data/raw/README.md` y guardarlos en `data/raw`.
3. Abrir los notebooks de `notebooks/` en orden (01, 02, ...) y ejecutarlos de principio a fin.

## Autora

**Carolina Yanzón** — Configuration & Information Management Specialist, en formación en Data Governance y Analytics Engineering.
[LinkedIn](https://linkedin.com/in/nellycarolina-yanzon-sarry-0b015314)
