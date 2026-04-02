# 🇲🇼 Malawi International Merchandise Trade Statistics — Data Mining Project

> **A four-module KNIME data mining analysis of Malawi's trade economy (2022–2025)**  
> *Time Series Forecasting · Commodity Clustering · Anomaly Detection · Association Rule Mining*

[![Live Dashboard](https://img.shields.io/badge/Live%20Dashboard-View%20Results-C9A84C?style=for-the-badge)](https://katema-philip.github.io/malawi-trade-mining/)
[![KNIME](https://img.shields.io/badge/Tool-KNIME%20Analytics%20Platform-orange?style=for-the-badge)](https://www.knime.com/)
[![Dataset](https://img.shields.io/badge/Source-Malawi%20NSO-blue?style=for-the-badge)](https://www.nsomalawi.mw/)

---

## 📊 Project Overview

This project applies four complementary data mining techniques to **3,000 records** of Malawi's International Merchandise Trade Statistics spanning **January 2022 – December 2025**, covering **25 import** and **25 export** commodity categories.

| Metric | Value |
|---|---|
| Total Imports (2022–2025) | **$13.1B USD** |
| Total Exports (2022–2025) | **$3.8B USD** |
| Cumulative Trade Deficit | **$9.3B USD** |
| Export Coverage Ratio | **28.7%** |
| Tobacco Share of Exports | **50.7%** |

---

## 🔬 Four Mining Modules

### Module 1 — Time Series Forecasting
Predicts monthly import and export values using lag features (lag-1, lag-3, lag-12) and cyclical seasonal encoding (sin/cos transformations). Compares Linear Regression vs Random Forest Regression.

| Model | Imports R² | Exports R² | Import MAPE | Export MAPE |
|---|---|---|---|---|
| Linear Regression | 0.546 | 0.513 | 8.7% | 32.0% |
| **Random Forest** | **0.721** | **0.638** | **7.2%** | **24.6%** |

**Key Finding:** Random Forest outperforms Linear Regression on all metrics. Exports are harder to forecast than imports due to Tobacco's auction season spike.

---

### Module 2 — Commodity Clustering
Clusters 25 export commodities by 48-month trade behaviour using k-Means and Hierarchical Clustering with PCA dimensionality reduction.

| Cluster | Commodities | Interpretation |
|---|---|---|
| Dominant Outlier | Tobacco, Other Exports | Behaviourally isolated — algorithmically confirmed |
| Mid-Tier Agricultural | Tea, Pulses, Groundnuts, Macadamia, Soya Beans | Best diversification candidates |
| Low-Value Mixed | Natural Rubber, Plastics, Scrap Metal, Sugar | Low volume, moderate variability |
| Marginal Mass | 14 remaining commodities | Undifferentiated — minimal trade impact |

**Key Finding:** Both algorithms assign all 25 commodities to identical clusters (100% agreement), confirming Tobacco's behavioural uniqueness without being provided its value.

---

### Module 4 — Anomaly Detection
Applies a rolling Z-Score method (12-month window) to flag statistically abnormal trade periods across imports and exports.

| Flag Type | Count | Primary Driver |
|---|---|---|
| Anomaly High | 2 | Aug 2024 tobacco record; Jan 2026 structural import surge |
| Anomaly Low | 1 | Apr 2023 Cyclone Freddy forex crisis |
| Elevated High | 13 | Post-Freddy reconstruction; El Niño food imports; pre-devaluation exports |
| Elevated Low | 13 | Post-devaluation compression; El Niño crop failure; Tanzania dispute |

**Four Macro Shocks Identified:**
1. 🌀 **Cyclone Freddy** — March 2023 · $680M economic damage
2. 💱 **44% Kwacha Devaluation** — November 2023
3. 🌵 **El Niño Drought** — January–September 2024 · 4.2M food insecure
4. 🚧 **Tanzania Trade Dispute** — March 2025 · transit route closed

**Key Finding:** The January 2026 import Anomaly High (Z=2.03, $390.7M) is not an isolated event — it is the structural capstone of a worsening pattern. World Bank: current account deficit near 20% of GDP, forex reserves below 1 month of imports.

---

### Module 5 — Association Rule Mining
Discovers commodity co-movement patterns using pairwise Apriori logic (Min Support: 0.3, Min Confidence: 0.6, Min Lift: 1.2).

**Import Rules — Top Associations (Lift 1.5):**
- Nuclear Reactors/Boilers ↔ Glass and Glassware *(construction cluster)*
- Electrical Machinery ↔ Plastics *(manufacturing cluster)*
- Animal/Vegetable Fats ↔ Vehicles *(discretionary/forex cluster)*

**Export Rules — Top Association (Lift 1.583):**
- **Spices ↔ Cotton** — strongest rule in the entire dataset (agro-ecological co-location)

**Key Finding:** Import co-movement is driven by **forex availability** (all categories respond to one binding constraint). Export co-movement is driven by **climate and agricultural geography** (harvest calendar + shared growing regions). This asymmetry — nature governing exports, finance governing imports — is the most succinct summary of Malawi's structural trade challenge.

---

## 📁 Repository Structure

```
malawi-trade-mining/
│
├── data/
│   ├── Malawi_Imports.csv              ← 1,500 rows · 25 commodities
│   ├── Malawi_Exports.csv              ← 1,500 rows · 25 commodities
│   └── Malawi_Trade_Combined.csv       ← 3,000 rows · combined with Trade_Type
│
├── knime/
│   └── Malawi_Trade_Mining.knwf        ← KNIME workflow export (all 4 modules)
│
├── dashboard/
│   └── Malawi_DataMining_Dashboard.html ← Interactive results dashboard (Plotly.js)
│
├── report/
│   └── Malawi_Data_Mining_Report.docx  ← Full written report (Word)
│
└── README.md
```

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| KNIME Analytics Platform | Data mining workflow (all 4 modules) |
| Python (scikit-learn) | Association Rule Mining via KNIME Python Script node |
| Plotly.js | Interactive results dashboard |
| Pandas / NumPy | Data preprocessing |

**KNIME Nodes Used:** CSV Reader · GroupBy · Sorter · Lag Column · Math Formula · Row Filter · Partitioning · Linear Regression Learner · Random Forest Learner (Regression) · Numeric Scorer · PCA · Normalizer · Pivoting · k-Means · Hierarchical Clustering · Moving Aggregation · Rule Engine · Python Script · Line Plot · Scatter Plot

---

## 📈 Key Results Summary

> *"Malawi's trade economy is caught between two binding constraints: export revenue captive to a single commodity (Tobacco) whose global demand is declining, and import capacity captive to a chronic foreign exchange shortage that the export concentration perpetuates. Breaking this cycle requires simultaneous action on export diversification and macroeconomic stabilisation."*

---

## 👤 Author

**Philip Katema**  
MS Data Analytics in Business · Seattle Pacific University  
6+ years experience in data analysis and management  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat-square)](https://linkedin.com/in/philip-katema)

---

## 📄 License

This project is for educational and portfolio purposes. Dataset sourced from the Malawi National Statistics Office (NSO).
