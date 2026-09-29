🇪🇸 Versión en español (esta página) · 🇬🇧 [English version](./README.md)

# 🏙️ Florida Investment Analysis — Power BI

Análisis de oportunidades de inversión inmobiliaria en condados de Florida, combinando población, crecimiento laboral, tasa de criminalidad y balance oferta/demanda para identificar las mejores zonas de entrada.

**[📄 Ver reporte (PDF)](./2.Screenshots) · [📊 Descargar .pbix](./1.Dashboard) · [🧮 Medidas DAX](./3.Dax)**

---

## 📌 Contexto del proyecto

Este proyecto fue desarrollado como parte de una evaluación técnica de análisis de inversión inmobiliaria. El objetivo del negocio: dado un dataset con indicadores demográficos y de mercado de varios condados de Florida, **identificar los 3 condados con mejor potencial de inversión** y sustentar la recomendación con datos.

El reto no era solo construir un dashboard, sino traducir métricas de mercado (demanda, oferta, crecimiento poblacional, criminalidad) en una decisión de negocio accionable.

## 🎯 Objetivo

Determinar qué condados —y a nivel más granular, qué ciudades dentro de Marion, Citrus y Polk— presentan mejor equilibrio entre demanda de mercado, capacidad de oferta, crecimiento poblacional/laboral y riesgo (criminalidad), para priorizar decisiones de inversión.

## 🧠 Metodología

1. **Ingesta de datos**: dataset con población, crecimiento laboral, tasa de criminalidad, demanda y oferta total por condado y por ciudad.
2. **Modelado en Power BI**: tabla única (`Tabla1`) con medidas DAX calculadas para agregaciones y ratios.
3. **Métricas derivadas**: además de las medidas base, se construyó un *Net Market Opportunity Index* y un ranking de oportunidad por condado.
4. **Reporte multi-página**:
   - Overview de población y distribución
   - Análisis de ratios de oferta/demanda por condado
   - Análisis comparativo (oferta/demanda/ratio) por condado y por población
   - Drill-down a nivel ciudad dentro de Marion, Citrus y Polk

## 📊 KPIs clave

| Métrica | Definición (DAX) | Qué decisión habilita |
|---|---|---|
| **Total_Demand** | `SUM(Tabla1[Total Demand])` | Tamaño real del mercado en la zona |
| **Total_Supply** | `SUM(Tabla1[Total Supply])` | Capacidad disponible / saturación del mercado |
| **Total_Ratio** | `Total_Demand / Total_Supply` | >1 = oportunidad (demanda excede oferta) · ≈1 = equilibrio · <1 = sobreoferta |
| **average_population** | `AVERAGE(Tabla1[Population Size])` | Escala demográfica para comparar densidad y potencial de mercado |
| **Net Market Opportunity Index** | Índice normalizado derivado del ratio | Ranking objetivo de qué condados priorizar |

## 🔎 Hallazgos clave

- El mercado agregado muestra **sobreoferta**: demanda total ≈15M vs. oferta total ≈18M (ratio global de **0.81**), con un ratio promedio de mercado de **0.87**.
- **Lee County** concentra la mayor población (99.2K) pero su ratio (0.83) indica un mercado ya saturado — no es el mejor punto de entrada pese a su tamaño.
- Al rankear por *Net Market Opportunity Index*, **Citrus** y **Marion County** son los únicos con índice positivo (+0.03), seguidos de **Polk** y **Volusia** en equilibrio (0.00). El resto muestra índice negativo (sobreoferta).
- A nivel ciudad (dentro de Marion/Citrus/Polk), **Citrus Springs** destaca con un ratio de **2.16** — demanda muy por encima de la oferta disponible, la señal más fuerte de oportunidad en todo el dataset.
- El crecimiento laboral es relativamente parejo a nivel ciudad (~29%) pero varía mucho más a nivel condado (14.9%–44.1%), lo que sugiere que el análisis a nivel ciudad da una imagen más estable para decisiones de corto plazo.
- La criminalidad no es uniforme dentro de un mismo condado: **Inverness** muestra un pico de 9.51% frente a un promedio cercano a 3.5–4% en las demás ciudades — un factor de riesgo a monitorear aunque su ratio de mercado sea favorable.

## 🏆 Recomendación — Top 3 condados para invertir

1. **Citrus County** — mejor posición en el ranking de oportunidad, y a nivel de ciudad (Citrus Springs) presenta el ratio demanda/oferta más alto de todo el dataset.
2. **Marion County** — empatado en el top del índice de oportunidad, con tasa de criminalidad por debajo del promedio (3.62%), lo que reduce el riesgo relativo de la inversión.
3. **Polk County** — mercado en equilibrio (índice neutro) pero con base poblacional sólida (35.5K), lo que ofrece un perfil de riesgo más conservador frente a los condados en sobreoferta clara.

> Lee County, pese a ser el mercado más grande, se descarta como prioridad por estar saturado (ratio <1 y sin margen de crecimiento evidente en el índice).

## 🖥️ Vista previa del dashboard

*(agrega aquí 2–3 capturas o un GIF corto desde `2.Screenshots/`, por ejemplo la página de Overview y la de ranking por condado)*

## ⚙️ Stack técnico

- **Power BI Desktop** — modelado, DAX y visualización
- **DAX** — medidas de agregación y ratios de mercado
- Dataset fuente en Excel

## 📁 Estructura del repositorio

```
├── 1.Dashboard/   → archivo .pbix
├── 2.Screenshots/ → capturas del reporte
├── 3.Dax/         → medidas DAX documentadas
└── 4.Data/        → dataset fuente
```

## 🚀 Cómo reproducirlo

1. Clona el repositorio
2. Abre `1.Dashboard/Dashboard_Florida.pbix` en Power BI Desktop
3. Actualiza el origen de datos apuntando al archivo en `4.Data/`
4. Navega entre las páginas del reporte para explorar cada nivel de análisis (condado → ciudad)

## ⚠️ Limitaciones y próximos pasos

- El análisis es una **foto estática**, no una serie de tiempo — un siguiente paso natural sería automatizar la actualización de datos (Python + API, o Power Automate) para monitorear cómo evoluciona el índice de oportunidad mes a mes.
- Se podría enriquecer el modelo con variables adicionales (costo de vida, precio promedio de propiedad) para pasar de un índice de oportunidad a una proyección de ROI.
- Un pipeline de validación de datos en Python antes de la carga a Power BI daría mayor trazabilidad y robustez al modelo.

## 📬 Contacto

*(tu nombre · LinkedIn · GitHub)*
