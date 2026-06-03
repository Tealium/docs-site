---
title: AgilOne Webtag Setup Guide
description: This article describes how to set up the AgilOne tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/agilone-webtag-tag/
---
## Prerequisites

* Authentication Key (Required for authenticating API calls to AgilOne)
* Tealium Event Extension (Optional, but highly recommended)

## Tag Configuration

First, go to the tag marketplace and add the AgilOne Web Tag Tag to your profile (See [Add a tag]()).

After adding the Tag, configure the below settings:

* Tenant ID: (Required) The tenant ID you received from AgilOne. You may specify the ID in this field or set it dynamically using [Data Mappings](#data-mappings).

## Load Rules

[Load Rules]() determine when and where to load an instance of this Tag on your site.

Recommended Load Rule: **Load on all pages**

## Data Mappings

Mapping is the process of sending data from a [Data Layer Variable]() to the corresponding destination variable of the vendor Tag. For instructions on how to map a Variable to a Tag destination, see Data Mappings.

The destination variables for the AgilOne Web Tag Tag are built into its Data Mapping tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Tenant ID| (Required) Tenant ID|
|Authentication Key| (Required) Authentication key-value|
|Search Term| The keyword used for searching the site|
|Event Name| Name of the event you want to trigger. Recommended for triggering events that are not already offered in the Tealium Event Extension.|
|Event Entity URL| URL of the page on which the event is happening|
|Event Entity Time| (Optional) timestamp of when the event is triggered. AgilOne recommends sending this value ONLY if the timestamp does not equal the time when the event is sent.|
|Event Entity Custom Data*| Additional data to send with the Event Entity|

The Event Entity Custom Data is not the same as the Event Custom Data category.

### E-Commerce

Since the AgilOne Web Tag Tag is e-commerce enabled, it will automatically use the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* you want to override any Extension mappings
* an ecommerce variable you want is not offered in the extension

|**Destination Name**| **Description**| **E-Commerce Extension Variable**|
|---| ---| ---|
|Order ID| Unique Order ID| `_corder`|
|Order Total| Total value of order| `_ctotal`|
|Order Subtotal| Subtotal amount of the order| `_csubtotal`|
|Shipping Amount| Shipping Amount| `_cship`|
|Tax Amount| Amount of Tax| `_ctax`|
|Order Organization ID| Order Organization ID| NA|
|Order Invoice Date| Invoice Date for the Order| NA|
|Order Custom Data| Custom Data for Order| NA|
|Customer ID| Unique customer ID| `_ccustid`|
|List of Product IDs| Array of Product IDs| `_cprod`|
|List of Transaction Item IDs| List of Transaction Item IDs| NA|
|List of Names| Array of Product Names| `_cprodname`|
|List of SKUs| List of SKUs| `_csku`|
|List of Brands| List of Brands| `_cbrand`|
|List of Categories| Array of Product Categories| `_ccat`|
|List of Quantities| Array of Product Quantities| `_cquan`|
|List of Prices| Array of Product Prices| `_cprice`|
|List of Discounts| List of Discounts| `_cpdisc` |
|List of Organization IDs| List of Organization IDs| NA|
|List of Product Types| List of Product Types| NA|
|List of Product Subtypes| List of Product Subtypes| NA|
|List of Product Shipping Revenues| List of Product Shipping Revenues| NA|
|List of Product Organization IDs| List of Product Organization IDs| NA|
|List of Product Ship Dates| List of Product Ship Dates| NA|
|List of Product Invoice Dates| List of Product Invoice Dates| NA|
|Product Custom Data| Product Custom Data| NA|

### Customer

|**Destination Name**| **Description**|
|---| ---|
|Customer Email| Customer&#39;s email address|
|Customer UUID| Customer&#39;s UUID|
|Customer Preference DNE| Email opt-out value|
|Customer Preference DNM| Postal opt-out value|
|Customer Preference DNC| Phone opt-out value|
|Customer Custom| Custom data about the customer|

### Current Cart

Map to these destinations to send data for the current cart items.

|**Destination Name**| **Description**|
|---| ---|
|Current Cart ID| Unique cart identifier|
|Current Cart Quantity| Quantity of each item in the cart|
|Current Cart Custom Data| Custom data associated each item in the cart|

To send data for cart updates (addition or removal), use the `_cprod` E-Commerce mapping. Refer to the [Sending Cart Updates section](#sending-cart-updates) for more.

### Event Custom Data

Use these mappings to send additional data for [standard events](#triggering-standard-events) only.

|**Destination Name**| **Description**|
|---| ---|
|Event Custom Data for Product View| Event Custom Data for Product View|
|Event Custom Data for Search| Event Custom Data for Search|
|Event Custom Data for Category View| Event Custom Data for Category View|
|Event Custom Data for Brand View| Event Custom Data for Brand View|
|Event Custom Data for Cart Update| Event Custom Data for Cart Update|
|Event Custom Data for Checkout| Event Custom Data for Checkout|

## Triggering Standard Events

Standard events supported by AgilOne are triggered through the [Tealium Events Extension](). That means you don&#39;t have to map the event name or trigger value for any event that is supported through the Extension. The Extension introduces standardized event names into your solution, along with a new Data Layer Variable called `tealium_event`. Each event is assigned a custom condition that matches your data layer implementation. When an event condition evaluates to `true`, the `tealium_event` is set to a pre-defined event value. Tealium&#39;s AgilOne Webtag template reads the predefined value and accordingly fires the event. For example, when the condition for &#34;Add to Cart&#34; evalutes to `true`, `tealium_event` will be set to `cart_add` and the cart event fires on the cart page.

Full list of events supported for AgilOne through Tealium Events Extension:

|**Event Name**| **tealium_event Variable Value**| **Supporting Extension**|
|---| ---| ---|
|User Login| `user_login`| Tealium Events|
|User Logout| `user_logout`| Tealium Events|
|Search Page View| `search`| Tealium Events|
|Product Detail Page View| `product_view`| Tealium Events|
|Category Page View| `category_view`| Tealium Events|
|Brand View| `brand_view`| --|
|Add to Cart| `cart_add`| Tealium Events|
|Remove from Cart| `cart_remove`| Tealium Events|
|Empty Cart| `cart_empty`| Tealium Events|
|Checkout| `checkout`| Tealium Events|

To send additional custom data with a standard event, map in the [Event Custom Data mappings under Standard Category](#event-custom-data).

### Triggering Non-standard Events

If the event you want to trigger is not offered in the Tealium Events Extension, there is an alternative. You may use the Set Data Value Extension instead to set the event trigger and event condition. Then, map the trigger variable to the Event Name destination (under Standard Category).

The Brand View event is an example of a non-standard event. Follow these steps to trigger the event:

1. [Add and configure a new Set Data Values Extension]() from the Extension marketplace.

1. Scope it to AgilOne Webtag.

1. Set the `event_name` Data Variable to the text `brand_view`. Remember: the `brand_view` value is predefined in the template and cannot be changed.

1. Add an event condition to evaluate the customer&#39;s brand view action. For example, `event_type` equals `brand_view`.
If you don&#39;t find the Variable you are looking, you may add it on the fly.

1. Go to the Tag&#39;s Data Mappings tab and map the `event_name` Variable to the Event Name destination (Standard category).

### Sending Cart Updates

Adding and removing items from a cart are treated as standard events and, therefore, easily triggered by the Tealium Events Extension. Sending data for the final cart (including the added or removed items) is a three-step process:

1. Configure the Tealium Events Extension to trigger the cart addition/removal event.
1. Go to the Tag&#39;s Current Cart mappings and map to the destinations of choice.
1. Go to the E-Commerce Extension and map the newly added or removed cart item to `_cprod`. This will capture the updated cart items separately.

When the add-to-cart/remove-from-cart event fires on a page, our Tag template will automatically piece together the added/removed item(s) with the current cart data and send the complete cart list.

To correctly identify a removed cart item, you must map it to both E-Commerce `cprod` and Current Cart.

### Vendor Documentation

* [AgilOne Resource](http://www.agilone.com/academy/)
