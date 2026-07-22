---
title: Oracle CX Tag Setup Guide
description: This article describes how to set up the Oracle CX Tag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/oracle-cx-tag/
---
## Tag Tips

* Supports these E-Commerce extension parameters:
  * Order ID (`_corder`)
  * List of Product IDs (`_cprod`)
  * List of Product SKUs (`_csku`)
  * List of Product Quantities (`_cquan`)
  * Order Total (`_ctotal`)
  * Sub Total (`_csubtotal`)
  * Shipping Amount (`_cship`)
  * Tax Amount (`_ctax`)
  * Currency (`_ccurrency`)
  * Promo Code (`_cpromo`)
  * List of Names (`_cprodname`)
  * List of Brands (`_cbrand`)
  * List of Categories (`_ccat`)
  * List of Categories 2 (`_ccat2`)
  * List of Prices (`_cprice`)
  * List of Discounts (`_cpdisc`)

## Tag Configuration

First, go to the tag marketplace and add the Oracle CX Tag tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Account ID**
  * Your Oracle Infinity Account ID.

* **Tag ID**
  * Your Oracle Infinity Tag ID.

* **Context**
  * Optional
  * The context for your Oracle Infinity Tag.
  * Example: `analytics:dev`

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`account_guid`| Account ID|
|`tag_id`| Tag ID|
|`context`| Context|

### Click Tracking Configuration

|Variable| Description|
|---| ---|
|`successCallback`| Success Callback Function|
|`failCallback`| Fail Callback Function|
|`mutation`| Mutation Function|
|`wt.dl`| Event ID|

### Commerce

|Variable| Description|
|---| ---|
|`wt.tx_i`| Invoice Number|
|`wt.tx_id`| Invoice Date|
|`wt.tx_it`| Invoice Time|
|`wt.mc_id`| Campaign ID|
|`wt.mc_ev`| Campaign Event|
|`wt.conv`| Conversion Nam|
|`wt.pn_sku`| Product SKU|
|`wt.pn_id`| Product Identifier|
|`wt.pn_fa`| Product Family|
|`wt.pn_gr`| Product Group|
|`wt.pn_sc`| Product Subgroup|
|`wt.pn_ma`| Product Manufacturer|
|`wt.pn_su`| Product Supplier|
|`wt.product_coupon`| Coupon Code|
|`wt.product_name`| Product Names|
|`wt.pn_gr`| Product Group|
|`wt.pn_sc`| Product Sub Group|
|`wt.product_price`| Product Price|
|`wt.product_discount`| Product Unit Discount|
|`wt.cart_total`| Cart Total|
|`wt.cart_subtotal`| Cart Subtotal|
|`wt.cart_shipping`| Cart Shipping|
|`wt.cart_tax`| Cart Tax|
|`wt.currency`| Currency|
|`wt.si_cs`| Conversion Step|
|`wt.si_n`| Scenario Name|
|`wt.si_p`| Scenario Step Name|
|`wt.si_x`| Scenario Step Number|
|`wt.tx_cartid`|  <ul><li>Cart ID</li><li>Overrides `_corder`.</li></ul> |
|`wt.tx_s`| Transaction Subtotal|
|`wt.tx_u`| Units|
|`wt.tx_e`| Transaction Event Type|

### Transaction Event Type

|Variable| Description|
|---| ---|
|`a`| Cart Addition|
|`p`| Purchase|
|`r`| Cart Removal|
|`v`| Product View|
|Custom| Custom|

### Content

|Variable| Description|
|---| ---|
|`wt.cg_n`| Content Group Name|
|`wt.cg_s`| Content Subgroup Name|
|`wt.ti`| Page Title|
|`page-uri`| Page URI|
|`wt.es`| Page URL|
|`domain`| Domain|
|`wt.oss`| On-site Search Phrase|
|`wt.oss_r`| On-site Search Success|

### Mobile Web and App

|Variable| Description|
|---| ---|
|`wt.a_ac`| App Ad Click|
|`wt.a_ai`| App Ad Impression|
|`wt.a_an`| App Ad Name|
|`wt.a_pub`| App Publisher|
|`wt.ct`| Connection Type|
|`wt.g_co`| Country of Origin|
|`wt.dm`| Device Model|
|`wt.ets`| Event Timestamp|
|`wt.gc`| Geolocation Coordinates|
|`wt.sys`| Mobile App Event Type|
|`wt.a_nm`| Mobile App Name|
|`wt.av`| Mobile App Version|
|`wt.a_dc`| Mobile Carrier|
|`wt.sdk_v`| Mobile SDK Build|

### Traffic Sources

|Variable| Description|
|---| ---|
|`referrer`| Referrer|
|`referrer-domain`| Referring Domain|
|`referrer-path`| Referring URI|
