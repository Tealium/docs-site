---
title: Amplitude Tag Setup (Deprecated)
description: This article describes how to set up the Amplitude tag in your Tealium iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/amplitude-tag/
---
This connector is now deprecated and no longer available in the tag marketplace. For the current connector, see the [Amplitude Browser SDK tag setup guide]().

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

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **API Key**  
The API or Project Key supplied by Amplitude.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`api_key`|  &lt;ul&gt;&lt;li&gt;The API or Project Key supplied by Amplitude.&lt;/li&gt;&lt;/ul&gt; |
|`batchEvents`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
|`cookieExpiration`|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;/ul&gt; |
|`cookieName`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;/ul&gt; |
|`deviceId`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;/ul&gt; |
|`deviceIdFromUrlParam`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
|`domain`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;/ul&gt; |
| `eventUploadPeriodMillis` |  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;/ul&gt; |
|`eventUploadThreshold`|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;/ul&gt; |
|`forceHttps`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
|`includeGclid`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
|`includeReferrer`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
| `includeUtm` |  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
|`language`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;/ul&gt; |
|`optOut`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
|`platform`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;/ul&gt; |
|`saveEvents`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
|`savedMaxCount`|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;/ul&gt; |
|`saveParamsReferrerOncePerSession`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
|`sessionTimeout`|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;/ul&gt; |
|`uploadBatchSize`|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;/ul&gt; |

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
| `order_id` |  &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_type`|  &lt;ul&gt;&lt;li&gt;Cart or Order Type&lt;/li&gt;&lt;li&gt;Overrides `_ctype`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt; &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices&lt;/li&gt;&lt;/ul&gt; &lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
