---
title: Google Universal Analytics Tag Enhanced E-Commerce
description: This article is an overview of setting up Enhanced Ecommerce tracking forthe Google Universal Analytics tag in Tealium iQ Tag Management.
url: https://docs.tealium.com/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/
---

<blockquote>
As of July 1, 2023, Google Universal Analytics properties stopped processing hits. This tag has been deprecated and no longer available in the tag marketplace. For the current tag, see [Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/).
</blockquote>


## Overview

Enhanced Ecommerce is an [advanced plugin for ecommerce tracking using Google Universal Analytics](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce) to track user interactions with products on your website, including: product impressions, product clicks, viewing product details, adding a product to a shopping cart, initiating the checkout process, transactions, and refunds.

## How it works

Enhanced Ecommerce tracking works with a combination of the [E-Commerce extension](https://docs.tealium.com/e-commerce-extension/) and [data mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/) in the [Google Universal Analytics tag](https://docs.tealium.com/google-universal-analytics-analyticsjs-tag/). The E-Commerce extension handles the most common ecommerce data, while the more advanced data is sent using data mappings in the tag configuration. Enhanced Ecommerce actions are also mapped in the tag as events.

## Enhanced E-commerce data and actions

The E-Commerce Extension settings cover many of the new Enhanced E-Commerce features. However, if your Universal Data Object (UDO) does not accommodate [the data required for Enhanced E-Commerce](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#ecommerce-data), you will have to add variables to your website's data layer.

Here is a recommended list of data layer variables to add, along with their matching variable in Enhanced Ecommerce.


<blockquote>
If a variable is marked as "n/a" in the E-Commerce Extension column, it must be added to the tag as a data mapping.
</blockquote>


## Impression data

When impression data is mapped and populated in the UDO it is passed to Google Analytics using the `ec:addImpression` command.

|Data Layer Variable| Google Key| E-Commerce<br> Extension|
|---| ---| ---|
|product\_impression\_id| id| n/a|
|product\_impression\_name| name| n/a|
|product\_impression\_list| list| n/a|
|product\_impression\_brand| brand| n/a|
|product\_impression\_category| category| n/a|
|product\_impression\_variant| variant| n/a|
|product\_impression\_position| position| n/a|
|product\_impression\_price| price| n/a|

## Product data

The product variables are used in any event that expects product data. The product data required by Enhanced Ecommerce is mapped automatically by the E-Commerce Extension (see table below). Product variables are passed to Google Analytics using the `ec:addProduct` command.

|Data Layer Variable| Google Key| E-Commerce<br> Extension|
|---| ---| ---|
|product\_id| id| \_cprod|
|product\_name| name| \_cprodname|
|product\_brand| brand| \_cbrand|
|product\_category| category| \_ccat|
|product\_variant| variant| n/a|
|product\_price| price| \_cprice |
|product\_quantity| quantity| \_cquan|
|product\_promo\_code| coupon| \_cpdisc|
|product\_position| position| n/a|

## Promotion data

When promotion data is mapped and populated in the UDOit is passed to Google Analytics using the `ec:addPromo` command.

|Data Layer Variable| Google Key| E-Commerce<br> Extension|
|---| ---| ---|
|promotion\_id| id| n/a|
|promotion\_name| name| n/a|
|promotion\_creative| creative| n/a|
|promotion\_position| position| n/a|

## Action data

The action variables are populated in any event that expect order data. The order data required by Enhanced Ecommerce is automatically mapped by the E-Commerce Extension (see table below). Action variables are passed to Google Analytics using the `ec:setAction` command.

|Data Layer Variable| Google Key| E-Commerce<br> Extension|
|---| ---| ---|
|order\_id| id| \_corder|
|order\_store| affiliation| \_cstore|
|order\_grand\_total| revenue| \_ctotal|
|order\_tax\_amount| tax| \_ctax|
|order\_shipping\_amount| shipping| \_cship|
|order\_promo\_code| coupon| \_cpromo|
|checkout\_step| step| n/a |
|shipping\_method,<br> shipping\_carrier,<br> payment\_method,<br> etc. <br> (various checkout options) | option| n/a |

## Data mapping

Enhanced Ecommerce actions are triggered using data mappings. A data mapping for an event matches the values of the event variable to the corresponding Enhanced Ecommerce action. These mappings results in triggering the `ec:setAction` command in Google Analytics.

Typical event variables in your data layer would be: `tealium_event`, `page_type`, or `event_name`.


The following are suggested Tealium events that map onto the expected Enhanced Ecommerce actions:

|Tealium Event/Page Type| Google Action<br> (enh\_action)|
|---| ---|
|product\_click| click|
|product\_view| detail|
|cart\_add| add|
|cart\_remove| remove|
|checkout| checkout|
|checkout\_option| checkout\_option|
|purchase| purchase|
|refund | refund|
|promo\_click| promo\_click|

## Examples

To trigger Enhanced E-Commerce actions map your event variable to an event in the data mappings.

### Product impression

You can send the following data with a product impression action:

* List of IDs (Required)
* List of Names
* List of Brands
* List of Categories
* List of Variants
* Product List Names

This event occurs on page load using `utag_data` or using `utag.view()` and triggers the `ec:addImpression` command in Google Analytics for each item in the arrays.

```js
// EXAMPLE CODE: Product Detail Page View
var utag_data = {
 "product_impression_id"       : ['P12345', 'P67890'],
 "product_impression_name"     : ['DV T-Shirt', 'DV Water Bottle'],
 "product_impression_brand"    : ['Tealium', 'Tealium'],
 "product_impression_variant"  : ['black', 'blue'],
 "product_impression_category" : ['Shirts', 'Home & Office'],
 "product_impression_list"     : ['Search Results', 'Search Results'],
 "product_impression_position" : [1, 2]
};
```

### Product click

Send the following data with a product `click` action:

* List of IDs (Required)
* List of Names
* List of Brands
* List of Categories
* List of Variants
* Product Position

This event is tracked using `utag.link()` and triggers the `ec:addProduct` and `ec:setAction` (click) command in Google Analytics.

```js
// EXAMPLE CODE: Product Click
utag.link({
  "tealium_event"    : "product_click",
  "product_id"       : ['P12345'],
  "product_name"     : ['DV T-Shirt'],
  "product_brand"    : ['Tealium'],
  "product_variant"  : ['black'],
  "product_category" : ['Shirts'],
  "product_position" : [1]
});

```

### Product view/detail

You can send the following data with a product `detail` action:

* List of IDs (Required)
* List of Names
* List of Brands
* List of Categories
* List of Variants

This event is tracked on page load using `utag_data` or using `utag.view()` and triggers the `ec:addProduct` and `ec:setAction` (detail) command in Google Analytics.

```js
// EXAMPLE CODE: Product Detail Page View
var utag_data = {
  "tealium_event"    : "product_view",
  "product_id"       : ['P12345'],
  "product_name"     : ['DV T-Shirt'],
  "product_brand"    : ['Tealium'],
  "product_variant"  : ['black'],
  "product_category" : ['Shirts']
};

```

### Cart add

You can send the following data with the cart `add` action:

* List of IDs
* List of Names
* List of Brands
* List of Categories
* List of Quantities
* List of Prices
* List of Discounts
* List of Variants
* Product Position

This event is tracked using  `utag.link()` and triggers the `ec:addProduct` and `ec:setAction` (add) command in Google Analytics.

```js
// EXAMPLE CODE: Product Add
utag.link({
  "tealium_event"    : 'cart_add',
  "product_id"       : ['P12345'],
  "product_name"     : ['DV T-Shirt'],
  "product_brand"    : ['Tealium'],
  "product_variant"  : ['black'],
  "product_category" : ['Shirts'],
  "product_price"    : ['23.49'],
  "product_quantity" : [1]
});

```

### Cart remove

You can send the following data with the cart `remove` action:

* List of IDs
* List of Names
* List of Brands
* List of Categories
* List of Quantities
* List of Prices
* List of Discounts
* List of Variants

This event is tracked using  `utag.link()` and triggers the `ec:addProduct` and `ec:setAction` (remove) command in Google Analytics.

```js
// EXAMPLE CODE: Product Cart Removal
utag.link({
  "tealium_event"    : 'cart_remove',
  "product_id"       : ['P12345'],
  "product_name"     : ['DV T-Shirt'],
  "product_brand"    : ['Tealium'],
  "product_variant"  : ['black'],
  "product_category" : ['Shirts'],
  "product_price"    : ['23.49'],
  "product_quantity" : [1]
});

```

### Checkout

You can send the following data with the `checkout` action:

* List of IDs
* List of Names
* List of Brands
* List of Categories
* List of Quantities
* List of Prices
* List of Discounts
* Checkout Step
* Checkout Option
* List of Variants
* Product Position

This event is tracked on page load using `utag_data` or using `utag.view()` and triggers the `ec:addProduct` and `ec:setAction` (checkout) command in Google Analytics.

```js
// EXAMPLE CODE: Checkout
var utag_data = {
  "tealium_event"    : 'checkout',
  "product_id"       : ['P1235', 'P67890'],
  "product_name"     : ['DV T-Shirt', 'DV Water Bottle'],
  "product_brand"    : ['Tealium', 'Tealium'],
  "product_variant"  : ['black', 'blue'],
  "product_category" : ['Shirts', 'Home & Office'],
  "product_price"    : ['23.39', '11.00'],
  "product_quantity" : [1, 2],
  "product_position" : [1, 2],
  "checkout_step"    : "1",
  "shipping_carrier" : 'FedEx'
};

```


<blockquote>
Checkout steps can be assigned more descriptive names using the [Checkout Funnel Configuration](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#checkout-funnel) within your Google Analytics account.
</blockquote>


### Checkout option

The Checkout Option action lets you capture information about the state of a checkout after the initial page view, when the visitor is interacting with the site.

You can send the following data with the checkout option action:

* Checkout Step
* Checkout Option

This event is tracked using  `utag.link()` and triggers the `ec:setAction` (checkout\_option) command in Google Analytics.

```js
// EXAMPLE CODE: Checkout Option
utag.link({
  "tealium_event"    : "checkout_option",
  "checkout_step"    : "2",
  "shipping_carrier" : "FedEx"
});
```

### Purchase

You can send the following data with the `purchase` action:

* Order ID
* Revenue
* Tax
* Shipping
* Promo Code
* List of IDs
* List of Names
* List of Brands
* List of Categories
* List of Quantities
* List of Prices
* List of Discounts
* List of Variants

This event is tracked on page load using `utag_data` or using `utag.view()` and triggers the and `purchase` command in Google Analytics.

```js
// EXAMPLE CODE: Checkout
// The following information should be in the data object on page load
var utag_data = {
  "tealium_event"         : 'purchase',
  "order_id"              : 'O1234567',
  "order_grand_total"     : '57.44',
  "order_tax_amount"      : '3.65',
  "order_shipping_amount" : '8.50',
  "order_promo_code"      : 'SALE20',
  "product_id"            : ['P1235', 'P67890'],
  "product_name"          : ['DV T-Shirt', 'DV Water Bottle'],
  "product_brand"         : ['Tealium', 'Tealium'],
  "product_variant"       : ['black', 'blue'],
  "product_category"      : ['Shirts', 'Home & Office'],
  "product_price"         : ['23.39', '11.00'],
  "product_quantity"      : [1, 2]
};

```

### Promo click

You can send the following data with a promo click action:

* Promotion ID
* Promotion Name
* Promotion Creative
* Promotion Position

This event is tracked using `utag.link()` and triggers the `ec:addPromo` and `ec:setAction` (promo\_click) command in Google Analytics.

```js
// EXAMPLE CODE: Promotion Click
utag.link({
  "tealium_event"      : "promo_click",
  "promotion_id"       : ['DV18-EARLY-REG'],
  "promotion_name"     : ['DV 2018 Early Registration'],
  "promotion_creative" : ['early_reg_promo1'],
  "promotion_position" : [1]
});

```

### Refund

To fire a refund action, you must have the Order ID of the transaction that is being refunded. For a partial refund, the Product IDs of any items being refunded must be present as well.

* Order ID
* List of Product IDs (for partial refund only)

* List of Quantities

This event is tracked on page load using `utag_data` or using `utag.view()` and triggers the `ec:addProduct` and `ec:setAction` (refund) command in Google Analytics.

```js
// EXAMPLE CODE: Refund
var utag_data = {
  "tealium_event"    : "refund",
  "order_id"         : 'O123456',
  "product_id"       : ['P12345'],
  "product_quantity" : [1]
};
```

## Additional resources

* [About Enhanced Ecommerce](https://support.google.com/analytics/answer/6014841?hl=en) (Google Analytics)
* [How to collect enhanced ecommerce data using analytics.js](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce) (Google Analytics)
