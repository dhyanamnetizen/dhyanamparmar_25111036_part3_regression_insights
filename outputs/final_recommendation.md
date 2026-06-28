# Final Business Recommendation
## Retail Chain Monthly Sales – Regression Analysis

---

## 1. Which Factors Appear Most Strongly Associated with Monthly Sales?

Based on the multiple regression model (R² = 0.8305), the factors most strongly and statistically significantly associated with monthly sales are:

| Factor | Direction | Strength | P-value |
|---|---|---|---|
| **Footfall** (customer visits) | Positive | Very strong | <0.0001 |
| **Inventory availability %** | Positive | Strong | <0.0001 |
| **Marketing spend** | Positive | Moderate | <0.0001 |
| **Staff count** | Positive | Moderate | 0.024 |
| **Region (South & West)** | Positive vs East | Moderate | <0.01 |
| **Store type (Residential)** | Negative vs Airport | Strong | <0.0001 |
| **Store type (High Street)** | Negative vs Airport | Moderate | 0.020 |

**Footfall is the single most powerful driver**, both in the simple model (R² = 0.736) and as the largest coefficient in the multiple model (each additional visitor → approximately +£28.70 in sales, holding all else constant).

---

## 2. Which Variables Should Leadership Focus On?

Leadership should concentrate on **three primary levers**:

### Priority 1 — Drive Footfall
Footfall alone explains 73.6% of monthly sales variation. Every strategy that increases customer visits will have the highest return:
- Improve store visibility and accessibility
- Run targeted local promotions and events
- Optimise store placement in high-traffic locations

### Priority 2 — Protect and Improve Inventory Availability
Each 1% improvement in inventory availability is associated with approximately **+£2,956 in monthly sales** (significant at p<0.0001). Stock-outs suppress revenue. Leadership should:
- Invest in demand forecasting and replenishment systems
- Prioritise high-turnover SKUs for availability guarantees

### Priority 3 — Invest in Marketing (With Measured ROI)
Each £1 of marketing spend is associated with approximately **+£1.16 in sales** — above break-even but with a modest multiplier. Marketing drives sales most likely through footfall. Leadership should:
- Evaluate marketing efficiency store-by-store (some stores convert better)
- Test increased marketing in South and West regions, which already outperform East

---

## 3. Which Variables Should NOT Be Over-Interpreted?

| Variable | Reason for Caution |
|---|---|
| `avg_discount_pct` | Not statistically significant in the multiple model (p=0.20). Discounting does not appear to increase total revenue and may even reduce it. Do **not** use blanket discounting as a sales lever. |
| `customer_rating` | No significant association with sales (p=0.64). Ratings may reflect experience quality but do not drive measurable revenue differences in this dataset. |
| `region_North` | Not significantly different from East after controlling for other factors (p=0.27). North underperformance is likely explained by store composition, not geography. |
| `store_type_Mall` | Not significantly different from Airport after controlling for other factors (p=0.31). |
| `staff_count` | While significant, the causal direction is unclear — busier stores both hire more staff and sell more. Hiring staff alone does not guarantee sales growth. |

---

## 4. What Business Action Would We Recommend?

### Immediate Actions (0–3 months)
1. **Launch a footfall-driving campaign** across all stores — specifically focusing on High Street and Residential stores which underperform Airport and Mall baselines by £21,712–£39,110 respectively.
2. **Audit inventory availability** at all stores, prioritising the 5 stores with largest negative residuals (STR-1017, STR-1012, STR-1023, STR-1007, STR-1077) which are underperforming despite having predicted inputs.
3. **Stop or reduce blanket discounting** — the data shows no revenue benefit. Redirect those funds into footfall-generation activities.

### Medium-Term Actions (3–12 months)
4. **Prioritise expansion and investment in South and West regions** — both show significantly higher sales than East (by £19,441 and £18,502 respectively) after controlling for store type and operating variables.
5. **Investigate high-positive-residual stores** (STR-1073, STR-1028, STR-1030) to identify best practices in management, merchandising, or local marketing for replication.
6. **Reconsider Residential store strategy** — these stores underperform Airport stores by ~£39,110 even after controlling for footfall and marketing. Consider whether investment in these stores should be redirected to higher-potential formats.

---

## 5. What Risks or Limitations Should Leadership Keep in Mind?

| Risk | Detail |
|---|---|
| **Short time window** | Only 4 months of data. Results may not reflect seasonal patterns (e.g., Christmas trading) which could significantly change variable relationships. |
| **Correlation ≠ Causation** | High footfall stores may simply be in better locations — building footfall elsewhere may not yield the same return. |
| **Omitted variables** | The model does not capture local competition intensity, macroeconomic conditions, or store-level management quality — all of which could drive residuals. |
| **Imputed missing data** | 14 missing values were filled with medians; if these are not missing at random, this introduces bias. |
| **Linearity assumption** | The model assumes a straight-line relationship between each variable and sales. In reality, diminishing returns (e.g., on marketing spend) likely exist. |

---

## 6. Why Does Regression Show Association but Not Automatically Prove Causation?

Regression is a **statistical tool that measures correlation** — how much two variables move together. It does not establish why they move together. Several reasons why association is not causation:

1. **Reverse causality**: High-performing stores may be given higher marketing budgets because they perform well — so marketing "predicts" sales not because it causes them, but because the chain invests more in already-strong stores.

2. **Confounding variables**: A third variable (e.g., store location quality) may cause both high footfall AND high sales. The regression attributes the effect to footfall, when really it is driven by the unobserved location variable.

3. **Selection effects**: Airport stores may serve wealthier, time-constrained travellers who spend more regardless of anything the retailer does — the "Airport" dummy is picking up this selection effect, not the store's operational quality.

4. **Historical data**: The model is built on past patterns. If the business changes its strategy (e.g., invests heavily in marketing for low-footfall stores), past coefficients may not accurately predict the outcome.

**For causal inference, leadership would need**: randomised A/B tests (e.g., randomly assign marketing budgets across stores), or natural experiments (e.g., a competitor closure in some markets).

---

## Conclusion

The regression analysis strongly supports a **footfall-first, inventory-second, targeted-marketing-third** strategy. Discounting is not supported by the evidence. Investment should be directed toward South and West regions, and leadership should act on the operational gaps identified in the underperforming store residuals. These recommendations are grounded in an 83%-accurate regression model but should be stress-tested through controlled pilots before company-wide rollout.
