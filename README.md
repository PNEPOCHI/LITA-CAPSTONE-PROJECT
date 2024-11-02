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
This Dataset will be given on the repository.
 This entails Sales data from a retail company (which include transaction details, product categories and regional data).

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
 - What total sales for each product category. 
  - What number of sales transactions in each region. 
  - What is the highest-selling product by total sales value. 
  - What is total revenue per product. 
   - What is monthly sales totals for the current year. 
   - who are top 5 customers by total purchase amount. 
   - What the percentage of total sales contributed by each region. 
   - What products with no sales in the last quarter.
   - What is the total number of customers from each region. 
     

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

### Data Visualization

#### POWER BI VISUALIZATION
-	The file was uploaded from excel workbook
-	The data was transformed by removing NULL columns
  
TABLE1 (SALES DATA)

 ![sales data](https://github.com/user-attachments/assets/762136ff-889f-42d1-88ca-12e79657c35d)


### Findings And Results
In summary;
In summary :

  •	Shoe is the highest sold product
  
  •	South the best-performing in terms of total sales.


### Recommendation
1.	Targeted Marketing Campaigns:
 -	Allocate marketing resources more effectively by focusing on high-revenue regions and promoting top-selling products.
  -	Create region-specific promotions based on performance, such as discounts for lower-performing regions to boost sales.
    
2.	Product Strategy:
  -	Increase stock and promote products that are in high demand.
  -	Review pricing strategies for low-performing products to make them more attractive or bundle them with popular items to increase sales.
    
3.	Seasonal Promotions:
  -	Plan targeted promotions and campaigns during months identified as high sales periods to maximize revenue.
  -	Prepare ahead for low-sales months by launching new promotions or product bundles to stimulate demand.
    
4.	Customer Retention Programs:
  -	Identify top customers and consider implementing loyalty programs or exclusive offers to maintain their engagement and increase their lifetime value.
    
5.	Pricing Adjustments:
  -	Evaluate if there’s room for adjusting the pricing of certain products to optimize profit margins without significantly impacting sales volume.
  -	Introduce discounts or value packs for slower-moving items to increase their turnover rate.
    
### License
This repository is licensed by [Apache 2.0](apache-2.0)
