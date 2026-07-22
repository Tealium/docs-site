---
title: Epsilon Site Tag Setup Guide
description: This article describes how to set up the Epsilon Site Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/epsilon-universal-site-tag/
---
## Tag Configuration

Go to the tag marketplace and add the Epsilon Site Tag. For more information about adding a tag, see [manage-tags](https://docs.tealium.com/manage-tags/).

After adding the tag, configure the following settings:

* **Domain and Tag Path**: The domain used within the tag. Refer to the tagging document provided by Epsilon.
* **Reverse Proxy Directory Path**: If you are using a reverse proxy, enter its path (for example `/tag_path`, or the custom path you have set up as the root of your reverse proxy).
* **Company ID**: The company ID  `dtm_cid`.
* **Secondary Company ID**: `dtm_cmagic`.
* **Form ID**: `dtm_fid`.
* **Integration Type**: The available settings are `Default` or `Limited`. Limited integrations should only be used if specified by Epsilon.
* **SPA Support**: When enabled, the `dtm_clear_tag=all` query string parameter is included on all requests.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Tag Configuration

|Variable| Type | Description|
|---| ---|---|
| `tag_domain`| String| Domain.|
| `tag_path`| String| Reverse proxy directory path.|
| `dtm_cid`| String| Company ID.|
| `dtm_cmagic`| String| Secondary company ID.|
| `dtm_fid`| String| Form ID.|
| `integration_type`| Boolean| Integration type.|
| `spa_support`| Boolean| SPA support.|

### Standard

|Variable| Type | Description|
|---| ---|---|
| `dtm_promo_id`| String| Promo ID.|
|`dtmc_tcf_string`| String| GDPR consent string.|
|`dtm_email_hash`| String| Email hash.|
| `dtm_user_id`| String| User ID.|
| `custom.myvar`| String| Custom.|
| `dtm_cookie_id` | String | Send the Cookie ID as a query parameter. |

### Page Visit

|Variable| Type | Description|
|---| ---|---|
| `dtmc_department`| String| Department.|
| `dtmc_category`| String| Category.|
| `dtmc_sub_category`| String| Sub-Category.|
| `dtmc_product_id`| String| Product ID.|
| `dtmc_brand`| String| Manufacturer brand.|
| `dtmc_upc`| String| Manufacturer UPC.|
| `dtmc_mpn`| String| Manufacturer model part number.|

### Conversion

|Variable| Type | Description|
|---| ---|---|
| `dtmc_conv_type`| String| Conversion type.|
| `dtmc_conv_store_location`| String| Store location.|
| `dtmc_transaction_id` (Overrides `_corder`| String| Order ID.|
| `dtm_conv_val` (Overrides `_csubtotal`| String| Order subtotal.|
| `dtm_conv_curr` (Overrides `_ccurrency`| String|  Order currency.|
| `product_id` (Overrides `_cprod`| Array| Product IDs.|
| `product_quantity` (Overrides `_cquan`| Array| Product quantities.|
| `product_unit_price` (Overrides `_cprice`| Array| Product prices.|
| `product_discount` (Overrides `_cpdisc`| Array| Product discount amount.|
|`dtm_items.myvar`| Array| Custom items attributes.|
