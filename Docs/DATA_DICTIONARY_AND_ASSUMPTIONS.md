# Data Dictionary and Assumptions

Project: Maven Fuzzy Factory E-commerce Analytics (Excel + Power BI)
Period: 19 Mar 2012 to 19 Mar 2015

> **How this was written.** It documents what is visible in the Power BI field list and the Excel workbook. Items marked **(unverified)** could not be confirmed from the screenshots and exports used to build this document: the underlying DAX formulas, model relationships, Power Query steps and some key columns were not reviewed. Please confirm them in your own model before relying on them.

---

## 1. Tables and columns (Power BI model)

Columns listed are those visible in the Power BI Data pane. Key columns (for example order or session IDs) were not all visible: **(unverified)**.

### website_sessions
| Column | Description |
|---|---|
| channel | Marketing channel group (gsearch nonbrand, gsearch brand, bsearch nonbrand, bsearch brand, socialbook desktop_targeted, socialbook pilot, Direct / Unattributed). How it is derived from the UTM fields is **(unverified)** |
| created_at / created_date | Session timestamp and date |
| device_type | desktop or mobile |
| http_referer | Referring URL |
| is_repeat_session | Flag for a repeat visitor session |
| utm_source, utm_campaign, utm_content | Campaign tracking fields |
| Session Type | Added column: "Repeat" or "New", derived from is_repeat_session |

### website_pageviews
| Column | Description |
|---|---|
| website_pageview_id | Pageview identifier |
| pageview_url | Page visited (for example /lander-5, /home, /billing, /billing-2) |
| created_at | Pageview timestamp |
| First Pageview Time | Calculated column (**definition unverified**) |
| Is Landing Page | Calculated column marking a session's first page (**definition unverified**) |

### orders
| Column | Description |
|---|---|
| created_at / created_date | Order timestamp and date |
| items_purchased | Number of items in the order |
| price_usd | Order price in USD |
| cogs_usd | Cost of goods sold in USD |
| primary_product_id | Product of the first item in the order |
| user_id | Customer identifier |

### order_items
| Column | Description |
|---|---|
| created_at / created_date | Item timestamp and date |
| price_usd | Item price in USD |
| cogs_usd | Item cost in USD |
| is_primary_item | Flag for the first item in an order |

### order_item_refunds
| Column | Description |
|---|---|
| order_item_refund_id | Refund identifier |
| refund_amount_usd | Refund amount in USD |
| created_at / created_date | Refund timestamp and date |

### products
| Column | Description |
|---|---|
| product_name | The Original Mr. Fuzzy, The Forever Love Bear, The Birthday Sugar Panda, The Hudson River Mini bear |
| created_at | Product launch timestamp |

### Dim Calendar
Date, Month Name, Month Number, Month-Year, Month-Year Sort, Quarter, Year. Used for monthly trends and year filtering.

### Funnel Stages
| Column | Description |
|---|---|
| Stage | Sessions, Product View, Cart, Billing, Order |
| Stage Order | Sort order of the stages |

### Table (insights table)
Columns FINDING, IMPACT, ACTION. Holds the Key Insights text shown on the Final Dashboard. (Consider renaming the table to "Insights".)

### Relationships
Not reviewed: **(unverified)**.

---

## 2. Business metrics

| Metric | Definition | Value |
|---|---|---|
| Sessions | Count of website sessions | 472,871 |
| Orders | Count of orders | 32,313 |
| Order items | Count of ordered items | 40,025 |
| Gross Revenue | Sum of item prices | $1,938,509.75 |
| Total Refunds | Sum of refund amounts | $85,338.69 |
| Net Revenue | Gross Revenue - Refunds | $1,853,171.06 |
| COGS | Sum of item costs | $722,370.25 |
| Gross Profit | Net Revenue - COGS | $1,130,800.81 |
| Gross Margin | Gross Profit / Net Revenue | 61.02% |
| Conversion Rate | Orders / Sessions | 6.83% |
| AOV | Gross Revenue / Orders | $59.99 |
| Items per order | Items sold / Orders | 1.24 |
| Refunded items | Count of refunded items | 1,731 |
| Refund Rate (items) | Refunded items / items sold | 4.32% |
| Refunds % of Revenue | Refund amount / Gross Revenue | 4.40% |
| Net Revenue per Session | Net Revenue / Sessions | $3.92 |
| Gross Margin before refunds (product level) | (Revenue - COGS) / Revenue | 62.74% overall |

Funnel step rates (Power BI Website Funnel page): Session to Product 55.2%, Product to Cart 36.3%, Cart to Billing 54.8%, Billing to Order 62.1%, Cart to Order 34.0%. Funnel counts: 473K sessions, 261K product views, 95K cart, 52K billing, 32K orders.

### Power BI measures visible in the field list
Average Order Value, Cart-to-Order Conversion Rate, Billing 2 Sessions, Billing Sessions, Billing to Order Conversion, Billing 2 to Order Conversion, Cart Sessions, Cart to Billing Conversion, Desktop Conversion Rate, Mobile Conversion Rate, Mobile Conversion Gap, Funnel Count, Item Refund Rate, Landing Page CVR, Landing Page Orders, Margin after Refunds, Monthly Sessions, Net Revenue per Session, Orders YoY %, Pageviews, Product COGS, Product Gross Profit, Product Refunds, Product Revenue, Product Units Sold, Product Page Sessions, Product to Cart Conversion, Profit after Refunds, Refund Rate (Items), Refund Rate by Product, Revenue, Revenue by Channel, Revenue Growth 2014 vs 2013, Revenue Jan-Feb 2014, Revenue Jan-Feb 2015, Revenue YoY %, Revenue YoY Like-for-Like, Sessions Reaching Page, Session to Product Conversion, Total COGS, Total Refunds, Jan-Feb YoY Revenue Growth.
**DAX formulas were not reviewed (unverified).**

---

## 3. Time periods and comparisons

| Item | Treatment |
|---|---|
| Data range | 19 Mar 2012 to 19 Mar 2015 |
| Partial months | March 2012 (starts on the 19th) and March 2015 (ends on the 19th) |
| Monthly trends | Full months only: Apr 2012 to Feb 2015 |
| 2013 vs 2012 | Apr to Dec only: $126,274.74 to $326,870.60 (+158.86%) |
| 2014 vs 2013 | Full year: $393,247.87 to $1,075,612.19 (+173.52%) |
| Jan-Feb 2015 vs Jan-Feb 2014 | $122,581.41 to $261,424.48 (+113.27%) |
| 2012 growth | Not shown (no 2011 data) |

The Power BI Executive Overview card shows "Gross Revenue Growth 2014 vs 2013 = 173.52%", which matches the gross revenue growth on the Excel YoY sheet. The formula behind the Power BI card was not reviewed **(unverified)**.

---

## 4. Assumptions

1. Revenue is the sum of item prices; refunds are subtracted for net revenue.
2. Gross Profit assumes COGS is not recovered when an item is refunded **(unverified against the source data)**.
3. Gross Margin uses Net Revenue as the denominator. Product-level margin on the product sheet is calculated before refunds, so the two margins (61.02% vs 62.74%) differ by design.
4. Conversion is session-level: one order per converting session.
5. AOV uses gross revenue.
6. Channel names come from the dataset's channel field; "Direct / Unattributed" groups sessions without campaign tracking **(grouping logic unverified)**.
7. "Illustrative" estimates are what-if calculations, not forecasts:
   - Mobile to 4.5%: 145,844 sessions x 1.41 points x $59.99 = about 2,055 orders, about $123K
   - gsearch nonbrand +0.5 point: 282,706 x 0.5% x $59.99 = about 1,400 orders, about $85K
   - Mr. Fuzzy refund rate from 5.11% to 2.23%: $1,211,058 x 2.88 points = about $35K

## 5. Limitations

- No advertising spend, so no channel ROI.
- No customer attributes beyond user_id and the repeat-session flag; no cohort or lifetime-value analysis.
- Device, channel and landing-page results are associations; channel mix may confound device results.
- Landing pages may have run in different time windows, so the 10.2% vs 3.4% gap may not be a clean comparison **(unverified)**.
- Workbook "Data Quality Checks" are reconciliation checks inside the project (sessions, orders, revenue, COGS, refunds, order items, net revenue, gross profit, margins, device/channel/product totals). All show PASS. They are not an independent audit of the raw data, and the check formulas were not reviewed **(unverified)**.
- Sample/fictional dataset: findings demonstrate analysis method.

## 6. Excel workbook sheets

Dashboard, KPI_Summary, Device_Analysis, Channel_Analysis, Product_Performance_Analysis, Order_&_Refund_Analysis, Monthly_Trend_Analysis, YoY_Analysis, Data_Quality_Checks, README, plus raw data tabs (orders, order_items, and others).
