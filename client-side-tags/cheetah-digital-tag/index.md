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

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

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

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tagtype`|  <ul><li>Tag Type</li><li>`img` or `iframe`</li></ul> |
|`cdomain`|  <ul><li>Client Domain</li></ul> |
|`aid`|  <ul><li>Affiliate ID</li></ul> |
|`cname`|  <ul><li>Client Name</li></ul> |
|`nval`|  <ul><li>N Value</li></ul> |
|`custom.myvar`|  <ul><li>Custom</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID</li><li>Overrides `_corder`.</li></ul> |
|`order_subtotal`|  <ul><li>Sub Total</li><li>Overrides `_csubtotal`.</li></ul> |
|`product_name`|  <ul><li>Array</li><li>List of Names</li><li>Overrides `_cprodname`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices</li><li>Overrides `_cprice`.</li></ul> |
