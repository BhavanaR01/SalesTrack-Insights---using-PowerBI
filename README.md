ShopNext Store Analysis
This project features a comprehensive Power BI dashboard designed to provide key insights into sales performance for a retail store named "ShopNext." The dashboard uses a variety of visualizations to analyze sales, orders, and customer behavior, helping stakeholders make data-driven decisions.

Key Features and Metrics
The dashboard is divided into several sections, each focusing on a different aspect of the business:

Total Sales Overview: A quick-glance section showing the total sales (14.2M), delayed orders (7K), and early orders (89K).

Product Performance: Visualizations that rank the top 10 highest and lowest-rated products, allowing for easy identification of popular and underperforming items.

Customer & Order Analysis:

Delayed Orders by Product Category: A bar chart showing which product categories have the most delayed orders, helping to pinpoint supply chain or fulfillment issues.

Early and Delayed Orders by Month: A line chart that tracks the trend of both early and delayed orders over time, providing a clear view of operational efficiency.

Revenue and Seasonal Trends:

State-Wise Analysis: A bar chart displaying sales performance across different states.

Revenue Analysis: A line chart that has trended over the years, from 2017 to 2019.

Seasonal Sales Analysis: A bar chart that breaks down sales by quarter, useful for understanding seasonal buying patterns.

Payment & Product Insights:

Payment Method Breakdown: A donut chart showing the distribution of sales across different payment methods (e.g., credit card, debit card, voucher).

Top 10 Best-Selling Product Categories: A list showing the product categories that generate the most sales.

This dashboard serves as a powerful tool for monitoring business health, identifying areas for improvement, and informing strategic planning.

DAX Measures
The dashboard's dynamic and calculated metrics are powered by DAX (Data Analysis Expressions). Here are some of the key measures likely used to create the visuals:

Total Sales: A simple aggregation of the sales amount column.

Code snippet

Total Sales = SUM('Sales'[Sales Amount])
Total Delayed Orders: This measure counts the number of orders where the delivery was after the estimated or due date. It would likely use a combination of COUNTROWS and FILTER.

Code snippet

Total Delayed Orders = 
CALCULATE(
    COUNTROWS('Orders'),
    FILTER(
        'Orders',
        'Orders'[Delivery Date] > 'Orders'[Estimated Date]
    )
)
Total Early Orders: Similarly, this measure counts orders delivered before the due date.

Code snippet

Total Early Orders = 
CALCULATE(
    COUNTROWS('Orders'),
    FILTER(
        'Orders',
        'Orders'[Delivery Date] < 'Orders'[Estimated Date]
    )
)
Top 10 Rated Products: To identify the top 10 products by rating, a ranking measure is essential, likely using the RANKX function.

Code snippet

Product Rank by Rating = 
RANKX(
    ALL('Products'[Product Name]),
    [Average Product Rating],
    ,
    DESC
)
(Note: This measure would be used in a visual-level filter to show only products where the Product Rank by Rating is less than or equal to 10.)

Revenue by Year: This time intelligence calculation would use a measure like Total Sales and display it over the date hierarchy. The visual itself handles the aggregation by year, but for more complex comparisons (e.g., year-over-year growth), DATESYTD or SAMEPERIODLASTYEAR would be used.

Revenue YTD = TOTALYTD([Total Sales], 'Date'[Date])
This project demonstrates proficiency in data modeling and DAX to transform raw data into a set of actionable business insights.
