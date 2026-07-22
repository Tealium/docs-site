---
title: Amplitude Tag Setup (Deprecated)
description: This article describes how to set up the Amplitude tag in your Tealium iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/amplitude-tag/
---

<blockquote>
This connector is now deprecated and no longer available in the tag marketplace. For the current connector, see the [Amplitude Browser SDK tag setup guide](https://docs.tealium.com/amplitude-browser-sdk-tag/).
</blockquote>


## Tag tips

* Conversion fires when Order ID is set.
* Supports the following E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Cart or Order Type (`_ctype`)
  * Customer ID (`_ccustid`)
  * List of Product IDs ( `_cprod`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **API Key**  
The API or Project Key supplied by Amplitude.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`api_key`|  <ul><li>The API or Project Key supplied by Amplitude.</li></ul> |
|`batchEvents`|  <ul><li>Boolean</li></ul> |
|`cookieExpiration`|  <ul><li>Number</li></ul> |
|`cookieName`|  <ul><li>String</li></ul> |
|`deviceId`|  <ul><li>String</li></ul> |
|`deviceIdFromUrlParam`|  <ul><li>Boolean</li></ul> |
|`domain`|  <ul><li>String</li></ul> |
| `eventUploadPeriodMillis` |  <ul><li>Number</li></ul> |
|`eventUploadThreshold`|  <ul><li>Number</li></ul> |
|`forceHttps`|  <ul><li>Boolean</li></ul> |
|`includeGclid`|  <ul><li>Boolean</li></ul> |
|`includeReferrer`|  <ul><li>Boolean</li></ul> |
| `includeUtm` |  <ul><li>Boolean</li></ul> |
|`language`|  <ul><li>String</li></ul> |
|`optOut`|  <ul><li>Boolean</li></ul> |
|`platform`|  <ul><li>String</li></ul> |
|`saveEvents`|  <ul><li>Boolean</li></ul> |
|`savedMaxCount`|  <ul><li>Number</li></ul> |
|`saveParamsReferrerOncePerSession`|  <ul><li>Boolean</li></ul> |
|`sessionTimeout`|  <ul><li>Number</li></ul> |
|`uploadBatchSize`|  <ul><li>Number</li></ul> |

### User Properties

Use these mappings to control user property operations that set and update user property values, such as location, language, account type, or player type.

Change `custom` to the name of the user property. For example, to map a user language create a mapping for `set.language`.

Learn more about [Amplitude User Properties](http://Set%20the value, and once set these values cannot be overwritten).

|Variable| Description|
|---| ---|
|add.custom| Increment the numerical value by a specified number|
|append.custom| Append the value to the property array|
|prepend.custom| Prepend the value to the property array|
|set.custom| Set or overwrite the property value|
|setOnce.custom| Set the value, and once set these values cannot be overwritten|
|unset.custom| Unset the value to null|

### Events

|Variable| Description|
|---| ---|
|Event Name|
|eventProperties.custom|

### E-Commerce

|Variable| Description|
|---| ---|
| `order_id` |  <ul><li>Order ID</li><li>Overrides `_corder`.</li></ul> |
|`order_type`|  <ul><li>Cart or Order Type</li><li>Overrides `_ctype`.</li></ul> |
|`customer_id`|  <ul><li>Customer ID</li><li>Overrides `_ccustid`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs</li><li>Overrides `_cprod`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul> <ul><li>Array</li><li>List of Prices</li></ul> </ul> <ul><li>Overrides `_cprice`.</li></ul> |
