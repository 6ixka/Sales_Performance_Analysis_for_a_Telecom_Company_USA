# Sales_Performance_Analysis_for_a_Telecom_Company_USA
A Data Analysis Project that Analysed  the sales performance of a Telecommunication  company Based in the United State. The company’s sales transaction data generated over the past years was used for this  analysis.

## Table of Content
[Project Overview](#project-overview)  <br> <br>

[Data Sources](#data-sources) <br> <br>

[Data Analysis Tools Used](#data-analysis-tools-used) <br> <br>

[Data Collection](#data-collection)  <br> <br>

[Data Cleaning and Formatting](#data-cleaning-and-formatting)  <br> <br>

[Loading Data into Power BI](#loading-data-into-power-bi) <br> <br>

[Exploratory Data Analysis (EDA)](exploratory-data-analysis-(eda))  <br> <br>

[Data Analysis](#data-analysis) <br> <br>
[]()
[]()
## Project Overview: 
This Data Analysis Project aims to provide  insights into the sales performance of a Telecommunication  company Based in the United State. 
__About the Company:__ The Telecommunication Company operates a B2B business model and  sells a wide variety of cell phones and devices, including __smartphones, tablets, smartwatches__.  They offer devices from all of the major manufacturers, such as Apple, Samsung, Google, and Motorola.

Various aspects of the company’s sales transaction data generated over the past years was  analysed  to gain insights into their __Customer Behaviour, Product Popularity, Top Performing  Channel of Marketing, Regional Performance  and Revenue Trends__ of the company since it began. 

We seek to identify __Top performing customers, products, channels of sales , region , trends, and the overall performance of the company__ , to enable the company to make data-driven decisions/recommendations and to gain a deeper understanding of the company’s overall performance. 

1. sales performance by customers <br> <br>

<img width="956" alt="Customer behaviour_SS" src="https://github.com/6ixka/Sales_Performance_Analysis_for_a_Telecom_Company_USA/assets/163520580/99187309-d74c-4f66-b8a6-ebdf58a557c9">

2. sales performance by channels <br> <br>

<img width="960" alt="Sales by channels_ss" src="https://github.com/6ixka/Sales_Performance_Analysis_for_a_Telecom_Company_USA/assets/163520580/b25787b9-33fe-45a4-a1f8-d67200639c44">

3. sales performance by region  <br> <br>

<img width="960" alt="Sales by region_ss" src="https://github.com/6ixka/Sales_Performance_Analysis_for_a_Telecom_Company_USA/assets/163520580/95682fb9-3909-46c1-b57e-6b3599e8f39f">

4. sales trends over the years <br> <br>

<img width="958" alt="Sales Trend over the years_ss" src="https://github.com/6ixka/Sales_Performance_Analysis_for_a_Telecom_Company_USA/assets/163520580/5802ae1c-7870-4cee-9688-63e9ec998064">




## Data Sources
__Sales Transaction Data:__ The primary dataset used for this data analysis project was sales transaction data, containing detailed information about each sales made by the company , and was extracted from the company’s database using __SQL codes__. 

Several SQL complex queries were written to the company’s database in order to extract the required data for this  data analysis project. 

Each SQL complex query was used to extract a particular aspect of the company’s sales data. 
The results were downloaded and saved as  the following csv files below: <br> <br>
                                                                                
“customers_behaviour_V2.csv” <br> <br>
“revenue_generated_by_channels_all_time_V2.csv” <br> <br>
“revenue_generated_by_region_all_time_V2.csv” <br> <br>
“revenue_trend_over_the_years_V2.csv” <br> <br>

## Data Analysis Tools Used:
- __SQL (PostgreSQL)__  <br> <br>
 for Data Collection <br> <br>
 for Data Cleaning <br> <br>
 for Data Analysis <br> <br>
- __Power BI__ <br> <br>
 for Data Modelling <br> <br>
 for Data Analysis <br> <br>
 for Data Visualization <br> <br>
 for Creating an Interactive Report <br> <br>

 ## Data Collection: 
-  __Database Inspection:__  In the initial data collection phase  I  inspected the company’s database using SQL code  to check for missing data __(NULL)__ in each of the tables in the company’s database. <br> <br>
- I extracted the  required data for the purpose of the data analysis project using __SQL complex query and SQL data aggregation__.  

 ## Data Cleaning and Formatting:
 - I used SQL codes to clean and format the data to conform to the required data format.
 - I downloaded the result of my SQL Queries from the company’s database  as a __csv file__ to my PC.

  ## Loading Data into Power BI:
- I loaded the downloaded csv files into Power BI for the purpose of Data Visualization and Building interactive dashboard/report.

  ## Exploratory Data Analysis (EDA):
 EDA involves exploring the sales data in order to answer some key questions such as : 
- Who are the top 10 customers of the company ?
- What particular products are the Top customers buying  ? 
- Comparative analysis to find out  the top selling product ?
- What Is the Total quantity of items a particular customer has ever bought from the company ? 
- What is the Total revenue generated by the company from a particular customer ? 
- What are the top performing channels of sales ? 
- What is the Total quantity of items sold through a particular channel ?
- What is the  Total Revenue generated  through a particular channel ?
- Which region is the best performing region ? 
- What is the Total quantity of items sold in a particular region ?
- What is the  Total Revenue generated  in a particular region?
- What is the peak sales period ? 
- What is the sales performance at a particular given time (year, month, day) ?  
- What is the sales trend between a particular period of time ? 
- What is the overall sales Trend of the company over the years ? 
- What is the overall sales performance of the company ?

  ## Data Analysis :
  
 ```SQL
  
  /* QUERY 1: SQL CODE SOLUTION FOR EXTRACTING THE Total Items and Total revenue generated by each customer  (CUSTOMERS BEHAVIOUR) */
 
SELECT a.name AS customers_name,
       SUM(o.smartphones_qty) ,
       SUM(o.smartwatches_qty),
       SUM(o.tablets_qty),
       SUM(o.total) AS total_quantity,
       SUM(o.total_amt_usd)AS total_revenue_usd
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY customers_name
ORDER BY total_revenue_usd  DESC

/*  QUERY 2 : SQL CODE SOLUTION FOR EXTRACTING THE Total Items and Total revenue generated by the company’s various channels of sales (SALES BY CHANNELS) */

SELECT w.channel AS channel_name,
       SUM(total) AS total_quantity,
       SUM(total_amt_usd) AS total_revenue_usd
FROM  orders o
JOIN accounts a
ON o.account_id=a.id
JOIN web_events w
ON a.id=w.account_id
GROUP BY channel_name
ORDER BY total_revenue_usd DESC

/* QUERY 3:SQL CODE SOLUTION FOR EXTRACTING THE Total Items and Total revenue generated by the company’s various regions of operations (SALES BY REGIONS) */

SELECT r.name AS region_name,
       SUM(o.total) AS total_quantity,
       SUM(o.total_amt_usd)AS total_revenue_usd
FROM orders o
JOIN accounts a
ON a.id = o.account_id
JOIN sales_reps s
ON a.sales_rep_id = s.id
JOIN region r
ON s.region_id = r.id
GROUP BY region_name
ORDER BY total_revenue_usd DESC


/* QUERY 4 : SQL CODE SOLUTION FOR EXTRACTING THE Total Items and Total revenue trend of the company over the years since inception (REVENUE TRENDS OVER THE YEARS) */

SELECT DATE_TRUNC ('year', occurred_at) AS year,
       SUM(total) AS total_quantity,  
       SUM (total_amt_usd) AS total_revenue_usd
FROM orders
GROUP BY year  
ORDER BY year 
```
## Results and Findings: 

The Analysis Results is summarised as follows: 

- The Company’s Top 3  Customers by ranking are 
  - 1st: EOG Resources : Bought a total of 56,410 items and has generated a Total revenue of  $382,870
  - 2nd: Mosaic :  Bought a total of 49,246 items and has generated a Total revenue of $345,620
  - 3rd: IBM :    Bought a total of 47,506 items and has generated a Total revenue of $326,820
 - The top 10 customers are buying smartphones and smartwatches in almost the same proportion with a slightly higher preference for smartphones .
 - The Overall Top selling product is smartphones , accounting for over 52% percent of total  sales and Revenue. 
 - The top performing channel of sales is Direct channel,  accounting for over 61 % percent of total  Sales and Revenue. 
 - The best performing region is the Northeast Region , accounting for over 33 % percent of total  Sales and Revenue. 
 - The company’s sales have been steadily increasing over the past years  with a noticeable peak in the holiday season in  2016, followed by a sudden decline in sales from 2017.

## Recommendations: 
__Based on the findings/results of this  data analysis project, I strongly  recommend the following actions :__
- The company should focus on expanding and promoting the smartphone product category. 
- The company should invest in marketing and promotions during peak sales season to maximise revenue. 
- The company should implement a customer segmentation strategy to target smartphones and smartwatches customers effectively. 
- The company should allocate more budget and resources to their Direct sales channel to maximise revenue. 
- The company should invest more resources  in their Northeast Region of operation  to maximise revenue. 


 
 




  





