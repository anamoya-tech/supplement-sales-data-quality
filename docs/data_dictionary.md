# Data Dictionary — Clean Data

This document describes the main fields available in the `clean_data` table, which represents the final, BI-ready output of the project.

Only derived and validated fields are documented here.

---

## Identifiers & Dates

* **date_clean**
  Cleaned transaction date in true date format.

* **month_clean**
  Reporting period derived from `date_clean`, formatted as `YYYY-MM`.

---

## Sales & Pricing

* **units_sold_clean**
  Number of units sold, converted to numeric.
  Invalid values are flagged as `CHECK_NUM`.

* **price_clean**
  Unit price converted to numeric, adjusted for locale formatting.

* **discount_clean**
  Discount rate applied to the sale (range 0–1).

* **units_returned_clean**
  Number of returned units, converted to numeric.

---

## Revenue Validation

* **revenue_clean**
  Reported revenue converted to numeric.

* **revenue_recalc**
  Expected revenue calculated as:

  ```
  units_sold_clean × price_clean × (1 − discount_clean)
  ```

* **revenue_diff**
  Difference between reported and recalculated revenue:

  ```
  revenue_clean − revenue_recalc
  ```

* **revenue_uplift**
  Relative difference between reported and expected revenue:

  ```
  (revenue_clean / revenue_recalc) − 1
  ```

---

## Categorical Fields

* **location_clean**
  Standardized country/location value (trimmed and uppercased).

* **platform_clean**
  Standardized sales platform (trimmed and uppercased).

* **category_clean**
  Standardized product category.

---

## Quality Flags

* **dup_flag**
  Indicates potential duplicate records based on the composite key:
  `Date + Product Name + Location + Platform`.

* **data_error_flag**
  TRUE if any technical data quality issue is detected (e.g. invalid numeric or date).

* **business_alert_flag**
  TRUE if business-rule inconsistencies are detected during revenue validation.

* **issue_flag**
  Master flag indicating any data quality or business validation issue.

---

## Notes

* The raw dataset remains unchanged.
* All fields in `clean_data` are derived through reproducible formulas.
* The table is designed to be directly usable in BI tools or downstream analysis.

