# Retail Chain Monthly Sales – Regression Analysis

## Business Problem Summary

The leadership team of a retail chain wants to understand what factors drive monthly sales performance across stores. They are evaluating business actions such as increasing marketing spend, improving inventory availability, changing discounting strategy, reallocating staff, and prioritising certain store types or regions. This analysis uses linear regression to identify which factors are most strongly associated with monthly sales.

---

## Dataset Description

- **File**: `business_regression_data.xlsx`
- **Rows**: 320 observations (80 stores × 4 months)
- **Columns**: 14 variables
- **Time period**: January – April 2025

---

## Task 1: Variable Identification

### 1. Dependent Variable
| Variable | Description |
|---|---|
| `monthly_sales` | Total monthly revenue per store (£) — the outcome we are trying to explain |

### 2. Potential Independent Variables
| Variable | Type | Notes |
|---|---|---|
| `footfall` | Numerical | Number of customer visits per month |
| `marketing_spend` | Numerical | Monthly marketing budget (£) |
| `avg_discount_pct` | Numerical | Average discount percentage offered |
| `staff_count` | Numerical | Number of staff in the store |
| `inventory_availability_pct` | Numerical | % of inventory in stock |
| `competitor_distance_km` | Numerical | Distance to nearest competitor (km) |
| `holiday_flag` | Binary (0/1) | Whether the month contains a public holiday |
| `customer_rating` | Numerical | Average customer satisfaction score |
| `region` | Categorical | East, North, South, West |
| `store_type` | Categorical | Airport, Mall, High Street, Residential |

### 3. Numerical Variables
`footfall`, `marketing_spend`, `avg_discount_pct`, `staff_count`, `inventory_availability_pct`, `competitor_distance_km`, `customer_rating`, `monthly_sales`, `monthly_profit`

### 4. Categorical Variables
`region` (4 levels: East, North, South, West), `store_type` (4 levels: Airport, Mall, High Street, Residential)

### 5. Variables That May Need Cleaning or Transformation
| Variable | Issue | Action Taken |
|---|---|---|
| `customer_rating` | 8 missing values | Imputed with median (3.8) |
| `competitor_distance_km` | 6 missing values | Imputed with median |
| `avg_discount_pct` | Expressed as decimal (0.0–0.26) | Noted; used as-is |
| `region`, `store_type` | Categorical strings | Encoded as dummy variables for regression |

### 6. Variables Not Useful for Regression
| Variable | Reason |
|---|---|
| `store_id` | Identifier only — no predictive value |
| `month` | Datetime index — only 4 unique values; would require time-series methods |
| `monthly_profit` | Outcome variable derived from sales — would cause leakage if used as predictor |

---

## Regression Approach

Linear regression was chosen to model the relationship between `monthly_sales` (dependent variable) and the independent variables listed above. Both simple (one predictor) and multiple (several predictors) regression models were built and compared.

## Dummy Variable Approach

`region` and `store_type` were converted to dummy variables using **drop-first encoding** to avoid multicollinearity (dummy variable trap).
- **Reference category for `region`**: East
- **Reference category for `store_type`**: Airport

This means all region and store-type coefficients are interpreted relative to East-region Airport stores.

## Model Comparison Summary

| Model | Predictors | R² |
|---|---|---|
| Simple – Footfall | footfall | 0.7363 |
| Simple – Marketing Spend | marketing_spend | 0.1672 |
| Multiple Regression | footfall + marketing_spend + staff_count + inventory_availability_pct + avg_discount_pct + region dummies + store_type dummies | 0.8305 |

## Final Model Selected

**Multiple Regression Model** (R² = 0.8305)

The multiple regression model explains approximately **83% of the variation** in monthly sales and is the most complete model for business decision-making.

## Business Recommendation

Leadership should **prioritise footfall growth** — it is by far the strongest predictor of sales. Marketing spend and inventory availability also show statistically significant positive associations. Discounting (avg_discount_pct) shows a negative relationship and is **not recommended** as a sales-growth lever. Regional differences (South and West outperform East) and store type (Residential stores underperform Airport stores) should inform store investment priorities.

## Assumptions and Limitations

- Regression shows **association, not causation** — e.g., higher marketing spend may be deployed in already stronger stores.
- The model assumes **linear relationships** between predictors and sales.
- Only 4 months of data — **seasonal effects** may not be fully captured.
- Store-level fixed effects are not controlled for — unobserved store quality differences may confound estimates.
- Missing values were imputed; if the missing pattern is non-random, this introduces bias.

## Screenshots Included

- `screenshots/simple_regression_output.png` — Simple regression (footfall model)
- `screenshots/multiple_regression_output.png` — Multiple regression summary
- `screenshots/model_comparison_preview.png` — Model comparison table
- `screenshots/residuals_preview.png` — Residual analysis preview
