# PORTFOLIO-PROJECT-SQL-Query

## Project Overview: Sales Analysis Insights

### Project Aims:
The primary objective of this project is to provide comprehensive insights into sales performance through a rigorous analysis of various sales metrics. By leveraging data-driven approaches, the project aims to uncover patterns, trends, and key indicators that can guide strategic decision-making and enhance overall business performance.

## Key Components:

1. Data Collection and Preparation:
   - Gather and consolidate sales data from various sources, including transaction records, customer databases, and marketing analytics.
   - Cleanse and preprocess the data to ensure accuracy and consistency.

2. Exploratory Data Analysis (EDA):
   - Perform exploratory data analysis to understand the distribution and characteristics of sales data
   - Identify outliers, missing values, and potential areas of interest for further investigation.
3.Sales Trends and Patterns:

- Analyze historical sales data to identify trends and patterns over time.
- Utilize statistical methods and machine learning algorithms to predict future sales trends.

### The SQL Code

```sql
-- I want to see which sub-category sells the most with this code

SELECT 
      [Sub_Category]
      ,sum([Sales]) Sales
FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset]
  group by
  Sub_Category
  order by 2 desc
  -- Answer: We can see that the best-selling sub-category is Health Drinks.

-- 2 I want to see what sells the most with this code
  SELECT 
    Year (Order_Date) 'Year'
      ,sum([Sales]) Sales
FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset]
  group by
  Year (Order_Date)
  order by 2 desc
  -- Answer: We can see that in 2018, it sold the most (indicating a trend from 2015 to 2018).

-- Now, I want to see which category sells the most
  SELECT 
      [Category]
      ,sum([Sales]) Sales
FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset]
  group by
    Category
  order by 2 desc
  -- Answer: The most sold category is Eggs, Meat & Fish.

-- I want to see which month has the best sales
   SELECT 
      Month(Order_Date) 'Months Sales'
      ,sum([Sales]) Sales
FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset]
where
year(Order_Date)='2018'
  group by
    Month(Order_Date)
  order by 2 desc
  -- Answer: In 2018, September is the best month, and in 2015, 2016, 2017, November is the best month.

-- Now, let's see which month had the most sales and quantity in 2015
         SELECT 
		 distinct
      Month(Order_Date) 'Months Sales'
      ,sum([Sales]) Sales
	  ,count([Order_Date]) quantity
FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset]
where
year(Order_Date)='2015'
  group by
    Month(Order_Date)
  order by 2 desc
  -- Answer: In 2015, 2016, 2017, the best month is November, and in 2018, September is the best month.

-- Now, let's see which category sells the most in November
       SELECT 
		 distinct
		 category
      ,Month(Order_Date) 'Months Sales'
      ,sum([Sales]) Sales
	  ,count([Order_Date]) quantity
FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset]
where
Month(Order_Date)= 11
  group by
  category
,Month(Order_Date)
  order by 3 desc
  -- Answer: In November, the most sold category is Snacks (وجبات خفيفة).

-- Now, let's see the best customers based on quantity
    SELECT 
		 distinct
		Customer_Name

      ,sum([Sales]) Sales
	  ,COUNT( [Order_ID]) quantity
	  ,max([Order_Date]) 'last order date'
	 ,( select max([Order_Date]) FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset] ) 'Max order date'
	 ,DATEDIFF(DD,max([Order_Date]),( select max([Order_Date]) FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset] )) Recency
FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset]

  group by
 Customer_Name
  order by 3 desc
  -- Answer: This query provides information on the best customers based on quantity.

-- Now, let's see which sub-category sells the most in March
  SELECT 
		 distinct
		 [Sub_Category]
      ,Month(Order_Date) 'Months Sales'
      ,sum([Sales]) Sales
	  ,count([Order_Date]) quantity
FROM [Ali ETL].[dbo].[Supermart Grocery Sales - Retail Analytics Dataset]
where
Month(Order_Date)= 8
  group by
  [Sub_Category]
,Month(Order_Date)
  order by 3 desc
  -- Answer: In March, the best-selling sub-category is Health Care.

-- Now, using this code, I will first use the CAST function to convert from string to numeric values, 
-- and then I will see how it sells in different departments (A, B, C) based on payment, quantity, and gross income.

  SELECT 
      [Branch]
      ,[City]
      ,[Customer type]
      ,[Payment]
      ,[Quantity]
      , sum(cast([gross income] as numeric)) 'Gross income'

  FROM [Ali ETL].[dbo].[supermarket_sales - Sheet1]
  where  Payment='cash'
  and Branch='B'
  group by
      [Branch]
      ,[City]
      ,[Customer type]
      ,[Payment]
      ,[Quantity]
	order by 6 desc
```



   
