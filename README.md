# AtliQ Supply Chain & Finance Analytics Using SQL Server
## 📌 Project Overview
**AtliQ Supply Chain & Finance Analytics** is an end-to-end SQL Server analytics project designed to transform transactional supply-chain and financial data into management-oriented business insights.
AtliQ operates in the hardware manufacturing and distribution environment, selling electronic products through **Direct, Retail and Distributor channels** across different markets. The project connects sales, customers, products, pricing, manufacturing costs, freight costs, deductions, forecasts and inventory information to analyze the financial and operational performance of the business.
The project focuses on answering practical business questions related to:

* Sales and revenue performance
* Customer segmentation and concentration
* Product profitability
* Manufacturing cost and gross margin
* Discount and deduction impact
* Freight-cost efficiency
* Demand forecasting
* Customer loyalty
* Inventory movement
* Product mix
* Geographic and channel performance

The project follows a **September–August fiscal year**, as specified in the project requirements.
The overall objective is to move beyond basic SQL querying and demonstrate how relational data can be converted into actionable finance and supply-chain insights.

## 💼 Business Problem

A hardware manufacturing and distribution company needs to monitor both its financial performance and supply-chain operations.
Management needs answers to questions such as:

* Which customers generate the highest sales volume and revenue?
* Which products generate stronger gross margins?
* How much revenue is lost through customer discounts?
* Are actual sales aligned with forecasts?
* Which markets have higher freight costs?
* Which products are moving efficiently through inventory?
* Which customers demonstrate repeat-purchase behavior?
* Which products and markets may require additional attention?
* How can financial and operational data be integrated into a repeatable analytical framework?

The project addresses these questions by combining multiple relational tables and applying SQL-based financial and operational analysis.

## 🎯 Project Objectives
The key objectives of the project were to:

1. Build a relational SQL Server environment for supply-chain and finance data.
2. Connect customer, product, sales, forecast, pricing, cost and deduction information.
3. Analyze sales trends and customer performance.
4. Segment customers based on observed sales volume and revenue.
5. Compare products based on sales and gross revenue.
6. Evaluate product profitability using gross price and manufacturing cost.
7. Measure the financial impact of pre-invoice deductions.
8. Compare freight costs across markets.
9. Analyze forecast versus actual sales.
10. Identify seasonal sales patterns.
11. Analyze customer loyalty based on observed purchase frequency.
12. Evaluate inventory movement using available inventory and sales data.
13. Analyze channel and geographic sales distribution.
14. Develop reusable SQL functions, procedures and triggers.
15. Establish a foundation for future dashboards and recurring management reporting.

## 🗄️ Dataset / Database Overview

The SQL model contains **nine core business tables** covering customers, products, monthly sales, forecasts, freight costs, gross prices, manufacturing costs, post-invoice deductions and pre-invoice deductions.
Additional SQL objects were created for audit logging, reusable functions, stored procedures and triggers.

### Dimension Tables
**1. `dim_customer`**
Contains customer master information including:

* Customer code
* Customer name
* Platform
* Channel
* Market
* Sub-zone
* Region

**Business use:** Customer segmentation, channel analysis, geographic analysis and customer-level demand analysis.

**2. `dim_product`**
Contains product master information including:

* Product code
* Division
* Segment
* Category
* Product
* Variant
* Inventory count

**Business use:** Product performance, product mix, profitability and inventory analysis.

### Fact Tables
**3. `fact_sales_monthly`**

Stores actual monthly sales transactions.
Key fields include:
* Date
* Product code
* Customer code
* Sold quantity
  
**Business use:** Sales trends, customer demand, product performance and forecast variance.

**4. `fact_forecast_monthly`**
Stores monthly forecast quantities by product and customer.

**Business use:** Forecast-versus-actual analysis and demand planning.

**5.`fact_gross_price`**
Stores product gross/base prices by fiscal year.

**Business use:** Gross revenue and pricing analysis.

**6. `fact_manufacturing_cost`**

Stores manufacturing costs by product and year.

**Business use:** Gross profit and margin analysis.

**7. `fact_pre_invoice_deductions`**

Stores customer-level pre-invoice deduction percentages.

**Business use:** Measuring the impact of discounts on gross revenue and net invoice revenue.

**8. `fact_post_invoice_deductions`**

Stores deductions applied after invoicing, including promotional and other deductions.

**Business use:** Understanding additional reductions in realized sales value.

**9. `fact_freight_cost`**

Stores market-level freight and other cost percentages.

**Business use:** Comparing logistics costs and identifying potential supply-chain cost optimization opportunities.

### Supporting Table

**`audit_log`**

Used to record sales-related audit events generated through SQL triggers.

The SQL implementation also creates user-defined functions, stored procedures and triggers to demonstrate reusable calculations, controls and automation.

## 🧮 Financial Logic Used

The project follows a simplified financial flow from gross price to gross profit.

**Net Invoice Sales**

Net Invoice Sales = Gross Price - Pre-Invoice Deduction

**Net Sales**

Net Sales
= Net Invoice Sales - Post-Invoice Deductions

**Gross Profit**

Gross Profit = Net Sales - COGS

The project defines COGS using manufacturing, freight and other costs.

**Gross Margin %**

Gross Margin % = Gross Profit / Net Sales × 100

This financial logic is explained in the SQL project documentation.

# 🔍 Analysis Performed

**1. Sales Trend Analysis**

Monthly sales quantities were aggregated by product and date to identify sales movement over time.

The supplied result set recorded **263 units of observed sales**.

The observed sales were concentrated around product `A0118150101` in the supplied transaction sample.

**2. Customer Segmentation**

Customers were analyzed using:

* Total sales quantity
* Purchase months
* Gross revenue
* Channel
* Market
* Region

Customers were segmented into:

* High Value
* Medium Value
* Low Value

using SQL `CASE` logic based on observed sales quantity.

**3. Customer Performance Analysis**

Customer `70002018` was the largest observed customer in the supplied sample:

* **77 units**
* **1,185.43 gross revenue**
* Approximately **29.3% of observed unit sales**

Customer `70002017` followed with:

* 51 units
* 785.16 gross revenue

The report explicitly notes that the sample is too small and concentrated to treat this as enterprise-wide customer concentration risk.

**4. Product Performance Analysis**

Products were compared using:

* Total sales quantity
* Gross revenue
* Revenue ranking

SQL window functions were used to rank products based on revenue.

**5. Profitability & Cost Analysis**

Product profitability was analyzed by comparing:

```text
Gross Price - Manufacturing Cost
```

The supplied product-year observations showed gross-profit margins between approximately:

**69.07% and 71.41%**

For product `A0118150101`, reported margins were:

* 2018: 70.00%
* 2019: 70.89%
* 2020: 69.07%
* 2021: 71.05%

This indicates a relatively stable margin range within the supplied observations.

**6. Discount Impact Analysis**

Pre-invoice deductions were analyzed to determine their impact on gross revenue and net invoice revenue.

For example, customer `70002018` had:

* Pre-invoice discount: **29.56%**
* Gross revenue: **1,185.43**
* Discount amount: **350.41**
* Net invoice revenue: **835.02**

This demonstrates how customer discount structures can materially reduce realized invoice revenue.

**7. Forecast Accuracy / Demand Planning Analysis**

Forecasted demand was compared with actual sales.

The supplied sample showed:

* Forecast quantity: **81 units**
* Actual sales: **263 units**
* Variance: **+182 units**
* Actual-to-forecast ratio: **324.69%**

Importantly, the project itself notes that this 324.69% value is an **actual-to-forecast ratio**, not a conventional forecast-accuracy score.

The practical finding is that actual demand substantially exceeded forecast in the supplied sample.

**8. Freight Cost Analysis**

Average freight percentages were compared across the listed markets.

| Market    | Average Freight % |
| --------- | ----------------: |
| India     |            2.780% |
| Germany   |            2.260% |
| Indonesia |            1.907% |

India had the highest average freight percentage in the supplied sample.

This should be treated as a comparative observation rather than proof of structural inefficiency because the underlying dataset is limited.

**9. Customer Loyalty Analysis**

Customer loyalty was evaluated using:

* Active purchase months
* Number of fiscal years with purchases

All 11 observed active support customers were classified as **Low Loyalty** in the supplied sample, with an average of one active purchase month and one fiscal year with purchases.

The report notes that the result may reflect the deliberately small sample.

**10. Inventory Analysis**

Inventory was compared with observed sales quantities.

For product `A0118150101`:

* Inventory: 1,000
* Sales: 263
* Simple turnover proxy: 0.263

Products `A0118150102` and `A0118150103` recorded no observed sales and were classified as **Slow / No Movement**.

This turnover measure is only a proxy because historical inventory snapshots are unavailable.

**11. Channel Performance Analysis**

Sales and gross revenue were grouped by customer channel to understand channel-level contribution.

The supplied results showed that observed channel revenue and sales volume were concentrated in the **Direct** channel.

**12. Geographic Sales Analysis**

Sales were analyzed by:

* Region
* Market
* Sales quantity
* Gross revenue

The supplied result set was concentrated in **India/APAC**, limiting broader geographic conclusions.

**13. Product Mix Analysis**

Product mix was analyzed using:

* Sales volume
* Revenue
* Estimated gross profit

This provides a framework for considering both demand and profitability rather than evaluating products using margin alone.

**14. Customer Lifetime Value – Observed Revenue**

Observed gross revenue and purchase months were calculated for customers.

The analysis represents **observed gross revenue**, rather than a full predictive customer lifetime value model.

**15. Price Analysis**

The project analyzed product price and sales quantities by fiscal year to provide a basis for future price-demand analysis.

A full price elasticity calculation was not performed because the available dataset is limited.

**16. Market Expansion Analysis**

Forecast quantities were aggregated by market and fiscal year to identify markets with higher forecasted demand.

# 📈 Key Findings / Results

| Area                        | Key Result            |
| --------------------------- | --------------------- |
| Observed Sales              | 263 units             |
| Observed Gross Revenue      | 4,048.94              |
| Largest Observed Customer   | Customer 70002018     |
| Largest Customer Sales      | 77 units              |
| Largest Customer Revenue    | 1,185.43              |
| Largest Customer Unit Share | 29.3%                 |
| Observed Gross Margin Range | Approx. 69.07%–71.41% |
| Forecast Quantity           | 81 units              |
| Actual Sales                | 263 units             |
| Forecast Variance           | +182 units            |
| Actual-to-Forecast Ratio    | 324.69%               |
| Highest Average Freight %   | India – 2.780%        |
| Inventory – A0118150101     | 1,000 units           |
| Sales – A0118150101         | 263 units             |
| Inventory Turnover Proxy    | 0.263                 |

All figures above refer to the supplied project/sample result set rather than audited company-wide performance.

# 💡 Business Insights

1. Demand planning requires attention

Actual sales were substantially higher than forecast in the supplied sample.

This indicates that forecast assumptions should be recalibrated using customer-level historical demand and rolling sales patterns.

2. Customer concentration should be monitored

Customer `70002018` generated the highest observed quantity and revenue.

Because the dataset is small, this should be viewed as a monitoring signal rather than evidence of enterprise-wide concentration risk.

3. Discount governance can affect realized revenue

The 29.56% pre-invoice discount for customer `70002018` reduced gross revenue by 350.41 in the supplied calculation.

Discounts should therefore be evaluated alongside customer volume and profitability.

4. Product margins were relatively stable

The supplied product-year observations showed gross margins within a relatively narrow 69–71% range.

This provides a useful basis for monitoring future cost and pricing movements.

5. Freight costs vary across markets

India had the highest average freight percentage among the three listed markets.

Further analysis of routes, carriers, service levels and logistics economics could help identify cost drivers.

6. Inventory is concentrated around observed demand

Product `A0118150101` accounted for the observed sales activity in the supplied inventory sample, while two other products showed no observed sales.

Inventory planning should therefore consider actual demand patterns rather than treating all products equally.

7. The SQL framework can support recurring management reporting
The combination of relational modelling, reusable functions, stored procedures, triggers and analytical queries creates a foundation that could later be connected to a BI dashboard or recurring reporting process.

# 📌 Actionable Recommendations
Based on the supplied project analysis:
1. **Recalibrate demand forecasts** using customer-level historical sales.
2. Track **forecast bias and absolute error** separately from the project's actual-to-forecast ratio.
3. Monitor high-volume customers and repeat-purchase behavior.
4. Review high customer discounts against volume and margin contribution.
5. Investigate freight-cost drivers in markets with higher freight percentages.
6. Prioritize inventory planning based on observed demand.
7. Investigate products with no observed movement.
8. Evaluate product mix using both profitability and sales volume.
9. Add additional business data for deeper strategic analysis.
10. Develop a future dashboard for recurring monitoring.

# ⚠️ Data Limitations
The project has several important limitations:
* The supplied dataset is a small/sample dataset.
* Technical/support customer and product records are included.
* The observed results are concentrated around one product, one channel and one market/region.
* Customer Acquisition Cost cannot be calculated because acquisition-spend data is unavailable.
* Competitor benchmarking cannot be calculated because competitor data is unavailable.
* Customer satisfaction cannot be calculated because feedback data is unavailable.
* Marketing campaign effectiveness cannot be calculated because campaign/spend/response data is unavailable.
* Inventory turnover is only a simple proxy because historical inventory snapshots are unavailable.
* The project's forecast metric is an actual-to-forecast ratio and should not be labelled as a conventional forecast-accuracy percentage.
These limitations are explicitly identified in the project report.

# 🏁 Conclusion
This project demonstrates an end-to-end Finance and Supply Chain Analytics workflow using SQL Server, beginning with relational data preparation and progressing into sales, customer, profitability, discount, freight, forecasting and inventory analysis.
The supplied results indicate that demand planning, discount governance and product/inventory focus are particularly relevant areas for management attention within the sample.
The project also demonstrates how SQL can be used not only for data retrieval but for creating a repeatable analytical framework that can support management reporting and future dashboard development.
For a production-level implementation, the next stage would be to expand the historical dataset, introduce standardized forecast-error metrics, capture inventory snapshots and add customer acquisition, competitor pricing, satisfaction and marketing datasets.
