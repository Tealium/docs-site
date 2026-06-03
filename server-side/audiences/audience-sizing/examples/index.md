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

1. In the sidebar, go to **AudienceStream &gt; Discover**.
1. Click the **Audience Sizing** tab.
1. Select a date range that represents the last 7 days.
1. Select or create the following rules:


[
  [
    {
      &#34;input&#34;: &#34;Favorite Product Category (favorite)&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;Jeans&#34;
    },
    {
      &#34;input&#34;: &#34;Lifetime Order Value&#34;,
      &#34;operator&#34;: &#34;less than or equal to&#34;,
      &#34;filter&#34;: &#34;500&#34;
    },
    {
      &#34;input&#34;: &#34;Days since last purchase&#34;,
      &#34;operator&#34;: &#34;greater than&#34;,
      &#34;filter&#34;: &#34;30&#34;
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

1. In the sidebar, go to **AudienceStream &gt; Discover**.
1. Click the **Audience Sizing** tab.
1. Select a date range that represents the December holiday season (for example, December 1 - December 31.
1. Select or create the following rules:  


[
  [
    {
      &#34;input&#34;: &#34;VIP Customer&#34;,
      &#34;operator&#34;: &#34;is assigned&#34;,
      &#34;filter&#34;: &#34;&#34;
    },
    {
      &#34;input&#34;: &#34;Marketing Channel Engagement (favorite)&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;email&#34;
    },
    {
      &#34;input&#34;: &#34;Coupon Usage Ratio&#34;,
      &#34;operator&#34;: &#34;greater than or equal to&#34;,
      &#34;filter&#34;: &#34;0.50&#34;
    }
  ]
]

