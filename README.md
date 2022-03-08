# PMG SQL Assessment

For the PMG SQL Challenge, I would be using MySQL and MySQL Workbench. To set up the environment for the challenege, I set up a server using MySQL, created a schema on MySQL Workbench, created the 2 tables and imported data from store_revenue.csv and marketing_data.csv.

## Question 1: Generate a query to get the sum of the clicks of the marketing data

To get the sum of the clicks, we would need aggregate sum function:

SELECT SUM(clicks) FROM marketing_data;

The result is 1792 clicks

## Question 2: Generate a query to gather the sum of revenue by geo from the store_revenue table

Since geo is from marketing_data table and revenue is from the store_revenue table, we would need to use join to combine the 2 tables to get the desired data:

SELECT SUM(SRT.revenue),MDT.geo FROM store_revenue SRT JOIN marketing_data MDT ON MDT.id=SRT.id group by MDT.geo;

Below is the result of the query:

![Screen Shot 2022-03-04 at 1 55 18 AM](https://user-images.githubusercontent.com/64288013/156714553-efec21ce-b787-437f-922b-734a36fff90d.png)

## Question 3: Merge these two datasets so we can see impressions, clicks, and revenue together by date and geo. Please ensure all records from each table are accounted for

We will use the same method from question 2 for this question:

SELECT MDT.impressions,MDT.clicks,SRT.revenue,MDT.date,MDT.geo FROM store_revenue SRT INNER JOIN marketing_data MDT on MDT.id=SRT.id

Below is the result of the query:

![Screen Shot 2022-03-08 at 5 46 00 PM](https://user-images.githubusercontent.com/64288013/157338592-d65018eb-4a00-4ff5-8dc1-be7acc94d4ef.png)

## Question 4: In your opinion, what is the most efficient store and why?
The most efficient store is:
- The store with the highest ratio of clicks to impressions, or click-through rate (CTR). We can calculate CTR by dividing the number of clicks by the number of impressions:

SELECT id, geo, (clicks/impressions)*100 AS CTR FROM marketing_data

![Screen Shot 2022-03-06 at 9 48 44 AM](https://user-images.githubusercontent.com/64288013/156928342-af894082-3126-4398-8328-6b0142a92e83.png)

Store with id 4 has the highest CTR (58.4%)

- The store with the highest profit. Revenue alone cannot indicate how effcient a store is because we have to take into account other external factors such as state sales tax, rent, and employee wages which differ depending on the state.

## Question 5: Generate a query to rank in order the top 10 revenue producing states

To rank in order the top 10 revenue producing states, we would be utilizing the DENSE_RANK function:

SELECT *
FROM(SELECT store_location,
DENSE_RANK() OVER (ORDER BY revenue DESC) AS revenue_rank
FROM store_revenue)
AS a
WHERE revenue_rank <=10;

This is the result of the query:

![Screen Shot 2022-03-04 at 2 37 06 AM](https://user-images.githubusercontent.com/64288013/156719952-b7637f30-cd42-4ad6-88f7-629b91b53472.png)




