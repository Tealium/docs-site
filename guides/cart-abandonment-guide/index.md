---
title: Cart abandonment guide
description: This guide shows how to target visitors who added products to the shopping cart but didn't complete a purchase.
url: https://docs.tealium.com/guides/cart-abandonment-guide/
---
This guide shows how to track basic cart abandonment by combining Tealium iQ Tag Management (Optional), Tealium AudienceStream CDP, and your email marketing connector.

![](/images/guides/cart-abandonment-flow-diagram.png)

The solution in this guide covers the following steps:

* [Step 1: Track events](#step-1-track-events)
* [Step 2: Define visitor attributes](#step-2-define-visitor-attributes)
* [Step 3: Define an audience](#step-3-define-an-audience)
* [Step 4: Configure a connector](#step-4-configure-a-connector)

## Required events and attributes

The following events should be tracked:
* `cart_add`
* `purchase`

In general, the following event attributes will be helpful in tracking cart abandonment activity. Your actual attribute names might differ.

| Attribute Name         | Example value |
|----------------------- |---------------|
|`cart_product_id`       | `[&#34;PROD123&#34;, &#34;PROD456&#34;]`|
|`cart_product_price`    | `[&#34;12.00&#34;, &#34;25.99&#34;]`|
|`cart_product_quantity` | `[&#34;2&#34;, &#34;2&#34;]`|
|`cart_product_sku`      | `[&#34;PR-RED-123&#34;, &#34;PR-BLK-456&#34;]` |
|`product_category`      | `[&#34;Shirts&#34;]`|
|`product_id`            | `[&#34;PROD678&#34;]`|
|`product_image_url`     | `[&#34;//example.com/path/image.gif&#34;]`|
|`product_name`          | `[&#34;Product Three&#34;]`|
|`product_price`         | `[&#34;18.00&#34;]`|
|`product_quantity`      | `[&#34;2&#34;]`|
|`product_sku`           | `[&#34;PR-BLU-678&#34;]`|
|`product_subcategory`   | `[&#34;T-Shirts&#34;]`|
|`tealium_event`         | `&#34;cart_add&#34;`|

For more information about tracking e-commerce events, see .


## Required visitor attributes

| Attribute Name | Type   | Scope   | Description        |
|----------------|--------|---------|--------------------|
| Added to Cart | Boolean | Visitor   | Signifies that a product was added to the shopping cart in the last visit.|
| Did Purchase | Boolean | Visitor   | Signifies that a purchase was made within the last visit. |
| Cart Abandoner | Badge  | Visitor | Signifies that the conditions for cart abandonment have been met.  |

## Step 1: Track events 

In this step, we use Tealium iQ events to send event and product information when a visitor adds a product to their cart.

If you already collect `cart_add` events, skip this step.

### Track Add to Cart events

To start, we need to know when a visitor adds something to their cart. Create an event listener to track when a user adds something to their cart.

In this use case, we are setting `tealium_event` to `cart_add`. 

1. Go to **Tag Management &gt; Events** and click **&#43;New Event**.
1. In the **Event Types** screen, select the **Click** event type and click **Next**.
1. In the **Configuration** screen, set the following values for your click event:
   * **Name**: Add to Cart
   * **Scope**: DOM Ready
   * **Tracking Event**: Link
   * **Event Triggers**: Mousedown
   * **Element Selector**: The selector that works best for your website, beginning with a hash `#`. For example, your website may have the selector `#add-to-cart` for the **Add to Cart** button.
   * Event Trigger Variables: Set Tealium Event to Text and enter `cart_add`
1. Click **Next**.

![](/images/guides/event_add_cart_to_pages.png)

Test your event configurations before publishing to production.

## Step 2: Define visitor attributes 

Now we need to create two boolean attributes:

* **Added to Cart (Boolean)**: determines if the visitor has added a product to their cart.
* **Did Purchase (Boolean)**: determines if the visitor completed a purchase during their last visit.

### Added to cart boolean

Create a visitor boolean attribute to track when a `cart_add` event has occurred.

1. Go to **Transform &gt; Visitor / Visit Attributes** and click **&#43;Add Attribute**.
1. In the **Add Attribute** screen, click **Visitor** and **Continue**.
1. Select **Boolean** and click **Continue**.
1. In the **Properties** section, enter `Added to Cart `as the title.
1. Click **Add Enrichment** to set the **Added to Cart** boolean to `false` and the scope to **NEW VISIT**.
1. Click **Add Enrichment** and set the **Added to Cart** boolean to `true` and the scope to **ANY EVENT**. 
1. Create a rule if it does not already exist:
    * **Title**: Event cart_add
    * Click **&#43;Attribute Condition**.
    * Select `tealium_event` is **equal (ignore case)** to `cart_add`.
1. Click **Save**.

![](/images/guides/boolean_added_to_cart.png)

### Did Purchase boolean

Create a visitor boolean attribute to track when a `purchase` event has occurred.

1. Go to **Transform &gt; Visitor / Visit Attributes** and click **&#43;Add Attribute**.
1. In the **Add Attribute** screen, click **Visitor** and **Continue**.
1. Select **Boolean** and click **Continue**.
1. In the **Properties** section, enter `Did Purchase` as the title.
1. Click **Add Enrichment** to set the **Purchase** boolean to `false` and the scope to **NEW VISIT**.
1. Click **Add Enrichment** to set the **Purchase** boolean to `true` for **Any Event**.
1. Create the following rule if it does not already exist:
    * **Title**: Purchase event
    * Click **&#43;Attribute Condition**.
    * Select `tealium_event` **contains (ignore case)** `purchase`.
    ![](/images/guides/boolean_purchase.png)
1. Click **Save**.
1. Click **Finish**.

### Cart Abandoner badge and rule

Before you create your audience, you&#39;ll need to create a badge to assign to visitors if they&#39;ve abandoned their cart using the boolean attributes you&#39;ve just created.

1. Go to **Transform &gt; Visitor / Visit Attributes** and click **&#43;Add Attribute**.
1. Select **Visitor** and then select **Badge**. 
1. In the **Properties** section, enter `Cart Abandoner `as the title.
1. Click **Add Enrichment** and **Assign a badge**.
1. For **Assign this badge to visitor**, select **VISIT ENDED** from the drop-down list.
1. Click **Create Rule** and set the following attribute conditions:
    * **Added to Cart** boolean:  is `true`
    * **Purchase boolean**: is `false`
1. Click **Add Enrichment** and **Remove badge**.
1. For **Remove this badge from Visitor** select **ANY EVENT**.
1. Click **Create Rule** and create the following rule if it does not already exist:
    * Set `tealium_event` to **contains (ignore case)** and `purchase`.
1. Click **Finish**.

![](/images/guides/badge_cart_abandoner.png)

## Step 3: Define an audience

Now you can easily create an audience using the badge you&#39;ve just created.

1. Go to **Activate &gt; Audiences** and click **&#43;New Audience**.
1. Add the following audience:
    * **Name**: Cart Abandoners
    * Select the **Cart Abandoner** badge from the first drop-down list and **is assigned** from the second drop-down list.
1. Click **Done**.
1. Save and publish your profile.

![](/images/guides/audience_cart_abandoners.png)

## Step 4: Configure a connector

With your attributes, badges, and audiences set up, you&#39;re ready to connect this new audience to your email marketing tools to retarget and convert these visitors.

Some of the common connectors and actions for cart abandonment include:

* [Adobe Campaign Classic]()
* [Iterable](): **Subscribe User to a List**, **Upsert User** action
* [Marketo](): **Add Lead to List** action
* [SendGrid](): **Upsert Contact** action

### Delayed actions

While you can often send an email to a user right after they abandon their cart, you may have a better chance of conversion by delaying the email. Use delayed actions to control the timing of your retargeting campaign connector.

For more information, see .

## Additional tracking

### Cart value

Consider tracking the value of the abandoned cart to allow you to create more specific segments of cart abandoners. These segments would use the `cart_total_value` attribute to determine the total value of all products in the cart.

* **Cart Abandoner - High Value**  
Has added a product to their cart, cart total value is greater than high custom value, and have not purchased.
* **Cart Abandoner - Medium Value**  
Has added a product to their cart, cart total value is between high and low custom values, and have not purchased.
* **Cart Abandoner - Low Value**  
Has added a product to their cart, cart total value is less than low custom value, and have not purchased.

### Supplemental attributes

Increase your understanding of customer behavior by tracking additional customer activity.

The following table lists more attributes to track for cart abandonment campaigns:

| Attribute Name | Attribute Type | Scope | Category | Notes  |
|---|---|---|---|---|
| Cart abandoner                  | Boolean/Badge  | Visitor  | Purchase Behavior | Applied at end of session if items added to cart and no purchase made this session                                                                                                   |
| Furthest stage of funnel reached| Badge          | Visit  | Purchase Behavior | Can be used in the following user flow: Acquisition &gt; Browsing &gt; Product Detail Page (PDP) view &gt; Add to cart &gt; View cart &gt; Purchase.                                                |
| Cart viewed this session        | Boolean        | Visit  | Purchase Behavior | Signifies if the user viewed the cart or only added to their cart.                                                                                                                   |
| Total cart value                | Number         | Visit  | Purchase Behavior | Useful for analysis, opportunity sizing and for future expansion into paid media.                                                                                                    |
| Days since last cart abandonment| Number         | Visitor| Purchase Behavior | Simple date count to assist with eligibility for Cart Abandoner. Can also be used for analysis.                                                                                       |
| Number of carts abandoned       | Number         | Visitor| Lifetime Behavior | Number that increments &#43;1 for each abandonment event.                                                                                                                                |
| Average order value             | Number         | Visitor| Lifetime Behavior | General behavioral understanding and future use case expansions.                                                                                                                     |
| Average item value              | Number         | Visitor| Lifetime Behavior | General behavioral understanding and future use case expansions.                                                                                                                     |
| Favorite categories             | Tally          | Visitor| Lifetime Behavior | General behavioral understanding and future use case expansions.                                                                                                                     |

For more robust retargeting, combine this basic cart abandonment configuration with mobile, and offline point of sale (POS) systems to monitor all potential product browsing and purchasing behavior. By including offline POS system data, users who purchase in-store can be automatically removed from online campaigns which makes retargeting campaigns more efficient. 

## Next steps

Now that you&#39;ve defined attributes for cart abandoners, they can also be used for personalization with solutions like Moments API.

For more information, see .
