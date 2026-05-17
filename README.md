# Demography_9219_Final_Project
Final project of demography

# Tablas de vida — Guerrero 2010, 2019 y 2021

**Autores:** Iván Aguilar Celis y Ana Paola Rivera Gallardo  
**Materia:** Demografía 9219  
**Estado:** Guerrero, México

## Descripción

Este proyecto construye tablas de vida por sexo para el estado de Guerrero
en los años 2010, 2019 y 2021, con el objetivo de analizar la evolución
de la mortalidad y el impacto de la pandemia de COVID-19.
Se incluye contexto demográfico, fórmulas actuariales, código documentado
y una comparativa internacional con Noruega.

## Estructura del repositorio

Demography_9219_Final_Project/
├── Proyecto_Final_9219.qmd         # Documento fuente en Quarto
├── Proyecto_Final_9219.pdf         # Informe final renderizado
├── Data/
│   ├── 00_Pob_Mitad_1950_2070.csv        # Proyecciones CONAPO
│   ├── INEGI(Defunciones Guerrero).xlsx   # Defunciones SINAIS/INEGI
│   ├── Mx_ARG_GUA.csv                    # Tasas Argentina y Guatemala
│   └── diagrama_flujo_tablas_vida.png    # Diagrama de flujo
└── README.md

## Fuentes de datos

| Dato | Fuente |
|------|--------|
| Población mitad de año | CONAPO — incluida en `Data/` |
| Defunciones Guerrero 1990–2024 | SINAIS/INEGI — incluida en `Data/` |
| Mortalidad internacional | UN WPP 2024 — descarga automática al renderizar |
| Población internacional | UN WPP 2024 — descarga automática al renderizar |

## Cómo reproducir

### Requisitos

- R >= 4.2
- Quarto >= 1.3
- Paquetes R: `tidyverse`, `data.table`, `readxl`, `kableExtra`,
  `lubridate`, `DemoTools`, `mipfp`, `rstan`, `openxlsx2`

### Instalación de paquetes

```r
install.packages(c("tidyverse", "data.table", "readxl",
                   "kableExtra", "lubridate", "mipfp", "openxlsx2"))

# DemoTools desde GitHub
remotes::install_github("timriffe/DemoTools")
```

### Renderizar el PDF

```bash
quarto render Proyecto_Final_9219.qmd
```

O desde RStudio: abrir `Proyecto_Final_9219.qmd` y hacer clic en **Render**.

> **Nota:** Los archivos de UN WPP se descargan automáticamente al renderizar.
> Se requiere conexión a internet en el primer render.

## Resultados principales

| Año | e₀ Hombres | e₀ Mujeres |
|-----|-----------|-----------|
| 2010 | 73.32 | 80.25 |
| 2019 | 74.30 | 81.40 |
| 2021 | 68.66 | 76.53 |

La caída de 2021 refleja el impacto del COVID-19 sobre una población
estructuralmente vulnerable por alta marginación y violencia crónica.
Guerrero perdió 5.6 años de esperanza de vida masculina en un solo año.
