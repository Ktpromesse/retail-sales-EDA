# Retail Sales Exploratory Data Analysis

An exploratory analysis of a synthetic (AI-generated, practice) retail sales dataset for an eight-store chain in Rwanda, covering January 2023 to December 2024. All amounts are in Rwandan francs (RWF).

## Contents

| File | Description |
|---|---|
| `retail_executed.ipynb` | The analysis notebook, executed end to end with outputs and charts |
| `retail_sales_eda.csv` | Raw dataset (9,430 rows, 15 columns) |
| `Retail_Sales_EDA_Report.docx` | Written report with findings, charts and recommendations |
| `figures/` | PNG charts used in the report |

## Dataset

One row per product line within an order.

| Column | Meaning |
|---|---|
| `order_id`, `line_number` | Order and line within the order |
| `order_date` | Date of the order |
| `store_id`, `store_region` | Store and its region |
| `customer_id`, `customer_segment` | Customer and segment (Individual, Small Business, Corporate) |
| `product_id`, `product_name`, `category` | Product details |
| `quantity`, `unit_price_rwf`, `discount_pct` | Units, list price, discount in whole percent (5.0 = 5%) |
| `sales_amount_rwf` | Net line revenue |
| `payment_method` | Mobile Money, Cash, Card or Bank Transfer |

## What the notebook does

1. Loads the data and inspects structure, types and missing values.
2. Cleans it:
   - recomputes missing `sales_amount_rwf` as `quantity × unit_price × (1 − discount/100)`
   - fills missing discounts with 0 and missing segment/payment values with "Unknown"
   - drops rows with missing dates (37)
   - standardises inconsistent labels (e.g. `BEVERAGES`, `Snack`, `kigali`, `North`, `MoMo`)
   - removes exact duplicate rows (30)
3. Profiles numeric columns, outliers, returns and skew.
4. Analyses monthly revenue, categories, products, regions, segments, payment methods and order-level average order value (AOV).

## Key results

- Net revenue: **90.07M RWF** across 3,300 orders and 958 customers; 2024 was **+20.4%** on 2023.
- Grocery Staples contribute 37.4% of revenue; Rice 5kg and Cooking Oil 3L together about 26%.
- Kigali accounts for 59.2% of revenue and has three of the eight stores.
- Corporate customers have a mean AOV of about 86.5k RWF, versus about 14.3k for individuals.
- Revenue peaks in December of both years, plus June and October 2024.

## Changes made to the original notebook

- Fixed `df['order_id', ]` (stray comma that caused a `KeyError`).
- Fixed the sales imputation: discounts are whole percents, so the formula needed `/ 100`. The old version created 32 false negative sales rows.
- Added a label-standardisation cell so categories, regions and payment methods are not split across spelling variants.
- Added a run-notes cell at the top. Some of the original markdown commentary quoted figures that differ from the notebook's output; the printed results and the report are authoritative.

## Running it

```bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook retail_executed.ipynb
```

Keep `retail_sales_eda.csv` in the same folder as the notebook.

## Limitations

The data is synthetic, so patterns reflect how it was generated rather than real customer behaviour. The analysis is descriptive only (no significance tests or forecasting).
