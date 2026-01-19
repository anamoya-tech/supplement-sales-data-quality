# Data Quality & Revenue Audit — Supplement Sales (Google Sheets)

## Project Overview
This project focuses on **data quality assessment, data cleaning, and business validation** using a real-world e-commerce sales dataset related to nutritional supplements.

The objective is not only to clean the data, but to **prove data readiness for BI** and to **validate key business metrics**, identifying patterns that are not immediately visible in the raw data.

The entire workflow is implemented in **Google Sheets**, following a reproducible, pipeline-style approach similar to SQL transformations.

---

## Project Objectives (SMART)

### 1. Data Quality Assessment
- Profile the raw dataset to detect:
  - Missing values
  - Numeric fields stored as text
  - Non-reporting-ready date formats
  - Duplicate records
- Quantify data quality using clear **BEFORE vs AFTER KPIs**.

### 2. Data Cleaning and Standardization
- Convert all numeric fields to proper numeric types.
- Normalize date formats and derive reporting periods.
- Standardize categorical fields (location, platform, category).
- Preserve the raw dataset without any modifications.

### 3. Business Validation
- Verify whether reported revenue follows the expected formula:
Units Sold × Price × (1 − Discount)
- Analyze discrepancies to determine whether they represent **data quality issues or business logic**.

---

## Dataset
- **Source:** Kaggle — Supplement Sales Dataset  
- **Rows:** 4,385  
- **Columns:** 10  
- **Granularity:** Weekly sales transactions  

**Main fields**
- Date  
- Product Name  
- Category  
- Units Sold  
- Price  
- Revenue  
- Discount  
- Units Returned  
- Location  
- Platform  

---

## Data Profiling (BEFORE — Raw Data)

### Key Findings
- **Missing values:** 0% across all columns.
- **Numeric fields stored as text (locale-related):**
- Price: 91.4%
- Revenue: 70.4%
- **Dates:** Stored in ISO format (`YYYY-MM-DD`), not directly usable for reporting under ES locale.
- **Duplicates:** 0 detected using the composite key:
Date + Product Name + Location + Platform

### Cardinality (Unique Values)
- Location: 3  
- Platform: 3  
- Category: 10  
- Product Name: 16  

---

## Cleaning Rules Applied

All transformations are applied **without modifying the raw data**.

### Numeric Type Enforcement
New fields created:
- `units_sold_clean`
- `price_clean`
- `revenue_clean`
- `discount_clean`
- `units_returned_clean`

Invalid conversions are explicitly flagged as `CHECK_NUM`.

---

### Revenue Audit (Critical Validation Step)
The original `Revenue` field is not assumed to be correct by default.

New metrics created:
- `revenue_recalc`
- `revenue_diff`
- `ratio = revenue_clean / revenue_recalc`
- `revenue_uplift = ratio − 1`

This enables full validation of reported revenue against a transparent expected model.

---

### Date Normalization
- `date_clean`: true date type
- `month_clean`: reporting period in `YYYY-MM` format

---

### Categorical Standardization
- `location_clean`: trimmed and uppercased
- `platform_clean`: trimmed and uppercased
- `category_clean`: standardized naming conventions

---

### Quality Flags
- `dup_flag`: duplicate detection
- `data_error_flag`: technical data quality issues
- `business_alert_flag`: business-rule inconsistencies
- `issue_flag`: combined quality indicator

---

## Dashboard Summary (AFTER — Clean Data)

### Data Quality KPIs
- **Total rows:** 4,385  
- **Data errors:** 0  
- **Duplicates:** 0  
- **Numeric fields valid:** 100%  
- **Valid dates:** 100%  

### Revenue Validation KPIs
- **Average revenue uplift:** 14.99%  
- **Median revenue uplift:** 13.64%  

---

## Key Business Insight

Reported revenue is **systematically higher** than the revenue expected after discounts.

- Revenue uplift typically ranges between **3% and 33%**.
- The uplift is:
- Consistent over time
- Consistent across platforms
- This strongly suggests the presence of **fees, taxes, or platform margins**, rather than data quality errors.

The conclusion is supported by:
- Monthly comparison of reported vs recalculated revenue
- Monthly average uplift trends
- Platform-level uplift comparison

---

## Project Structure

- **RAW_Supplement_Sales_Weekly_Expanded**  
Original dataset, preserved intact.

- **clean_data**  
Fully cleaned, BI-ready dataset with validation metrics and flags.

- **cleaning_log**  
Detailed log documenting every transformation, rule applied, and its impact.

- **data_quality_dashboard**  
Final dashboard including:
- BEFORE vs AFTER quality KPIs
- Revenue audit visualizations
- Time-based and platform-based insights

---

## Skills Demonstrated
- Data profiling and quality assessment
- Locale-aware data cleaning
- Reproducible transformation pipelines
- Revenue and metric validation
- Analytical storytelling through dashboards

---

## Next Step (Planned)
- **Revenue uplift by Country × Platform**
- Pivot table and heatmap analysis
- Identification of regional pricing or fee differences

---

## Status
Project complete up to the **data quality and revenue audit phase**.  
Ready for portfolio presentation and interview discussion.
