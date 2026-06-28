# Model Equations & Dummy Variable Explanation

## Dummy Variable Approach

Categorical variables cannot be used directly in linear regression. We convert them into **dummy (binary) variables** — one column per category, where 1 = "belongs to this group" and 0 = "does not".

### Variables Encoded
- **`region`**: 4 categories → 3 dummies (East dropped as reference)
- **`store_type`**: 4 categories → 3 dummies (Airport dropped as reference)

### Reference Categories
| Variable | Reference Category | Reason |
|---|---|---|
| `region` | **East** | Dropped first category alphabetically (drop_first=True) |
| `store_type` | **Airport** | Dropped first category alphabetically |

**Why drop one?** Including all 4 dummies would create perfect multicollinearity (the dummy variable trap). The dropped category is the **baseline** — all other category coefficients are interpreted as the difference from that baseline.

---

## Simple Regression Equations

### Model 1: Footfall → Monthly Sales (Best Simple Model)

**Equation:**
```
monthly_sales = 430,183.45 + 35.6780 × footfall
```

| Metric | Value |
|---|---|
| R² | 0.7363 |
| Coefficient (footfall) | 35.68 |
| P-value | < 0.0001 |
| Intercept | 430,183.45 |

**Coefficient interpretation**: Each additional customer visit per month is associated with approximately **£35.68 in additional monthly sales**.

**Business interpretation**: Footfall is the single most powerful driver of sales in this dataset. Stores that attract more customers generate substantially higher revenue. Actions that drive store visits (location improvements, events, promotions) are likely to have the highest sales impact.

**Useful for regression?** Yes — statistically significant, high R², strong business logic.

---

### Model 2: Marketing Spend → Monthly Sales

**Equation:**
```
monthly_sales = 561,127.83 + 2.1296 × marketing_spend
```

| Metric | Value |
|---|---|
| R² | 0.1672 |
| Coefficient (marketing_spend) | 2.1296 |
| P-value | < 0.0001 |

**Coefficient interpretation**: Each additional £1 of marketing spend is associated with approximately **£2.13 in additional monthly sales** — a positive but modest return when considered alone.

**Business interpretation**: Marketing spend has a statistically significant but weaker association with sales compared to footfall. It likely works through driving footfall (an indirect effect). On its own, it explains only 17% of sales variation.

**Useful for regression?** Moderately — significant but limited explanatory power alone.

---

### Model 3: Staff Count → Monthly Sales

**Equation:**
```
monthly_sales = 367,504.12 + 16,984.03 × staff_count
```

| Metric | Value |
|---|---|
| R² | 0.6523 |
| Coefficient (staff_count) | 16,984.03 |
| P-value | < 0.0001 |

**Business interpretation**: More staff is strongly associated with higher sales. However, causality is ambiguous — larger/busier stores need more staff AND generate more sales.

---

### Model 4: Inventory Availability → Monthly Sales

**Equation:**
```
monthly_sales = 485,092.15 + 2,217.83 × inventory_availability_pct
```

| Metric | Value |
|---|---|
| R² | 0.0131 |
| Coefficient | 2,217.83 |
| P-value | 0.0406 |

**Business interpretation**: A weak but statistically significant positive relationship. Higher stock availability is associated with marginally higher sales, but the effect is small.

---

### Model 5: Avg Discount % → Monthly Sales

**Equation:**
```
monthly_sales = 692,163.18 + (−138,730.45) × avg_discount_pct
```

| Metric | Value |
|---|---|
| R² | 0.0083 |
| Coefficient | −138,730.45 |
| P-value | 0.1040 |

**Business interpretation**: Discounting shows a **negative** (though not statistically significant) association with sales. Deeper discounts do not appear to increase total sales revenue in this dataset — and may actually reduce it.

**Useful for regression?** No — p-value > 0.05, very low R².

---

### Model 6: Customer Rating → Monthly Sales

**Equation:**
```
monthly_sales = 697,498.52 + (−5,284.87) × customer_rating
```

| Metric | Value |
|---|---|
| R² | 0.0007 |
| Coefficient | −5,284.87 |
| P-value | 0.6376 |

**Business interpretation**: Customer rating shows no statistically significant relationship with sales in this dataset. This is surprising but may reflect that rating captures satisfaction after the visit rather than driving new visits.

**Useful for regression?** No — not statistically significant.

---

## Multiple Regression Equation

**Full equation:**
```
monthly_sales = 136,399.23
  + 28.70  × footfall
  + 1.16   × marketing_spend
  + 2,853.23 × staff_count
  + 2,956.05 × inventory_availability_pct
  − 47,096.98 × avg_discount_pct
  + 7,700.57  × region_North
  + 19,440.63 × region_South
  + 18,502.25 × region_West
  − 21,712.03 × store_type_High Street
  − 9,802.25  × store_type_Mall
  − 39,110.24 × store_type_Residential
```

### Interpretation of Each Coefficient

| Variable | Coefficient | P-value | Significant? | Business Meaning |
|---|---|---|---|---|
| Intercept | 136,399 | 0.0019 | Yes | Baseline sales for East-region Airport store with all numerics at zero |
| footfall | 28.70 | <0.0001 | **Yes** | Each extra visitor → +£28.70 in sales |
| marketing_spend | 1.16 | <0.0001 | **Yes** | Each extra £1 marketing → +£1.16 in sales |
| staff_count | 2,853.23 | 0.0236 | **Yes** | Each extra staff member → +£2,853 in sales |
| inventory_availability_pct | 2,956.05 | <0.0001 | **Yes** | Each 1% more stock available → +£2,956 in sales |
| avg_discount_pct | −47,097 | 0.1996 | No | Discounting not significant when controlling for other factors |
| region_North | 7,701 | 0.2739 | No | North similar to East after controlling for other factors |
| region_South | 19,441 | 0.0071 | **Yes** | South stores sell £19,441 more than East (same store type) |
| region_West | 18,502 | 0.0035 | **Yes** | West stores sell £18,502 more than East (same store type) |
| store_type_High Street | −21,712 | 0.0203 | **Yes** | High Street sells £21,712 less than Airport stores |
| store_type_Mall | −9,802 | 0.3116 | No | Mall similar to Airport after controlling for other factors |
| store_type_Residential | −39,110 | <0.0001 | **Yes** | Residential sells £39,110 less than Airport stores |

### R-squared
- **R² = 0.8305** — the multiple regression model explains approximately **83% of the variation** in monthly sales across all stores and months.

---

## Final Model Selected

**Multiple Regression Model**

### Reason for Selection
1. **Highest R²** (0.8305) — explains more variance than any simple model.
2. **Statistically significant key predictors**: footfall, marketing_spend, staff_count, inventory_availability_pct, South and West regions, High Street and Residential store types.
3. **Business completeness**: captures multiple levers leadership can act on simultaneously.
4. **Controls for confounders**: by including region and store type dummies, the coefficients on numeric variables are adjusted for structural store differences.

The simple footfall model (R² = 0.7363) is the best single-variable model and remains a useful quick-reference tool, but the multiple regression provides richer, more actionable business insights.

### Variables Statistically Weak or Difficult to Interpret
- `avg_discount_pct` — not significant in the multiple model (p=0.20); the effect appears absorbed by footfall
- `customer_rating` — no significant relationship found (p=0.64)
- `region_North` — not significantly different from East (p=0.27)
- `store_type_Mall` — not significantly different from Airport (p=0.31)
