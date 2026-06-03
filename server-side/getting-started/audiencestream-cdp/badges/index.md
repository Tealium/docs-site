---
title: Attributes Badges
description: This document explains visitor attributes badges.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/badges/
---
Badges are visitor attributes that represent interesting behavior patterns. Badges are assigned or removed from visitors based on the logic of their enrichments. This logic determines when to assign a badge, which is typically done using one or more conditions or setting a threshold that needs to be met.

## Example badges

Here are some example badges:

|Big Spenders|Cart Abandoner|Multi-Device User|Test Group B|
|------------|--------------|-----------------|------------|
|![](/images/server-side/getting-started/audiencestream-cdp/attributes-badges/big-spenders.png) | ![](/images/server-side/getting-started/audiencestream-cdp/attributes-badges/cart-abandoner.png) | ![](/images/server-side/getting-started/audiencestream-cdp/attributes-badges/multi-device-user.png) |  ![](/images/server-side/getting-started/audiencestream-cdp/attributes-badges/test-group-b.png) | 
| Average Order Value is greater than 100. | Had unpurchased items in cart when visit ended. | Lifetime number of devices used is greater than 1. | Part of a randomly assigned test group. |

## Create a badge

![](/images/server-side/getting-started-audiencestream-badge-vip.png)

We will build on the previous attribute, Lifetime Order Value, to create a **VIP** badge that will identify visitors that have spent more than $500.

Follow these steps to create a badge:

1. Navigate to **AudienceStream &amp;gt; Attributes** and click **Add Attribute**.
1. Select the scope of **Visitor** and click **Continue**.
1. Select the data type **Badge** and click **Continue**.
1. Enter the name of the attribute: `VIP`.
1. Click **Add Enrichment** and select **Assign Badge**.
1. Leave the **WHEN** set to **Any Event**, then click **Create a New Rule**.
1. Create a rule that identifies when the lifetime order amount has reached 500, for example:  
`Lifetime Order Value greater than 500`
1. Click **Save**, then **Finish**.

Now you have a visitor badge that will keep track of customers that match the behavior pattern defined in the enrichment rules.