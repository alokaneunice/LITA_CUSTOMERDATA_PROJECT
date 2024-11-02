# LITA_CUSTOMERDATA_PROJECT

[PROJECT OVERVIEW FOR CUSTOMER SUBSCRIPTION DATA](#project-overview-for-customer-subscription-data)

[DATA SOURCE](#data-source)

[TOOLS USED](#tools-used)

[EXPLORATORY DATA ANALYSIS](#exploratory-data-analysis)

[CALCULATING KEY METRICS](#calculating-key-metrics)

[DATA VISUALIZATION](#data-visualization)

[PIVOT TABLES](#pivot-tables)

[PIVOT CHART](#pivot-chart)


## PROJECT TITLE: TREND ANALYSIS OF CUSTOMER SUBSCRIPTION DATASET
### PROJECT OVERVIEW FOR CUSTOMER SUBSCRIPTION DATA
The analyzed data will provide a comprehensive look at customer subscription patterns and revenue generated. This will enable insights into the high demand subscription type and how cancelled subscription affects the store.
### DATA SOURCE
The data used was provided by the Incubator Hub for LITA project. LITA is an acronym for LADIES IN TECH AFRICA, an initiative to empower women in the Technological ambience.
### TOOLS USED
- Microsoft Excel for data cleaning and analyses. [Download Here](www.microsoft.com)
- SQL for querying data
- Power BI for data visualizations
### EXPLORATORY DATA ANALYSIS
  1. Open the "LITA Capstone Dataset.xlsx" file in Excel.
     -  Highlight all the data, sort the data in descending or ascending order.
     - Using Conditional Formatting, check for the number of missing or blank cells within the specified range.
     - All duplicates were also removed from the tables.

  2. Create Pivot Tables to display:
     - Revenue lost due to cancellation: shows how much revenue was lost by customers' cancellation of subscription.
     - Total customers who subcribed: displays counts of customer per subscription type.
     - Monthly Subscription Trends: illustrates subscription trends over the months.
     - Average subscription per subscription type: calculating to find out the average subscriptions made over the subscription types.
  ### CALCULATING KEY METRICS
  1. Finding the duration of subscription per customer. Where "E" stands for subscriptionStart, "F" connotes subscriptionEnd, and "d" is for days
     ```
     =DATEDIF(E2, F2, "d")
     ```
  2. Average subscription duration per customer. Where "I" is for column with duration in days
     ```
     =AVERAGE(I2:I33788)
     ```
  3. Retrieve the total number of customers from each region.
     
    SELECT Region, COUNT(CustomerID) AS TotalCustomers
    FROM [dbo].[CustomerData$]
    GROUP BY Region
    
  4. Find the most popular subscription type by the number of customers.
     
    SELECT TOP 1 (SubscriptionType), COUNT(CustomerID) AS NumberOfCustomers
    FROM [dbo].[CustomerData$]
    GROUP BY SubscriptionType
    ORDER BY NumberOfCustomers DESC
    
  5. Find customers who canceled their subscription within 6 months.
````
     SELECT CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd,canceled
     FROM CustomerData$
     WHERE canceled = 1
    AND datediff(month, subscriptionEnd, SubscriptionStart) <= 6
````
  6. Calculate the average subscription duration for all customers.
````
     SELECT AVG (DATEDIFF(day, SubscriptionStart, SubscriptionEnd)) AS avg_subscription_duration 
     FROM CustomerData$
````    
  7. Find customers with subscriptions longer than 12 months.
 ```` 
      SELECT CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd
      FROM [dbo].[CustomerData$]
      WHERE DATEDIFF(MONTH, SubscriptionEnd, SubscriptionStart) > 12
  ````
  8. Calculate total revenue by subscription type.
 ```` 
     SELECT SubscriptionType, SUM (Revenue) AS Total_Revenue
     FROM [dbo].[CustomerData$]
     GROUP BY Subscriptiontype
  ````
  9. Find the top 3 regions by subscription cancellations.
  
    SELECT TOP 3 Region, COUNT(CustomerID) AS CancellationCount
    FROM [dbo].[CustomerData$]
    WHERE Canceled = 1
    GROUP BY Region
    ORDER BY CancellationCount DESC 
  
  10. Find the total number of active and canceled subscriptions.

     SELECT 
      SUM(CASE WHEN Canceled = 0 THEN 1 ELSE 0 END) AS ActiveSubscriptions,
      SUM(CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) AS CanceledSubscriptions
    FROM [dbo].[CustomerData$]

### DATA VISUALIZATION

![CUSTOMERDATDASHBOARD](https://github.com/user-attachments/assets/67d2fcec-ce6d-441b-9db9-a818ae3f6518)

### PIVOT TABLES
 
![PIVOTTABLECUSTOMERDATA](https://github.com/user-attachments/assets/a38580e5-533f-47d5-bcd9-fe5ecac0e8d3)

### PIVOT CHART

![PIVOTCHARTCUSTOMERDATA](https://github.com/user-attachments/assets/19582f44-8bd5-401b-866f-14defedfb01b)
