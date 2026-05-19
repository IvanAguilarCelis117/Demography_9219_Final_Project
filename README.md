# Tablas de Vida — Guerrero 2010, 2019 y 2021

**Autores:** Iván Aguilar Celis y Ana Paola Rivera Gallardo  
**Materia:** Demografía 9219  
**Institución:** Facultad de Ciencias, UNAM  

---

<p align="center">
  <img src="data/Foto_de_Guerrero.jpg" width="600" alt="Estado de Guerrero, México"/>
</p>

---

## Descripción

Este proyecto construye tablas de vida por sexo para el estado de Guerrero
en los años 2010, 2019 y 2021, con el objetivo de analizar la evolución
de la mortalidad y el impacto de la pandemia de COVID-19.

Guerrero es un caso singular en México: ocupa el **primer lugar nacional
en marginación** (CONAPO 2020) y ha sido consistentemente una de las
entidades más violentas del país, con una tasa de homicidios que en 2010
triplicaba el promedio nacional. Estos factores estructurales, combinados
con el impacto del COVID-19 en 2021, configuran un perfil de mortalidad
que este proyecto documenta con herramientas demográficas formales.

El análisis incluye pirámides poblacionales (1970, 2010, 2019, 2021),
modelos de crecimiento exponencial, tasas específicas de mortalidad con
comparativa internacional contra Noruega, tablas de vida completas con
convenciones Coale-Demeny, y análisis del impacto del COVID-19.

---

## Diagrama de flujo metodológico

<p align="center">
  <img src="data/diagrama_flujo_tablas_vida.png" width="500"
       alt="Diagrama de flujo: construcción de tablas de vida"/>
</p>

---

## Resultados principales

### Esperanza de vida al nacer — Guerrero

| Año  | e₀ Hombres | e₀ Mujeres | Diferencia H vs M |
|------|:----------:|:----------:|:-----------------:|
| 2010 | 73.32      | 80.25      | -6.93             |
| 2019 | 74.30      | 81.40      | -7.10             |
| 2021 | **68.66**  | **76.53**  | -7.87             |

> **Guerrero perdió 5.6 años de esperanza de vida masculina en un solo año** —
> el hallazgo central del análisis.

### Tasas brutas de mortalidad (por 1,000 hab.)

| Año  | Hombres | Mujeres |
|------|:-------:|:-------:|
| 2010 | ~5.8    | ~3.6    |
| 2019 | ~6.1    | ~3.8    |
| 2021 | ~8.4    | ~5.9    |

### Parámetros del modelo

| Parámetro | Valor |
|-----------|-------|
| Raíz de la tabla $l_0$ | 100,000 |
| Grupo abierto | 85+ |
| Convención $a_x$ | Coale-Demeny |
| Población expuesta | Mitad de año — 1 julio |
| Fórmula | $N(t+0.5) = N(t) \cdot e^{0.5r}$, $r = \ln(N_{t+1}/N_t)$ |

---

## Estructura del repositorio

```
Demography_9219_Final_Project/
├── Proyecto_Final_9219.qmd              # Documento fuente en Quarto
├── Proyecto_Final_9219.pdf              # Informe final renderizado
├── README.md
└── data/
    ├── 00_Pob_Mitad_1950_2070.csv       # Proyecciones CONAPO
    ├── INEGI(Defunciones Guerrero).xlsx  # Defunciones SINAIS/INEGI
    ├── WPP2024_deaths_m.xlsx            # Muertes ONU — hombres
    ├── WPP2024_deaths_f.xlsx            # Muertes ONU — mujeres
    ├── WPP2024_population_m.xlsx        # Población ONU — hombres
    ├── WPP2024_population_f.xlsx        # Población ONU — mujeres
    ├── Mx_ARG_GUA.csv                   # Tasas Argentina y Guatemala
    ├── diagrama_flujo_tablas_vida.png   # Diagrama de flujo
    ├── Foto_de_Guerrero.jpg             # Mapa para portada
    ├── UNAM-Logo.png                    # Logo UNAM
    └── FC-Logo.png                      # Logo FC (ver nota abajo)
```

> **Nota sobre FC-Logo:** el logo original está en `.webp`, que LaTeX no soporta.
> Conviértelo a PNG una sola vez antes de renderizar:
> ```bash
> # Mac (sips viene preinstalado):
> sips -s format png data/FC-Logo.webp --out data/FC-Logo.png
>
> # Linux (requiere ImageMagick):
> convert data/FC-Logo.webp data/FC-Logo.png
>
> # Windows (PowerShell con ImageMagick):
> magick data/FC-Logo.webp data/FC-Logo.png
> ```

---

## Cómo reproducir — instrucciones completas

### Paso 1 — Instalar R y RStudio

- **R** (>= 4.2): https://cran.r-project.org
- **RStudio** (recomendado): https://posit.co/download/rstudio-desktop

### Paso 2 — Instalar Quarto

Quarto viene incluido en versiones recientes de RStudio. Si no lo tienes:
https://quarto.org/docs/get-started

### Paso 3 — Instalar paquetes de R

Abre RStudio y corre en la consola **antes** de renderizar por primera vez:

```r
# Paquetes de CRAN
install.packages(c(
  "tidyverse",    # manipulación de datos
  "data.table",   # lectura rápida de CSV grandes
  "readxl",       # lectura de Excel
  "kableExtra",   # tablas con formato LaTeX
  "lubridate",    # manejo de fechas
  "mipfp",        # métodos demográficos
  "openxlsx2",    # escritura de Excel
  "rstan"         # requerido por DemoTools
))

# DemoTools desde GitHub
install.packages("remotes")
remotes::install_github("timriffe/DemoTools")
```

> **Windows:** `rstan` requiere instalar
> [Rtools](https://cran.r-project.org/bin/windows/Rtools/) primero.
>
> **Mac:** si falla `rstan`, corre antes:
> ```r
> install.packages("StanHeaders")
> install.packages("rstan", type = "source")
> ```

### Paso 4 — Instalar LaTeX

El PDF se genera con LuaLaTeX. Si no tienes LaTeX instalado, la opción
más sencilla es TinyTeX — se instala desde R y descarga automáticamente
los paquetes que falten al compilar:

```r
install.packages("tinytex")
tinytex::install_tinytex()
```

### Paso 5 — Convertir el logo (solo la primera vez)

```bash
sips -s format png data/FC-Logo.webp --out data/FC-Logo.png
```

### Paso 6 — Renderizar

```bash
quarto render Proyecto_Final_9219.qmd
```

O desde RStudio: abrir `Proyecto_Final_9219.qmd` → clic en **Render**.

El PDF se genera en la misma carpeta como `Proyecto_Final_9219.pdf`.

---

## Fuentes de datos

| Dato | Fuente | Incluido en repo |
|------|--------|:----------------:|
| Población mitad de año 1950–2070 | CONAPO | ✓ |
| Defunciones Guerrero 1990–2024 | SINAIS/INEGI | ✓ |
| Muertes por edad y sexo (internacional) | UN WPP 2024 | ✓ |
| Población por edad y sexo (internacional) | UN WPP 2024 | ✓ |
| Tasas Argentina y Guatemala | Ejercicio de clase | ✓ |

---

## Notas metodológicas

- La **población expuesta** $N_x$ se aproxima al 1 de julio con crecimiento
  exponencial: $N(t+0.5) = N(t) \cdot e^{0.5r}$, $r = \ln(N_{t+1}/N_t)$
- Los valores de $a_x$ siguen las **convenciones Coale-Demeny**:
  $a_0$ depende de $m_0$; $a_{1-4} = 1.5$; grupos quinquenales $a_x = 2.5$
- Para el grupo abierto $85+$: $L_{85+} = l_{85+} / m_{85+}$

---

## Referencias

- Coale, A. J., y Demeny, P. (1966). *Regional model life tables and stable populations*. Princeton University Press.
- CONAPO (2020). *Índice de marginación por entidad federativa*. https://www.conapo.gob.mx
- INEGI (2010, 2019, 2021). *Estadísticas de defunciones registradas*. SINAIS. https://www.inegi.org.mx
- UN DESA (2024). *World Population Prospects 2024*. https://population.un.org/wpp/
- SESNSP (2022). *Incidencia delictiva del fuero común: homicidio doloso 2011–2021*. https://www.gob.mx/sesnsp
- Wachter, K. W. (2014). *Essential Demographic Methods*. Harvard University Press.

---

*Proyecto para la materia Demografía 9219 · Facultad de Ciencias · UNAM · 2026*
