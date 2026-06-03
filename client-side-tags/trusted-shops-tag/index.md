---
title: Trusted Shops Tag Setup Guide
description: This article describes how to set up the Trusted Shops tag.
url: https://docs.tealium.com/client-side-tags/trusted-shops-tag/
---
## Tag tips

* Use mapping to dynamically override the standard config values.
* When an order ID is set (usually on an order confirmation page), the hidden `trustedShopsCheckout` `&lt;div&gt;` will be added to the page. The following `&lt;span&gt;` tags will be created inside the `&lt;div&gt;` if their values are set by the E-Commerce extension or with a mapping:
    * `tsCheckoutOrderNr`
    * `tsCheckoutBuyerEmail`
    * `tsCheckoutOrderAmount`
    * `tsCheckoutOrderCurrency`
    * `tsCheckoutOrderPaymentType`
    * `tsCheckoutOrderEstDeliveryDate`

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Trusted Shops ID**: Provided by Trusted Shops.
* **Y-Offset**: Offset from the page bottom.
* **Variant**: Custom element ID is required for `custom` and `custom_reviews` variants.
* **Custom Element ID**: Required for `custom` and `custom_reviews` variants.
* **Trustcard Direction**: For custom variants.
* **Disable Responsive Behaviour**: Disable the request for reviews on purchases.
* **Disable Trust Badge**: Disable the display of the trust badge.

## Load rules

Load the tag on all pages or set conditions for when the tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `_tsid`| Trusted Shops ID   |
| `_tsConfig.yOffset`| Y-offset   |
|  `_tsConfig.variant`  | Variant. This value can be `text`, `default`, `small`, `reviews`, `custom`, or `custom_reviews`. |
| `_tsConfig.customElementId` | Custom element ID.  |
| `_tsConfig.trustcardDirection`   | Trustcard direction. This value can be `topRight`, `topLeft`, `bottomRight`, `bottomLeft`. |
| `_tsConfig.disableResponsive` | Disable responsive behavior. This value can be `false` or `true`. |
| `_tsConfig.disableTrustBadge`| Disable trust badge. This value can be `false` or `true`. |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| `order_id` (Overrides `_corder`)| Order ID   |
| `order_total` (Overrides `_ctotal`)| Order total   |
| `order_currency` (Overrides `_ccurrency`)| Currency   |
| `customer_id` (Overrides `_ccustid`)| Customer ID   |
| `tsCheckoutOrderPaymentType`| Order payment type   |
| `tsCheckoutOrderEstDeliveryDate`| Order estimated delivery Date   |