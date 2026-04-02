# Data Files

## Source
Malawi National Statistics Office (NSO) — International Merchandise Trade Statistics

## Files

### Malawi_Imports.csv
- **Rows:** 1,500
- **Period:** January 2022 – January 2026 (partial)
- **Columns:** Year, Month #, Month, Commodity, Unit, Quantity, Amount_USD, Trade_Type
- **Commodities:** 25 import categories including Petrol, Diesel, Fertilizer, Machinery, Pharmaceuticals

### Malawi_Exports.csv
- **Rows:** 1,500
- **Period:** January 2022 – January 2026 (partial)
- **Columns:** Year, Month #, Month, Commodity, Unit, Quantity, Amount_USD, Trade_Type
- **Commodities:** 25 export categories including Tobacco, Tea, Pulses, Groundnuts, Macadamia Nuts

### Malawi_Trade_Combined.csv
- **Rows:** 3,000 (Imports + Exports combined)
- **Columns:** Same as above
- **Trade_Type column:** "Import" or "Export" — use this to filter in analysis

## Key Statistics

| Metric | Value |
|---|---|
| Total Imports (2022–2025) | $13.1B USD |
| Total Exports (2022–2025) | $3.8B USD |
| Trade Deficit (2022–2025) | $9.3B USD |
| Export Coverage Ratio | 28.7% |
| Tobacco Share of Exports | 50.7% |

## Notes
- 60 null values in the `Unit` column are expected — some commodities report value only without quantity
- 2026 data contains only January — filter to `Year <= 2025` for full-year analysis
- `Amount_USD` is the primary analysis column — `Quantity` varies by unit type across commodities
