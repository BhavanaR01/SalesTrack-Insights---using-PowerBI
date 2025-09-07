Step 1: Import Data

You’ll need these tables (can be CSV/Excel/SQL source):

Sales → OrderID, ProductID, CustomerID, Date, Revenue, Quantity, PaymentType

Products → ProductID, Category, Subcategory, Price

Customers → CustomerID, Location, Age, Gender, FeedbackScore

Deliveries → OrderID, DeliveryDate, ExpectedDeliveryDate

Payments → PaymentID, OrderID, PaymentMode, PaymentStatus

🔹 Step 2: Data Modeling

Create relationships between tables:

Sales[ProductID] → Products[ProductID]

Sales[CustomerID] → Customers[CustomerID]

Sales[OrderID] → Deliveries[OrderID]

Sales[OrderID] → Payments[OrderID]

Mark Date table as a proper date dimension for time intelligence.

🔹 Step 3: Create DAX Measures
📊 Revenue & Sales Performance
Total Revenue = SUM(Sales[Revenue])

Total Orders = DISTINCTCOUNT(Sales[OrderID])

Avg Order Value = [Total Revenue] / [Total Orders]

Revenue Growth % =
VAR CurrentMonth = [Total Revenue]
VAR PreviousMonth =
    CALCULATE([Total Revenue], DATEADD('Date'[Date], -1, MONTH))
RETURN
DIVIDE(CurrentMonth - PreviousMonth, PreviousMonth)

🚚 Delivery Performance
Delivery Delay Days =
DATEDIFF(Deliveries[ExpectedDeliveryDate], Deliveries[DeliveryDate], DAY)

On-Time Deliveries % =
DIVIDE(
    COUNTROWS(FILTER(Deliveries, [Delivery Delay Days] <= 0)),
    COUNTROWS(Deliveries)
)

💳 Payment Trends
Failed Payments % =
DIVIDE(
    COUNTROWS(FILTER(Payments, Payments[PaymentStatus] = "Failed")),
    COUNTROWS(Payments)
)

😀 Customer Feedback
Avg Feedback Score = AVERAGE(Customers[FeedbackScore])

🔹 Step 4: Build Visuals in Power BI

Sales & Revenue Dashboard

KPI cards: Total Revenue, Total Orders, Avg Order Value

Line chart: Revenue over time

Bar chart: Revenue by Category / Location

Delivery Dashboard

Gauge: On-Time Deliveries %

Histogram: Delivery Delay Days

Map: Delivery performance by city

Payments Dashboard

Pie chart: Payment Mode distribution

KPI: Failed Payments %

Customer Dashboard

Bar chart: Avg Feedback Score by Product Category

Line chart: Feedback Trend over months
