---
title: An Introduction to the Data Layer
description: This article introduces the data layer and explains what it is, how it works, and the benefits of implementing one.
url: https://docs.tealium.com/platforms/getting-started-web/data-layer/an-introduction-to-the-data-layer/
---
## What is a data layer?

A data layer is a specification for the customer interaction tracking that flows from your digital properties. This tracked activity comes from many sources, including desktop and mobile websites, mobile apps, connected devices, and offline sources to name a few. The data layer powers your third-party vendor solutions and becomes the foundation of your data-driven initiatives.

The definition of your data layer starts with identifying the most important activity of your visitors, called _events_. Events encompass everything from page views and site searches to logins, purchases, or any customer action that informs your critical business decisions. Each event contains contextual information, called _event attributes_. The data layer comprises a list of these events and their corresponding attributes.

The Tealium data layer uses a variable named `tealium_event` to identify the events you track. You can define your own event names, but we have a [standard set of events](/platforms/getting-started-web/data-layer/definitions/) to get you started.

Here are a few examples of events that are common to many data layer definitions:

### Examples

#### Site Search

|**Event Attribute**| **Description**| **Example Value**|
|---| ---| ---|
|`tealium_event`| The event being tracked.| `search`|
|`page_type`| The type of page being viewed.| `search`|
|`search_keyword`| The term entered into the search.| `red boots`|
|`search_results`| The number of search results returned.| `42`|

#### Newsletter Signup

|**Event Attribute**| **Description**| **Example Value**|
|---| ---| ---|
|`tealium_event`| The event being tracked.| `newsletter_signup`|
|`newsletter_name`| The name of the newsletter.| `Weekly Digest`|

#### Add to Cart

|**Event Attribute**| **Description**| **Example Value**|
|---| ---| ---|
|`tealium_event`| The event being tracked.| `cart_add`|
|`product_id`| The ID of the product added to the cart.| `B51378`|
|`product_name`| The name of the product added to the cart.| `Widget XYZ`|
|`product_quantity`| The quantity of the product added to the cart.| `2`|

After these events and attributes are defined for your business, your data layer serves as the one true definition of your data across all digital assets and customer interactions.

## Why do I need a data layer?

The data layer helps you take ownership of your most valuable asset--your data. You rely on many third-party vendors to power your business, each with their own data collection needs, and the data layer is a centralized definition of that data. A well-defined and managed data layer brings the following benefits:

* **Governance**  
Take control of your data by establishing a governance policy around your data layer.
* **Standardization**  
Use terminology that makes sense to your organization. 
* **Marketing Agility**  
A well implemented data layer allows your marketing strategies to adjust quickly to changing conditions by eliminating your dependency on development resources. 
* **Time and Cost Savings**  
Save time and money for developers by eliminating constant requests for incremental changes to your website and mobile app.

## How it works

After your data layer is defined, install it across your digital properties. Follow the installation guides for each platform to ensure the specifications of the data layer are followed consistently. This data is then used in your tag vendor configurations and campaign strategies.

We recommend a naming convention that is simple and easy to understand. Some examples include:

|**Event Attribute**| **Description**| **Example Value**|
|---| ---| ---|
|`order_id`| The unique ID of a completed order.| `1234`|
|`order_total`| The total amount paid for the order.| `123.45`|
|`customer_id`| A unique ID for the visitor.| `0123456789`|
|`customer_zip`| The visitor&#39;s zip code.| `92101`|

These attributes can be sent to your third-party vendors in the format that they require. This process is made simple with the Tealium Customer Data Hub.

As an example, the attribute named `order_id` is referenced by vendors using several different names, such as `s.purchase_id`, `transid`, `pid`, and `oid` to name a few. If the data layer defines `order_id` as the attribute for online purchases, then that single source of data can be reused to send that value to the other vendors in the format that they expect.

| Event Attribute | Event Value | Vendor Attribute| Vendor Name|
| ---| ---| ---| ---|
| `order_id` | `1234` | `s.purchase_id` | Adobe Analytics|
| | | `transid`| Rocket Fuel|
| | | `pid`| X (Formerly Twitter) Conversions|
| | | `oid`| Conversant|

![](/images/platforms/getting-started-web/data-layer-data-to-vendors.png)