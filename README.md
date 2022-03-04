# PMG SQL Assessment
For the PMG SQL Challenge, I would be using MySQL Workbench as my SQL Editor. After creating the Schema, creating tables
## Question 1: Generate a query to get the sum of the clicks of the marketing data
To get the sum of the clicks, we would need aggregate sum function:

select sum(clicks) from marketing_data;
 
## Question 2: Generate a query to gather the sum of revenue by geo from the store_revenue table

Since geo is from marketing_data table and revenue is from the store_revenue table, we would need to use join to combine the 2 tables to get the desired data:

select sum(R.revenue),S.geo from store_revenue R join marketing_data S on S.id=R.id group by S.geo;

