---
title: Cheetah Digital Tag Setup Guide
description: This article describes how to set up the Cheetah Digital tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/cheetah-digital-tag/
---
## Tag tips

* Supports the following E-Commerce extension parameters:
  * Order ID
  * Order Subtotal
  * List of Product Names
  * List of Product Quantities
  * List of Product Prices
* Use mapping to:
  * Override the standard configuration values
  * Override the E-Commerce extension values
  * Pass additional data

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Tag Type**
* **Client Domain**  
The Client Domain is the same as the click-through domain for the client, such as `e.clientdomain.com`. If the client is using `clientname.chtah.com`, this should be `p.chtah.com`.
* **Affiliate ID**  
Affiliate ID used to send mailings to be tracked. For multiple affiliates in the same pixel, use a period to separate affiliates. Example: `123456789.987654321`. The number of affiliates should be small, between 2 and 3. The maximum is 10.
* **Client Name**  
(Required for Image tag type) Alphanumeric name, 10 characters or less, typically an abbreviation of the client name.
* **N Value**  
(Required for iFrame tag type) Value of `n` querystring parameter.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tagtype`|  &lt;ul&gt;&lt;li&gt;Tag Type&lt;/li&gt;&lt;li&gt;`img` or `iframe`&lt;/li&gt;&lt;/ul&gt; |
|`cdomain`|  &lt;ul&gt;&lt;li&gt;Client Domain&lt;/li&gt;&lt;/ul&gt; |
|`aid`|  &lt;ul&gt;&lt;li&gt;Affiliate ID&lt;/li&gt;&lt;/ul&gt; |
|`cname`|  &lt;ul&gt;&lt;li&gt;Client Name&lt;/li&gt;&lt;/ul&gt; |
|`nval`|  &lt;ul&gt;&lt;li&gt;N Value&lt;/li&gt;&lt;/ul&gt; |
|`custom.myvar`|  &lt;ul&gt;&lt;li&gt;Custom&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Sub Total&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Names&lt;/li&gt;&lt;li&gt;Overrides `_cprodname`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
