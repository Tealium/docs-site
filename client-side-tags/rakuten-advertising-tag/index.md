---
title: Rakuten Advertising Tag Setup Guide
description: This article describes how to set up the Rakuten Advertising tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/rakuten-advertising-tag/
---
## Tag tips

* If you paste the `affiliateConfig` object in the **Extract From Code** field, the tag automatically populates `ranMID`, `discountType`, and `includeStatus` parameters. 
* Conversion fires when Order ID is set.
* Affiliate functionality is only available when **Allow Commission** is set to `True`.
* Supports these E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Sub Total (`_csubtotal`)
  * Tax Amount (`_ctax`)
  * Currency (`_ccurrency`)
  * Promo Code (`_cpromo`)
  * Customer ID (`_ccustid`)
  * List of Product IDs (`_cprod`)
  * List of Names (`_cprodname`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)
  * List of Discounts (`_cpdisc`)

### Tag configuration

First, go to Tealium's tag marketplace and add the Rakuten Marketing tag . For more information, see [Manage tags](https://docs.tealium.com/manage-tags/).

After adding the tag, configure the following settings:

* **Tracking Key**: Your site-specific tracking key issued by your Rakuten Marketing integration contact.
* **Rakuten Affiliate Merchant ID**: A 4 or 5-digit merchant ID.
* **Tax Rate**: Tax rate as a percentage value. For example, `20` for UK VAT of 20%.
* **Rakuten Display Merchant ID**: * A 4-digit merchant ID.
* **Rakuten Search Merchant ID**: Search Config rsMID (`rsMID`).
* **Conversion Type**: The default value is `sale`, but can be set to anything.
* **Discount Type**: The discount type for affiliate sales. The default value is `amount`, but can be set to `percentage`.
* **Include Status**: Whether to include the order status in the tag. The default value is `true`.

### Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

#### Standard

|Variable| Description|
|---| ---|
|`trackingKey`|  <ul><li>Tracking Key</li></ul> |
|`siteSection`|  <ul><li>Site Section</li></ul> |
|`conversionType`|  <ul><li>Conversion Type</li></ul> |
|`customerStatus`|  <ul><li>Customer Status</li></ul> |
|`discountAmount`|  <ul><li>Discount Amount</li></ul> |
|`optionalData`|  <ul><li>Optional Data</li></ul> |

#### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID.</li><li>Overrides `_corder` .</li></ul> |
|`order_subtotal`|  <ul><li>Sub Total.</li><li>Overrides `_csubtotal`.</li></ul> |
|`order_tax`|  <ul><li>Tax Amount.</li><li>Overrides `_ctax`.</li></ul> |
|`order_currency`|  <ul><li>Currency.</li><li>Overrides `_ccurrency`.</li></ul> |
|`order_coupon_code`|  <ul><li>Promo Code.</li><li>Overrides `_cpromo`.</li></ul> |
|`order_consumed`|  <ul><li>Consumed.</li></ul> |
|`order_shipped_country`|  <ul><li>Order Shipped Country.</li></ul> |
|`order_status`|  <ul><li>Order Status.</li><li>Values are:  <ul><li>Existing</li><li>Returning</li><li>New</li></ul> </li></ul> |
| `order_shipped` |  <ul><li>Order Shipped.</li></ul> |
|`order_site_name`|  <ul><li>Site Name.</li></ul> |
|`customer_id`|  <ul><li>Customer ID.</li><li>Overrides `_ccustid`.</li></ul> |
|`customer_score`|  <ul><li>Customer Score.</li></ul> |
|`customer_country`|  <ul><li>Customer Country.</li><li>Overrides `_ccountry`.</li><li>Used in place of `order_shipped_country` if `order_shipped_country` is not provided.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs.</li><li>Used in place of `product_sku` if `product_sku` is not provided.</li><li>Overrides `_cprod`.</li></ul> |
|`product_name`|  <ul><li>Array</li><li>List of Names.</li><li>Overrides `_cprodname`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities.</li><li>Overrides `_cquan` .</li></ul> |
|`product_sku`|  <ul><li>Array</li><li>List of SKUs.</li><li>Overrides `_csku`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices.</li><li>Overrides `_cprice`.</li></ul> |
|`product_discount`|  <ul><li>Array</li><li>List of Discounts.</li><li>Overrides `_cpdisc`.</li></ul> |
|`product_brand`|  <ul><li>Array</li><li>List of Brands.</li><li>Overrides `_cbrand`.</li></ul> |
|`product_category`|  <ul><li>Array</li><li>List of Categories.</li><li>Overrides `_ccat` .</li></ul> |
|`product_category_id`|  <ul><li>Array</li><li>List of Category IDs.</li></ul> |
|`product_coupon`|  <ul><li>Array</li><li>List of Coupons.</li></ul> |
|`product_is_clearance`|  <ul><li>Array</li><li>List of Clearance Statuses.</li></ul> |
|`product_is_sale`|  <ul><li>Array</li><li>List of Sales Statuses.</li></ul> |
|`product_margin`|  <ul><li>Array</li><li>List of Margins.</li></ul> |

#### Affiliate

|Variable| Description|
|---| ---|
|`allowCommission`|  <ul><li>Allow Commission</li><li>Values are `true` or `false`.</li></ul> |
|`affiliateConfig.ranMID`|  <ul><li>ranMID</li></ul> |
| `affiliateConfig.taxRate` |  <ul><li>Tax Rate</li></ul> |
| `affiliateConfig.discountType` |  <ul><li>Discount Type</li></ul> |
|`affiliateConfig.tagType`|  <ul><li>Tag Type</li></ul> |
|`affiliateConfig.includeStatus`|  <ul><li>Include Status</li><li>Values are `true` or `false`.</li></ul> |
|`affiliateConfig.removeOrderTax`|  <ul><li>Remove Order Tax</li><li>Values are `true` or `false`.</li></ul> |
|`affiliateConfig.removeTaxFromProducts`|  <ul><li>Remove Tax From Products</li><li>Values are `true` or `false`.</li></ul> |
|`affiliateConfig.removeTaxFromDiscount`|  <ul><li>Remove Tax From Discount.</li><li>Values are `true` or `false`.</li></ul> |
|`affiliateConfig.centValues`|  <ul><li>Cent Values.</li><li>Values are `true` or `false`.</li></ul> |
|`affiliateConfig.nonCentCurrencies`|  <ul><li>Non cent currencies.</li><li>Can accept an Array or a String containing a comma-separated list of currencies.</li></ul> |

#### Display

|Variable| Description|
|---| ---|
|`displayConfig.rdMID`|  <ul><li>rdMID</li></ul> |
|`displayConfig.domain`|  <ul><li>Domain</li></ul> |
|`displayConfig.tagType`|  <ul><li>Tag Type</li></ul> |
|`displayConfig.includeStatus`|  <ul><li>Include Status</li></ul> |
|`displayConfig.allowCommission`|  <ul><li>Allow Commission</li></ul> |
|`displayConfig.removeTaxFromProducts`|  <ul><li>Remove Tax From Products</li><li>Values are `true` or `false`.</li></ul> |
|`displayConfig.removeTaxFromDiscount`|  <ul><li>Remove Tax From Discount</li><li>Values are `true` or `false`.</li></ul> |
|`displayConfig.taxRate`|  <ul><li>Tax Rate</li></ul> |

#### Search

|Variable| Description|
|---| ---|
|`searchConfig.rsMID`|  <ul><li>rsMID</li></ul> |
|`searchConfig.conversionType`|  <ul><li>Conversion Type</li></ul> |
|`searchConfig.accountID`|  <ul><li>Account ID</li></ul> |
|`searchConfig.clickID`|  <ul><li>Click ID</li></ul> |
