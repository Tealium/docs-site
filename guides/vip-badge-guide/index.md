---
title: VIP badge
description: This guide explains how to build a VIP badge to identify your most important customers.
url: https://docs.tealium.com/guides/vip-badge-guide/
---
## How it works

![](https://docs.tealium.com/images/server-side/getting-started-audiencestream-badge-vip.png)

A VIP is a high-valued customer who keeps returning to the site and purchasing. VIPs are a great audience to target because they are more likely to purchase from you than others and they are not going to be as price sensitive as other audiences.

### Conditions

The metrics that determine a VIP visitor vary depending on your industry. Here are some examples of what a VIP visitor might mean to your business:

* **Travel**: you might measure a VIP by miles traveled, amount of money spent, or number of cities or countries traveled to.
* **Finance**: you might measure a VIP by the total amount of a person's assets held by the institution.
* **Media**: you might measure VIP status by the amount of money a customer spends on premium services or subscriptions, or the amount spent on on-demand products.
* **Tech**: you might measure VIP status by the amount of money a customer spends on the latest products and services.

In addition, you can decide how and when to measure the key VIP metrics:

* **Accumulation thresholds**: A total order value, total miles traveled, or total loyalty points.
* **Time-based thresholds**: Totals over a particular time frame.
* **Social engagement thresholds**: Interactions with your brand through social media, such as the number of likes on the visitor's posts about your brand.
* **Feedback and review engagement thresholds**: Visitors who provide positive feedback and reviews.

The great thing about Tealium AudienceStream is that you can create multiple VIP audiences with differing criteria and thresholds, and tailor experiences to each VIP audience.

## Requirements

#### Required event attributes

| Attribute Name | Type| Example| 
| --- | --- | --- |
| `order_id` |  UDO Variable |  `123456` | 
| `order_subtotal` |  UDO Variable |  `1500.00` | 
| `customer_email` |  UDO Variable |  `user@example.com` | 

#### Required visitor attributes

For the Lifetime value example:

| Attribute Name | Type| 
| --- | --- |
| Customer email |  String | 
| Lifetime order total | String |

For the Time-based example:

| Attribute Name | Type| 
| --- | --- |
| Customer email |  String | 
| Rolling order total for past 90 days | Timeline |
| Order subtotals in past 90 days | Number |

## Lifetime value example

In the following example, we create a VIP badge for customers who have spent over $10,000 in their lifetimes and then create an audience with visitors who own that badge.

### Step 1 - Create attributes

First, create a visitor number attribute named "Lifetime order total" with the following enrichment:

```
Increment or Decrement Number by "order_subtotal"
WHEN: Any event
Rule "tealium_event" equals (ignore case) "purchase"
Rule "order_id" is assigned
```

![](https://docs.tealium.com/images/guides/lifetime-order-total-attribute.png)

Next, create a visitor string attribute named "Customer email" to collect the visitor's email address:

```
Set String to customer_email
WHEN: Any event
Rule "customer_email" is assigned.
Rule "customer_email" contains "@"
```

![](https://docs.tealium.com/images/guides/customer-email-attribute-assigned.png)

For more information about adding attributes, see [Add an attribute](https://docs.tealium.com/manage-as-attributes/#add-an-attribute).

### Step 2 - Create VIP badge

Now that we can measure the total amount a visitor has spent and whether they have an email address, we can create the VIP badge based on those attributes.

Create a visitor badge attribute named "Customer VIP" with the following enrichment:

```
Assign this badge to visitor
WHEN: Any event
Rule "Lifetime Order Total" greater than or equal to "10000"
Rule "Customer email" is assigned
```

![](https://docs.tealium.com/images/guides/customer-vip-badge-lifetime-total.png)

### Step 3 - Create the audience

Now we can create an audience based on the VIP badge:

1. Go to **Audiences**.
1. Click **+ New Audience**.
1. In the **Title** field, enter `VIP`.
1. From the **Where** drop-down list, select **Customer VIP**.
1. Select **is assigned**.
1. Click **Done**.

![](https://docs.tealium.com/images/guides/vip-badge-audience.png)

For more information, see .

## Time-based example

In the following example, we create a VIP badge for customers who have made $10,000 in purchases in the past 90 days and then create an audience with visitors who own that badge. Visitors who no longer meet the requirements are removed from the audience after 90 days.

### Step 1 - Create attributes

First, create a visitor timeline attribute named "Order subtotals in past 90 days" with the following two enrichments:

```
Set each event in timeline Order subtotals in past 90 days to expire after 90 days
WHEN: Any event

Record an event for timeline Order subtotals in past 90 days
Capture data for "order_subtotal"
WHEN: New visit
```

![](https://docs.tealium.com/images/guides/order-subtotals-in-past-90-days.png)

Next, create a visitor string attribute named "Customer email" to collect the visitor's email address:

```
Set String to customer_email
WHEN: Any event
Rule "customer_email" is assigned.
Rule "customer_email" contains "@"
```

![](https://docs.tealium.com/images/guides/customer-email-attribute-assigned.png)

Then, create a visitor number attribute named "Rolling order total for past 90 days" with the following enrichment:

```
Set Number Rolling order total for past 90 days to the rolling sum of order_subtotal captures in timeline Order subtotals in past 90 days
WHEN Any event
```

![](https://docs.tealium.com/images/guides/rolling-order-total-for-past-90-days.png)

### Step 2 - Create VIP badge

Now that we can measure the total amount a visitor has spent and whether they have an email address, we can create the VIP badge based on those attributes.

Create a visitor badge attribute named "Customer VIP" with the following enrichment:

```
Assign this badge to visitor
WHEN: Any event
Rule "Rolling order total for past 90 days" greater than or equal to "10000"

Remove this badge to visitor
WHEN: Any event
Rule "Rolling order total for past 90 days" less than "10000"
```

![](https://docs.tealium.com/images/guides/customer-vip-rolling-total.png)

### Step 3 - Create the audience

Now we can create an audience based on the VIP badge:

1. Go to **Audiences**.
1. Click **+ New Audience**.
1. In the **Title** field, enter `VIP`.
1. From the **Where** drop-down list, select **Customer VIP**.
1. Select **is assigned**.
1. Under **Options**, select a 90 day retention time.
1. Click **Done**.

![](https://docs.tealium.com/images/guides/vip-badge-audience.png)

For more information, see .

## Activate the audience

At this point, you're ready to activate the audience through any of our hundreds of vendor integrations.

How can you target VIP customers?

* **Exclusive offers and discounts**: Provide VIP customers with exclusive offers, discounts, or early access to new products or promotions as a token of appreciation for their loyalty. Create VIP-only sales events, flash deals, or limited-time promotions to incentivize repeat purchases and drive engagement.
* **VIP loyalty programs**: Implement a VIP loyalty program with tiered rewards, special benefits, and VIP-only privileges for top-spending customers. Offer perks such as free shipping, dedicated customer service support, birthday gifts, or VIP events to enhance the customer experience and foster loyalty.
* **Personal shopping experiences**: Offer personalized shopping experiences for VIP customers, such as dedicated account managers, personal shoppers, or concierge services. Provide tailored product recommendations, style advice, or customization options to cater to their individual preferences and needs.
* **VIP events and experiences**: Host exclusive VIP events, workshops, or networking opportunities to engage and connect with high-value customers. Invite VIP customers to special events such as product launches, VIP previews, or behind-the-scenes tours to strengthen relationships and foster brand loyalty.
* **Feedback and surveys**: Seek feedback from VIP customers to understand their preferences, expectations, and pain points. Conduct surveys, focus groups, or one-on-one interviews to gather insights and suggestions for improving the VIP experience and tailoring your offerings to their needs.
* **Social recognition and appreciation**: Acknowledge and celebrate VIP customers on social media platforms, company newsletters, or your website. Highlight their contributions, testimonials, or success stories to showcase their value and inspire loyalty among other customers.