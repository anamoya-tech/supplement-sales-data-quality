# Cleaning Log

This document records the main data cleaning and validation steps applied during the project.
All transformations were performed on derived tables in Google Sheets, while the raw dataset was kept intact.

---

## Summary

* **Raw data modified:** No
* **Cleaning approach:** Reproducible, formula-based transformations
* **Scope:** Data quality, standardization, and revenue validation

---

## Cleaning Steps

| Step | Field(s)                   | Issue Type              | Rule Applied                                          | Before                   | After                  | Notes                                |
| ---: | -------------------------- | ----------------------- | ----------------------------------------------------- | ------------------------ | ---------------------- | ------------------------------------ |
|    1 | Dataset structure          | Process control         | Raw data kept intact, clean_data derived via formulas | Single editable table    | Raw + clean separation | Ensures traceability                 |
|    2 | Price, Revenue             | Numeric format (locale) | Replace decimal separator and convert to numeric      | Text values (e.g. 31.98) | Numeric values         | ES locale issue                      |
|    3 | Units Sold, Units Returned | Numeric validation      | Convert to numeric and flag errors                    | Mixed types              | Numeric or CHECK_NUM   | Prevents silent errors               |
|    4 | Discount                   | Numeric validation      | Convert to numeric rate (0–1)                         | Text / numeric mix       | Numeric or CHECK_NUM   | Used for revenue audit               |
|    5 | Date                       | Date format             | Parse ISO date to true date type                      | Text (YYYY-MM-DD)        | Date type              | Reporting-ready                      |
|    6 | Date                       | Derivation              | Create reporting month field                          | No month field           | month_clean (YYYY-MM)  | Used for trends                      |
|    7 | Location                   | Text standardization    | TRIM + UPPER                                          | Inconsistent casing      | Standardized values    | Improves grouping                    |
|    8 | Platform                   | Text standardization    | TRIM + UPPER                                          | Inconsistent casing      | Standardized values    | Improves grouping                    |
|    9 | Revenue                    | Business validation     | Recalculate expected revenue                          | Reported only            | Recalc + diff          | Audit step                           |
|   10 | Revenue                    | Business insight        | Compute revenue uplift                                | No uplift metric         | uplift per row         | Key finding                          |
|   11 | Dataset                    | Duplicate detection     | Composite key check                                   | Unknown                  | 0 duplicates           | Date + Product + Location + Platform |
|   12 | Dataset                    | Quality control         | Data and business flags                               | No flags                 | issue_flag fields      | Centralized validation               |

---

## Outcome

* No technical data quality errors detected after cleaning.
* No duplicate records found.
* Revenue audit revealed a **systematic uplift** relative to the expected calculation.
* Uplift patterns were consistent across time, platforms, and countries.

The cleaning process confirms that observed revenue differences are likely driven by **business rules** rather than data quality issues.

