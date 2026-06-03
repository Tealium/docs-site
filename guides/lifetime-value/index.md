---
title: Lifetime value
description: This article explains the concept of lifetime value (LTV) and outlines strategies for measuring it and using it effectively.
url: https://docs.tealium.com/guides/lifetime-value/
---
## How it works

Lifetime value (LTV) refers to the total revenue a customer is expected to generate for your business over the course of their relationship. This metric goes beyond the immediate value of a purchase and includes repeat purchases, referrals, and overall contributions to your revenue.

Understanding LTV provides insight into the long-term profitability of individual customers. Tracking LTV helps your identify valuable customers, optimize marketing strategies, and increase overall profitability.

In Tealium AudienceStream, LTV serves as a real-time indicator of customer value, offering your actionable insights into purchasing behavior. By leveraging LTV data, you can refine your customer engagement strategies, focus on retention, and drive revenue growth through more precise targeting and personalized experiences.

## Where to use LTV

You can use LTV in the following ways:

* **Identify high-value customers**: Analyzing LTV lets you pinpoint customers who generate the most revenue. This information can guide personalized marketing efforts and retention strategies.
* **Optimize marketing investments**: LTV helps companies allocate marketing budgets wisely, focusing on customers with the highest potential value, ensuring that resources are spent on campaigns and channels that bring the best returns.
* **Tailor customer experiences**: With LTV insights, you can create personalized experiences, such as tailored product recommendations and promotions for high-value customers, improving satisfaction and loyalty.
* **Predict future revenue**: LTV lets you forecast future revenue from current customers, guiding decisions on growth strategies, product development, and pricing.

## By industry

LTV’s importance varies from industry to industry:

* **Retail**: In retail, LTV helps identify customers who make frequent purchases or larger orders. Retailers can then offer personalized promotions to retain these high-value customers, improving long-term profitability.
* **Media**: Media companies use LTV to refine subscription models and content strategies. By understanding the long-term value of subscribers, they can adjust pricing and content offerings to meet the preferences of their most valuable viewers.
* **Financial services**: In financial services, LTV is used to predict customer lifetime revenue. Banks and other institutions can use this information to target customers with higher potential for additional services like loans or investment accounts.
* **Travel and hospitality**: Hotels and airlines use LTV to identify loyal customers and offer personalized perks like upgrades or discounts. This helps encourage repeat business and strengthens customer relationships.

## LTV and conversions

Incorporating LTV into conversion marketing strategies improves the effectiveness of your campaigns. By focusing on high-LTV customers, you can create more targeted efforts that result in better conversions.

For instance, a software company might identify website visitors who have shown interest through previous purchases. The company can then target these visitors with personalized campaigns, leading to higher conversion rates.

## LTV and retargeting

LTV helps with retargeting efforts in the following ways:

* **Segmenting audiences**: Marketers can segment audiences by LTV to tailor offers, focusing on high-value customers with more personalized campaigns.
* **Improving customer retention**: Businesses can prioritize high-LTV customers in retention efforts, enhancing satisfaction and reducing churn.
* **Upselling and cross-selling**: LTV data helps identify customers who are more likely to respond to upsell or cross-sell offers.
* **Tracking campaign effectiveness**: By monitoring changes in LTV over time, companies can assess how effective their retargeting campaigns are and adjust strategies as needed.

## How to track LTV

### Collect visitor properties

Tracking LTV requires capturing and analyzing various visitor properties that provide insights into the behavior, preferences, and purchasing patterns of customers.

The following visitor properties are required for LTV tracking:

* **Demographic data**:  Information like age, gender, and location helps you understand customer preferences and tailor marketing efforts.
* **Purchase history**: Data on past transactions, purchase frequency, and average order value gives insights into a customer&#39;s buying behavior.

### Analyze key metrics

Calculating LTV involves analyzing several key metrics that provide insights into the revenue potential of individual customers over their entire relationship with your business.

The following key metrics, logic, and formulas are commonly used to calculate LTV:

* **Average purchase value (APV)**: The average amount of revenue generated from each transaction made by a customer.
  * **Formula**: APV = Total revenue / Number of transactions
  * **Example**: If a customer makes five purchases totaling $500 over the course of their relationship with a company, the APV is $100 ($500 / 5).
* **Average purchase frequency rate (APFR)**: How often a customer makes purchases within a specific timeframe.
  * **Formula**: APFR = Number of transactions / Number of unique customers
  * **Example**: If 100 unique customers make a total of 500 transactions in a year, the APFR is 5 (500 / 100).
* **Customer lifespan (CL)**: The average duration of time a customer remains active and makes purchases before churning.
  * **Formula**: CL = 1 / Churn rate
  * **Example**: If the churn rate is 20% per year, the customer lifespan is 5 years (1 / 0.20).
* **Customer lifetime value (CLTV)**: The total revenue expected from a customer over their entire relationship with a business.
  * **Formula**: CLTV = APV × APFR × CL
  * **Example**: Using the previous examples, if APV is $100, APFR is 5, and CL is 5 years, the CLTV is $2,500 ($100 × 5 × 5).
* **Churn rate**: The percentage of customers who stop purchasing from a company within a specific time frame.
  * **Formula**: Churn rate = (Number of customers at start of period - Number of customers at end of period) / Number of customers at start of period
  * **Example**: If a company starts the year with 1,000 customers and ends with 800, the churn rate is 20% [(1000 - 800) / 1000].

By analyzing these key metrics and applying the respective formulas, you can calculate customer LTV accurately and gain valuable insights into the long-term revenue potential of your customer base.

For a step-by-step example of how to track Customer Lifetime Value in AudienceStream, see [VIP Badge Guide]().
