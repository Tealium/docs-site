---
title: Attributes Enrichments
description: After you identify the attributes you want, you will configure them with enrichments.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/enrichments/
---
Enrichments are business rules that determine when and how to update the values of attributes. Each data type offers its own selection of enrichments for manipulating the attribute&#39;s value. For example, the number attribute offers the enrichment &#34;Increment or Decrement Number&#34; for adding or subtracting number values.

## Enrichment conditions

Each enrichment is set to occur at a specific time. This is the **WHEN** setting. The following options are available for each visit and visitor attribute:

* **New Visitor** – occurs the first time a visitor comes to your site
* **New Visit** – occurs on a new visit by a visitor
* **Any Event** – occurs on any event
* **Visit Ended** – occurs when a visit ends

You can also create a custom condition, called a rule, that will determine when the enrichment will occur.

## Create a visitor attribute

![](/images/server-side/getting-started-audiencestream-lifetime-order-value.png)

Let&#39;s look at an example of a popular e-commerce visitor attribute called **Lifetime Order Value**. This is a visitor attribute that calculates the cumulative amount spent by the customer for all completed orders. To calculate this value, we also need to know when purchases occur and the amount of those purchases, so the attribute dependencies are:

* `order_total` – event attribute for order total amounts.
* `purchase` – an event to track completed purchases.

To get started with adding this attribute, follow these steps:

1. Navigate to **AudienceStream &gt; Attributes** and click **Add Attribute**.
1. Select the scope of **Visitor** and click **Continue**.
1. Select the data type **Number** and click **Continue**.
1. Enter the name of the attribute, `Lifetime Order Value`.
1. Click **Add Enrichment** and select **Increment or Decrement Number**.
1. Select the attribute containing the value to increment by (`order_total`).
1. Leave the **WHEN** set to **Any Event** and then click **Create a New Rule**.
1. Create a rule that identifies when a purchase event has occurred, for example:  
`tealium_event EQUALS purchase`
1. Click **Save**, then **Finish**.

You have just created a visitor attribute with an enrichment to keep track of the total amount spent in completed orders.

![](/images/server-side/getting-started-audiencestream-enrichment.png)

Next, we will learn about the two more special attributes called badge and visitor ID.