---
title: Google Universal Analytics Tag Enhanced E-Commerce
description: This article is an overview of setting up Enhanced Ecommerce tracking forthe Google Universal Analytics tag in Tealium iQ Tag Management.
url: https://docs.tealium.com/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/
---
 As of July 1, 2023, Google Universal Analytics properties stopped processing hits. This tag has been deprecated and no longer available in the tag marketplace. For the current tag, see [Google Analytics 4](). 

## Overview

Enhanced Ecommerce is an [advanced plugin for ecommerce tracking using Google Universal Analytics](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce) to track user interactions with products on your website, including: product impressions, product clicks, viewing product details, adding a product to a shopping cart, initiating the checkout process, transactions, and refunds.

## How it works

Enhanced Ecommerce tracking works with a combination of the [E-Commerce extension]() and [data mapping](/iq-tag-management/data-mappings/manage/) in the [Google Universal Analytics tag](). The E-Commerce extension handles the most common ecommerce data, while the more advanced data is sent using data mappings in the tag configuration. Enhanced Ecommerce actions are also mapped in the tag as events.

## Enhanced E-commerce data and actions

The E-Commerce Extension settings cover many of the new Enhanced E-Commerce features. However, if your Universal Data Object (UDO) does not accommodate [the data required for Enhanced E-Commerce](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#ecommerce-data), you will have to add variables to your website&#39;s data layer.

Here is a recommended list of data layer variables to add, along with their matching variable in Enhanced Ecommerce.

If a variable is marked as &#34;n/a&#34; in the E-Commerce Extension column, it must be added to the tag as a data mapping.

## Impression data

When impression data is mapped and populated in the UDO it is passed to Google Analytics using the `ec:addImpression` command.

|Data Layer Variable| Google Key| E-Commerce&lt;br&gt; Extension|
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

|Data Layer Variable| Google Key| E-Commerce&lt;br&gt; Extension|
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

|Data Layer Variable| Google Key| E-Commerce&lt;br&gt; Extension|
|---| ---| ---|
|promotion\_id| id| n/a|
|promotion\_name| name| n/a|
|promotion\_creative| creative| n/a|
|promotion\_position| position| n/a|

## Action data

The action variables are populated in any event that expect order data. The order data required by Enhanced Ecommerce is automatically mapped by the E-Commerce Extension (see table below). Action variables are passed to Google Analytics using the `ec:setAction` command.

|Data Layer Variable| Google Key| E-Commerce&lt;br&gt; Extension|
|---| ---| ---|
|order\_id| id| \_corder|
|order\_store| affiliation| \_cstore|
|order\_grand\_total| revenue| \_ctotal|
|order\_tax\_amount| tax| \_ctax|
|order\_shipping\_amount| shipping| \_cship|
|order\_promo\_code| coupon| \_cpromo|
|checkout\_step| step| n/a |
|shipping\_method,&lt;br&gt; shipping\_carrier,&lt;br&gt; payment\_method,&lt;br&gt; etc. &lt;br&gt; (various checkout options) | option| n/a |

## Data mapping

Enhanced Ecommerce actions are triggered using data mappings. A data mapping for an event matches the values of the event variable to the corresponding Enhanced Ecommerce action. These mappings results in triggering the `ec:setAction` command in Google Analytics.

Typical event variables in your data layer would be: `tealium_event`, `page_type`, or `event_name`.


The following are suggested Tealium events that map onto the expected Enhanced Ecommerce actions:

|Tealium Event/Page Type| Google Action&lt;br&gt; (enh\_action)|
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
 &#34;product_impression_id&#34;       : [&#39;P12345&#39;, &#39;P67890&#39;],
 &#34;product_impression_name&#34;     : [&#39;DV T-Shirt&#39;, &#39;DV Water Bottle&#39;],
 &#34;product_impression_brand&#34;    : [&#39;Tealium&#39;, &#39;Tealium&#39;],
 &#34;product_impression_variant&#34;  : [&#39;black&#39;, &#39;blue&#39;],
 &#34;product_impression_category&#34; : [&#39;Shirts&#39;, &#39;Home &amp; Office&#39;],
 &#34;product_impression_list&#34;     : [&#39;Search Results&#39;, &#39;Search Results&#39;],
 &#34;product_impression_position&#34; : [1, 2]
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
  &#34;tealium_event&#34;    : &#34;product_click&#34;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;],
  &#34;product_position&#34; : [1]
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
  &#34;tealium_event&#34;    : &#34;product_view&#34;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;]
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
  &#34;tealium_event&#34;    : &#39;cart_add&#39;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;],
  &#34;product_price&#34;    : [&#39;23.49&#39;],
  &#34;product_quantity&#34; : [1]
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
  &#34;tealium_event&#34;    : &#39;cart_remove&#39;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;],
  &#34;product_price&#34;    : [&#39;23.49&#39;],
  &#34;product_quantity&#34; : [1]
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
  &#34;tealium_event&#34;    : &#39;checkout&#39;,
  &#34;product_id&#34;       : [&#39;P1235&#39;, &#39;P67890&#39;],
  &#34;product_name&#34;     : [&#39;DV T-Shirt&#39;, &#39;DV Water Bottle&#39;],
  &#34;product_brand&#34;    : [&#39;Tealium&#39;, &#39;Tealium&#39;],
  &#34;product_variant&#34;  : [&#39;black&#39;, &#39;blue&#39;],
  &#34;product_category&#34; : [&#39;Shirts&#39;, &#39;Home &amp; Office&#39;],
  &#34;product_price&#34;    : [&#39;23.39&#39;, &#39;11.00&#39;],
  &#34;product_quantity&#34; : [1, 2],
  &#34;product_position&#34; : [1, 2],
  &#34;checkout_step&#34;    : &#34;1&#34;,
  &#34;shipping_carrier&#34; : &#39;FedEx&#39;
};

```

Checkout steps can be assigned more descriptive names using the [Checkout Funnel Configuration](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce#checkout-funnel) within your Google Analytics account.

### Checkout option

The Checkout Option action lets you capture information about the state of a checkout after the initial page view, when the visitor is interacting with the site.

You can send the following data with the checkout option action:

* Checkout Step
* Checkout Option

This event is tracked using  `utag.link()` and triggers the `ec:setAction` (checkout\_option) command in Google Analytics.

```js
// EXAMPLE CODE: Checkout Option
utag.link({
  &#34;tealium_event&#34;    : &#34;checkout_option&#34;,
  &#34;checkout_step&#34;    : &#34;2&#34;,
  &#34;shipping_carrier&#34; : &#34;FedEx&#34;
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
  &#34;tealium_event&#34;         : &#39;purchase&#39;,
  &#34;order_id&#34;              : &#39;O1234567&#39;,
  &#34;order_grand_total&#34;     : &#39;57.44&#39;,
  &#34;order_tax_amount&#34;      : &#39;3.65&#39;,
  &#34;order_shipping_amount&#34; : &#39;8.50&#39;,
  &#34;order_promo_code&#34;      : &#39;SALE20&#39;,
  &#34;product_id&#34;            : [&#39;P1235&#39;, &#39;P67890&#39;],
  &#34;product_name&#34;          : [&#39;DV T-Shirt&#39;, &#39;DV Water Bottle&#39;],
  &#34;product_brand&#34;         : [&#39;Tealium&#39;, &#39;Tealium&#39;],
  &#34;product_variant&#34;       : [&#39;black&#39;, &#39;blue&#39;],
  &#34;product_category&#34;      : [&#39;Shirts&#39;, &#39;Home &amp; Office&#39;],
  &#34;product_price&#34;         : [&#39;23.39&#39;, &#39;11.00&#39;],
  &#34;product_quantity&#34;      : [1, 2]
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
  &#34;tealium_event&#34;      : &#34;promo_click&#34;,
  &#34;promotion_id&#34;       : [&#39;DV18-EARLY-REG&#39;],
  &#34;promotion_name&#34;     : [&#39;DV 2018 Early Registration&#39;],
  &#34;promotion_creative&#34; : [&#39;early_reg_promo1&#39;],
  &#34;promotion_position&#34; : [1]
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
  &#34;tealium_event&#34;    : &#34;refund&#34;,
  &#34;order_id&#34;         : &#39;O123456&#39;,
  &#34;product_id&#34;       : [&#39;P12345&#39;],
  &#34;product_quantity&#34; : [1]
};
```

## Additional resources

* [About Enhanced Ecommerce](https://support.google.com/analytics/answer/6014841?hl=en) (Google Analytics)
* [How to collect enhanced ecommerce data using analytics.js](https://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce) (Google Analytics)
