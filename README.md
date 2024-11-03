# LITA_CUSTOMERDATA_PROJECT

[PROJECT OVERVIEW FOR CUSTOMER SUBSCRIPTION DATA](#project-overview-for-customer-subscription-data)

[DATA SOURCE](#data-source)

[TOOLS USED](#tools-used)

[EXPLORATORY DATA ANALYSIS](#exploratory-data-analysis)

[CALCULATING KEY METRICS](#calculating-key-metrics)

[DATA VISUALIZATION](#data-visualization)

[PIVOT TABLES](#pivot-tables)

[PIVOT CHART](#pivot-chart)

[INSIGHTS GENERATED](#insights-generated)

[RECOMMENDATIONS](#recommendations)

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

### INSIGHTS GENERATED
The Customer data analysis uncovered some interesting patterns in how customers use their subscriptions. With a variety of plans available, the "Basic" subscription emerged as the most popular, accounting for over 50% of all subscriptions. It seems that simplicity and affordability have won over a large part of the customer base. In terms of commitment, the subscribers have an average subscription duration of 365 days. This steady yearly cycle reflects customers’ satisfaction and trust, as they renew their plans for a full year on average. One region, however, stands out: the East. Unlike other regions, where some customers occasionally cancel their plans, the East shows a remarkable commitment to their subscriptions, with zero cancellations on record. This region’s loyalty adds a unique dynamic to the customer insights. Lastly, the total revenue generated from all subscriptions reached an impressive 68 million. This figure reflects both the loyalty and the value the customers place on the company, building a strong financial foundation for the store's service.
### RECOMMENDATIONS
Based on the customer data analysis, here are several recommendations to enhance subscription retention, attract new customers, and maximize revenue:

### 1. *Enhance the Basic Subscription*
   - *Maintain Simplicity*: Since the "Basic" subscription is the most popular, continue to emphasize its simplicity and affordability in marketing efforts.
   - *Introduce Add-Ons*: Consider offering optional add-ons or upgrades that enhance the Basic plan without complicating it, allowing customers to customize their experience.

### 2. *Leverage Customer Loyalty*
   - *Reward Long-Term Subscribers*: Implement a loyalty program that rewards customers for their continued subscription, such as discounts on renewals or exclusive content for those who renew after their first year.
   - *Highlight Customer Testimonials*: Use testimonials from satisfied customers, especially from the East region, in marketing materials to build trust and attract new subscribers.

### 3. *Target the East Region*
   - *Special Promotions*: Since the East region has shown remarkable commitment, consider creating special offers or incentives for the East to further capitalize on this loyalty.
   - *Community Engagement*: Develop community engagement initiatives or events in the East that foster a sense of belonging and deepen customer relationships.

### 4. *Reduce Cancellations in Other Regions*
   - *Understand Cancellation Reasons*: Conduct surveys or interviews with customers who cancel their subscriptions to understand their reasons, allowing you to address pain points effectively.
   - *Re-engagement Campaigns*: Implement re-engagement campaigns targeting former subscribers with personalized offers or updates on new features that might entice them to return.

### 5. *Expand Subscription Options*
   - *Introduce Tiered Plans*: Consider introducing tiered subscription plans (Family plans) that cater to different customer needs and preferences, potentially attracting a wider audience.
   - *Trial Periods*: Offer trial periods for higher-tier plans to encourage customers to experience premium features without commitment, which can lead to conversions.

### 6. *Focus on Customer Experience*
   - *Improve Onboarding*: Ensure that the onboarding process for new subscribers is smooth and informative, helping them understand the value of their subscription right from the start.
   - *Regular Updates and Communication*: Keep subscribers informed about new features, updates, and benefits through regular communication, enhancing their overall experience.

### 7. *Data-Driven Marketing*
   - *Analyze Customer Behavior*: Use analytics to track usage patterns and preferences, allowing for more targeted marketing campaigns that resonate with different segments of your customer base.
   - *Personalized Recommendations*: Implement personalized recommendations based on customer behavior, encouraging upgrades or additional subscriptions that align with their interests.

### 8. *Revenue Growth Strategies*
   - *Upsell and Cross-Sell*: Identify opportunities to upsell existing customers to higher-tier plans or cross-sell complementary services that enhance the subscription experience.
   - *Seasonal Promotions*: Introduce seasonal promotions or limited-time offers to drive new subscriptions and renewals during peak times.

By implementing these recommendations, the company can enhance customer loyalty, reduce cancellations, and ultimately drive revenue growth while maintaining a strong foundation built on subscriber satisfaction.
