---
title: Webtrekk Tag Setup Guide
description: This article describes how to set up the Webtrekk tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/webtrekk-tag/
---## Requirements

* Webtrekk account

## Supported versions

* v5.5.1 (Recommended)
* v4.4.7
* v4.4.4

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Title**
  * The default is "Webtrekk".
  * You may replace it with a descriptive name of choice.
* **Library Version**
  * Choose the version of your Webtrekk pixel from this list. For example: tracking script.
* **Track ID**
  * Enter the numeric track ID you received from Webtrekk.
  * Track ID can be located in the Webtrekk tool, under **System Configuration &gt; Data Collection**.
* **Track Domain**
  * Enter the tracking URL (excluding the https/http protocol), as specified in your Webtrekk pixel, such as `track.XXXX.net`
* **TagIntegration Customer ID**
  * Enter your SafeTag identifier.
  * This is defined in the `safetag` object and required if you are loading the TagIntegration file from a Webtrekk server.
* **TagIntegration Domain**
  * Enter the SafeTag domain.
  * Required if you are loading the TagIntegration file from a Webtrekk server.
* **Param First**
  * Enter the list of parameters in the order you want them passed in the request.
  * Separate the parameters with semi-colon (**;**).
* **Site Domain**
  * (Optional) Enter the domain of the site being tracked.
* **Link Tracking**
  * Select one of the following preferred settings for tracking visitor actions/events, clicks, downloads, etc.   
    * **Link** (default)
      * Sends the value of `href` attribute, such as the destination page URL in the clicked link, as the action/event name.
      * For example, if the clicked link is `<a href="example.htm">Click here</a>`, the value `example.htm` is passed.
    * **Standard**
      * Sends the value of the `name` attribute as the action/event name.
      * For example, if the clicked link is `<a href="example.htm" name="example_name">Click here</a>`, the value `example_name `is passed.
    * **None**
      * Disables link/event tracking for the tag instance.
* **Link Track Attribute**
  * Optional configuration for **Standard** tracking option.
  * Enter the HTML attribute that you want to use instead of the default `name` attribute for assigning the action/event name.
  * For example, in this link `<a href="example.htm" name="internal_id" rel="example">Click here</a>`, you may use `rel` instead of `name`.
* **Link Track Params**
  * (Optional) Configuration for **Link** tracking option.
  * Enter the name of the querystring parameter with which to track the clicked link.
  * Use commas to separate multiple parameters.
  * For example: `<a href="example.htm?page=10">Go to page 10</a>`
* **Link Track Downloads**
  * Enter the list of file types you want to track for downloads.
  * Use semi-colons to separate multiple entries.
  * For example: `zip;raw;doc`
* **Pixel Sampling**:
  * Lets you control the percentage of traffic that is reported to Webtrekk.
  * Enter a numeric value.
* **Force HTTPS**:
  * Choose whether or not to force send a request as secure.
  * Default setting is OFF.
* **Cookie Handling**
  * Choose the type of cookie you prefer to use for tracking visitors on your site.  
    * First party
      * Default
      * Recommended)
      * Cookie value set by your site domain
    * Third party
      * Cookie value set by Webtrekk.
* **Cookie Domain**
  * Applies to first party cookies only.
  * If your top level domain is double-barrelled (suffixed by an additional identifier such as `.co`, `.uk`, etc.), you must specify it here in order for the cookies to be set correctly.
* **mediaCode**
  * Enter the media code parameter with which to identify and track your campaign.
* **mediaCodeCookie**
  * Enter the media code cookie parameter with which to track a campaign only once per session.
  * If the `mediaCode` query parameter is in the address bar, set the value to `sid`.
* **WT Object Name**
  * Pre-populated by `wt `which is the default object for a single tag instance.
  * If you are loading multiple tag instances on the same page, replace with a unique object name in each of those tags.
* **Heat Map tracking**
  * Choose whether or not you want to activate Heatmap tracking for this tag instance.
  * Default setting is OFF.
* **Form tracking**
  * Choose whether or not you want to activate Form tracking for this tag instance.
  * Default setting is OFF.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

Recommended Rule: All Pages (default)

## Data mappings

Mapping is the process of sending data from a [Data Layer Variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a Variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

### Standard Category

Map to these destinations to either override or dynamically populate the tag settings.


<blockquote>
These mappings apply to your global `Webtrekk.js` configuration.
</blockquote>


|Tag Destination| Description|
|---| ---|
|WT object name|  <ul><li>Object name for uniquely identifying the tag instance.</li><li>Default value is `wt`.</li></ul> |
|Cookie OptOut Name|  <ul><li>Name of the `webtrekkOptOut` cookie</li></ul> |
|Cookie OptOut Time Frame|  <ul><li>Lifespan of the `webtrekkoptout` cookie</li></ul> |
|Parameters to Include First|  <ul><li>List of parameters separated by semi-colon.</li><li>Parameters are sent in the order listed in the variable.</li></ul> |
|Ignore Pre-rendering|  <ul><li>Flag (Boolean value) to determine whether or not to track pre-rendered pages</li></ul> |
|Form Path Analysis|  <ul><li>Flag (Boolean value) to enable or disable form field tracking </li></ul> |
|tabBrowsing|  <ul><li>Flag (Boolean value) for tracking browser tab views.</li><li>Default value is false </li></ul> |
|globalVisitorIds|
|execRTA|  <ul><li>Flag (Boolean value) for enabling or disabling Webtrekk’s Real Time Bidding (RTB) service</li></ul> |
|execCDB|  <ul><li>Flag (Boolean value) for enabling or disabling Webtrekk’s Cross Device Bridge (CDB) technology</li></ul> |
|useCDBCache|  <ul><li>Flag (Boolean value) for enabling or disabling the use of image cache cookie</li></ul> |
|useCDBScript|
|requestLimitAmount|  <ul><li>The maximum number of requests that can be sent</li></ul> |
|requestLimitTime|  <ul><li>The permissible time limit for sending the maximum number of requests </li></ul> |
|Track ID|  <ul><li>Numeric identifier of the tracking pixel you received from Webtrekk.</li><li>Track ID can also be found in the Webtrekk tool, under **System Configuration &gt; Data Collection**.</li></ul> |
|Track Domain|  <ul><li>Tracking URL, excluding https/http protocol), as specified in your Webtrekk pixel.</li></ul> |
|Site Domain|  <ul><li>Domain of the site being tracked.</li></ul> |
|Link Tracking|  <ul><li>Event tracking settings for tracking visitor actions, clicks, and downloads.</li><li>Webtrekk supports two options: Link and Standard.</li></ul> |
|Link Track Attribute|  <ul><li>Applies to "Standard" tracking option.</li><li>This attribute is used for determining the name of the event/action.</li><li>Mapping to this destination overrides the default "name".</li></ul> |
|Link Track Params|  <ul><li>Applies to "Link" tracking option in the global configuration.</li><li>Mapping to this destination sends the query string parameter with which to track the clicked link.</li></ul> |
|Link Track Pattern|  <ul><li>Regular Expression for filtering undesirable parameter(s) out of the Link Track Parameter query string.</li></ul> |
|Link Track Replace|  <ul><li>Replacement character with which to replace the filtered parameters in the Link Track Parameter.</li></ul> |
|Link Track Ignore Pattern|  <ul><li>Regular Expression to exclude individual links from being tracked</li></ul> |
|No Delay Link Track Attribute|  <ul><li>Disables delaying of links that are explicitly tagged with this parameter</li></ul> |
|Link Track Downloads|  <ul><li>List of file types that you want to track for downloads in the global configuration.</li><li>For example: `zip;raw;doc`</li></ul> |
|Pixel Sampling|  <ul><li>Percentage of traffic reported to Webtrekk.</li></ul> |
|Force HTTPS|  <ul><li>Force send a request as secure.</li><li>Data source must contain the value `1` for activation and  for deactivation.</li></ul> |
|Cookie Handling|  <ul><li>Either first or third party cookie for tracking visitors on your site.</li><li>First party is default and recommended.</li></ul> |
|Cookie Domain|  <ul><li>Applies to `firstparty` cookies only.</li><li>Map to this destination if your top level domain is double barrelled. For example, it is suffixed by an additional identifier such as `.co`, `.uk`, etc.</li></ul> |
|contentId|  <ul><li>Identifies a page by its unique name rather than its URL.</li></ul> |
|Heat map|  <ul><li>Activate/deactivate Heatmap in the global configuration.</li><li>Data source value must equal `1` for activation and  for deactivation.</li></ul> |
|Form|  <ul><li>Activate/deactivate Form tracking in the global configuration.</li><li>Data source value must equal `1` for activation and  for deactivation.</li></ul> |
|executePluginFuntion|  <ul><li>List of Plugin functions</li></ul> |
|Media Code|  <ul><li>Parameter for tracking campaigns.</li></ul> |
|Media Code cookie|  <ul><li>Parameter for tracking a campaign ONLY once per session.</li></ul> |
|SafeTag Async|  <ul><li>Flag (Boolean value) to determine whether or not to load the tag asynchronously</li></ul> |
|SafeTag Timeout|  <ul><li>The maximum amount of time to wait for the TagIntegration file to load. </li></ul> |
|SafeTag Domain|  <ul><li>TagIntegration domain</li></ul> |
|SafeTag Customer ID|  <ul><li>TagIntegration customer identifier</li></ul> |
|SafeTag Custom Domain|  <ul><li>Custom domain from where the TagIntegration file should load</li></ul> |
|SafeTag CustomPath|  <ul><li>Path of the JavaScript file, for custom domain</li></ul> |
|SafeTag Option [Object]|  <ul><li>Additional TagIntegration information</li></ul> |
|SafeTag Option|
|Custom wt config item|

### General Category

Map to these destinations for reporting custom/optional parameters such as Visitor IDs, Session, and Categories.

|Tag Destination| Description|
|---| ---|
|Custom Visitor ID|  <ul><li>Map to this destination for sending unique visitor identifier.</li></ul> |
|URM categories|  <ul><li>URM Categories in your Webtrekk tool</li></ul> |
|Email RID|  <ul><li>Email recipient ID</li></ul> |
|Email Opt-In|  <ul><li>Email Opt In status.</li><li>Possible values:  <ul><li>`1` (yes)</li><li>`2` (no)</li><li>`3` (unknown)</li></ul> </li></ul> |
|Gender|  <ul><li>Gender</li><li>Possible values:  <ul><li>`1` (male)</li><li>`2` (female)</li><li>`3` (unknown) </li></ul> </li></ul> |
|Birthday|  <ul><li>Date of birth (`YYYYMMDD`)</li></ul> |
|Birthday Year|  <ul><li>Year of birth (`YYYY`)</li></ul> |
|Birthday Month|  <ul><li>Month of birth (`MM`)</li></ul> |
|Birthday Day|  <ul><li>Date of birthday (`DD`)</li></ul> |
|CRM Category 1 to 10|  <ul><li>Custom categories for sending CRM information such as membership type, age, and gender.</li><li>Before mapping, make sure the category is defined in your Webtrekk tool.</li></ul> |
|Custom Session Parameter 1 to 10|  <ul><li>Custom parameters for sending additional visit/session information such as login status, registration status, and test group for A/B testing.</li><li>Before mapping, make sure the session parameter is defined in your Webtrekk tool.</li></ul> |

### Page Data Category

|Tag Destination| Description|
|---| ---|
|Page Content ID|  <ul><li>Identifies a page by its unique name rather than its URL and is set in the page-specific configuration.</li></ul> |
|Content Group 1 to 25|  <ul><li>Map to these destinations to send up to 50 custom parameters for a page.</li><li>Make sure the Content Group you are mapping to is also defined in your Webtrekk tool.</li></ul> |
|Custom Parameter 1 to 50|  <ul><li>Map to these destinations to send up to 50 custom parameters for a page.</li></ul> |

### Search and Form Tracking

Map to these destinations for sending internal search and form input parameters.

|Tag Destination| Description|
|---| ---|
|Internal Search|  <ul><li>Search keywords/terms used by visitors to look up your site</li></ul> |
|Form Tracking|  <ul><li>Activate/deactivate Form tracking in the page-specific configuration</li><li>Data source must contain the value `1` for activation and  for deactivation.</li></ul> |
|Form Attribute|  <ul><li>This attribute is used for determining the name of the form.</li><li>Mapping to this destination overrides the default "name" attribute.</li></ul> |
|Form Value Attribute|  <ul><li>This attribute is used for determining the name of the form when the form field is a 'radio' or a 'checkbox'.</li><li>Mapping to this destination overrides the default `value` attribute.</li></ul> |
|Form Field Attribute| ---|
|Full Content Form Tracking| Sends the first 30 characters of a free-text field.|
|Anonymous Form Tracking|  <ul><li>Contents of the form will not be sent to Webtrekk.</li><li>Mapping to this destination makes the form data anonymous.</li></ul> |
|Form HTML Id|  <ul><li>Method from tracking forms reloaded by Ajax.</li><li>Mapping to this destination invokes the method</li></ul> |

### Click Tracking

|Tag Destination| Description|
|---| ---|
|Heatmap|  <ul><li>Activate/deactivate Heatmap in the page-specific configuration.</li><li>Data source value must equal `1` for activation and  for deactivation.</li></ul> |
|Heatmap reference point id|  <ul><li>ID of the element being used as a point of reference for Heatmaps.</li></ul> |
|Link Track|  <ul><li>Event tracking settings in the page-specific configuration.</li><li>Webtrekk supports 'Link' and 'Standard' settings.</li></ul> |
|Link Track Attribute|  <ul><li>Applies to "Standard" tracking option in the page-specific configuration.</li><li>This attribute is used for determining the name of the event/action.</li><li>Mapping to this destination overrides the default "name".</li></ul> |
|Link Tracks Params|  <ul><li>Applies to "Link" tracking option in the page-specific configuration.</li><li>Mapping to this destination sends the query string parameter of the tracked link.</li></ul> |
|Link Track Pattern|  <ul><li>Regular Expression for filtering undesirable parameter(s) out of the Link Track Parameter query string.</li><li>Applies to page-specific configuration.</li></ul> |
|Link Track Replace|  <ul><li>Replacement character for replacing the filtered parameters in the Link Track Parameter.</li><li>Applies to page-specific configuration.</li></ul> |
|Link Track Downloads|  <ul><li>List of file types that you want to track for downloads.</li><li>Applies to page-specific configuration.</li><li>Example: `zip;raw;doc`</li></ul> |
|Link ID for custom utag.link tracking|  <ul><li>Name of the tracked link.</li></ul> |
|Custom Click parameter 1 to 10|  <ul><li>Custom parameters for click tracking.</li><li>The Link ID value must be mapped in order for your custom click parameter(s) to be sent.</li><li>Before mapping, make sure the parameter is also defined in your Webtrekk tool.</li></ul> |

### Campaign Tracking

Map to these destinations for sending optional and custom campaign parameters


<blockquote>
These mappings apply to page-specific configurations.
</blockquote>


|Tag Destination| Description|
|---| ---|
|Media Code|  <ul><li>Parameter for tracking campaigns.</li></ul> |
|Media Code Cookie|  <ul><li>Parameter for tracking a campaign ONLY once per session.</li></ul> |
|Campaign ID|  <ul><li>Media code parameter followed by `%3D` and the parameter value</li></ul> |
|Campaign Action|  <ul><li>Determines whether the visitor's response to a campaign was 'view' or 'click'.</li></ul> |
|Custom Campaign Parameters 1 to 10|  <ul><li>Custom parameters for campaign tracking.</li><li>Before mapping, make sure the parameter is defined in your Webtrekk tool.</li></ul> |

### E-Commerce Category

Since the Webtrekk tag is e-commerce enabled, it will automatically use the default [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) mappings. Manually mapping in this category is generally not needed unless:

* you want to override any Extension mappings
* an e-commerce variable you want is not offered in the extension

|Tag Destination| Description| E-Commerce Extension Mappings |
|---| ---| ---|
|Order ID|  <ul><li>Unique identifier of the final order</li></ul> | `_corder`|
|Order Total|  <ul><li>Total amount after shipping and tax.</li></ul> | `_ctotal`|
|Currency|  <ul><li>Currency used by the customer to make the payment</li></ul> | `_ccurrency`|
|Coupon Value|  <ul><li>The value of the coupon used in the order</li></ul> | N//A|
|List of product names|  <ul><li>Name of each product in the product array</li></ul> | `_cprodname`|
|List of product quantities|  <ul><li>Quantity of each product in the product array</li></ul> | `_cquan`|
|List of product prices|  <ul><li>Unit price of each product in the product array</li></ul> | `_cprice`|
|List of product categories (productCategories[1])|  <ul><li>Category of each product in the product array</li></ul> | `_ccat`|
|List of product brands (productCategory[2])|  <ul><li>Brand of each product in the product array</li></ul> | `_cbrand`|
|List of product subcategories (productCategory[3])|  <ul><li>Sub-category of each product in the product array</li></ul> | `_ccat2`|
|Product Status|  <ul><li>Indicates if the product was viewed, added to cart, or checked out from the cart.</li></ul> | N/A|
|Product Category 1 to 25|  <ul><li>Custom category with which a product can be associated only once.</li><li>You may map up to 25 unique categories.</li><li>Before mapping, make sure the product category is defined in your Webtrekk tool.</li></ul> | N/A|
|Custom E-Commerce Parameter 1 to 50|  <ul><li>Custom parameters for sending additional product- and order-level data.</li><li>You may map up to 50 unique parameters.</li><li>Before mapping, make sure the parameter(s) is defined in your Webtrekk tool.</li></ul> | N/A|
