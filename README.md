# Tablas de vida — Guerrero 2010, 2019 y 2021

**Materia:** Demografía 9219 · UNAM  
**Autores:** Iván Aguilar Celis · Ana Paola Rivera Gallardo  
**Estado analizado:** Guerrero, México  
**Última actualización:** mayo 2026

---

## ¿De qué trata este proyecto?

Construimos tablas de vida de período por sexo para el estado de **Guerrero** en los años **2010, 2019 y 2021**, usando defunciones registradas del SINAIS/INEGI y proyecciones de población del CONAPO. El objetivo es cuantificar cómo la violencia estructural crónica y la pandemia de COVID-19 afectaron la esperanza de vida en una de las entidades más marginadas de México.

---

## Mapa de ubicación

```
         ┌─────────────────────────────────┐
         │         MÉXICO                  │
         │                                 │
         │        ╔═══════╗               │
         │        ║GUERRERO║  ← entidad   │
         │        ╚═══════╝  analizada    │
         │          Costa del Pacífico     │
         └─────────────────────────────────┘
```

> Guerrero se ubica en la costa del Pacífico sur de México. Capital: Chilpancingo de los Bravo.  
> Municipios relevantes: Acapulco (zona metropolitana más grande), Zihuatanejo, Iguala, Taxco.

---

## Contexto demográfico clave

| Indicador | Valor | Fuente |
|---|---|---|
| Población 2010 | 3,471,744 hab | CONAPO |
| Población 2019 | 3,604,522 hab | CONAPO |
| Población 2021 | 3,598,332 hab | CONAPO |
| Índice de marginación 2020 | **0.40 — Muy alto** (1.° nacional) | CONAPO |
| Tasa de homicidios 2010 | ~63 por 100,000 hab (3× promedio nacional) | SESNSP |
| Homicidios dolosos 2011–2021 | 24,009 (4.° lugar nacional) | SESNSP |

---

## Resultados principales

### Esperanza de vida al nacer (e₀)

| Año | Hombres | Mujeres | Brecha H–M |
|-----|--------:|--------:|-----------:|
| 2010 | 73.32 años | 80.25 años | 6.93 años |
| 2019 | 74.30 años | 81.40 años | 7.10 años |
| **2021** | **68.66 años** | **76.53 años** | **7.87 años** |

> **Hallazgo central:** En 2021 los hombres de Guerrero perdieron **5.64 años** de esperanza de vida respecto a 2019 — consecuencia directa del COVID-19 sobre una infraestructura de salud ya debilitada por la alta marginación.

### Evolución visual (texto)

```
e₀ Hombres
74.30 ┤ 2019  ██████████████████████████████████████
73.32 ┤ 2010  █████████████████████████████████████
68.66 ┤ 2021  ██████████████████████████████████   ← COVID

e₀ Mujeres  
81.40 ┤ 2019  ████████████████████████████████████████
80.25 ┤ 2010  ███████████████████████████████████████
76.53 ┤ 2021  █████████████████████████████████████   ← COVID
```

---

## Estructura del repositorio

```
Demography_9219_Final_Project/
│
├── README.md                          ← este archivo
├── Proyecto_Final_9219.qmd            ← documento fuente Quarto
├── Proyecto_Final_9219.pdf            ← informe final compilado
│
├── Data/
│   ├── 00_Pob_Mitad_1950_2070.csv     ← proyecciones de población CONAPO
│   │                                     (entidades federativas, por edad y sexo,
│   │                                      1950–2070, mitad de año)
│   │
│   ├── INEGI(Defunciones Guerrero).xlsx  ← defunciones registradas SINAIS/INEGI
│   │                                        (Guerrero, grupos quinquenales,
│   │                                         por sexo, 1990–2024)
│   │
│   ├── Mx_ARG_GUA.csv                 ← tasas de mortalidad Argentina y Guatemala
│   │                                     (ejercicio comparativo, año 2018)
│   │
│   └── diagrama_flujo_tablas_vida.png ← diagrama del proceso metodológico
│
└── Graficas/                          ← gráficas exportadas del análisis
    ├── piramide_1970.png
    ├── piramide_2010.png
    ├── piramide_2019.png
    ├── piramide_2021.png
    ├── log_mx_2010.png
    ├── log_mx_2019.png
    ├── log_mx_2021.png
    ├── log_mx_comparativo.png
    ├── guerrero_vs_noruega_2019.png
    ├── lx_supervivencia.png
    ├── qx_probabilidad_muerte.png
    └── e0_evolucion.png
```

---

## Diagrama de flujo del proceso

```
  ┌─────────────────────────────────┐
  │   Fuentes de datos               │
  │   SINAIS/INEGI  ·  CONAPO       │
  └────────────┬────────────────────┘
               │
       ┌───────┴────────┐
       ▼                ▼
  ┌─────────┐     ┌──────────┐
  │ Def D_x │     │ Pob N_x  │
  │  INEGI  │     │  CONAPO  │
  └────┬────┘     └─────┬────┘
       └────────┬────────┘
                ▼
  ┌─────────────────────────────┐
  │  Limpieza y estandarización  │
  │  Grupos quinquenales         │
  │  2010 / 2019 / 2021          │
  └──────────────┬──────────────┘
                 ▼
  ┌─────────────────────────────┐
  │  Tasa central de mortalidad  │
  │  m_x = D_x / N_x            │
  └──────────────┬──────────────┘
                 ▼
  ┌─────────────────────────────┐
  │  Probabilidad de muerte      │
  │  q_x — convención Coale-    │
  │  Demeny para a_x            │
  └──────────────┬──────────────┘
                 ▼
  ┌─────────────────────────────┐
  │  Tabla de vida completa      │
  │  l_x → d_x → L_x → T_x     │
  │  Raíz = 100,000             │
  └──────────┬───────┬──────────┘
             ▼       ▼
    ┌──────────┐  ┌────────┐
    │  e₀ por  │  │Gráficas│
    │sexo y año│  │log(mx) │
    └──────────┘  │ lx, qx │
                  └────────┘
```

---

## Fórmulas utilizadas

### Tasa central de mortalidad
```
m_x = D_x / N_x
```

### Probabilidad de muerte (Coale-Demeny)
```
q_x = (n · m_x) / (1 + (n − a_x) · m_x)

a_0 = 0.07 + 1.7·m_0    si m_0 ≥ 0.107
a_0 = 0.14 + 2.0·m_0    si m_0 < 0.107
a_x = 1.5  para grupo 1–4
a_x = 2.5  para grupos quinquenales 5–85
q_85+ = 1  (grupo abierto)
```

### Tabla de vida
```
l_{x+n} = l_x · (1 − q_x)       sobrevivientes
d_x     = l_x · q_x              muertes en el intervalo
L_x     = n·l_x − (n−a_x)·d_x   años-persona vividos
L_85+   = l_85+ / m_85+          grupo abierto
T_x     = Σ L_i  (de x a 85+)   años-persona acumulados
e_x     = T_x / l_x              esperanza de vida
```

---

## Fuentes de datos

| Dato | Fuente | Incluido en repo |
|------|--------|:---:|
| Población mitad de año (1950–2070) | CONAPO — [gob.mx/conapo](https://www.gob.mx/conapo) | ✅ `Data/` |
| Defunciones Guerrero (1990–2024) | SINAIS/INEGI — [inegi.org.mx](https://www.inegi.org.mx/sistemas/olap/proyectos/bd/continuas/mortalidad/defunciones.asp) | ✅ `Data/` |
| Mortalidad internacional (WPP 2024) | UN — [population.un.org/wpp](https://population.un.org/wpp/) | 🌐 descarga automática |
| Población internacional (WPP 2024) | UN — [population.un.org/wpp](https://population.un.org/wpp/) | 🌐 descarga automática |
| Tasas Argentina y Guatemala | Ejercicio de clase | ✅ `Data/` |

---

## Cómo reproducir el análisis

### Requisitos

- R ≥ 4.2
- Quarto ≥ 1.3
- Conexión a internet (primera vez, para descargar datos de UN WPP)

### Instalar paquetes

```r
install.packages(c(
  "tidyverse", "data.table", "readxl",
  "kableExtra", "lubridate", "mipfp", "openxlsx2"
))

# DemoTools — desde GitHub
remotes::install_github("timriffe/DemoTools")
```

### Renderizar el informe

```bash
quarto render Proyecto_Final_9219.qmd
```

O desde RStudio: abrir `Proyecto_Final_9219.qmd` → clic en **Render**.

> Los datos de UN WPP (~500 MB comprimidos) se descargan automáticamente en el primer render. En renders posteriores se leen desde caché.

---

## Descripción de las gráficas

| Gráfica | Qué muestra |
|---------|-------------|
| `piramide_*.png` | Estructura por edad y sexo de Guerrero en 1970, 2010, 2019 y 2021. Evidencia la transición demográfica y el estrechamiento progresivo de la base. |
| `log_mx_*.png` | Logaritmo de tasas específicas de mortalidad por sexo. La joroba masculina en 20–34 años refleja sobremortalidad por violencia. |
| `log_mx_comparativo.png` | Comparación de los tres años simultáneamente. La curva 2021 está sistemáticamente por encima en adultos. |
| `guerrero_vs_noruega_2019.png` | Brecha de mortalidad entre Guerrero y Noruega (referencia internacional de alta esperanza de vida). |
| `lx_supervivencia.png` | Curva de supervivencia l_x. En 2021 cae más rápido a partir de los 50 años. |
| `qx_probabilidad_muerte.png` | Probabilidad de morir q_x. Salto pronunciado en hombres de 60–75 años en 2021. |
| `e0_evolucion.png` | Evolución de e₀ por sexo en los tres años. Caída dramática de 2019 a 2021. |

---

## Interpretación resumida

**2010 → 2019 (tendencia pre-pandemia)**  
Guerrero mostró mejoría moderada: +1.0 año en hombres, +1.2 en mujeres. Avance limitado por el primer lugar nacional en marginación y tasas de homicidio que triplicaban el promedio nacional.

**2021 (impacto COVID-19)**  
Hombres: −5.64 años · Mujeres: −4.87 años respecto a 2019. El exceso de mortalidad se concentró en adultos de 50–74 años, edades con mayor letalidad por COVID-19. La infraestructura sanitaria de Guerrero, ya debilitada, no pudo absorber la demanda.

**Patrón masculino estructural**  
En los tres años, la curva log(m_x) masculina muestra una joroba característica en 20–34 años ausente en Noruega — huella directa de la violencia como causa de muerte evitable.

---

## Referencias

- Coale, A. J. & Demeny, P. (1966). *Regional model life tables and stable populations*. Princeton University Press.
- CONAPO (2023). *Proyecciones de la población de México y entidades federativas, 1950–2070*.
- INEGI (2010, 2019, 2021). *Estadísticas de defunciones registradas (EDR)*. SINAIS.
- Preston, S. H., Heuveline, P. & Guillot, M. (2001). *Demography: Measuring and modeling population processes*. Blackwell.
- SESNSP (2022). *Incidencia delictiva del fuero común: homicidio doloso 2011–2021*.
- United Nations (2024). *World Population Prospects 2024*. [population.un.org/wpp](https://population.un.org/wpp/)
- Wachter, K. W. (2014). *Essential Demographic Methods*. Harvard University Press.

---

*Proyecto para la materia Demografía 9219 · Facultad de Ciencias · UNAM · 2026*
