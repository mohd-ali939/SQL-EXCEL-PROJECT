# SQL-EXCEL-PROJECT
I would like share the Query used to analyse the data from Pizza Sales here:

# Total Revenue
SELECT 
    ROUND(SUM(total_price), 0) AS Total_Revenue
FROM
    pizza_sales;

#Average order value 
SELECT 
    ROUND(SUM(total_price) / COUNT(DISTINCT order_id),
            2) AS Average_Order_Value
FROM
    pizza_sales;

#Total Pizza sold

SELECT 
    SUM(quantity) AS Total_pizza_sold
FROM
    pizza_sales;

#Total orders placed
SELECT 
    COUNT(DISTINCT order_id) AS Total_Orders
FROM
    pizza_sales;

# Average Pizzas per order
SELECT 
    ROUND(SUM(quantity) / COUNT(DISTINCT order_id),
            2) AS Average_Pizzas_per_Order
FROM
    pizza_sales;

# total pizza order in days of week
SELECT 
    DAYNAME(STR_TO_DATE(order_date, '%d-%m-%Y')) AS Order_Day,
    COUNT(DISTINCT order_id) AS Total_order
FROM
    pizza_sales
GROUP BY Order_Day;

 #total Pizza sold on hours basis
SELECT 
    HOUR(order_time) AS Order_hour,
    COUNT(DISTINCT order_id) AS Total_order
FROM
    pizza_sales
GROUP BY Order_hour
ORDER BY 1 ASC;

# Percent of sales by Pizza Category
SELECT 
    pizza_category,
    ROUND(SUM(total_price) * 100 / (SELECT 
                    SUM(total_price)
                FROM
                    pizza_sales),
            2) as percent_contribution
FROM
    pizza_sales
GROUP BY pizza_category;

#Percentage of sales by pizza size
 SELECT 
    pizza_size,
    ROUND(SUM(total_price) * 100 / (SELECT 
                    SUM(total_price)
                FROM
                    pizza_sales),
            2) AS Percent_contribution
FROM
    pizza_sales
GROUP BY pizza_size;                                                                      

#Total Pizzas sold by pizza category

SELECT 
    pizza_category, SUM(quantity) AS Total_pizza_sold
FROM
    pizza_sales
GROUP BY pizza_category
Order by Total_pizza_sold desc;

#Top 5 best sellers by total pizza sold

SELECT 
    pizza_name, SUM(quantity) AS Total_pizza_sold
FROM
    pizza_sales
GROUP BY pizza_name 
Order by Total_pizza_sold desc
Limit 5;

#Bottom 5 worst sellers by total pizza sold

SELECT 
    pizza_name, SUM(quantity) AS Total_pizza_sold
FROM
    pizza_sales
GROUP BY pizza_name 
Order by Total_pizza_sold asc
Limit 5;
