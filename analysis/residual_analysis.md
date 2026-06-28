# Residual Analysis – Multiple Regression Final Model

## Overview

Residuals = Actual Monthly Sales − Predicted Monthly Sales

A positive residual means the store **outperformed** what the model predicted.
A negative residual means the store **underperformed** what the model predicted.

---

## Predicted vs Actual Sales (Final Multiple Regression Model)

Model R² = 0.8305 — approximately 83% of variation in monthly sales is captured by the model.

---

## Top 5 Stores with Largest Positive Residuals (Model Under-Predicts)

| Store ID | Store Type | Region | Actual Sales (£) | Predicted Sales (£) | Residual (£) |
|---|---|---|---|---|---|
| STR-1073 | Residential | East | 813,317 | 705,926 | +107,391 |
| STR-1028 | Mall | East | 713,611 | 607,256 | +106,355 |
| STR-1026 | Mall | East | 625,514 | 521,904 | +103,610 |
| STR-1030 | Residential | West | 820,519 | 720,348 | +100,171 |
| STR-1051 | Airport | East | 787,716 | 688,752 | +98,964 |

### Business Interpretation – Positive Residuals

These stores are **outperforming model expectations**. Possible explanations:

- **Local demand factors** not captured in the model — e.g., nearby new housing developments, transport hubs, or anchor tenants attracting additional footfall.
- **Exceptional store management** — strong local leadership, better merchandising, or superior customer service beyond what the rating score captures.
- **Untracked marketing activities** — local events, community partnerships, or social-media-driven traffic.
- **Store-specific competitive advantages** — a competitor closure, exclusive products, or favourable lease/layout.

**Leadership action**: Investigate what STR-1073, STR-1028, STR-1030 are doing differently. If replicable, these become best-practice case studies. Consider rewarding or promoting their store managers.

---

## Top 5 Stores with Largest Negative Residuals (Model Over-Predicts)

| Store ID | Store Type | Region | Actual Sales (£) | Predicted Sales (£) | Residual (£) |
|---|---|---|---|---|---|
| STR-1017 | High Street | West | 685,379 | 846,818 | −161,439 |
| STR-1012 | Residential | West | 595,468 | 731,509 | −136,042 |
| STR-1023 | Mall | South | 627,172 | 756,600 | −129,428 |
| STR-1007 | Mall | West | 800,452 | 913,025 | −112,573 |
| STR-1077 | Residential | South | 538,376 | 637,359 | −98,983 |

### Business Interpretation – Negative Residuals

These stores are **underperforming model expectations** — they have the footfall, staff, and marketing inputs that should deliver higher sales, but they are not converting.

- **Conversion failures**: Visitors are not completing purchases — possibly due to poor in-store experience, stock-outs at key SKUs, or pricing issues.
- **Marketing mis-targeting**: Marketing spend may be attracting window-shoppers rather than buyers.
- **Operational issues**: High shrinkage, slow checkout, or poor store layout may be suppressing actual revenue.
- **Local economic headwinds**: These stores may be in areas facing specific income pressures or competitor campaigns not captured in the data.

**Leadership action**: Priority operational audit of STR-1017, STR-1012, STR-1023. Investigate footfall-to-transaction conversion rates and basket size. Check if avg_discount_pct at these stores is unusually high (indicating margin dilution alongside revenue shortfall).

---

## Under-Prediction vs Over-Prediction Patterns by Store Type

| Store Type | Average Residual (£) | Interpretation |
|---|---|---|
| Airport | Slightly positive | Model tends to slightly under-predict Airport stores |
| Mall | Mixed — some very negative | Model struggles with Mall variability |
| High Street | Negative | High Street stores frequently underperform predictions |
| Residential | Mixed | Wide spread — both over- and under-performers |

### Does the Model Over-Predict or Under-Predict Certain Store Types?

- **High Street stores** appear consistently **over-predicted** by the model. This suggests that, even after applying the High Street dummy penalty (−£21,712), some structural disadvantage of High Street stores is not fully captured. This may relate to competition from online retail or foot traffic quality (browsing vs buying).
- **Airport stores** are generally **under-predicted**, suggesting the model's Airport baseline may be conservative — airports may have unique captive-audience advantages.
- **Mall and Residential** show high variance in residuals, indicating that within these categories, individual store-level factors matter a great deal.

---

## Summary

The multiple regression model performs well overall (R² = 0.83), but residuals reveal that store-level idiosyncrasies — management quality, local conditions, and conversion efficiency — account for the remaining 17% of unexplained variation. A natural next step would be to incorporate store-fixed effects or additional qualitative variables.
