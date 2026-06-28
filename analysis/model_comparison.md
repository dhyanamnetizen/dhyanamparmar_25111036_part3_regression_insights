# Model Comparison

## Overview

This document compares all regression models built on the retail chain monthly sales dataset.

---

## Model Comparison Table

| Model Name | Dependent Variable | Independent Variable(s) | R² | Key Significant Variables | Business Usefulness | Limitations |
|---|---|---|---|---|---|---|
| Simple Model 1 – Footfall | monthly_sales | footfall | **0.7363** | footfall (p<0.0001) | High — footfall is actionable and easy to track | Cannot separate effect of store size/type |
| Simple Model 2 – Marketing Spend | monthly_sales | marketing_spend | 0.1672 | marketing_spend (p<0.0001) | Moderate — marketing ROI ≈ £2.13 per £1 spent | Low R²; ignores all other drivers |
| Simple Model 3 – Staff Count | monthly_sales | staff_count | 0.6523 | staff_count (p<0.0001) | Moderate — but staff and footfall are correlated | Endogeneity risk (larger stores hire more) |
| Simple Model 4 – Inventory | monthly_sales | inventory_availability_pct | 0.0131 | inventory_availability_pct (p=0.04) | Low — small effect size | Only explains 1.3% of variance |
| Simple Model 5 – Discount | monthly_sales | avg_discount_pct | 0.0083 | None (p=0.10) | None — not significant | Does not predict sales |
| Simple Model 6 – Customer Rating | monthly_sales | customer_rating | 0.0007 | None (p=0.64) | None — no relationship found | Captures lagging satisfaction, not demand |
| **Multiple Regression (Final)** | monthly_sales | footfall + marketing_spend + staff_count + inventory_availability_pct + avg_discount_pct + region dummies + store_type dummies | **0.8305** | footfall, marketing_spend, staff_count, inventory_availability_pct, region_South, region_West, store_type_High Street, store_type_Residential | **High** — most complete model for decisions | Assumes linearity; 4 months only; no causal inference |

---

## Detailed Comparison

### Model Name & Variables Used

| Model | Dependent | Independent |
|---|---|---|
| Simple – Footfall | monthly_sales | footfall |
| Simple – Marketing Spend | monthly_sales | marketing_spend |
| Multiple Regression (Final) | monthly_sales | footfall, marketing_spend, staff_count, inventory_availability_pct, avg_discount_pct, region_North, region_South, region_West, store_type_High Street, store_type_Mall, store_type_Residential |

### R-Squared Comparison

| Model | R² | Interpretation |
|---|---|---|
| Simple – Footfall | 0.7363 | 73.6% of sales variation explained |
| Simple – Marketing Spend | 0.1672 | 16.7% of sales variation explained |
| Multiple Regression | **0.8305** | **83.1% of sales variation explained** |

The multiple regression model provides the **best explanatory power**, improving on the best simple model by approximately **9.4 percentage points**.

### Significant Variables (p < 0.05)

| Model | Significant Variables |
|---|---|
| Simple – Footfall | footfall |
| Simple – Marketing Spend | marketing_spend |
| Multiple Regression | footfall, marketing_spend, staff_count, inventory_availability_pct, region_South, region_West, store_type_High Street, store_type_Residential |

### Business Usefulness

| Model | Helps Decision-Making? | Key Insight |
|---|---|---|
| Simple – Footfall | Yes | Footfall is the #1 lever; driving store visits drives revenue |
| Simple – Marketing Spend | Partially | Marketing has a positive but modest direct effect on sales |
| Multiple Regression | **Yes – most complete** | Simultaneously shows what leadership can act on: footfall growth, marketing investment, inventory, and where store type/region matters |

### Limitations

| Model | Limitations |
|---|---|
| Simple – Footfall | Omits marketing, inventory, store type; overstates footfall effect if correlated with omitted variables |
| Simple – Marketing Spend | Low R²; marketing likely works through footfall (indirect), so direct effect underestimated |
| Multiple Regression | Assumes linearity; cross-sectional limitations over only 4 months; cannot prove causation; missing competitor strategy and external economic data |

---

## Conclusion

The **multiple regression model** is selected as the final model. It is the most statistically powerful (R² = 0.8305), includes multiple business levers, controls for structural store differences (type and region), and provides the richest basis for leadership decision-making.

The **simple footfall model** remains a useful, easy-to-communicate model for quick reference and store-level monitoring.
