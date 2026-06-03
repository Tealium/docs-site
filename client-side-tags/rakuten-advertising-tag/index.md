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

First, go to Tealium&#39;s tag marketplace and add the Rakuten Marketing tag . For more information, see [Manage tags]().

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

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

#### Standard

|Variable| Description|
|---| ---|
|`trackingKey`|  &lt;ul&gt;&lt;li&gt;Tracking Key&lt;/li&gt;&lt;/ul&gt; |
|`siteSection`|  &lt;ul&gt;&lt;li&gt;Site Section&lt;/li&gt;&lt;/ul&gt; |
|`conversionType`|  &lt;ul&gt;&lt;li&gt;Conversion Type&lt;/li&gt;&lt;/ul&gt; |
|`customerStatus`|  &lt;ul&gt;&lt;li&gt;Customer Status&lt;/li&gt;&lt;/ul&gt; |
|`discountAmount`|  &lt;ul&gt;&lt;li&gt;Discount Amount&lt;/li&gt;&lt;/ul&gt; |
|`optionalData`|  &lt;ul&gt;&lt;li&gt;Optional Data&lt;/li&gt;&lt;/ul&gt; |

#### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Overrides `_corder` .&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Sub Total.&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;Tax Amount.&lt;/li&gt;&lt;li&gt;Overrides `_ctax`.&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;Currency.&lt;/li&gt;&lt;li&gt;Overrides `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;Promo Code.&lt;/li&gt;&lt;li&gt;Overrides `_cpromo`.&lt;/li&gt;&lt;/ul&gt; |
|`order_consumed`|  &lt;ul&gt;&lt;li&gt;Consumed.&lt;/li&gt;&lt;/ul&gt; |
|`order_shipped_country`|  &lt;ul&gt;&lt;li&gt;Order Shipped Country.&lt;/li&gt;&lt;/ul&gt; |
|`order_status`|  &lt;ul&gt;&lt;li&gt;Order Status.&lt;/li&gt;&lt;li&gt;Values are:  &lt;ul&gt;&lt;li&gt;Existing&lt;/li&gt;&lt;li&gt;Returning&lt;/li&gt;&lt;li&gt;New&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
| `order_shipped` |  &lt;ul&gt;&lt;li&gt;Order Shipped.&lt;/li&gt;&lt;/ul&gt; |
|`order_site_name`|  &lt;ul&gt;&lt;li&gt;Site Name.&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;Customer ID.&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_score`|  &lt;ul&gt;&lt;li&gt;Customer Score.&lt;/li&gt;&lt;/ul&gt; |
|`customer_country`|  &lt;ul&gt;&lt;li&gt;Customer Country.&lt;/li&gt;&lt;li&gt;Overrides `_ccountry`.&lt;/li&gt;&lt;li&gt;Used in place of `order_shipped_country` if `order_shipped_country` is not provided.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs.&lt;/li&gt;&lt;li&gt;Used in place of `product_sku` if `product_sku` is not provided.&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Names.&lt;/li&gt;&lt;li&gt;Overrides `_cprodname`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities.&lt;/li&gt;&lt;li&gt;Overrides `_cquan` .&lt;/li&gt;&lt;/ul&gt; |
|`product_sku`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of SKUs.&lt;/li&gt;&lt;li&gt;Overrides `_csku`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices.&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
|`product_discount`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Discounts.&lt;/li&gt;&lt;li&gt;Overrides `_cpdisc`.&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Brands.&lt;/li&gt;&lt;li&gt;Overrides `_cbrand`.&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Categories.&lt;/li&gt;&lt;li&gt;Overrides `_ccat` .&lt;/li&gt;&lt;/ul&gt; |
|`product_category_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Category IDs.&lt;/li&gt;&lt;/ul&gt; |
|`product_coupon`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Coupons.&lt;/li&gt;&lt;/ul&gt; |
|`product_is_clearance`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Clearance Statuses.&lt;/li&gt;&lt;/ul&gt; |
|`product_is_sale`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Sales Statuses.&lt;/li&gt;&lt;/ul&gt; |
|`product_margin`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Margins.&lt;/li&gt;&lt;/ul&gt; |

#### Affiliate

|Variable| Description|
|---| ---|
|`allowCommission`|  &lt;ul&gt;&lt;li&gt;Allow Commission&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.ranMID`|  &lt;ul&gt;&lt;li&gt;ranMID&lt;/li&gt;&lt;/ul&gt; |
| `affiliateConfig.taxRate` |  &lt;ul&gt;&lt;li&gt;Tax Rate&lt;/li&gt;&lt;/ul&gt; |
| `affiliateConfig.discountType` |  &lt;ul&gt;&lt;li&gt;Discount Type&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.tagType`|  &lt;ul&gt;&lt;li&gt;Tag Type&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.includeStatus`|  &lt;ul&gt;&lt;li&gt;Include Status&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.removeOrderTax`|  &lt;ul&gt;&lt;li&gt;Remove Order Tax&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.removeTaxFromProducts`|  &lt;ul&gt;&lt;li&gt;Remove Tax From Products&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.removeTaxFromDiscount`|  &lt;ul&gt;&lt;li&gt;Remove Tax From Discount.&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.centValues`|  &lt;ul&gt;&lt;li&gt;Cent Values.&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.nonCentCurrencies`|  &lt;ul&gt;&lt;li&gt;Non cent currencies.&lt;/li&gt;&lt;li&gt;Can accept an Array or a String containing a comma-separated list of currencies.&lt;/li&gt;&lt;/ul&gt; |

#### Display

|Variable| Description|
|---| ---|
|`displayConfig.rdMID`|  &lt;ul&gt;&lt;li&gt;rdMID&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.domain`|  &lt;ul&gt;&lt;li&gt;Domain&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.tagType`|  &lt;ul&gt;&lt;li&gt;Tag Type&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.includeStatus`|  &lt;ul&gt;&lt;li&gt;Include Status&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.allowCommission`|  &lt;ul&gt;&lt;li&gt;Allow Commission&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.removeTaxFromProducts`|  &lt;ul&gt;&lt;li&gt;Remove Tax From Products&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.removeTaxFromDiscount`|  &lt;ul&gt;&lt;li&gt;Remove Tax From Discount&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.taxRate`|  &lt;ul&gt;&lt;li&gt;Tax Rate&lt;/li&gt;&lt;/ul&gt; |

#### Search

|Variable| Description|
|---| ---|
|`searchConfig.rsMID`|  &lt;ul&gt;&lt;li&gt;rsMID&lt;/li&gt;&lt;/ul&gt; |
|`searchConfig.conversionType`|  &lt;ul&gt;&lt;li&gt;Conversion Type&lt;/li&gt;&lt;/ul&gt; |
|`searchConfig.accountID`|  &lt;ul&gt;&lt;li&gt;Account ID&lt;/li&gt;&lt;/ul&gt; |
|`searchConfig.clickID`|  &lt;ul&gt;&lt;li&gt;Click ID&lt;/li&gt;&lt;/ul&gt; |
