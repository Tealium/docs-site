---
title: Audience Sizing examples
description: This article provides examples of the Audience Sizing feature.
url: https://docs.tealium.com/server-side/audiences/audience-sizing/examples/
---
## Example: Retarget past purchasers

In this example, you want to retarget customers who meet the following conditions:

* Visited your site in the last week.
* Have not purchased in the last 30 days.
* Purchased more than $500 in their lifetime.
* Have a favorite product category of `Jeans`.

This example assumes that you have already set up the necessary date selections and rules to identify:

* A customer’s favorite product category.
* Their lifetime order value.
* The number of days since their last purchase.

### Steps

Use the following steps:

1. In the sidebar, go to **Activate > Discover**.
1. Click the **Audience Sizing** tab.
1. Select a date range that represents the last 7 days.
1. Select or create the following rules:


[
  [
    {
      "input": "Favorite Product Category (favorite)",
      "operator": "equals",
      "filter": "Jeans"
    },
    {
      "input": "Lifetime Order Value",
      "operator": "less than or equal to",
      "filter": "500"
    },
    {
      "input": "Days since last purchase",
      "operator": "greater than",
      "filter": "30"
    }
  ]
]


## Example: Retarget holiday coupon shoppers

In this example, you want to retarget customers who:

* Visited your site during the December holiday season.
* Are currently classified as VIP Customers.
* Engage most with email.
* Frequently use coupons.

This example assumes that you have already set up the necessary date selections and rules to identify:

* VIP Customers.
* The marketing channel they engage with most.
* Their coupon usage frequency.

1. In the sidebar, go to **Activate > Discover**.
1. Click the **Audience Sizing** tab.
1. Select a date range that represents the December holiday season (for example, December 1 - December 31.
1. Select or create the following rules:  


[
  [
    {
      "input": "VIP Customer",
      "operator": "is assigned",
      "filter": ""
    },
    {
      "input": "Marketing Channel Engagement (favorite)",
      "operator": "equals",
      "filter": "email"
    },
    {
      "input": "Coupon Usage Ratio",
      "operator": "greater than or equal to",
      "filter": "0.50"
    }
  ]
]

