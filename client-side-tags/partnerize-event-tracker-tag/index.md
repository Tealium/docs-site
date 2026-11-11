---
title: Partnerize event tracker tag setup guide
description: This article describes how to set up the Partnerize Event Tracker tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/partnerize-event-tracker-tag/
---
## Tag tips

* Order Currency defaults to the E-Commerce extension value.
* This tag uses the following E-Commerce extension parameters:
    * Order ID
    * Order Currency
    * Order Promo Code
    * List of SKUs
    * List of Categories
    * List of Quantities
    * List of Prices
* Custom Product Parameter mappings should be arrays.
* Custom Conversion Parameter mappings should be strings.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Campaign**: The default Campaign.
* **Adref**: A Partnerize-provided value.
* **Customer Type**: The default customer type.
* **Country**: The two-letter ISO code for the country of the visitor or point of sale.
* **Default Currency**: The three-letter ISO code for the currency the conversion occurs in.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
| --- | --- |
| Campaign | (campaign) |
| Customertype | (customertype) |
| Custref/Customer ID | (customer_id) |
| Country | (country) |
| Adref | (adref) |
| Custom Conversion Parameter | (conversion.###) |
| Custom Product Parameter | (product.###) |

### E-Commerce

| Variable | Description |
| --- | --- |
| Conversionref/Order ID | (order_id) (Overrides _corder) |
| Currency | (currency) (Overrides _ccurrency) |
| Voucher/Promo Code | (voucher) (Overrides _cpromo) |
| List of SKUs (product_sku) (Overrides _csku) | [Array] |
| List of Categories (product_category) (Overrides _ccat) | [Array] |
| List of Quantities (product_quantity) (Overrides _cquan) | [Array] |
| List of Prices (product_unit_price) (Overrides _cprice) | [Array] |