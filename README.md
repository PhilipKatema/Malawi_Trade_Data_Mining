# 🇲🇼 Malawi International Merchandise Trade Statistics - Data Mining Project

> **A four-module KNIME data mining analysis of Malawi's trade economy (2022-2025)**  
> *Time Series Forecasting · Commodity Clustering · Anomaly Detection · Association Rule Mining*

[![Live Dashboard](https://img.shields.io/badge/Live%20Dashboard-View%20Results-C9A84C?style=for-the-badge)](https://philipkatema.github.io/Portfolio/post/malawi_trade_profile/Malawi_Trade_mining_dashboard)
[![KNIME](https://img.shields.io/badge/Tool-KNIME%20Analytics%20Platform-orange?style=for-the-badge)](https://www.knime.com/)
[![Dataset](https://img.shields.io/badge/Source-Malawi%20NSO-blue?style=for-the-badge)](https://www.nsomalawi.mw/)

---

## 📊 Project Overview

This project applies four complementary data mining techniques to **3,000 records** of Malawi's International Merchandise Trade Statistics spanning **January 2022 - December 2025**, covering **25 import** and **25 export** commodity categories.

| Metric | Value |
|---|---|
| Total Imports (2022-2025) | **$13.1B USD** |
| Total Exports (2022-2025) | **$3.8B USD** |
| Cumulative Trade Deficit | **$9.3B USD** |
| Export Coverage Ratio | **28.7%** |
| Tobacco Share of Exports | **50.7%** |

---

## 🔬 Four Mining Modules

### Module 1 - Time Series Forecasting
Predicts monthly import and export values using lag features (lag-1, lag-3, lag-12) and cyclical seasonal encoding (sin/cos transformations). Compares Linear Regression vs Random Forest Regression on a temporally ordered 80/20 train-test split.

| Model | Imports R² | Exports R² | Import MAPE | Export MAPE |
|---|---|---|---|---|
| Linear Regression | 0.546 | 0.513 | 8.7% | 32.0% |
| **Random Forest** | **0.721** | **0.638** | **7.2%** | **24.6%** |

**Key Finding:** Random Forest outperforms Linear Regression on all metrics. Export forecasting is harder than import forecasting - Tobacco's auction season creates spikes that are difficult to predict from lag features alone without commodity-level price data. Incorporating external shock indicators is identified as a logical next step for future modelling work.

---

### Module 2 - Commodity Clustering
Clusters 25 export commodities by 48-month trade behaviour using k-Means and Hierarchical Clustering (Average linkage) with Min-Max normalisation and PCA dimensionality reduction.

| Cluster | Commodities | Interpretation |
|---|---|---|
| Dominant Outlier | Tobacco, Other Exports | Behaviourally isolated - confirmed by both algorithms independently |
| Mid-Tier Agricultural | Tea, Pulses, Groundnuts, Macadamia, Soya Beans | Distinct seasonal patterns - most viable diversification candidates based on cluster separation |
| Low-Value Mixed | Natural Rubber, Plastics, Scrap Metal, Sugar | Low volume, moderate variability |
| Marginal Mass | 14 remaining commodities | Near-identical PCA coordinates - undifferentiated trade behaviour |

**Key Finding:** Both algorithms assign all 25 commodities to identical clusters (100% agreement). Tobacco's behavioural uniqueness is confirmed algorithmically without the algorithms being provided its value - its seasonal auction cycle and scale create a trade signature no other commodity in the dataset replicates.

---

### Module 4 - Anomaly Detection
Applies a rolling Z-Score method (12-month preceding window) to flag statistically abnormal trade periods. A four-tier classification is used: Anomaly (|Z| > 2.0), Elevated High, Normal, Elevated Low.

| Flag | Count | Primary Events |
|---|---|---|
| Anomaly High | 2 | Aug 2024 tobacco season record; Jan 2026 structural import surge |
| Anomaly Low | 1 | Apr 2023 post-Cyclone Freddy forex crisis |
| Elevated High | 13 | Post-Freddy humanitarian response; El Niño food imports; kwacha devaluation period |
| Elevated Low | 13 | Post-devaluation import compression; El Niño crop failure; Tanzania trade dispute |

**Four Macro Shocks Identified:**
1. 🌀 **Cyclone Freddy** - March 2023 · $680M economic damage (UNDRR, 2024)
2. 💱 **44% Kwacha Devaluation** - November 2023 (Bloomberg, 2023)
3. 🌵 **El Niño Drought** - 2024 · state of disaster declared in 23 of 28 districts (OCHA, 2024)
4. 🚧 **Tanzania Trade Dispute** - March 2025 · transit route closed, fertilizer exports suspended (World Bank, 2025)

**Key Finding:** The January 2026 import Anomaly High (Z=2.03, $390.7M against a rolling mean of $314.8M) is not an isolated event - it exceeds an already-elevated 2025 baseline, consistent with a pattern of structural deterioration. World Bank (2025) confirms Malawi's current account deficit near 20% of GDP with forex reserves below one month of imports.

---

### Module 5 - Association Rule Mining
Discovers commodity co-movement patterns using pairwise Apriori logic (Min Support: 0.3, Min Confidence: 0.6, Min Lift: 1.2), applied separately to imports and exports.

**Import Rules - Top Associations (Lift 1.5):**
- Nuclear Reactors/Boilers ↔ Glass and Glassware *(infrastructure/rebuilding periods)*
- Electrical Machinery ↔ Plastics *(shared procurement cycles for industrial inputs)*
- Animal/Vegetable Fats ↔ Vehicles *(co-movement consistent with forex availability)*

**Export Rules - Strongest Association (Lift 1.583):**
- **Spices ↔ Cotton** - strongest rule in the entire dataset, consistent with agro-ecological co-movement

**Key Finding:** Import co-movement is consistent with a single binding constraint - foreign exchange availability - with all categories peaking and dropping together regardless of sector. Export co-movement is consistent with seasonal calendars and likely shared growing conditions. This asymmetry is the most succinct summary of Malawi's structural trade challenge as observed in this dataset.

---

## 📁 Repository Structure

```
malawi-trade-mining/
│
├── data/
│   ├── README.md                       ← Column reference + key statistics
│   ├── Malawi_Imports.csv              ← 1,500 rows · 25 commodities
│   ├── Malawi_Exports.csv              ← 1,500 rows · 25 commodities
│   └── Malawi_Trade_Combined.csv       ← 3,000 rows · combined with Trade_Type
│
├── knime/
│   └── KNIME_WORKFLOW_INSTRUCTIONS.md  ← Import guide + required extensions
│
├── report/
│   └── Malawi_Data_Mining_Report_v2.docx ← Full written report (corrected v2)
│
├── docs/
│   ├── index.html                      ← Interactive results dashboard (Plotly.js)
│   └── _config.yml                     ← GitHub Pages config
│
├── .github/
│   └── deploy.yml                      ← GitHub Actions auto-deploy workflow
│
├── README.md
├── LICENSE
└── .gitignore
```

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| KNIME Analytics Platform | Data mining workflow - all 4 modules |
| Python (scikit-learn, pandas) | Association Rule Mining via KNIME Python Script node |
| Plotly.js | Interactive results dashboard |

**KNIME Nodes Used:** CSV Reader · GroupBy · Sorter · Lag Column · Math Formula · Row Filter · Partitioning · Linear Regression Learner · Random Forest Learner (Regression) · Numeric Scorer · PCA · Normalizer · Pivoting · k-Means · Hierarchical Clustering · Moving Aggregation · Rule Engine · Python Script · Line Plot · Scatter Plot

---

## 📚 Key Sources

| Source | Used For |
|---|---|
| Malawi NSO | Primary dataset |
| World Bank Malawi Economic Monitor (2025) | Current account deficit, forex reserves |
| UNDRR Southern Africa Cyclone Analysis (2024) | Cyclone Freddy damage figures |
| OCHA Malawi Drought Flash Appeal (2024) | El Niño disaster declaration, food insecurity figures |
| Bloomberg (2023) | 44% kwacha devaluation figures |
| FEWS NET (2023) | Post-Freddy forex reserve levels |
| IFPRI (2024) | El Niño food import recommendations |
| African Development Bank (2024) | Devaluation economic impact |
| Tobacco Journal International (2025) | Tobacco demand trajectory |

---

## 👤 Author

**Philip Katema**  
MS Data Analytics in Business · Seattle Pacific University  
6+ years experience in data analysis and management

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat-square)](linkedin.com/in/phillip-katema-419632b3/)

---

## 📄 License

MIT License. Dataset sourced from the Malawi National Statistics Office (NSO). See LICENSE for full terms.
