---
title: comScore Digital Analytix Tag Setup Guide
description: This article describes how to set up the comScore Digital Analytix tag.
url: https://docs.tealium.com/client-side-tags/comscore-digital-analytix-tag/
---
## Tag tips

* comScore is now GDPR-compliant. You can indicate a visitor&#39;s consent by setting the `cs_ucfr` parameter to 0 (no consent) or 1 (consent). By default the `cs_ucfr parameter` is set to 0. You can set this parameter with a mappings. You may have to update this tag&#39;s template to take advantage of this feature.
* Use mapping to add additional `c-parameters`.
* Order tracking is triggered automatically when an Order ID is set by the E-Commerce extension.
* Supports the following E-Commerce extension values:
    * Order ID
    * Shipping Amount
    * Customer ID
    * List of Product IDs
    * List of Brands
    * List of Categories
    * List of Categories 2
    * List of Quantities
    * List of Prices

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

Configure the following settings:

* **Client ID**: Your comScore Client ID (c2)
* **Stream Sense Video Tracking**: 
* **Form Identifier**: Enter a Form ID or Name to enable form measurements. Enter * to measure all forms. Use mapping to measure hidden form fields. Leave this field blank to disable form tracking.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `c1`  | &lt;ul&gt;&lt;li&gt;C1&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;/ul&gt; |
| `c2`  | &lt;ul&gt;&lt;li&gt;Client ID&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;/ul&gt; |
| `ns_type` | &lt;ul&gt;&lt;li&gt;NS Type&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;/ul&gt; |
| `form` | &lt;ul&gt;&lt;li&gt;Form identifier&lt;/li&gt;&lt;/ul&gt; |
| `form_normal`  | &lt;ul&gt;&lt;li&gt;Normal Form Fields&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;/ul&gt; |
| `form_hidden`  | &lt;ul&gt;&lt;li&gt;Hidden Form Fields&lt;/li&gt;&lt;li&gt; Array&lt;/li&gt;&lt;/ul&gt; |
| `form_submit`  | &lt;ul&gt;&lt;li&gt;Report Submit Events&lt;/li&gt;&lt;li&gt; Boolean&lt;/li&gt;&lt;/ul&gt; |
| `form_abandon`  | &lt;ul&gt;&lt;li&gt;Report Abandon Events&lt;/li&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
| `form_failure`  | &lt;ul&gt;&lt;li&gt;Report Failure Events&lt;/li&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
| `cs_ucfr`  | &lt;ul&gt;&lt;li&gt;Consent State&lt;/li&gt;&lt;li&gt;[0/1]&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| `order_id` | &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`&lt;/li&gt;&lt;/ul&gt; |
| `order_shipping` | &lt;ul&gt;&lt;li&gt;Shipping Amount&lt;/li&gt;&lt;li&gt;Overrides `_cship`&lt;/li&gt;&lt;/ul&gt; |
| `customer_id` | &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`&lt;/li&gt;&lt;/ul&gt; |
| `product_id` | &lt;ul&gt;&lt;li&gt;List of Product IDs&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Overrides `_cprod`&lt;/li&gt;&lt;/ul&gt; |
| `product_brand` | &lt;ul&gt;&lt;li&gt;List of Brands&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Overrides `_cbrand`&lt;/li&gt;&lt;/ul&gt; |
| `product_category` | &lt;ul&gt;&lt;li&gt;List of Categories&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Overrides `_ccat`&lt;/li&gt;&lt;/ul&gt; |
| `product_subcategory` | &lt;ul&gt;&lt;li&gt;List of Sub Categories&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Overrides `_ccat`&lt;/li&gt;&lt;/ul&gt; |
| `product_quantity` | &lt;ul&gt;&lt;li&gt;List of Quantities&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Overrides `_cquan`&lt;/li&gt;&lt;/ul&gt; |
| `product_unit_price` | &lt;ul&gt;&lt;li&gt;List of Prices&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Overrides `_cprice`&lt;/li&gt;&lt;/ul&gt; |   