# Data Quality & Revenue Audit — Supplement Sales (Google Sheets)

## Overview
This project focuses on **data quality assessment and revenue validation** using a real-world e-commerce sales dataset related to nutritional supplements.

The goal is to ensure the data is **BI-ready** and to validate whether reported revenue follows the expected business logic.

All work is implemented in **Google Sheets**, using a reproducible pipeline approach (raw → clean → aggregate → dashboard).

---

## Objectives
- Assess data quality (formats, dates, duplicates)
- Clean and standardize the dataset without modifying raw data
- Validate reported revenue against an expected calculation
- Identify and explain meaningful business patterns

---

## Dataset
- **Source:** Kaggle — Supplement Sales Dataset  
- **Rows:** 4,385  
- **Granularity:** Weekly sales transactions  

Key fields include Date, Product, Units Sold, Price, Revenue, Discount, Location, and Platform.

---

## Data Quality (BEFORE → AFTER)
- Missing values: **0%**
- Numeric fields stored as text (raw):
  - Price: 91.4%
  - Revenue: 70.4%
- Duplicates: **0** (Date + Product + Location + Platform)

After cleaning:
- Numeric fields valid: **100%**
- Dates normalized: **100%**
- Dataset ready for reporting

---

## Revenue Validation
Reported revenue was audited using the expected formula:
Units Sold × Price × (1 − Discount)

New metrics were created:
- Recalculated revenue
- Revenue difference
- Revenue uplift = (reported / expected) − 1

---

## Key Insight
Reported revenue is **systematically higher** than expected after discounts.

- **Average uplift:** ~15%
- **Median uplift:** ~14%
- Pattern is stable over time, platforms, and countries

This suggests **undocumented business rules** (fees, taxes, or platform margins) rather than data quality errors.

---

## Dashboard
The final dashboard includes:
- Data quality KPIs (BEFORE vs AFTER)
- Reported vs recalculated revenue (monthly)
- Average revenue uplift by platform
- Revenue uplift trends over time
- Country × platform uplift heatmap

---

## Skills Demonstrated
- Data profiling and cleaning
- Revenue and metric validation
- Reproducible analysis in Google Sheets
- Analytical interpretation and communication

---

## Next Step
Validate the observed revenue uplift with Finance or Operations teams to document the official revenue calculation logic.

---

## Status
Project completed and ready for portfolio and interview presentation.

