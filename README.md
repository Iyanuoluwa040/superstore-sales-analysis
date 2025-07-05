# Superstore-Sales-Analysis

## Table of Content
  - [Project Overview](#project-overview)
  - [Data Sources](#data-sources)
  - [Data Analysis](#data-analysis)
  - [Key Insight](key-insight)
  - [Recommendation](#recommendation)
  - [Conclusion](#conclusion)

### Project Overview

A data driven sales performance dashboard analyzing over 9,575 retail transactions to uncover what’s working and what’s not. This project explores profit margins, customer segments, product categories, and shipping efficiency to deliver actionable insights and KPIs. Includes interactive pivot tables, visual dashboards, and recommendations for business optimization.

![Customer](https://github.com/user-attachments/assets/10c8bc6b-6cc8-4024-87f3-a060610196a9)

### Data Sources

- Dataset Name: Sample Superstore Dataset. [Download here](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)
- Format: CSV file 

Fields Included:

- Order Details: Order ID, Order Date, Ship Date, Ship Mode
- Customer Info: Customer ID, Customer Name, Segment, Region, Country
- Product Info: Product ID, Category, Sub-Category, Product Name
- Performance Metrics: Sales, Quantity, Discount, Profit 

### Tools

  - MySql - Data cleaning 
  - Excel - Pivot tables and dashboard layout 

### Data Cleaning

In the data preparation phase, i perform the following task
1. Create a table structure
2. Import the data
3. Clean column formats dates, strings
4. Create calculated columns shipping delay
5. Remove duplicates

### Exploratory Data Analysis

The goal of EDA was to understand patterns, trends, and anomalies in the sales dataset, such as 

  - What is working?
  - What is not working?
  - what we should focus on

### Data Analysis
Include some code worked with

```sql
SELECT * FROM new_schema.`sample - superstore`;

create table Saging
like C;

Insert into saging
Select*
from new_schema.`sample - superstore`;

Select *
from saging;

Select *,
row_number() over (
	partition by 'Order ID', 'Order Date', 'Ship Date', 'Ship Mode', 'Customer ID' , 'Customer Name', Segment,
    Country, City, State, 'Postal Code', Region,
	'Product ID', Category, 'Sub-Category', 'Product Name', Sales, Quantity, Discount, Profit) as ranking
from saging;


With dup_cte as
(
Select *,
row_number() over (
	partition by 'Order ID', 'Order Date', 'Ship Date', 'Ship Mode', 'Customer ID' , 'Customer Name', Segment,
    Country, City, State, 'Postal Code', Region,
	'Product ID', Category, 'Sub-Category', 'Product Name', Sales, Quantity, Discount, Profit) as ranking
from saging
) 
Select *
from Dup_cte
where ranking >1;


CREATE TABLE `saging2` (
  `Row ID` int DEFAULT NULL,
  `Order ID` text,
  `Order Date` text,
  `Ship Date` text,
  `Ship Mode` text,
  `Customer ID` text,
  `Customer Name` text,
  `Segment` text,
  `Country` text,
  `City` text,
  `State` text,
  `Postal Code` int DEFAULT NULL,
  `Region` text,
  `Product ID` text,
  `Category` text,
  `Sub-Category` text,
  `Product Name` text,
  `Sales` double DEFAULT NULL,
  `Quantity` int DEFAULT NULL,
  `Discount` double DEFAULT NULL,
  `Profit` double DEFAULT NULL,
  `ranking` int
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


Insert into saging2
Select *,
row_number() over (
	partition by 'Order ID', 'Order Date', 'Ship Date', 'Ship Mode', 'Customer ID' , 'Customer Name', Segment,
    Country, City, State, 'Postal Code', Region,
	'Product ID', Category, 'Sub-Category', 'Product Name', Sales, Quantity, Discount, Profit) as ranking
from saging;


    
select *
from saging2;

     Delete
 from saging2
 where ranking >1;
    
 alter table saging2
 drop column ranking

```

### Key Insight

What’s Working and What’s Not

1. High-Performing Products:
   - Copiers, Phones, Accessories, Paper, Labels all have strong profit margins (20–42%) and solid sales.
   - These items generate a healthy return on investment and should be promoted or scaled.

2. Top Segments & Quarters:
   - The Consumer Segment leads in total sales ($1.14M).
   - Q3 and Q4 contribute the highest sales and profit.

3. Efficient Shipping:
   - Same Day shipping has the lowest average delay (0.05 days) and still supports profitable sales.

4. Unprofitable Sub-Categories:
   -  Tables, Bookcases, and Machines are losing money, despite high sales.
   -  Example: Tables lost $17,590 despite generating over $200K in sales.

5. Low Profit Margins:
   - Binders and Chairs are selling a lot but deliver very low or negative margins, indicating possible over discounting or cost issues.

6. Shipping Delays:
   -  Standard Class has the longest delay (5 days average), which may affect customer satisfaction in the long run.

### Recommendation 

  - Double down on high-margin items (Copiers, Paper, Accessories).
  - Review pricing/costs for loss-making items like Tables and Machines.
  - Reassess discount strategy for Binders and Chairs consider margin-based discount control.
  - Improve efficiency in Standard Class shipping to reduce delays.

### Conclusion

This analysis reveals critical insights into the performance of sales, product categories, customer segments, and shipping practices.

  - The business demonstrates strong overall performance, with over $2.26 million in sales and a profit of $281K, supported by high-margin products like Copiers, Accessories, and Paper.
  - However, several high sale items such as Tables, Machines, and Binders are either underperforming or even incurring losses, primarily due to low or negative profit margins.       		This suggests potential inefficiencies in pricing, procurement, or discount strategies.
  - The Consumer segment and Quarters lead in both sales and profitability, indicating these are strong markets worth investing further in.
  - Shipping analysis reveals that Same Day and First Class methods are more efficient than Standard Class, which has the longest delays, potentially impacting customer satisfaction.    

  
    
    


