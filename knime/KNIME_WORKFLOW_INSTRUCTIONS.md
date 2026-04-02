# KNIME Workflow

## How to Import

1. Open KNIME Analytics Platform
2. Go to **File → Import KNIME Workflow**
3. Select the `.knwf` file from this folder
4. Click **Finish**

## Workflow Structure

The workflow contains four annotated modules:

| Module | Label in KNIME | Input |
|---|---|---|
| 1 | TIME SERIES FORECASTING | Malawi_Trade_Combined.csv |
| 2 | COMMODITY CLUSTERING | Malawi_Exports.csv |
| 4 | Z-SCORE ANOMALY DETECTION | Malawi_Imports.csv + Malawi_Exports.csv |
| 5 | ASSOCIATION RULE MINING | Malawi_Imports.csv + Malawi_Exports.csv |

## Required KNIME Extensions

Install via **Help → Install New Software → KNIME Extensions**:

- KNIME Machine Learning Extension (Random Forest, k-Means)
- KNIME Statistics Extension
- KNIME Time Series Analysis (Lag Column, Moving Aggregation)
- KNIME Python Integration

## Python Environment

The Association Rule Mining module (Module 5) uses the Python Script node.
Required packages:
```
pip install pandas numpy scikit-learn
```

## Notes

- Export the workflow from KNIME via **File → Export KNIME Workflow → .knwf**
- Place the exported `.knwf` file in this folder before uploading to GitHub
- Data files are in `/data` — update CSV Reader node paths if needed after import
