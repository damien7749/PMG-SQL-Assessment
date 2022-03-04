# PMG SQL Assessment

For the PMG SQL Challenge, I would be using MySQL Workbench as my SQL editor. To set up the environment for the challenege, I set up a server using MySQL, created a schema on MySQL workbench, created the 2 tables and imported data from store_revenue.csv and marketing_data.csv

## Question 1: Generate a query to get the sum of the clicks of the marketing data

To get the sum of the clicks, we would need aggregate sum function:

select sum(clicks) from marketing_data;

The result is 1792 clicks
 
## Question 2: Generate a query to gather the sum of revenue by geo from the store_revenue table

Since geo is from marketing_data table and revenue is from the store_revenue table, we would need to use join to combine the 2 tables to get the desired data:


select sum(R.revenue),S.geo from store_revenue R join marketing_data S on S.id=R.id group by S.geo;

Below is the result of the query:![Screen Shot 2022-03-03 at 8 17 45 PM](https://user-images.githubusercontent.com/64288013/156680812-14df88d8-43e6-4427-b8ac-39bc925f8b7c.png)

## Question 3: Merge these two datasets so we can see impressions, clicks, and revenue together by date and geo. Please ensure all records from each table are accounted for

We will use the same method from question 2 for this question:

select sum(R.revenue),S.impressions ,S.clicks from store_revenue R join marketing_data S on S.id=R.id group by S.geo,S.date;




