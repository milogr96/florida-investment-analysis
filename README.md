🇪🇸 [Versión en español](./README.es.md) · 🇬🇧 English version (this page)

# 🏙️ Florida Investment Analysis

Real estate investment opportunity analysis across Florida counties, combining population, job growth, crime rate, and supply/demand balance to identify the strongest entry points.

**[📄 View report (PDF)](./2.Screenshots) · [📊 Download .pbix](./1.Dashboard) · [🧮 DAX Measures](./3.Dax)**

---

## 📌 Project Context

This project was built as part of a technical assessment on real estate investment analysis. The business objective: given a dataset with demographic and market indicators across several Florida counties, **identify the top 3 counties with the strongest investment potential** and back the recommendation with data.

The challenge wasn't just building a dashboard — it was translating market metrics (demand, supply, population growth, crime) into an actionable business decision.

## 🎯 Objective

Determine which counties — and at a more granular level, which cities within Marion, Citrus, and Polk — show the best balance between market demand, supply capacity, population/job growth, and risk (crime rate), in order to prioritize investment decisions.

## 🧠 Methodology

1. **Data ingestion**: dataset with population, job growth, crime rate, total demand, and total supply by county and by city.
2. **Power BI modeling**: single table (`Tabla1`) with DAX measures for aggregations and ratios.
3. **Derived metrics**: on top of the base measures, a *Net Market Opportunity Index* and an opportunity ranking by county were built.
4. **Multi-page report**:
   - Population size and distribution overview
   - Supply/demand ratio analysis by county
   - Comparative analysis (supply/demand/ratio) by county and by population
   - City-level drill-down within Marion, Citrus, and Polk

## 📊 Key KPIs

| Metric | Definition (DAX) | Business decision it enables |
|---|---|---|
| **Total_Demand** | `SUM(Tabla1[Total Demand])` | Actual market size in the area |
| **Total_Supply** | `SUM(Tabla1[Total Supply])` | Available capacity / market saturation |
| **Total_Ratio** | `Total_Demand / Total_Supply` | >1 = opportunity (demand exceeds supply) · ≈1 = equilibrium · <1 = oversupply |
| **average_population** | `AVERAGE(Tabla1[Population Size])` | Demographic scale to compare density and market potential |
| **Net Market Opportunity Index** | Normalized index derived from the ratio | Objective ranking of which counties to prioritize |

## 🔎 Key Insights

- The aggregate market shows **oversupply**: total demand ≈15M vs. total supply ≈18M (overall ratio of **0.81**), with a market-wide average ratio of **0.87**.
  
- **Lee County** has by far the largest population (99.2K) but its ratio (0.83) points to an already-saturated market — not the best entry point despite its size.
  
- Ranking by *Net Market Opportunity Index*, **Citrus** and **Marion County** are the only ones with a positive index (+0.03), followed by **Polk** and **Volusia** at equilibrium (0.00). The rest show a negative index (oversupply).
  
- At the city level (within Marion/Citrus/Polk), **Citrus Springs** stands out with a ratio of **2.16** — demand far above available supply, the strongest opportunity signal in the entire dataset.
  
- Job growth is relatively even at the city level (~29%) but varies much more at the county level (14.9%–44.1%), suggesting city-level analysis gives a more stable picture for short-term decisions.
  
- Crime rate isn't uniform within the same county: **Inverness** shows a spike of 9.51% versus an average close to 3.5–4% in the other cities — a risk factor worth monitoring even when its market ratio is favorable.

## 🏆 Recommendation — Top 3 Counties to Invest In

1. **Citrus County** — top position in the opportunity ranking, and at the city level (Citrus Springs) shows the highest demand/supply ratio in the entire dataset.
   
2. **Marion County** — tied for the top opportunity index, with a crime rate below average (3.62%), which lowers the relative risk of the investment.
   
3. **Polk County** — market at equilibrium (neutral index) but with a solid population base (35.5K), offering a more conservative risk profile compared to counties in clear oversupply.

> Lee County, despite being the largest market, is ruled out as a priority since it's saturated (ratio <1 with no clear growth margin in the index).

## 🖥️ Dashboard Preview


## ⚙️ Tech Stack

- **Power BI Desktop** — modeling, DAX, and visualization
- **DAX** — aggregation measures and market ratios
- Source dataset in Excel

## 📁 Repository Structure

```
├── 1.Dashboard/   → .pbix file
├── 2.Screenshots/ → report screenshots
├── 3.Dax/         → documented DAX measures
└── 4.Data/        → source dataset
```

## 🚀 How to Reproduce

1. Clone the repository
2. Open `1.Dashboard/Dashboard_Florida.pbix` in Power BI Desktop
3. Refresh the data source pointing to the file in `4.Data/`
4. Navigate through the report pages to explore each level of analysis (county → city)

## ⚠️ Limitations & Next Steps

- The analysis is a **static snapshot**, not a time series a natural next step would be automating the data refresh (Python + API, or Power Automate) to track how the opportunity index evolves month over month.
  
- The model could be enriched with additional variables (cost of living, average property price) to move from an opportunity index to an actual ROI projection.
  
- A Python-based data validation pipeline before loading into Power BI would add more traceability and robustness to the model.

