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

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Title**
  * The default is &#34;Webtrekk&#34;.
  * You may replace it with a descriptive name of choice.
* **Library Version**
  * Choose the version of your Webtrekk pixel from this list. For example: tracking script.
* **Track ID**
  * Enter the numeric track ID you received from Webtrekk.
  * Track ID can be located in the Webtrekk tool, under **System Configuration &amp;gt; Data Collection**.
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
      * For example, if the clicked link is `&lt;a href=&#34;example.htm&#34;&gt;Click here&lt;/a&gt;`, the value `example.htm` is passed.
    * **Standard**
      * Sends the value of the `name` attribute as the action/event name.
      * For example, if the clicked link is `&lt;a href=&#34;example.htm&#34; name=&#34;example_name&#34;&gt;Click here&lt;/a&gt;`, the value `example_name `is passed.
    * **None**
      * Disables link/event tracking for the tag instance.
* **Link Track Attribute**
  * Optional configuration for **Standard** tracking option.
  * Enter the HTML attribute that you want to use instead of the default `name` attribute for assigning the action/event name.
  * For example, in this link `&lt;a href=&#34;example.htm&#34; name=&#34;internal_id&#34; rel=&#34;example&#34;&gt;Click here&lt;/a&gt;`, you may use `rel` instead of `name`.
* **Link Track Params**
  * (Optional) Configuration for **Link** tracking option.
  * Enter the name of the querystring parameter with which to track the clicked link.
  * Use commas to separate multiple parameters.
  * For example: `&lt;a href=&#34;example.htm?page=10&#34;&gt;Go to page 10&lt;/a&gt;`
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

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

Recommended Rule: All Pages (default)

## Data mappings

Mapping is the process of sending data from a [Data Layer Variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a Variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

### Standard Category

Map to these destinations to either override or dynamically populate the tag settings.

These mappings apply to your global `Webtrekk.js` configuration.

|Tag Destination| Description|
|---| ---|
|WT object name|  &lt;ul&gt;&lt;li&gt;Object name for uniquely identifying the tag instance.&lt;/li&gt;&lt;li&gt;Default value is `wt`.&lt;/li&gt;&lt;/ul&gt; |
|Cookie OptOut Name|  &lt;ul&gt;&lt;li&gt;Name of the `webtrekkOptOut` cookie&lt;/li&gt;&lt;/ul&gt; |
|Cookie OptOut Time Frame|  &lt;ul&gt;&lt;li&gt;Lifespan of the `webtrekkoptout` cookie&lt;/li&gt;&lt;/ul&gt; |
|Parameters to Include First|  &lt;ul&gt;&lt;li&gt;List of parameters separated by semi-colon.&lt;/li&gt;&lt;li&gt;Parameters are sent in the order listed in the variable.&lt;/li&gt;&lt;/ul&gt; |
|Ignore Pre-rendering|  &lt;ul&gt;&lt;li&gt;Flag (Boolean value) to determine whether or not to track pre-rendered pages&lt;/li&gt;&lt;/ul&gt; |
|Form Path Analysis|  &lt;ul&gt;&lt;li&gt;Flag (Boolean value) to enable or disable form field tracking &lt;/li&gt;&lt;/ul&gt; |
|tabBrowsing|  &lt;ul&gt;&lt;li&gt;Flag (Boolean value) for tracking browser tab views.&lt;/li&gt;&lt;li&gt;Default value is false &lt;/li&gt;&lt;/ul&gt; |
|globalVisitorIds|
|execRTA|  &lt;ul&gt;&lt;li&gt;Flag (Boolean value) for enabling or disabling Webtrekk’s Real Time Bidding (RTB) service&lt;/li&gt;&lt;/ul&gt; |
|execCDB|  &lt;ul&gt;&lt;li&gt;Flag (Boolean value) for enabling or disabling Webtrekk’s Cross Device Bridge (CDB) technology&lt;/li&gt;&lt;/ul&gt; |
|useCDBCache|  &lt;ul&gt;&lt;li&gt;Flag (Boolean value) for enabling or disabling the use of image cache cookie&lt;/li&gt;&lt;/ul&gt; |
|useCDBScript|
|requestLimitAmount|  &lt;ul&gt;&lt;li&gt;The maximum number of requests that can be sent&lt;/li&gt;&lt;/ul&gt; |
|requestLimitTime|  &lt;ul&gt;&lt;li&gt;The permissible time limit for sending the maximum number of requests &lt;/li&gt;&lt;/ul&gt; |
|Track ID|  &lt;ul&gt;&lt;li&gt;Numeric identifier of the tracking pixel you received from Webtrekk.&lt;/li&gt;&lt;li&gt;Track ID can also be found in the Webtrekk tool, under **System Configuration &amp;gt; Data Collection**.&lt;/li&gt;&lt;/ul&gt; |
|Track Domain|  &lt;ul&gt;&lt;li&gt;Tracking URL, excluding https/http protocol), as specified in your Webtrekk pixel.&lt;/li&gt;&lt;/ul&gt; |
|Site Domain|  &lt;ul&gt;&lt;li&gt;Domain of the site being tracked.&lt;/li&gt;&lt;/ul&gt; |
|Link Tracking|  &lt;ul&gt;&lt;li&gt;Event tracking settings for tracking visitor actions, clicks, and downloads.&lt;/li&gt;&lt;li&gt;Webtrekk supports two options: Link and Standard.&lt;/li&gt;&lt;/ul&gt; |
|Link Track Attribute|  &lt;ul&gt;&lt;li&gt;Applies to &#34;Standard&#34; tracking option.&lt;/li&gt;&lt;li&gt;This attribute is used for determining the name of the event/action.&lt;/li&gt;&lt;li&gt;Mapping to this destination overrides the default &#34;name&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Link Track Params|  &lt;ul&gt;&lt;li&gt;Applies to &#34;Link&#34; tracking option in the global configuration.&lt;/li&gt;&lt;li&gt;Mapping to this destination sends the query string parameter with which to track the clicked link.&lt;/li&gt;&lt;/ul&gt; |
|Link Track Pattern|  &lt;ul&gt;&lt;li&gt;Regular Expression for filtering undesirable parameter(s) out of the Link Track Parameter query string.&lt;/li&gt;&lt;/ul&gt; |
|Link Track Replace|  &lt;ul&gt;&lt;li&gt;Replacement character with which to replace the filtered parameters in the Link Track Parameter.&lt;/li&gt;&lt;/ul&gt; |
|Link Track Ignore Pattern|  &lt;ul&gt;&lt;li&gt;Regular Expression to exclude individual links from being tracked&lt;/li&gt;&lt;/ul&gt; |
|No Delay Link Track Attribute|  &lt;ul&gt;&lt;li&gt;Disables delaying of links that are explicitly tagged with this parameter&lt;/li&gt;&lt;/ul&gt; |
|Link Track Downloads|  &lt;ul&gt;&lt;li&gt;List of file types that you want to track for downloads in the global configuration.&lt;/li&gt;&lt;li&gt;For example: `zip;raw;doc`&lt;/li&gt;&lt;/ul&gt; |
|Pixel Sampling|  &lt;ul&gt;&lt;li&gt;Percentage of traffic reported to Webtrekk.&lt;/li&gt;&lt;/ul&gt; |
|Force HTTPS|  &lt;ul&gt;&lt;li&gt;Force send a request as secure.&lt;/li&gt;&lt;li&gt;Data source must contain the value `1` for activation and  for deactivation.&lt;/li&gt;&lt;/ul&gt; |
|Cookie Handling|  &lt;ul&gt;&lt;li&gt;Either first or third party cookie for tracking visitors on your site.&lt;/li&gt;&lt;li&gt;First party is default and recommended.&lt;/li&gt;&lt;/ul&gt; |
|Cookie Domain|  &lt;ul&gt;&lt;li&gt;Applies to `firstparty` cookies only.&lt;/li&gt;&lt;li&gt;Map to this destination if your top level domain is double barrelled. For example, it is suffixed by an additional identifier such as `.co`, `.uk`, etc.&lt;/li&gt;&lt;/ul&gt; |
|contentId|  &lt;ul&gt;&lt;li&gt;Identifies a page by its unique name rather than its URL.&lt;/li&gt;&lt;/ul&gt; |
|Heat map|  &lt;ul&gt;&lt;li&gt;Activate/deactivate Heatmap in the global configuration.&lt;/li&gt;&lt;li&gt;Data source value must equal `1` for activation and  for deactivation.&lt;/li&gt;&lt;/ul&gt; |
|Form|  &lt;ul&gt;&lt;li&gt;Activate/deactivate Form tracking in the global configuration.&lt;/li&gt;&lt;li&gt;Data source value must equal `1` for activation and  for deactivation.&lt;/li&gt;&lt;/ul&gt; |
|executePluginFuntion|  &lt;ul&gt;&lt;li&gt;List of Plugin functions&lt;/li&gt;&lt;/ul&gt; |
|Media Code|  &lt;ul&gt;&lt;li&gt;Parameter for tracking campaigns.&lt;/li&gt;&lt;/ul&gt; |
|Media Code cookie|  &lt;ul&gt;&lt;li&gt;Parameter for tracking a campaign ONLY once per session.&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Async|  &lt;ul&gt;&lt;li&gt;Flag (Boolean value) to determine whether or not to load the tag asynchronously&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Timeout|  &lt;ul&gt;&lt;li&gt;The maximum amount of time to wait for the TagIntegration file to load. &lt;/li&gt;&lt;/ul&gt; |
|SafeTag Domain|  &lt;ul&gt;&lt;li&gt;TagIntegration domain&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Customer ID|  &lt;ul&gt;&lt;li&gt;TagIntegration customer identifier&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Custom Domain|  &lt;ul&gt;&lt;li&gt;Custom domain from where the TagIntegration file should load&lt;/li&gt;&lt;/ul&gt; |
|SafeTag CustomPath|  &lt;ul&gt;&lt;li&gt;Path of the JavaScript file, for custom domain&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Option [Object]|  &lt;ul&gt;&lt;li&gt;Additional TagIntegration information&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Option|
|Custom wt config item|

### General Category

Map to these destinations for reporting custom/optional parameters such as Visitor IDs, Session, and Categories.

|Tag Destination| Description|
|---| ---|
|Custom Visitor ID|  &lt;ul&gt;&lt;li&gt;Map to this destination for sending unique visitor identifier.&lt;/li&gt;&lt;/ul&gt; |
|URM categories|  &lt;ul&gt;&lt;li&gt;URM Categories in your Webtrekk tool&lt;/li&gt;&lt;/ul&gt; |
|Email RID|  &lt;ul&gt;&lt;li&gt;Email recipient ID&lt;/li&gt;&lt;/ul&gt; |
|Email Opt-In|  &lt;ul&gt;&lt;li&gt;Email Opt In status.&lt;/li&gt;&lt;li&gt;Possible values:  &lt;ul&gt;&lt;li&gt;`1` (yes)&lt;/li&gt;&lt;li&gt;`2` (no)&lt;/li&gt;&lt;li&gt;`3` (unknown)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Gender|  &lt;ul&gt;&lt;li&gt;Gender&lt;/li&gt;&lt;li&gt;Possible values:  &lt;ul&gt;&lt;li&gt;`1` (male)&lt;/li&gt;&lt;li&gt;`2` (female)&lt;/li&gt;&lt;li&gt;`3` (unknown) &lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Birthday|  &lt;ul&gt;&lt;li&gt;Date of birth (`YYYYMMDD`)&lt;/li&gt;&lt;/ul&gt; |
|Birthday Year|  &lt;ul&gt;&lt;li&gt;Year of birth (`YYYY`)&lt;/li&gt;&lt;/ul&gt; |
|Birthday Month|  &lt;ul&gt;&lt;li&gt;Month of birth (`MM`)&lt;/li&gt;&lt;/ul&gt; |
|Birthday Day|  &lt;ul&gt;&lt;li&gt;Date of birthday (`DD`)&lt;/li&gt;&lt;/ul&gt; |
|CRM Category 1 to 10|  &lt;ul&gt;&lt;li&gt;Custom categories for sending CRM information such as membership type, age, and gender.&lt;/li&gt;&lt;li&gt;Before mapping, make sure the category is defined in your Webtrekk tool.&lt;/li&gt;&lt;/ul&gt; |
|Custom Session Parameter 1 to 10|  &lt;ul&gt;&lt;li&gt;Custom parameters for sending additional visit/session information such as login status, registration status, and test group for A/B testing.&lt;/li&gt;&lt;li&gt;Before mapping, make sure the session parameter is defined in your Webtrekk tool.&lt;/li&gt;&lt;/ul&gt; |

### Page Data Category

|Tag Destination| Description|
|---| ---|
|Page Content ID|  &lt;ul&gt;&lt;li&gt;Identifies a page by its unique name rather than its URL and is set in the page-specific configuration.&lt;/li&gt;&lt;/ul&gt; |
|Content Group 1 to 25|  &lt;ul&gt;&lt;li&gt;Map to these destinations to send up to 50 custom parameters for a page.&lt;/li&gt;&lt;li&gt;Make sure the Content Group you are mapping to is also defined in your Webtrekk tool.&lt;/li&gt;&lt;/ul&gt; |
|Custom Parameter 1 to 50|  &lt;ul&gt;&lt;li&gt;Map to these destinations to send up to 50 custom parameters for a page.&lt;/li&gt;&lt;/ul&gt; |

### Search and Form Tracking

Map to these destinations for sending internal search and form input parameters.

|Tag Destination| Description|
|---| ---|
|Internal Search|  &lt;ul&gt;&lt;li&gt;Search keywords/terms used by visitors to look up your site&lt;/li&gt;&lt;/ul&gt; |
|Form Tracking|  &lt;ul&gt;&lt;li&gt;Activate/deactivate Form tracking in the page-specific configuration&lt;/li&gt;&lt;li&gt;Data source must contain the value `1` for activation and  for deactivation.&lt;/li&gt;&lt;/ul&gt; |
|Form Attribute|  &lt;ul&gt;&lt;li&gt;This attribute is used for determining the name of the form.&lt;/li&gt;&lt;li&gt;Mapping to this destination overrides the default &#34;name&#34; attribute.&lt;/li&gt;&lt;/ul&gt; |
|Form Value Attribute|  &lt;ul&gt;&lt;li&gt;This attribute is used for determining the name of the form when the form field is a &#39;radio&#39; or a &#39;checkbox&#39;.&lt;/li&gt;&lt;li&gt;Mapping to this destination overrides the default `value` attribute.&lt;/li&gt;&lt;/ul&gt; |
|Form Field Attribute| ---|
|Full Content Form Tracking| Sends the first 30 characters of a free-text field.|
|Anonymous Form Tracking|  &lt;ul&gt;&lt;li&gt;Contents of the form will not be sent to Webtrekk.&lt;/li&gt;&lt;li&gt;Mapping to this destination makes the form data anonymous.&lt;/li&gt;&lt;/ul&gt; |
|Form HTML Id|  &lt;ul&gt;&lt;li&gt;Method from tracking forms reloaded by Ajax.&lt;/li&gt;&lt;li&gt;Mapping to this destination invokes the method&lt;/li&gt;&lt;/ul&gt; |

### Click Tracking

|Tag Destination| Description|
|---| ---|
|Heatmap|  &lt;ul&gt;&lt;li&gt;Activate/deactivate Heatmap in the page-specific configuration.&lt;/li&gt;&lt;li&gt;Data source value must equal `1` for activation and  for deactivation.&lt;/li&gt;&lt;/ul&gt; |
|Heatmap reference point id|  &lt;ul&gt;&lt;li&gt;ID of the element being used as a point of reference for Heatmaps.&lt;/li&gt;&lt;/ul&gt; |
|Link Track|  &lt;ul&gt;&lt;li&gt;Event tracking settings in the page-specific configuration.&lt;/li&gt;&lt;li&gt;Webtrekk supports &#39;Link&#39; and &#39;Standard&#39; settings.&lt;/li&gt;&lt;/ul&gt; |
|Link Track Attribute|  &lt;ul&gt;&lt;li&gt;Applies to &#34;Standard&#34; tracking option in the page-specific configuration.&lt;/li&gt;&lt;li&gt;This attribute is used for determining the name of the event/action.&lt;/li&gt;&lt;li&gt;Mapping to this destination overrides the default &#34;name&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Link Tracks Params|  &lt;ul&gt;&lt;li&gt;Applies to &#34;Link&#34; tracking option in the page-specific configuration.&lt;/li&gt;&lt;li&gt;Mapping to this destination sends the query string parameter of the tracked link.&lt;/li&gt;&lt;/ul&gt; |
|Link Track Pattern|  &lt;ul&gt;&lt;li&gt;Regular Expression for filtering undesirable parameter(s) out of the Link Track Parameter query string.&lt;/li&gt;&lt;li&gt;Applies to page-specific configuration.&lt;/li&gt;&lt;/ul&gt; |
|Link Track Replace|  &lt;ul&gt;&lt;li&gt;Replacement character for replacing the filtered parameters in the Link Track Parameter.&lt;/li&gt;&lt;li&gt;Applies to page-specific configuration.&lt;/li&gt;&lt;/ul&gt; |
|Link Track Downloads|  &lt;ul&gt;&lt;li&gt;List of file types that you want to track for downloads.&lt;/li&gt;&lt;li&gt;Applies to page-specific configuration.&lt;/li&gt;&lt;li&gt;Example: `zip;raw;doc`&lt;/li&gt;&lt;/ul&gt; |
|Link ID for custom utag.link tracking|  &lt;ul&gt;&lt;li&gt;Name of the tracked link.&lt;/li&gt;&lt;/ul&gt; |
|Custom Click parameter 1 to 10|  &lt;ul&gt;&lt;li&gt;Custom parameters for click tracking.&lt;/li&gt;&lt;li&gt;The Link ID value must be mapped in order for your custom click parameter(s) to be sent.&lt;/li&gt;&lt;li&gt;Before mapping, make sure the parameter is also defined in your Webtrekk tool.&lt;/li&gt;&lt;/ul&gt; |

### Campaign Tracking

Map to these destinations for sending optional and custom campaign parameters

These mappings apply to page-specific configurations.

|Tag Destination| Description|
|---| ---|
|Media Code|  &lt;ul&gt;&lt;li&gt;Parameter for tracking campaigns.&lt;/li&gt;&lt;/ul&gt; |
|Media Code Cookie|  &lt;ul&gt;&lt;li&gt;Parameter for tracking a campaign ONLY once per session.&lt;/li&gt;&lt;/ul&gt; |
|Campaign ID|  &lt;ul&gt;&lt;li&gt;Media code parameter followed by `%3D` and the parameter value&lt;/li&gt;&lt;/ul&gt; |
|Campaign Action|  &lt;ul&gt;&lt;li&gt;Determines whether the visitor&#39;s response to a campaign was &#39;view&#39; or &#39;click&#39;.&lt;/li&gt;&lt;/ul&gt; |
|Custom Campaign Parameters 1 to 10|  &lt;ul&gt;&lt;li&gt;Custom parameters for campaign tracking.&lt;/li&gt;&lt;li&gt;Before mapping, make sure the parameter is defined in your Webtrekk tool.&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce Category

Since the Webtrekk tag is e-commerce enabled, it will automatically use the default [E-Commerce Extension]() mappings. Manually mapping in this category is generally not needed unless:

* you want to override any Extension mappings
* an e-commerce variable you want is not offered in the extension

|Tag Destination| Description| E-Commerce Extension Mappings |
|---| ---| ---|
|Order ID|  &lt;ul&gt;&lt;li&gt;Unique identifier of the final order&lt;/li&gt;&lt;/ul&gt; | `_corder`|
|Order Total|  &lt;ul&gt;&lt;li&gt;Total amount after shipping and tax.&lt;/li&gt;&lt;/ul&gt; | `_ctotal`|
|Currency|  &lt;ul&gt;&lt;li&gt;Currency used by the customer to make the payment&lt;/li&gt;&lt;/ul&gt; | `_ccurrency`|
|Coupon Value|  &lt;ul&gt;&lt;li&gt;The value of the coupon used in the order&lt;/li&gt;&lt;/ul&gt; | N//A|
|List of product names|  &lt;ul&gt;&lt;li&gt;Name of each product in the product array&lt;/li&gt;&lt;/ul&gt; | `_cprodname`|
|List of product quantities|  &lt;ul&gt;&lt;li&gt;Quantity of each product in the product array&lt;/li&gt;&lt;/ul&gt; | `_cquan`|
|List of product prices|  &lt;ul&gt;&lt;li&gt;Unit price of each product in the product array&lt;/li&gt;&lt;/ul&gt; | `_cprice`|
|List of product categories (productCategories[1])|  &lt;ul&gt;&lt;li&gt;Category of each product in the product array&lt;/li&gt;&lt;/ul&gt; | `_ccat`|
|List of product brands (productCategory[2])|  &lt;ul&gt;&lt;li&gt;Brand of each product in the product array&lt;/li&gt;&lt;/ul&gt; | `_cbrand`|
|List of product subcategories (productCategory[3])|  &lt;ul&gt;&lt;li&gt;Sub-category of each product in the product array&lt;/li&gt;&lt;/ul&gt; | `_ccat2`|
|Product Status|  &lt;ul&gt;&lt;li&gt;Indicates if the product was viewed, added to cart, or checked out from the cart.&lt;/li&gt;&lt;/ul&gt; | N/A|
|Product Category 1 to 25|  &lt;ul&gt;&lt;li&gt;Custom category with which a product can be associated only once.&lt;/li&gt;&lt;li&gt;You may map up to 25 unique categories.&lt;/li&gt;&lt;li&gt;Before mapping, make sure the product category is defined in your Webtrekk tool.&lt;/li&gt;&lt;/ul&gt; | N/A|
|Custom E-Commerce Parameter 1 to 50|  &lt;ul&gt;&lt;li&gt;Custom parameters for sending additional product- and order-level data.&lt;/li&gt;&lt;li&gt;You may map up to 50 unique parameters.&lt;/li&gt;&lt;li&gt;Before mapping, make sure the parameter(s) is defined in your Webtrekk tool.&lt;/li&gt;&lt;/ul&gt; | N/A|
