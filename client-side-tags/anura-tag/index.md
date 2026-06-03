---
title: Anura Tag Setup Guide Tag Management
description: This article describes how to set up the Anura tag in your Tealium iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/anura-tag/
---Anura is an ad fraud detection solution that analyzes your traffic to identify real users versus bots, malware, and fraudulent human users. This article describes how to configure the Anura marketplace tag for Tealium iQ Tag Management (TiQ).

The Anura tag places your basic Anura response, such as &#34;good&#34;, &#34;suspect&#34;, etc. Response Variable Name in your requested Response Location. If you are using Script Response the Response Object Variable Name will be available in the default Anura window object.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Title**
  * The default is Anura.
  * You may replace it with a custom name of choice.
  * Assign a unique name when using multiple tags by the same vendor.
* **Instance ID**
  * The Instance ID assigned by your account representative.
* **Source Tracking ID**
  * A variable that you declare to identify traffic within the Anura interface.
* **Campaign Tracking ID**
  * A subset variable of the Source Tracking ID that you declare to help identify traffic within the Anura interface.
* **Response Object Variable Name**
  * The variable name of the JavaScript object that initial response data will be assigned to.
* **Result Method**
  * The method used to query for results.
  * Options are Script Response or Direct Response.
* **Response Location**  
  * The location to put the results in.
  * Options are Window Variable, Session Storage, or Local Storage.
* **Response Variable Name**
  * The name of the Response Location variable in which to place the final Anura response.

## Load rules

[Load Rules]() determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **Load on All Pages**

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the Anura tag are built into its Data Mapping tab. Available categories are:

### Standard

|Tag Destination| Description| Variable|
|---| ---| ---|
|Instance|  &lt;ul&gt;&lt;li&gt;(Required) Your instance ID.&lt;/li&gt;&lt;/ul&gt; | `instance`|
|Source Tracking ID|  &lt;ul&gt;&lt;li&gt;(Optional) A variable, declared by you, to identify source traffic within the Anura dashboard.&lt;/li&gt;&lt;li&gt;Maximum of 128 characters.&lt;/li&gt;&lt;li&gt;May not equal the following values: &#34;all sources&#34;, &#34;all campaigns&#34;, &#34;&amp;&#34;, &#34;\*&#34;, &#34;?&#34;, &#34;%&#34;.&lt;/li&gt;&lt;li&gt;Allowed to start with: &#34;$&#34;, &#34;\_&#34;, or &#34;a-z&#34; characters, followed by &#34;a-z&#34; and &#34;0-9&#34; characters.&lt;/li&gt;&lt;/ul&gt; | `source`|
|Campaign Tracking ID|  &lt;ul&gt;&lt;li&gt;(Optional) A subset of the source variable, declared by you, to identify campaign traffic within the Anura dashboard.&lt;/li&gt;&lt;li&gt;Maximum of 128 characters.&lt;/li&gt;&lt;li&gt;May not equal the following values: &#34;all sources&#34;, &#34;all campaigns&#34;, &#34;&amp;&#34;, &#34;\*&#34;, &#34;?&#34;, &#34;%&#34;.&lt;/li&gt;&lt;/ul&gt; | `campaign`|
|Unique External ID|  &lt;ul&gt;&lt;li&gt;(Optional) A unique external tracking ID, declared by you, that is used to query the result from Anura servers.&lt;/li&gt;&lt;li&gt;Maximum of 128 characters.&lt;/li&gt;&lt;/ul&gt; | `exid`|
|Response Object Variable Name|  &lt;ul&gt;&lt;li&gt;(Optional) The variable name of the JavaScript object that response data will be assigned to.&lt;/li&gt;&lt;li&gt;This variable contains the response ID, in addition to other data, that lets you make real-time decisions.&lt;/li&gt;&lt;li&gt;Maximum of 128 characters.&lt;/li&gt;&lt;/ul&gt; | `variable`|
|Result Method|  &lt;ul&gt;&lt;li&gt;(Optional) The result method.&lt;/li&gt;&lt;/ul&gt; | `result_method`|
|Result Location|  &lt;ul&gt;&lt;li&gt;(Optional) The result location.&lt;/li&gt;&lt;/ul&gt; | `result_location`|
|Response Variable Name|  &lt;ul&gt;&lt;li&gt;(Optional) The Response Variable Name.&lt;/li&gt;&lt;/ul&gt; | `response_variable`|
|Visitor IP Address|  &lt;ul&gt;&lt;li&gt;(Required) The IP address of your visitor.&lt;/li&gt;&lt;li&gt;IPv6 addresses are also supported.&lt;/li&gt;&lt;/ul&gt; | `ip`|
|Visitor User Agent|  &lt;ul&gt;&lt;li&gt;(Optional) The user agent string of your visitor.&lt;/li&gt;&lt;/ul&gt; | `ua`|

### E-Commerce

Since the Anura tag is e-commerce enabled, it will automatically use the default [E-Commerce extension]() mappings. Manually mapping in this category is generally not needed unless you want to override extension mappings or an e-commerce variable is not offered in the extension.

|Destination| Description| E-Commerce Extension Variable|
|---| ---| ---|
|Order ID|  Unique identifier assigned to the final order. | `_corder`|
|Sub Total|  Sub total amount of the final order. | `_csubtotal`|
|Currency|  Currency used in the payment. | `_ccurrency`|
|List of Product IDs|  Unique identifier of each product in the product array. | `_cprod`|
|List of Product Names|  Name of each product in the product array. | `_cprodname`|
|List of Brand|  Brand of each product in the product array. | `_cbrand`|
|List of Categories|  Name of each product in the product array. | `_ccat`|
|List of Quantities|  Quantity of each product in the product array. | `_cquan`|
|List of Prices|  Unit price of each product in the product array. | `_cprice`|
|e-comm destination name| Insert description.| N/A|

## Vendor Documentation

* [Anura Docs](https://docs.anura.io/)
