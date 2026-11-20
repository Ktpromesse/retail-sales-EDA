# Dataset 1: Retail Sales (`retail_sales_eda.csv`)

**SYNTHETIC DATA.** Imaginary supermarket chain with 8 stores in Rwanda. Not real sales.

**One row = one order line** (one product within one order). An order can have 1-6 lines, so `order_id` repeats; `order_id` + `line_number` identifies a line (before any duplicate rows). Size: about 9,430 rows x 15 columns.
Period: 2023-01-01 to 2024-12-31. Currency: Rwandan francs (RWF).

**Business definition:** `sales_amount_rwf` = `quantity` x `unit_price_rwf` x (1 - `discount_pct`/100), rounded to the nearest whole RWF. Returns have negative quantity and negative sales.

| Column | Meaning | Type / units | Possible values |
|---|---|---|---|
| order_id | Order identifier, shared by all lines of the order | text | ORD-000001 ... |
| line_number | Position of the line within the order | integer | 1-6 |
| order_date | Date of the order | text, YYYY-MM-DD | 2023-01-01 to 2024-12-31 |
| store_id | Store code | text | S01-S08 |
| store_region | Region of the store | text | Kigali, Northern, Southern, Eastern, Western |
| customer_id | Customer code (same customer can appear in many orders) | text | C0001-C1000 |
| customer_segment | Type of customer | text | Individual, Small Business, Corporate |
| product_id | Product code | text | P001-P040 |
| product_name | Product description | text | 40 products |
| category | Product category | text | 8 categories (e.g. Fresh Produce, Beverages) |
| quantity | Units sold on the line | integer | normally positive |
| unit_price_rwf | Price per unit before discount | RWF | positive integer |
| discount_pct | Percentage discount on the line | percent | 0, 5, 10, 15, 20 |
| sales_amount_rwf | Revenue of the line after discount | RWF | see definition |
| payment_method | How the order was paid (same for all lines of an order) | text | Cash, Mobile Money, Card, Bank Transfer |

**Source/licence:** none (synthetic). Free to use.
**Generation:** random orders sampled over dates (with weekday, monthly and growth effects built in), customers, stores, products and prices (with mild price drift), quantities and discounts. Data-quality issues were then injected.
**Limitations:** no real-world validity; patterns are simplified; store, product and customer behaviour is invented; no costs or profit columns.

**Data-quality categories to look for:** missing values in several columns, exact duplicate rows, inconsistent text labels, unusual numeric values, and values that may not reconcile with the business definition above. Locations/counts are not disclosed.

**Possible EDA questions (not answered)**
- How is revenue distributed across days, weeks, months, and years? Is there seasonality or growth?
- How do categories, products, stores and regions compare on units sold and revenue?
- How are quantity, price and discount distributed? Are there outliers?
- Do discounts relate to quantity or sales amount?
- How do customer segments differ in order size, basket composition and payment method?
- How many lines does a typical order have? What is the average order value?
- Which rows do not satisfy the sales formula, and why might that be?
