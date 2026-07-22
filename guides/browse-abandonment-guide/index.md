---
title: Browse abandonment guide
description: This guide describes how to target visitors in real time who have browsed products on a site without adding them to the shopping cart, also known as browse abandonment.
url: https://docs.tealium.com/guides/browse-abandonment-guide/
---
## Benefits

Browse abandonment remarketing strategies are effective for the following reasons:

* **Capitalizes on Intent**: Visitors who browse multiple products demonstrate an intent to shop, making them prime candidates for targeted marketing.
* **Increases Conversions**: Personalized follow-up messages, such as emails or ads featuring the products they viewed, remind and motivate customers to return and make a purchase.
* **Improves ROI**: By focusing on users who have already expressed interest, you allocate marketing resources to audiences with a higher likelihood of conversion.
* **Reduces Cart Abandonment**: By engaging customers earlier in their journey, you might prevent them from leaving before adding items to their cart.
* **Builds Brand Awareness**: Repeated exposure through remarketing keeps your brand top-of-mind, even if they don't immediately convert.

## What to measure

Browse abandonment can be tracked in several different ways:

* Counting the number of product pages viewed.
* Counting products browsed within a particular category to demonstrate category affinity.
* Measuring the length of time spent on product pages.

This guide shows you how to create a basic browse abandonment configuration that identifies visitors who browse five or more products on a site, but do not add any products to their cart or make a purchase. You can adjust the threshold to fit your audience.

After the visitors have been identified, you can take action on them through a server-side connector to your email marketing service.

## Requirements

This use case requires the following: 

* Tracked events:
  * 
  * 
  * 
* Tealium AudienceStream

In general, the following event attributes will be helpful in tracking browse abandonment activity. Your actual attribute names might differ.

| Attribute Name         | Example value |
|----------------------- |---------------|
|`product_id`            | `["PROD678"]`|
|`product_image_url`     | `["//example.com/path/image.gif"]`|
|`product_name`          | `["Product Three"]`|
|`product_price`         | `["18.00"]`|
|`product_quantity`      | `["2"]`|
|`product_sku`           | `["PR-BLU-678"]`|
|`product_subcategory`   | `["T-Shirts"]`|
|`tealium_event`         | `product_view` or `cart_add` or `purchase`|
|`customer_email`        | `user@example.com` |

For more information about the data layer definition for retail, see [retail](https://docs.tealium.com/retail/).

### Required AudienceStream Attributes

| Attribute Name | Type   | Scope   | Description    |
|----------------|--------|---------|----------------|
| Added to Cart | Boolean | Visit | Indicates that an **Add to Cart** event has occurred.   |
| Purchased | Boolean | Visit | Indicates that a **Purchase** event has occurred.   |
| Number of Products Browsed | Number | Visitor | Counts the number of product pages a visitor has viewed across visits.    |
| Browse Abandoner | Badge  | Visitor |  Indicates that the visitor has viewed a specified number of product detail pages without adding a product to the cart.  |

## Step 1: Create visitor attributes

Create the following attributes:

* **Added to Cart**: A boolean that represents if the user has added a product to their cart. 
* **Purchased**: A boolean that represents if the user has completed a purchase. 
* **Number of Products Browsed**: A number to count the total number of products that the visitor has browsed.
* **Browse Abandoner**: A badge to assign to visitors if they’ve viewed five or more products without adding any to their cart.

### Create Added to Cart attribute

Create a boolean visit attribute named `Added to Cart` with the following enrichments:

* Set to `false` on **NEW VISIT**.
* Set to `true` on **ANY EVENT** where `tealium_event` is **equal (ignore case)** to `cart_add`.

![](https://docs.tealium.com/images/guides/boolean_added_to_cart.png)

### Create Purchased attribute

Create a boolean visit attribute named `Purchased` with the following enrichments:

* Set to `false` on **NEW VISIT**.
* Set to `true` on **ANY EVENT** where `tealium_event` is **equal (ignore case)** to `purchase`.

![](https://docs.tealium.com/images/guides/boolean_purchased.png)

### Create email_address attribute

Create a string visitor attribute named `email_address` with the following enrichment:

* Set to `customer_email` on **ANY EVENT**.

![](https://docs.tealium.com/images/guides/string_email_address.png)

### Create Number of Products Browsed attribute

Create a number visitor attribute named `Number of Products Browsed` with the following enrichment:

* **Increment Number** by `1` on **ANY EVENT** where `tealium_event` **contains (ignore case)** `product_view`.

![](https://docs.tealium.com/images/guides/count_of_products_browsed.png)

### Create Browse Abandoner badge

Before you create your audience, you’ll need to create a badge to assign to visitors if they’ve abandoned their product browsing session after viewing five or more products, haven't added products to their cart, or haven't made a purchase. This badge uses the boolean attributes you created.

Create a badge visitor attribute named `Browse Abandoner` with the following enrichments:

* **Assign this badge to visitor** on **VISIT ENDED** where **Number of Products Browsed** is greater than or equal to `5`
* **Remove this badge from visitor** on **VISIT ENDED** where **Number of Products Browsed** is less than `5` or `Added to Cart` **is true** or `Purchased` **is true**.

![](https://docs.tealium.com/images/guides/browse_abandoner_badge.png) 

## Step 2: Create an audience

Now you can create a **Browse Abandoners** audience with the following conditions:

* **Browse Abandoner** badge is assigned.
* **email_address** string is assigned.

![](https://docs.tealium.com/images/guides/audience_browse_abandoners.png) 

## Step 3: Configure a connector

With your attributes, badges, and audiences set up, you're ready to connect this new audience to your email marketing tools to re-engage and convert these audiences.

Some common connectors and actions for browse abandonment include:

* [Adobe Campaign Classic](https://docs.tealium.com/adobe-campaign-classic-connector/)
* [Iterable](https://docs.tealium.com/iterable-connector/): **Subscribe User to a List**, **Upsert User** action
* [Marketo](https://docs.tealium.com/marketo-connector/): **Add Lead to List** action
* [SendGrid](https://docs.tealium.com/sendgrid-connector/): **Upsert Contact** action

For example, you could set up the Marketo connector to add a visitor's email address to a browse abandoner marketing list. Customize your connector actions to trigger only for when a visitor joins the Browse Abandonment audience.

![](https://docs.tealium.com/images/guides/browse_abandoner_marketo_1.png) 

![](https://docs.tealium.com/images/guides/browse_abandoner_marketo_3.png) 

For more information, see .

### Delayed actions

While you can often send out an email to a user right after they abandon their product browsing session, you may have a higher chance of conversion by delaying the email for your target audience. Use delayed actions to set connector action delays in Tealium and then trigger your email workflows in your vendor of choice.


<blockquote>
We recommend that you set a delay for an hour or so to remarket visitors that have an interest in buying, but not lose the visitor to a competitive site.
</blockquote>


For detailed information about how to use delayed actions in Tealium, [about-delayed-actions](https://docs.tealium.com/about-delayed-actions/).

## Next steps

This guide illustrates how to build a basic browse abandoner email retargeting campaign. You can increase your understanding of customer behavior by using additional attributes in your campaigns. The following table shows some possible options for browse abandonment-related attributes:

| Attribute Name                  | Attribute Type | Scope  | Category         | Notes |
|---|---|---|---|---|
| Furthest stage of funnel reached| Funnel          | Visit  | Purchase Behavior | Can be used in the following user flow: Acquisition > Browsing > Product Detail Page (PDP) view.    |
| Average item price purchased             | Number         | Visitor| Lifetime Behavior | A rolling average of the price of all items that the visitor has purchased.     |
| Average product price browsed | Number | Visitor | Lifetime Behavior | A rolling average of the price of all items that the visitor has browsed. |

You can also consider customizing the level of browse abandonment for the user:

* **Browse Abandoner - High Value**  
The products viewed have a total value greater than a high custom value, and have not purchased.
* **Browse Abandoner - Low Value**  
The products viewed have a total value less than a high custom value, and have not purchased.
* **Browse Abandoner - Medium Value**  
The products viewed have a total value between the high and low custom values.

The configuration in this guide can also be used for personalization with Tealium solutions like Moments API. For more information, see [About Moments API](https://docs.tealium.com/about-moments-api/). The audiences you have created can also be used in social and display marketing for retargeting as illustrated below:

![](https://docs.tealium.com/images/guides/browse-abandonment-flow-diagram.png)