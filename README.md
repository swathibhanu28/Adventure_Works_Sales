# Adventure_Works_Sales

Power BI project analyzing global sales, profitability, customer demographics, and product returns for Adventure Works, a multinational bike and cycling-accessories manufacturer.

## Project Overview

This project analyzes three years (2020-2022) of Adventure Works sales transactions to understand revenue performance, profitability, customer demographics, and regional sales patterns. The dataset covers **56,046 order line items** across **25,164 orders** placed by **17,416 customers** in 6 countries.

A star-schema data model was built in Power BI, connecting one fact table (Sales) to five dimension tables and a separate Returns fact table, with custom DAX measures driving a 4-page interactive dashboard.


## Dataset Information

- **Source:** Adventure Works sales sample dataset
- **Sales records:** 56,046 line items (2020-2022)
- **Time Period:** January 2020 - June 2022
- **Customers:** 17,416 unique
- **Products:** 130 unique SKUs sold 
- **Countries:** United States, Canada, United Kingdom, Germany, France, Australia

**Tables used:**
| Table | Description |
|---|---|
| `Sales Data` (2020/2021/2022) | Order date, product, customer, territory, quantity per line item |
| `Returns Data` | Returned product, return date, territory, quantity |
| `Product Lookup` | SKU, name, color, size, cost, price |
| `Product Subcategories Lookup` | Subcategory → category mapping |
| `Product Categories Lookup` | Bikes, Components, Clothing, Accessories |
| `Customer Lookup` | Demographics — age, gender, income, education, occupation, marital status |
| `Territory Lookup` | Region, country, continent |
| `Calendar Lookup` | Date dimension for time intelligence |


## Objectives

- Track sales and profit trends over time
- Identify which product categories and regions drive the most revenue
- Profile the customer base by demographics
- Quantify and locate product returns
- Translate findings into concrete business recommendations


## Tools & Technologies

- Power BI Desktop
- Power Query (data cleaning & transformation)
- DAX (custom measures, time intelligence)
- Star-schema data modeling
- Bing Maps visual (geographic sales)


## Data Modeling

Built a star schema with `Sales Data` as the central fact table:

- **Sales Data** - `Customer Lookup` (many-to-one on CustomerKey)
- **Sales Data** - `Product Lookup` (many-to-one on ProductKey)
- **Sales Data** - `Territory Lookup` (many-to-one on TerritoryKey)
- **Sales Data** - `Calendar Lookup` (many-to-one on OrderDate)
- **Product Lookup** - `Product Subcategories Lookup` → `Product Categories Lookup` (snowflaked product hierarchy)
- **Returns Data** - `Product Lookup` and `Territory Lookup` (separate fact table, shares dimensions with Sales)


### Data Cleaning (Power Query)

- Combined three yearly sales files (2020, 2021, 2022) into a single Sales table
- Corrected data types (dates, keys, numeric fields)
- Built the product hierarchy by joining Product → Subcategory → Category
- Verified referential integrity between fact and dimension tables before modeling

### DAX Measures

measures were written to support the dashboard, ranging from simple aggregations to explicit time-intelligence and iterator-based calculations:

| Measure | Technique |
|---|---|
| Total Sales (Australia) / Total Sales (US) | Filtered measures |
| Total Txn Amt (Explicit Measure) | Explicit DAX |
| Total Profit (Explicit Measure) | Explicit DAX |
| Avg Sales | Average aggregation |
| Max Txn Amt | Max aggregation |
| Profit(%) | Ratio measure |
| Total Orders / Total Products | Distinct counts |
| Unique Customers (who purchased) | Distinct count with filter |
| Unique Products Sold | Distinct count |



## Dashboard Overview

The dashboard has **4 pages**, navigated through a custom icon-based menu:

**1. Summary** - KPI cards, sales & profit trend over time, sales by product category, sales by region, products sold vs. returns by country

<img width="1377" height="734" alt="image" src="https://github.com/user-attachments/assets/2af0c1cd-a037-45cd-bfdf-376aac73fb14" />


**2. Customers** - Education level, marital status, occupation, and age distribution, with slicers for gender, homeowner status, and income category

<img width="1355" height="741" alt="image" src="https://github.com/user-attachments/assets/b323a89b-4a7c-4389-bd54-2906802141c9" />


**3. Region** - Country-wise sales on an interactive map, region-wise sales bar chart

<img width="1348" height="744" alt="image" src="https://github.com/user-attachments/assets/a5741bee-2798-4328-8ebb-7d215fbf4248" />


**4. Products** - Sales by bike subcategory, sales by product color

<img width="1370" height="739" alt="image" src="https://github.com/user-attachments/assets/c68344b9-008d-46f7-bb5d-ed2691c7bbce" />


### Key Metrics

| Metric | Value |
|---|---|
| Total Sales | $24.9M |
| Total Profit | $10.46M |
| Profit Margin | ~42% |
| Total Orders | 25,164 |
| Total Customers | 17,416 |
| Products Sold | 130 |
| Total Returns (units) | 1,828 |
| Return Rate (by units sold) | ~2.2% |


## Key Insights

- **Bikes drive ~95% of revenue** ($23.6M); Accessories and Clothing trail far behind despite a much larger SKU count.
- **Road Bikes is the top subcategory** ($11.3M), ahead of Mountain Bikes ($8.6M) and Touring Bikes ($3.8M).
- **Sales grew ~3x** from ~$585K/month (Jan 2020) to ~$1.8M/month (mid-2022).
- **US and Australia are the top markets**, together over 60% of revenue; UK, Germany, France, and Canada follow.
- **Revenue is concentrated in a few regions** - Australia and US Southwest/Northwest lead, while Southeast, Northeast, and Central US are negligible.
- **Black, Red, and Yellow are the best-selling colors**, with Black alone outselling the next two combined.
- **Accessories have the highest return volume** (1,130 units) despite the lowest revenue share.
- **Core customers are aged 40–70** with Bachelors/Partial College education, mostly in Professional or Skilled Manual occupations.


## Business Recommendations

- **Diversify category revenue** - bundle Accessories/Clothing with bike purchases to grow attachment rate.
- **Investigate Accessories returns** - disproportionately high return volume suggests a quality or sizing issue worth a root-cause review.
- **Prioritize Road and Mountain Bikes** in inventory and marketing, since they drive ~84% of bike revenue.
- **Expand underperforming US territories** (Southeast, Northeast, Central) - likely a distribution gap, not low demand, given strong Southwest/Northwest performance.
- **Target the 40-70, Bachelors/Partial-College segment** in campaigns, as it's the proven core customer base.



## Conclusion

This project shows that Adventure Works' growth has been strong but narrow - concentrated in Bikes, in two countries, and in a handful of regions within those countries. The dashboard surfaces where the business is winning (Road/Mountain Bikes, US, Australia) and where there's untapped opportunity (Accessories/Clothing growth, underperforming US territories, Accessories return rates) - turning raw transactional data into a clear set of next steps for the business.


## Project Files

- `AdventureSales.pbix` - Power BI project file 
