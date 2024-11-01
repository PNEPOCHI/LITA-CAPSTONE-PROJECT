# LITA-CAPSTONE-PROJECT
## TABLE OF CONTENT
[Project Overview](#project-overview)

[Data Source](#data-source)

[Data Tools](#data-tools)

[Data Preparation And Cleaning](#data-preparation-and-cleaning)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

[Findings and Results](#findings-and-results)

[Recommendation](#recommendation)

[License](#license)


### Project Overview
The goal of this project is to analyze sales performance data to uncover insights regarding sales trends, product performance and regional sales efficiency. This will involve using  Excel for data cleaning and preprocesing, SQL for data extraction and Power BI for interactive visualization and reporting.

### Data Source
This Dataset will be given on the respository.
 This entails Sales data from a retail company (which include transaction details, product categories, customer demographics, and regional data).

 ### DATA TOOLS
 EXCEL for Data cleaning and preprocesing
  SQL for Data extraction
  POWER BI for interactive visualization

### Data Preparation And Cleaning
#### STEP 1: DATA UNDERSTANDING AND PREPARATION

-  Load the Excel file and inspect the data fields, types, and overall data quality.
- Identify key columns and data structures.
- Note any duplicates
        
#### STEP 2: DATA CLEANING IN EXCEL
  -  Removed all duplicate rows that may distort the analysis.
-  Create new calculated fields, like total sales

  ### Exploratory Data Analysis 

 - summarize total sales by product, region, and month using pivot Table
  - using pivot tables to find subscription patterns.
  - What total sales for each product category. 
  - What number of sales transactions in each region. 
  - What is the highest-selling product by total sales value. 
  - What is total revenue per product. 
   - What is monthly sales totals for the current year. 
   - who are top 5 customers by total purchase amount. 
   - What the percentage of total sales contributed by each region. 
   - What products with no sales in the last quarter.
   - What is the total number of customers from each region. 
   - What the most popular subscription type by the number of customers. 
   - What is the average subscription duration for all customers. 
   - customers with subscriptions longer than 12 months. 
   - What is the total revenue by subscription type. 
   - What is the top 3 regions by subscription cancellations. 
   - What isthe total number of active and canceled subscriptions.

     ### Data Analysis
   #### TABLE 1(FINDINGS AND RESULT)
     
  
![TABLE 1 1](https://github.com/user-attachments/assets/8f5f169b-4432-44f2-92c9-241a24cc9532)

This table entails Total sales by Product, at end of the Analysis, it was determined that SHOE is the highest sold product with a Total sale of 613,380 while SOCKS is the lowest sold product with a Total Sale of 180,785

#### RECOMMENDATION

The marketing Department should focus more on SOCKS And the production department should focus on producing more SHOES

#### TABLE 2 (FINDINGS AND RESULT)

![TABLE 2](https://github.com/user-attachments/assets/36401b7b-3097-495d-abec-45d17cbfbc59)

This table entails Total sales by Region and Product, at end of the Analysis, it was determined that SOUTH has the highest sales with a value of 927,830 with SHOE as the highest sold product with a value of 546,300 and Socks lowest sold product with the value of 133,920

West has the lowest Sales with a value of 300,345 with Hat as the highest sold product with a value of 174,300 while Socks is the lowest sold with the value 46,865

East total sales value is 485,925 with shirt as the highest sold product with value of 237,600 and shoe is the lowest sold product with value of 37,200 

Nouth total sales value is 387,000 with shirt has highest sold product with value 248,000 and Hat is lowest sold product with a value of 34,720

According to my findings SOUTH has the highest sold product which is SHOE with value of 546,300 while NOUTH has the lowest sold product which is Hat with a value 34,720

#### RECOMMENDATION

 There should be increase in supply of product with high sales value while product with low sales value needs marketers

#### TABLE 3(FINDINGS AND RESULT)
 
![TABLE 3](https://github.com/user-attachments/assets/c076c075-4822-4174-8ad4-685747760d13)

This table entails total sales by month. At ending of the analysis, it was determined that in 2023 the highest sales were made in February with value of 247,500 while the lowest sales were made in April with a value of 7,425.

In 2024 the highest were made in February with the value of 298,800 while the lowest sales were made July with the value of 37,200

According to my findings February has the highest sales in both years while the April 2023 has the lowest sales

#### RECOMDATION

According to the sales trend more goods should be supply in February

#### TABLE 4(FINDINGS AND RESULT) 

![TABLE 4](https://github.com/user-attachments/assets/f477954c-0993-4677-8188-454077a2f9e3)

This table entails Revenue by subscription type, there are basically 3 types of subscription which are BASIC, PREMIUM AND STANDARD 
Basic has the highest Revenue with a value of 33,776,737 while Standard has the lowest Revenue with a value of 16,864,376 

#### RECOMDATION

Base on this Analysis, the company should have a promo package for STANDARD AND PREMIUM SUBSCRIPTION

#### SQL ANALYSIS
-	The file was converted to csv format and imported to SQL server
-	Tables were created for sales Data and customer data

QUERY 1 (Total sales for product category)
```sql  
select * from [dbo].[capstonesalesdata]
```
```sql
SELECT PRODUCT,sum(TOTAL_SALES) as totalsales
from [dbo].[capstonesalesdata]
GROUP BY PRODUCT
```
QUERY 2(NUMBER OF SALES TRANSACTION IN EACH REGION)
```sql
SELECT (region) AS region_count, SUM(quantity) AS total_quantity
FROM [dbo].[capstonesalesdata]
GROUP BY region
ORDER BY total_quantity ASC
```
QUERY 3(HIGHEST SELLING PRODUCT BY VALUE)
```sql
select product, max (total_sales) as highestsales
from [dbo].[capstonesalesdata]
group by product
order by highestsales DESC
```
QUERY 4(TOTAL REVUNUE PER PRODUCT)
```sql
SELECT Product, 
       SUM(TOTAL_SALES) AS TotalQuantitySold
FROM [dbo].[capstonesalesdata]
GROUP BY Product
ORDER BY TotalQuantitySold DESC
```
#### QUERY 4(TOTAL SALES FOR THE CURRENT YEAR 2023)
```sql
SELECT FORMAT(orderdate, '2023-01') AS yearmonth,
       SUM(total_sales) AS monthlysales
FROM [dbo].[capstonesalesdata]
WHERE YEAR(orderdate) = 2023
GROUP BY FORMAT(orderdate, '2023-01')
ORDER BY yearmonth
```
#### QUERY 5(TOP 5 CUSTOMER)
```sql
select top 5 
sum (total_sales) AS total_sales_sum, Customer_id
from [dbo].[capstonesalesdata]
group by customer_id
order by total_sales_sum desc
```
#### QUERY 6(PERCENTAGE OF TOTAL SALES BY REGION)
```sql
select region,
sum(total_sales) as totalrevenue,
(sum(total_sales)*100/(select sum(total_sales)from litasalesdata))as
sales_percentage
from
[dbo].[capstonesalesdata]
group by region
order by totalrevenue desc
```
#### QUERY 7(PRODUCT THAT WAS NOT SOLD IN THE LAST QUARTER)
```sql
SELECT product
FROM [dbo].[capstonesalesdata]
WHERE product NOT IN (
SELECT product
    FROM litasalesdata
    WHERE orderdate >= DATEADD(QUARTER, -1, GETDATE()) -- Last quarter
)
GROUP BY product
```
#### QUERY 8
```sql
select * from [dbo].[capstonecustomerdata]
```
(NUMBER OF CUSTOMER PER REGION)
```sql
SELECT COUNT(customerName) AS totalcustomer, region
FROM [dbo].[capstonecustomerdata]
WHERE region IN ('north', 'south', 'west', 'east')
GROUP BY region
ORDER BY region
```

#### QUERY 9 (MOST POPULAR SUBSCRIPTION TYPE BY NUMBER OF CUSTOMER)
```sql
SELECT 
    subscriptionType,
    COUNT(customerName) AS CustomerCount
FROM 
    [dbo].[capstonecustomerdata]
GROUP BY 
    subscriptionType
ORDER BY 
    CustomerCount DESC
```

#### QUERY 10 (CUSTOMER THAT CANCELED THEIR SUBSCRIPTION WITHIN 6MONTHS)
```sql
SELECT customerName
FROM [dbo].[capstonecustomerdata]
WHERE canceled = 'true' 
AND SubscriptionEnd >= DATEADD(MONTH, -6, GETDATE()) 
ORDER BY SubscriptionEnd DESC
```
#### QUERY 11 (SUBSCRIPTION DURATION FOR EACH CUSTOMER)
```sql
SELECT 
    customerName, 
    SUM(DATEDIFF(DAY, 
                 CONVERT(datetime, subscriptionStart, 120), 
                 CONVERT(datetime, subscriptionEnd, 120))) AS subscriptionDuration
From
    [dbo].[capstonecustomerdata]
GROUP BY 
    customerName
ORDER BY 
    SubscriptionDuration
```
   #### QUERY 12 (AVERAGE SUBSCRIPTION DURATION)
```sql
SELECT 
    AVG(subscriptionDuration) AS averageSubscriptionDuration
FROM (
    SELECT 
        DATEDIFF(DAY, subscriptionStart, subscriptionEnd) AS subscriptionDuration
    FROM 
        [dbo].[capstonecustomerdata]
    WHERE
        subscriptionStart IS NOT NULL AND
        subscriptionEnd IS NOT NULL
) AS customerDurations
```

#### QUERY 13(CUSTOMERS SUBSCRIPTION THAT IS MORE THAN 12 MONTHS)
```sql
SELECT
    customerName,
    DATEDIFF(MONTH, 
             CONVERT(datetime, subscriptionStart, 120), 
             CONVERT(datetime, subscriptionEnd, 120)) AS subscriptionDurationInMonths
FROM 
    [dbo].[capstonecustomerdata]
WHERE 
    subscriptionStart IS NOT NULL AND
    subscriptionEnd IS NOT NULL
    AND DATEDIFF(MONTH, 
                 CONVERT(datetime, subscriptionStart, 120), 
                 CONVERT(datetime, subscriptionEnd, 120)) > 12
```
#### QUERY 14(TOTAL REVENUE BY SUBSCRIPTION TYPE)
```sql
select
subscriptiontype,
sum(revenue) as totalrevenue
from [dbo].[capstonecustomerdata]
group by SubscriptionType
order by totalrevenue
```
#### QUERY 15(TOP 3 REGION BY SUBSCRIPTION CANCELATION)
```sql
SELECT TOP 3 region, COUNT(*) AS cancellation_count
FROM [dbo].[capstonecustomerdata]
WHERE canceled = 'TRUE'
GROUP BY region
ORDER BY cancellation_count DESC
```

#### QUERY 16(TOTAL NUMBER OF ACTIVE AND CANCELED SUBSCRIPTION)
```sql
SELECT 
  SUM(CASE WHEN canceled ='TRUE' THEN 1 ELSE 0 END) AS totalcanceled,
  SUM(CASE WHEN canceled = 'FALSE' THEN 1 ELSE 0 END) AS totalactive
FROM [dbo].[capstonecustomerdata]
```
### Data Visualization
#### POWER BI VISUALIZATION
-	The file was uploaded from excel workbook
-	The data was transformed by removing NULL columns
  
TABLE1 (SALES DATA)

 ![sales data](https://github.com/user-attachments/assets/762136ff-889f-42d1-88ca-12e79657c35d)

TABLE 2(CUSTOMER DATA)

![customer data](https://github.com/user-attachments/assets/d2c5c13d-3f50-461d-975f-f7950c3930f5)

### Findings And Results
In summary;
1.	Focus on Premium Subscribers: Since Premium subscribers are the highest contributors to revenue, focusing on retention, personalized offers, and loyalty programs for this segment will likely yield the highest .
2.	Target Basic  subscribers for Upselling: For customers in basic scription, targeted campaigns that encourage upgrades to Standard or Premium subscriptions could increase their lifetime value.
3.	Regional Marketing: High-performing regions should continue to be nurtured, while regions with a high proportion of Basic subscribers might benefit from promotional activities to encourage upgrades.
4.	Product and Inventory Optimization: Ensure sufficient stock of top-performing products, especially around peak sales months, to meet demand and minimize stockouts.
These findings enable data-driven strategies, helping the company to optimize customer engagement, increase revenue, and better manage customer retention.

### Recommendation
This segmentation model provides a strategic foundation to:

Tailor marketing and engagement strategies per segment to maximize customer lifetime value.
Focus on regions and subscription types driving the most revenue.
Enhance product management by prioritizing high-performing products and addressing low-performing ones.
Overall, this analysis enables data-driven decision-making, allowing for more effective resource allocation, targeted marketing efforts, and strategic planning aligned with customer behavior patterns.

### License
This repository is licensed by [Apache 2.0](apache-2.0)
