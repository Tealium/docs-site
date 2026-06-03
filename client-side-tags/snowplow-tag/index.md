---
title: Snowplow Tag Setup Guide
description: This article describes how to set up the Snowplow tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/snowplow-tag/
---
## Tag Tips

* Supports the E-Commerce extension
* Use mapping to:
  * Dynamically override the standard configuration values
  * Dynamically override the E-Commerce extension values
  * Trigger Structured Event tracking
  * Trigger Unstructured Event tracking

* Structured and Unstructured Event tracking is triggered when the Structured/Unstructured Event Action is defined with mappings.

## Tag Configuration

First, go to the tag marketplace and add the Snowplow tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Code Version**
  * Select a tag version (**2.18.2**, **3.1.2**, or **3.23.0**)

* **Title**
  * Assign a unique name when using multiple tags by the same vendor.

* **Snowplow Object (Required)**
  * A unique name for your global Snowplow object.
  * The Snowplow object name is defined as `window.snowplow.name`.

* **Snowplow Base URL (Required)**
  * URL representing the Snowplow tracker with version.
  * Example format: `//d1fc8wv8zag5ca.cloudfront.net/x.xx.x/sp.js`

* **Tracker Namespace (Required)**
  * The namespace for your Snowplow tracker.
  * Use data mapping to dynamically override this value.

* **Tracker End Point (Required)**
  * The collector end point URI for your Snowplow tracker.
  * Use data mapping to dynamically override this value.

* **Cookie Domain**
  * The top level domain your cookies should be set at.
  * Example `.mysite.com`.
  * Use data mapping to dynamically override this value.

* **Enable Link Tracking**
  * Add event listeners to your link clicks.
  * Possible values are `True` or `False`.
  * Use data mapping to dynamically override this value.

* **Enable Activity Tracking**
  * Enable &#39;page ping&#39; events to track user activity on the page.
  * Possible values are `True` or `False`.
  * Use data mapping to dynamically override this value.

* **Enable Error Tracking**
  * Track unhandled exceptions in your JavaScript code.
  * Possible values are `True` or `False`.
  * Use data mapping to dynamically override this value.

* **Enable Preserve Page View**
  * Regenerate the webpage context only when the whole HTML page is loaded.
  * Possible values are `True` or `False`.
  * Use data mapping to dynamically override this value.

* **Publish** **Locations**
  * The tag will only be published to the locations selected: `Dev`, `QA`, `Prod`, or `Custom`.

* **Advanced Settings**
  * Descriptive notes about this tag and how it is used within your organization.

## Load Rules

[Load Rules]() determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **All Pages**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the Snowplow tag are built into its **Data Mapping** tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
| `customURL` |  &lt;ul&gt;&lt;li&gt;Custom URL&lt;/li&gt;&lt;li&gt;Set a custom URL for the page.&lt;/li&gt;&lt;/ul&gt; |
| `referrerURL` |  &lt;ul&gt;&lt;li&gt;Custom Referrer URL.&lt;/li&gt;&lt;li&gt;Set a custom URL for the referrer.&lt;/li&gt;&lt;/ul&gt; |
| `pageTitle` |  &lt;ul&gt;&lt;li&gt;Page Title&lt;/li&gt;&lt;li&gt;Set the title of the page.&lt;/li&gt;&lt;/ul&gt; |
| `cookieTimeOut` |  &lt;ul&gt;&lt;li&gt;Cookie Time Out&lt;/li&gt;&lt;li&gt;Set the time (in seconds) that the session cookie should remain active.&lt;/li&gt;&lt;li&gt;Default is 30 minutes (1800 seconds).&lt;/li&gt;&lt;/ul&gt; |
| `enableAT` |  &lt;ul&gt;&lt;li&gt;Enable Activity Tracking&lt;/li&gt;&lt;li&gt;Enable `page ping` events to track user activity on the page.&lt;/li&gt;&lt;li&gt;Value Options: `true` or `false`&lt;/li&gt;&lt;/ul&gt; |
| `minimumVisitLength` |  &lt;ul&gt;&lt;li&gt;Minimum Visit Length&lt;/li&gt;&lt;li&gt;Set the time between page load and the first page ping, in seconds.&lt;/li&gt;&lt;/ul&gt; |
| `heartBeat` |  &lt;ul&gt;&lt;li&gt;Heartbeat&lt;/li&gt;&lt;li&gt;Set the time between page pings, in seconds.&lt;/li&gt;&lt;/ul&gt; |
| `enableET` |  &lt;ul&gt;&lt;li&gt;Enable Error Tracking&lt;/li&gt;&lt;li&gt;Track unhandled exceptions in your JavaScript code.&lt;/li&gt;&lt;li&gt;Value Options: `true` or `false`&lt;/li&gt;&lt;/ul&gt; |
| `preservePageView` |  &lt;ul&gt;&lt;li&gt;Preserve Page View&lt;/li&gt;&lt;li&gt;Regenerate the webpage context only when the whole HTML page is loaded.&lt;/li&gt;&lt;li&gt;Value Options: `true` or `false`&lt;/li&gt;&lt;/ul&gt; |

### Tracker

|**Destination Name**| **Description**|
|---| ---|
| `trk_namespace` |  &lt;ul&gt;&lt;li&gt;Tracker Namespace&lt;/li&gt;&lt;li&gt;The namespace for your Snowplow tracker.&lt;/li&gt;&lt;li&gt;Use to override the configuration settings.&lt;/li&gt;&lt;li&gt;Use this to dynamically override the configuration value.&lt;/li&gt;&lt;/ul&gt; |
| `trk_endpoint` |  &lt;ul&gt;&lt;li&gt;Tracker End Point&lt;/li&gt;&lt;li&gt;The collector end point URI for your Snowplow tracker.&lt;/li&gt;&lt;li&gt;Use this to dynamically override the configuration value.&lt;/li&gt;&lt;/ul&gt; |
| `trk_cookieDomain` |  &lt;ul&gt;&lt;li&gt;Cooklie Domain&lt;/li&gt;&lt;li&gt;The top level domain your cookies should be set at.&lt;/li&gt;&lt;li&gt;Use this to dynamically override the configuration value.&lt;/li&gt;&lt;/ul&gt; |
| `trk_cookieName` |  &lt;ul&gt;&lt;li&gt;Coolie Name&lt;/li&gt;&lt;li&gt;Set the base name for the Snowplow cookies.&lt;/li&gt;&lt;li&gt;Default value is **sp**.&lt;/li&gt;&lt;/ul&gt; |
| `trk_appId` |  &lt;ul&gt;&lt;li&gt;App ID&lt;/li&gt;&lt;li&gt;Set the application ID for your tracker events.&lt;/li&gt;&lt;li&gt;You can send different IDs from different pages to distinguish events&lt;/li&gt;&lt;/ul&gt; |
| `trk_platform` |  &lt;ul&gt;&lt;li&gt;Platform&lt;/li&gt;&lt;li&gt;Set the platform type for your tracker.&lt;/li&gt;&lt;li&gt;Default value is **web**.&lt;/li&gt;&lt;li&gt;For value options, see [Potential platform values](https://github.com/snowplow/snowplow/wiki/SnowPlow-Tracker-Protocol#appid)&lt;/li&gt;&lt;/ul&gt; |
| `trk_send` |  &lt;ul&gt;&lt;li&gt;Sending Tracker&lt;/li&gt;&lt;li&gt;String/Array&lt;/li&gt;&lt;li&gt;Namespace value to identify multiple items from the same source (such as ads).&lt;/li&gt;&lt;li&gt;When populated it is attached to page views, ad impressions, ad conversions, ad clicks, and link clicks.&lt;/li&gt;&lt;/ul&gt; |
| `trk_encodeBase64` |  &lt;ul&gt;&lt;li&gt;Use Encode Base 64&lt;/li&gt;&lt;li&gt;Set whether self-describing events and custom contexts are encoded into base64.&lt;/li&gt;&lt;li&gt;Default is true.&lt;/li&gt;&lt;li&gt;Value Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
| `trk_respectDoNotTrack` |  &lt;ul&gt;&lt;li&gt;Respect Do Not Track&lt;/li&gt;&lt;li&gt;Set whether the browser Do Not Track option is respected.&lt;/li&gt;&lt;li&gt;Default value is `false`.&lt;/li&gt;&lt;li&gt;Value Options are `true` or `false`&lt;/li&gt;&lt;/ul&gt; |
| `trk_userFingerprint` |  &lt;ul&gt;&lt;li&gt;User Finger Print&lt;/li&gt;&lt;li&gt;Set whether Snowplow generates a user fingerprint based on browser features.&lt;/li&gt;&lt;li&gt;Default value is `true`.&lt;/li&gt;&lt;li&gt;Value Options are `true` or `false`&lt;/li&gt;&lt;/ul&gt; |
| `trk_userFingerprintSeed` |  &lt;ul&gt;&lt;li&gt;User Finger Print Seed&lt;/li&gt;&lt;li&gt;Set the hash seed used to generate the user fingerprint.&lt;/li&gt;&lt;li&gt;Default is `123412414`&lt;/li&gt;&lt;/ul&gt; |
| `trk_pageUnloadTimer` |  &lt;ul&gt;&lt;li&gt;Page Unload Timer&lt;/li&gt;&lt;li&gt;Set the time period (in milliseconds) to wait before unloading the page after an event has been fired.&lt;/li&gt;&lt;li&gt;Default 500 milliseconds.&lt;/li&gt;&lt;/ul&gt; |
| `trk_forceSecure` |  &lt;ul&gt;&lt;li&gt;Force Secure Tracker&lt;/li&gt;&lt;li&gt;Set tracker to force **https** even if the current page is http.&lt;/li&gt;&lt;li&gt;Default value is `false`.&lt;/li&gt;&lt;li&gt;Value Options are `true` or `false`&lt;/li&gt;&lt;/ul&gt; |
| `trk_sendAsPost` |  &lt;ul&gt;&lt;li&gt;Send as POST&lt;/li&gt;&lt;li&gt;Set events using a POST request instead of a GET request.&lt;/li&gt;&lt;li&gt;Default value is `false`.&lt;/li&gt;&lt;li&gt;Value Options are `true` or `false`&lt;/li&gt;&lt;/ul&gt; |
| `trk_bufferSize` |  &lt;ul&gt;&lt;li&gt;Buffer Size&lt;/li&gt;&lt;li&gt;Set the size of the buffer for batching events when using POST.&lt;/li&gt;&lt;li&gt;Default value is **1**.&lt;/li&gt;&lt;/ul&gt; |
| `trk_maxPostBytes` |  &lt;ul&gt;&lt;li&gt;Max POST Bytes&lt;/li&gt;&lt;li&gt;Set the maximum size of POST requests sent to the Collector (in bytes).&lt;/li&gt;&lt;li&gt;Default value is 40,000 bytes.&lt;/li&gt;&lt;/ul&gt; |
| `trk_storageStrategy` |  &lt;ul&gt;&lt;li&gt;State Storage Strategy&lt;/li&gt;&lt;li&gt;Set the strategy for storing the tracker&#39;s state.&lt;/li&gt;&lt;li&gt;Default cookie.&lt;/li&gt;&lt;li&gt;Value Options: `cookie`, `localStorage`, or `none`&lt;/li&gt;&lt;/ul&gt; |
|`trk_cookieLifetime`|  &lt;ul&gt;&lt;li&gt;Cookie LIfetime&lt;/li&gt;&lt;li&gt;Set the retention time (in seconds) for the domain-specific visitor cookie.&lt;/li&gt;&lt;li&gt;Default value is 2 years. There are 86,400 seconds in a day.&lt;/li&gt;&lt;/ul&gt; |
|`trk_contextVendor`|  &lt;ul&gt;&lt;li&gt;Context Editor&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Set an array of predefined contexts to automatically send with every event.&lt;/li&gt;&lt;li&gt;[Vendor options](https://github.com/snowplow/snowplow/wiki/1-General-parameters-for-the-Javascript-tracker#predefined-contexts)&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

Since the Snowplow tag is e-commerce enabled, it automatically uses the default E-Commerce extension mappings. Manually mapping in this category is generally not needed unless you want to override extension mappings or an e-commerce variable you want is not offered in the extension.

|**Destination Name**| **Description**|
|---| ---|
| `order_id` |  &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_corder`.&lt;/li&gt;&lt;/ul&gt; |
| `order_total` |  &lt;ul&gt;&lt;li&gt;Order Total&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ctotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;Order Shipping Amount&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cship`.&lt;/li&gt;&lt;/ul&gt; |
| `order_tax` |  &lt;ul&gt;&lt;li&gt;Order Tax Amount&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ctax`.&lt;/li&gt;&lt;/ul&gt; |
|`order_store`|  &lt;ul&gt;&lt;li&gt;Order Store&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cstore`.&lt;/li&gt;&lt;/ul&gt; |
| `order_currency` |  &lt;ul&gt;&lt;li&gt;Order Currency&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ccustid`.&lt;/li&gt;&lt;/ul&gt; |
| `customer_city` |  &lt;ul&gt;&lt;li&gt;Customer City&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ccity`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_state`|  &lt;ul&gt;&lt;li&gt;Customer State&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cstate`.&lt;/li&gt;&lt;/ul&gt; |
| `customer_country` |  &lt;ul&gt;&lt;li&gt;Customer Country&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ccountry`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;List of Product Names&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cprodname`.&lt;/li&gt;&lt;/ul&gt; |
| `product_sku` |  &lt;ul&gt;&lt;li&gt;List of Product SKUs&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_csku`.&lt;/li&gt;&lt;/ul&gt; |
| `product_category` |  &lt;ul&gt;&lt;li&gt;List of Product Categories&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;List of Product Quantities&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
| `product_unit_price` |  &lt;ul&gt;&lt;li&gt;List of Product Unit Prices&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Use this to override the default e-commerce value `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
| `ecm_schema` |  &lt;ul&gt;&lt;li&gt;Transaction Context Schema&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
| `ecm_context.data` |  &lt;ul&gt;&lt;li&gt;Transaction Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `ecm_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `ecm_contextObj` |  &lt;ul&gt;&lt;li&gt;Transaction User-Defined Content&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

### Link Tracking

|**Destination Name**| **Description**|
|---| ---|
| `enableLCT` |  &lt;ul&gt;&lt;li&gt;Enable Link Click Tracking&lt;/li&gt;&lt;li&gt;Add event listeners to your link clicks.&lt;/li&gt;&lt;li&gt;Value Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_blacklist` |  &lt;ul&gt;&lt;li&gt;Blacklist&lt;/li&gt;&lt;li&gt;String/Array&lt;/li&gt;&lt;li&gt;A list of CSS classes that should be ignored by the link click tracker.&lt;/li&gt;&lt;li&gt;All other links will be tracked.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_whitelist` |  &lt;ul&gt;&lt;li&gt;Whitelist&lt;/li&gt;&lt;li&gt;String/Array&lt;/li&gt;&lt;li&gt;A list of CSS classes that should be tracked by the link click tracker.&lt;/li&gt;&lt;li&gt;All other links will be ignored.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_filter` |  &lt;ul&gt;&lt;li&gt;Filter&lt;/li&gt;&lt;li&gt;A function (or function reference) which should return either `true` or `false`.&lt;/li&gt;&lt;li&gt;All items returning `true` will be tracked.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_pseudoClicks` |  &lt;ul&gt;&lt;li&gt;Pseudo Clicks&lt;/li&gt;&lt;li&gt;Set whether middle clicks should be recognized as a click event.&lt;/li&gt;&lt;li&gt;Default value is `false`.&lt;/li&gt;&lt;li&gt;Value Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_clickContent` |  &lt;ul&gt;&lt;li&gt;Click Content&lt;/li&gt;&lt;li&gt;Set whether click events should capture the innerHTML of the link.&lt;/li&gt;&lt;li&gt;Value Options are `true` or `false`&lt;/li&gt;&lt;/ul&gt; |
|`ltr_url`|  &lt;ul&gt;&lt;li&gt;URL&lt;/li&gt;&lt;li&gt;For manually-tracked events.&lt;/li&gt;&lt;li&gt;Set the target URL.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_elementId` |  &lt;ul&gt;&lt;li&gt;Element ID&lt;/li&gt;&lt;li&gt;For manually-tracked events.&lt;/li&gt;&lt;li&gt;Set the link ID for the element.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_elementClasses` |  &lt;ul&gt;&lt;li&gt;Element Classes&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;For manually-tracked events.&lt;/li&gt;&lt;li&gt;Set the link classes for the element.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_elementTarget` |  &lt;ul&gt;&lt;li&gt;Element Target&lt;/li&gt;&lt;li&gt;For manually-tracked events.&lt;/li&gt;&lt;li&gt;Set the link target for the element.&lt;/li&gt;&lt;/ul&gt; |
|`ltr_elementClickContent`|  &lt;ul&gt;&lt;li&gt;Element Click Content&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;For manually-tracked events.&lt;/li&gt;&lt;li&gt;Set the link content for the element.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_schema` |  &lt;ul&gt;&lt;li&gt;Context Schema&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_context.data` |  &lt;ul&gt;&lt;li&gt;Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `ltr_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `ltr_contextObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Context&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

### Ad Tracking

|**Destination Name**| **Description**|
|---| ---|
|`adtracking`|  &lt;ul&gt;&lt;li&gt;Ad Tracking&lt;/li&gt;&lt;li&gt;Set the type of ad being tracked.&lt;/li&gt;&lt;li&gt;Ad events will only fire if this is populated.&lt;/li&gt;&lt;li&gt;Value Options are `impression`, `click`, or `conversion`.&lt;/li&gt;&lt;/ul&gt; |
| `ad_impressionId` |  &lt;ul&gt;&lt;li&gt;Impression ID&lt;/li&gt;&lt;li&gt;Set the identifier for the current impression instance.&lt;/li&gt;&lt;/ul&gt; |
| `ad_costModel` |  &lt;ul&gt;&lt;li&gt;Cost Model&lt;/li&gt;&lt;li&gt;Set the cost model for your campaign.&lt;/li&gt;&lt;li&gt;Value Options: `cpc`, `cpm`, or `cpa`&lt;/li&gt;&lt;/ul&gt; |
| `ad_cost` |  &lt;ul&gt;&lt;li&gt;Cost&lt;/li&gt;&lt;li&gt;Set the cost for the ad.&lt;/li&gt;&lt;/ul&gt; |
|`ad_targetUrl`|  &lt;ul&gt;&lt;li&gt;Target URL&lt;/li&gt;&lt;li&gt;Set the destination URL for the ad.&lt;/li&gt;&lt;/ul&gt; |
|`ad_bannerId`|  &lt;ul&gt;&lt;li&gt;Banner ID&lt;/li&gt;&lt;li&gt;Set the `adserver` identifier for the ad.&lt;/li&gt;&lt;/ul&gt; |
| `ad_zoneId` |  &lt;ul&gt;&lt;li&gt;Zone ID&lt;/li&gt;&lt;li&gt;Set the `adserver` identifier for the zone where the ad is located.&lt;/li&gt;&lt;/ul&gt; |
| `ad_advertiserId` |  &lt;ul&gt;&lt;li&gt;Advertiser ID&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Set the `adserver` identifier for the advertiser the campaign belongs to.&lt;/li&gt;&lt;/ul&gt; |
| `ad_campaignId` |  &lt;ul&gt;&lt;li&gt;Campaign ID&lt;/li&gt;&lt;li&gt;Set the `adserver` identifier for the campaign the banner belongs to.&lt;/li&gt;&lt;/ul&gt; |
| `ad_clickId` |  &lt;ul&gt;&lt;li&gt;Click ID&lt;/li&gt;&lt;li&gt;Set the identifier for the current click instance.&lt;/li&gt;&lt;/ul&gt; |
| `ad_conversionId` |  &lt;ul&gt;&lt;li&gt;Conversion ID&lt;/li&gt;&lt;li&gt;Set the identifier for the current conversion instance.&lt;/li&gt;&lt;/ul&gt; |
| `ad_category` |  &lt;ul&gt;&lt;li&gt;Category&lt;/li&gt;&lt;li&gt;Set the category for the conversion.&lt;/li&gt;&lt;/ul&gt; |
| `ad_action` |  &lt;ul&gt;&lt;li&gt;Action&lt;/li&gt;&lt;li&gt;Set the type of user interaction for the conversion.&lt;/li&gt;&lt;/ul&gt; |
| `ad_property` |  &lt;ul&gt;&lt;li&gt;Property&lt;/li&gt;&lt;li&gt;Set the object description for the conversion.&lt;/li&gt;&lt;/ul&gt; |
| `ad_initialValue` |  &lt;ul&gt;&lt;li&gt;Initial Value&lt;/li&gt;&lt;li&gt;Set the initial worth of the conversion.&lt;/li&gt;&lt;/ul&gt; |
| `ad_schema` |  &lt;ul&gt;&lt;li&gt;Context Schema&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
| `ad_context.data` |  &lt;ul&gt;&lt;li&gt;Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `ad_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `ad_contextObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Context&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

### Page View Custom Context

|**Destination Name**| **Description**|
|---| ---|
| `cc_schema` |  &lt;ul&gt;&lt;li&gt;Context Schema&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
|`cc_context.data`|  &lt;ul&gt;&lt;li&gt;Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `cc_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `cc_contextObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Context&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

### Social Tracking

|**Destination Name**| **Description**|
|---| ---|
| `sot_action` |  &lt;ul&gt;&lt;li&gt;Action&lt;/li&gt;&lt;li&gt;The action performed by the user.&lt;/li&gt;&lt;/ul&gt; |
| `sot_network` |  &lt;ul&gt;&lt;li&gt;Social Network&lt;/li&gt;&lt;li&gt;The network the user interacted with.&lt;/li&gt;&lt;/ul&gt; |
| `sot_target` |  &lt;ul&gt;&lt;li&gt;Target&lt;/li&gt;&lt;li&gt;The object the performed action is on.&lt;/li&gt;&lt;/ul&gt; |
| `sot_schema` |  &lt;ul&gt;&lt;li&gt;Context Schema&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
| `sot_context.data` |  &lt;ul&gt;&lt;li&gt;Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `sot_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `sot_contextObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Context&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

### Form Tracking

|**Destination Name**| **Description**|
|---| ---|
| `enableFormTracking` |  &lt;ul&gt;&lt;li&gt;Enable Form Tracking&lt;/li&gt;&lt;li&gt;Set whether form changes and submissions should be tracked.&lt;/li&gt;&lt;li&gt;Value Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
| `ftr_formBlacklist` |  &lt;ul&gt;&lt;li&gt;Forms Custom Blacklist&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;A list of form CSS classes that should be ignored by the form tracker.&lt;/li&gt;&lt;li&gt;All other links will be tracked.&lt;/li&gt;&lt;li&gt;Examples: login form, request form&lt;/li&gt;&lt;/ul&gt; |
| `ftr_formWhitelist` |  &lt;ul&gt;&lt;li&gt;Forms Custom Whitelist&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;A list of form CSS classes that should be tracked by the form tracker.&lt;/li&gt;&lt;li&gt;All other links will be ignored.&lt;/li&gt;&lt;li&gt;Examples: login form, request form&lt;/li&gt;&lt;/ul&gt; |
| `ftr_fieldBlacklist` |  &lt;ul&gt;&lt;li&gt;Fields Custom Blacklist&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;A list of field CSS classes that should be ignored by the form tracker.&lt;/li&gt;&lt;li&gt;All other links will be tracked.&lt;/li&gt;&lt;li&gt;Examples: password field, email field&lt;/li&gt;&lt;/ul&gt; |
| `ftr_fieldWhitelist` |  &lt;ul&gt;&lt;li&gt;Fields Custom Whitelist&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;A list of field CSS classes that should be tracked by the form tracker.&lt;/li&gt;&lt;li&gt;All other links will be ignored.&lt;/li&gt;&lt;li&gt;Examples: password field, email field&lt;/li&gt;&lt;/ul&gt; |
| `ftr_filterForm` |  &lt;ul&gt;&lt;li&gt;Custom Form Filter Function&lt;/li&gt;&lt;li&gt;A function (or function reference) which should return either `true` or `false`.&lt;/li&gt;&lt;li&gt;All items returning `true` will be tracked.&lt;/li&gt;&lt;/ul&gt; |
| `ftr_filterField` |  &lt;ul&gt;&lt;li&gt;Custom Field Filter Function&lt;/li&gt;&lt;li&gt;A function (or function reference) which should return either `true` or `false`.&lt;/li&gt;&lt;li&gt;All items returning `true` will be tracked.&lt;/li&gt;&lt;/ul&gt; |
| `ftr_ctmConfig` |  &lt;ul&gt;&lt;li&gt;User-Defined Config&lt;/li&gt;&lt;li&gt;A custom configuration object with the above properties.&lt;/li&gt;&lt;li&gt;Use in place of the individual properties.&lt;/li&gt;&lt;/ul&gt; |

### Cart Tracking

|**Destination Name**| **Description**|
|---| ---|
| `cartTracking` |  &lt;ul&gt;&lt;li&gt;Cart Tracking&lt;/li&gt;&lt;li&gt;Set the type of cart event being tracked.&lt;/li&gt;&lt;li&gt;Cart events will only fire if this is populated.&lt;/li&gt;&lt;li&gt;Value Options are `cart_add` or `cart_remove`.&lt;/li&gt;&lt;/ul&gt; |
| `cart_sku` |  &lt;ul&gt;&lt;li&gt;Cart Item SKU&lt;/li&gt;&lt;li&gt;The SKU of the item being moved in the cart.&lt;/li&gt;&lt;/ul&gt; |
| `cart_name` |  &lt;ul&gt;&lt;li&gt;Cart Item Name&lt;/li&gt;&lt;li&gt;The name of the item being moved in the cart.&lt;/li&gt;&lt;/ul&gt; |
| `cart_category` |  &lt;ul&gt;&lt;li&gt;Cart Item Category&lt;/li&gt;&lt;li&gt;The category of the item being moved in the cart.&lt;/li&gt;&lt;/ul&gt; |
| `cart_price` |  &lt;ul&gt;&lt;li&gt;Cart Item Unit Price&lt;/li&gt;&lt;li&gt;The price of the item being moved in the cart.&lt;/li&gt;&lt;/ul&gt; |
| `cart_quantity` |  &lt;ul&gt;&lt;li&gt;Cart Item Quantity&lt;/li&gt;&lt;li&gt;The quantity of the item being moved in the cart.&lt;/li&gt;&lt;/ul&gt; |
| `cart_currency` |  &lt;ul&gt;&lt;li&gt;Cart Item Currency&lt;/li&gt;&lt;li&gt;The currency of the item being moved in the cart.&lt;/li&gt;&lt;/ul&gt; |
| `cart_schema` |  &lt;ul&gt;&lt;li&gt;Context Schema&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
| `cart_context.data` |  &lt;ul&gt;&lt;li&gt;Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `cart_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `cart_contextObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Context&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

### Site Search Tracking

|**Destination Name**| **Description**|
|---| ---|
| `sst_terms` |  &lt;ul&gt;&lt;li&gt;Search Terms&lt;/li&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;A list of terms used in the site search.&lt;/li&gt;&lt;li&gt;Search events will only fire if this is populated.&lt;/li&gt;&lt;/ul&gt; |
|`sst_filters`|  &lt;ul&gt;&lt;li&gt;Search Filters&lt;/li&gt;&lt;li&gt;A JSON object defining the filter types and terms.&lt;/li&gt;&lt;/ul&gt; |
| `sst_totalResults` |  &lt;ul&gt;&lt;li&gt;Total Results Found&lt;/li&gt;&lt;li&gt;The total number of results found for the search&lt;/li&gt;&lt;/ul&gt; |
| `sst_pageResults` |  &lt;ul&gt;&lt;li&gt;First Page Results&lt;/li&gt;&lt;li&gt;The number of results displayed on the first page.&lt;/li&gt;&lt;/ul&gt; |
| `sst_schema` |  &lt;ul&gt;&lt;li&gt;Context Schema&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
| `sst_context.data` |  &lt;ul&gt;&lt;li&gt;Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `sst_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `sst_contextObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Context&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

### Structured Event

|**Destination Name**| **Description**|
|---| ---|
| `stctCat` |  &lt;ul&gt;&lt;li&gt;Category&lt;/li&gt;&lt;li&gt;The name of the group of objects you are tracking.&lt;/li&gt;&lt;/ul&gt; |
| `stctActn` |  &lt;ul&gt;&lt;li&gt;Action Name&lt;/li&gt;&lt;li&gt;The name of the user interaction for the objects you are tracking.&lt;/li&gt;&lt;/ul&gt; |
| `stctLabel` |  &lt;ul&gt;&lt;li&gt;Label&lt;/li&gt;&lt;li&gt;An additional name which identifies the specific object you are tracking.&lt;/li&gt;&lt;/ul&gt; |
| `stctProp` |  &lt;ul&gt;&lt;li&gt;Property&lt;/li&gt;&lt;li&gt;An additional item describing the object or action performed on it.&lt;/li&gt;&lt;/ul&gt; |
| `stctVal` |  &lt;ul&gt;&lt;li&gt;Value&lt;/li&gt;&lt;li&gt;An additional decimal number describing the user interaction.&lt;/li&gt;&lt;/ul&gt; |
| `stc_schema` |  &lt;ul&gt;&lt;li&gt;Context schema&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
|`stc_context.data`|  &lt;ul&gt;&lt;li&gt;Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `stc_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `stc_contextObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Context&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

### Unstructured Event

|**Destination Name**| **Description**|
|---| ---|
| `unstctDataSchema` |  &lt;ul&gt;&lt;li&gt;Schema&lt;/li&gt;&lt;li&gt;The JSON schema describing the event. Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
| `unstctData.data` |  &lt;ul&gt;&lt;li&gt;User-Defined Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the event.&lt;/li&gt;&lt;li&gt;Replace the `data` in `unstctData.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `unstctDataObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Data Object&lt;/li&gt;&lt;li&gt;A custom configuration object with the above properties.&lt;/li&gt;&lt;li&gt;Use in place of the individual properties.&lt;/li&gt;&lt;/ul&gt; |
| `stc_schema` |  &lt;ul&gt;&lt;li&gt;Context Schema&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
| `nstc_context.data` |  &lt;ul&gt;&lt;li&gt;Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `unstc_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `unstc_contextObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Context&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

### Consent Tracking

|**Destination Name**| **Description**|
|---| ---|
| `consentGranted` |  &lt;ul&gt;&lt;li&gt;User Granted Consent&lt;/li&gt;&lt;li&gt;Used to track a user opting into data collection.&lt;/li&gt;&lt;li&gt;A consent document context is attached to the event if at least the `id` and `version` arguments are supplied.&lt;/li&gt;&lt;/ul&gt; |
| `consentWithdrawn` |  &lt;ul&gt;&lt;li&gt;User Withdrew Some Consent&lt;/li&gt;&lt;li&gt;Used to track a user withdrawing consent for data collection.&lt;/li&gt;&lt;li&gt;A consent document context is attached to the event if at least the `id` and `version` arguments are supplied.&lt;/li&gt;&lt;/ul&gt; |
| `allConsentWithdrawn` |  &lt;ul&gt;&lt;li&gt;User Withdrew All Consent&lt;/li&gt;&lt;li&gt;Specifies whether all consent should be withdrawn.&lt;/li&gt;&lt;/ul&gt; |
| `con_documentId` |  &lt;ul&gt;&lt;li&gt;Consent Document ID&lt;/li&gt;&lt;li&gt;The consent document is a custom context storing the arguments supplied to the method (in both granted and withdrawn events, this is: `id`, `version`, `name`, and `description`).&lt;/li&gt;&lt;li&gt;In either consent method, additional documents can be appended to the event by passing an array of consent document self-describing JSONs in the context argument.&lt;/li&gt;&lt;/ul&gt; |
| `con_documentVer` |  &lt;ul&gt;&lt;li&gt;Consent Document Version&lt;/li&gt;&lt;li&gt;Required&lt;/li&gt;&lt;li&gt;Version of the document granting consent&lt;/li&gt;&lt;/ul&gt; |
| `con_documentName` |  &lt;ul&gt;&lt;li&gt;Consent Document Name&lt;/li&gt;&lt;li&gt;Name of the consent document.&lt;/li&gt;&lt;/ul&gt; |
| `con_documentDesc` |  &lt;ul&gt;&lt;li&gt;Consent Document Description&lt;/li&gt;&lt;li&gt;Description of the consent document.&lt;/li&gt;&lt;/ul&gt; |
| `con_documentExpiry` |  &lt;ul&gt;&lt;li&gt;Consent Document Expiration&lt;/li&gt;&lt;li&gt;Specifies that the user consents to the attached documents until the date-time provided, after which the consent is no longer valid.&lt;/li&gt;&lt;/ul&gt; |
| `unstc_schema` |  &lt;ul&gt;&lt;li&gt;Context Schema&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The JSON schema describing the context.&lt;/li&gt;&lt;li&gt;Must be present in an Iglu library.&lt;/li&gt;&lt;/ul&gt; |
| `nstc_context.data` |  &lt;ul&gt;&lt;li&gt;Context Data&lt;/li&gt;&lt;li&gt;Data values to be tracked by the context.&lt;/li&gt;&lt;li&gt;Replace the `data` in `unstc_context.data` with the name associated with your value when mapping.&lt;/li&gt;&lt;/ul&gt; |
| `con_contextObj` |  &lt;ul&gt;&lt;li&gt;User-Defined Context&lt;/li&gt;&lt;li&gt;A custom context object with schema and data properties.&lt;/li&gt;&lt;/ul&gt; |

## Vendor Documentation

* [SnowPlow Javascript Tracker documentation](https://docs.snowplowanalytics.com/docs/collecting-data/collecting-from-own-applications/javascript-trackers/)
