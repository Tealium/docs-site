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

First, go to the tag marketplace and add the Snowplow tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

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
  * Enable 'page ping' events to track user activity on the page.
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

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **All Pages**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for the Snowplow tag are built into its **Data Mapping** tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
| `customURL` |  <ul><li>Custom URL</li><li>Set a custom URL for the page.</li></ul> |
| `referrerURL` |  <ul><li>Custom Referrer URL.</li><li>Set a custom URL for the referrer.</li></ul> |
| `pageTitle` |  <ul><li>Page Title</li><li>Set the title of the page.</li></ul> |
| `cookieTimeOut` |  <ul><li>Cookie Time Out</li><li>Set the time (in seconds) that the session cookie should remain active.</li><li>Default is 30 minutes (1800 seconds).</li></ul> |
| `enableAT` |  <ul><li>Enable Activity Tracking</li><li>Enable `page ping` events to track user activity on the page.</li><li>Value Options: `true` or `false`</li></ul> |
| `minimumVisitLength` |  <ul><li>Minimum Visit Length</li><li>Set the time between page load and the first page ping, in seconds.</li></ul> |
| `heartBeat` |  <ul><li>Heartbeat</li><li>Set the time between page pings, in seconds.</li></ul> |
| `enableET` |  <ul><li>Enable Error Tracking</li><li>Track unhandled exceptions in your JavaScript code.</li><li>Value Options: `true` or `false`</li></ul> |
| `preservePageView` |  <ul><li>Preserve Page View</li><li>Regenerate the webpage context only when the whole HTML page is loaded.</li><li>Value Options: `true` or `false`</li></ul> |

### Tracker

|**Destination Name**| **Description**|
|---| ---|
| `trk_namespace` |  <ul><li>Tracker Namespace</li><li>The namespace for your Snowplow tracker.</li><li>Use to override the configuration settings.</li><li>Use this to dynamically override the configuration value.</li></ul> |
| `trk_endpoint` |  <ul><li>Tracker End Point</li><li>The collector end point URI for your Snowplow tracker.</li><li>Use this to dynamically override the configuration value.</li></ul> |
| `trk_cookieDomain` |  <ul><li>Cooklie Domain</li><li>The top level domain your cookies should be set at.</li><li>Use this to dynamically override the configuration value.</li></ul> |
| `trk_cookieName` |  <ul><li>Coolie Name</li><li>Set the base name for the Snowplow cookies.</li><li>Default value is **sp**.</li></ul> |
| `trk_appId` |  <ul><li>App ID</li><li>Set the application ID for your tracker events.</li><li>You can send different IDs from different pages to distinguish events</li></ul> |
| `trk_platform` |  <ul><li>Platform</li><li>Set the platform type for your tracker.</li><li>Default value is **web**.</li><li>For value options, see [Potential platform values](https://github.com/snowplow/snowplow/wiki/SnowPlow-Tracker-Protocol#appid)</li></ul> |
| `trk_send` |  <ul><li>Sending Tracker</li><li>String/Array</li><li>Namespace value to identify multiple items from the same source (such as ads).</li><li>When populated it is attached to page views, ad impressions, ad conversions, ad clicks, and link clicks.</li></ul> |
| `trk_encodeBase64` |  <ul><li>Use Encode Base 64</li><li>Set whether self-describing events and custom contexts are encoded into base64.</li><li>Default is true.</li><li>Value Options are `true` or `false`.</li></ul> |
| `trk_respectDoNotTrack` |  <ul><li>Respect Do Not Track</li><li>Set whether the browser Do Not Track option is respected.</li><li>Default value is `false`.</li><li>Value Options are `true` or `false`</li></ul> |
| `trk_userFingerprint` |  <ul><li>User Finger Print</li><li>Set whether Snowplow generates a user fingerprint based on browser features.</li><li>Default value is `true`.</li><li>Value Options are `true` or `false`</li></ul> |
| `trk_userFingerprintSeed` |  <ul><li>User Finger Print Seed</li><li>Set the hash seed used to generate the user fingerprint.</li><li>Default is `123412414`</li></ul> |
| `trk_pageUnloadTimer` |  <ul><li>Page Unload Timer</li><li>Set the time period (in milliseconds) to wait before unloading the page after an event has been fired.</li><li>Default 500 milliseconds.</li></ul> |
| `trk_forceSecure` |  <ul><li>Force Secure Tracker</li><li>Set tracker to force **https** even if the current page is http.</li><li>Default value is `false`.</li><li>Value Options are `true` or `false`</li></ul> |
| `trk_sendAsPost` |  <ul><li>Send as POST</li><li>Set events using a POST request instead of a GET request.</li><li>Default value is `false`.</li><li>Value Options are `true` or `false`</li></ul> |
| `trk_bufferSize` |  <ul><li>Buffer Size</li><li>Set the size of the buffer for batching events when using POST.</li><li>Default value is **1**.</li></ul> |
| `trk_maxPostBytes` |  <ul><li>Max POST Bytes</li><li>Set the maximum size of POST requests sent to the Collector (in bytes).</li><li>Default value is 40,000 bytes.</li></ul> |
| `trk_storageStrategy` |  <ul><li>State Storage Strategy</li><li>Set the strategy for storing the tracker's state.</li><li>Default cookie.</li><li>Value Options: `cookie`, `localStorage`, or `none`</li></ul> |
|`trk_cookieLifetime`|  <ul><li>Cookie LIfetime</li><li>Set the retention time (in seconds) for the domain-specific visitor cookie.</li><li>Default value is 2 years. There are 86,400 seconds in a day.</li></ul> |
|`trk_contextVendor`|  <ul><li>Context Editor</li><li>Array</li><li>Set an array of predefined contexts to automatically send with every event.</li><li>[Vendor options](https://github.com/snowplow/snowplow/wiki/1-General-parameters-for-the-Javascript-tracker#predefined-contexts)</li></ul> |

### E-Commerce

Since the Snowplow tag is e-commerce enabled, it automatically uses the default E-Commerce extension mappings. Manually mapping in this category is generally not needed unless you want to override extension mappings or an e-commerce variable you want is not offered in the extension.

|**Destination Name**| **Description**|
|---| ---|
| `order_id` |  <ul><li>Order ID</li><li>Use this to override the default e-commerce value `_corder`.</li></ul> |
| `order_total` |  <ul><li>Order Total</li><li>Use this to override the default e-commerce value `_ctotal`.</li></ul> |
|`order_shipping`|  <ul><li>Order Shipping Amount</li><li>Use this to override the default e-commerce value `_cship`.</li></ul> |
| `order_tax` |  <ul><li>Order Tax Amount</li><li>Use this to override the default e-commerce value `_ctax`.</li></ul> |
|`order_store`|  <ul><li>Order Store</li><li>Use this to override the default e-commerce value `_cstore`.</li></ul> |
| `order_currency` |  <ul><li>Order Currency</li><li>Use this to override the default e-commerce value `_ccurrency`.</li></ul> |
|`customer_id`|  <ul><li>Customer ID</li><li>Use this to override the default e-commerce value `_ccustid`.</li></ul> |
| `customer_city` |  <ul><li>Customer City</li><li>Use this to override the default e-commerce value `_ccity`.</li></ul> |
|`customer_state`|  <ul><li>Customer State</li><li>Use this to override the default e-commerce value `_cstate`.</li></ul> |
| `customer_country` |  <ul><li>Customer Country</li><li>Use this to override the default e-commerce value `_ccountry`.</li></ul> |
|`product_name`|  <ul><li>List of Product Names</li><li>Array</li><li>Use this to override the default e-commerce value `_cprodname`.</li></ul> |
| `product_sku` |  <ul><li>List of Product SKUs</li><li>Array</li><li>Use this to override the default e-commerce value `_csku`.</li></ul> |
| `product_category` |  <ul><li>List of Product Categories</li><li>Array</li><li>Use this to override the default e-commerce value `_ccat`.</li></ul> |
|`product_quantity`|  <ul><li>List of Product Quantities</li><li>Array</li><li>Use this to override the default e-commerce value `_cquan`.</li></ul> |
| `product_unit_price` |  <ul><li>List of Product Unit Prices</li><li>Array</li><li>Use this to override the default e-commerce value `_cprice`.</li></ul> |
| `ecm_schema` |  <ul><li>Transaction Context Schema</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
| `ecm_context.data` |  <ul><li>Transaction Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `ecm_context.data` with the name associated with your value when mapping.</li></ul> |
| `ecm_contextObj` |  <ul><li>Transaction User-Defined Content</li><li>A custom context object with schema and data properties.</li></ul> |

### Link Tracking

|**Destination Name**| **Description**|
|---| ---|
| `enableLCT` |  <ul><li>Enable Link Click Tracking</li><li>Add event listeners to your link clicks.</li><li>Value Options are `true` or `false`.</li></ul> |
| `ltr_blacklist` |  <ul><li>Blacklist</li><li>String/Array</li><li>A list of CSS classes that should be ignored by the link click tracker.</li><li>All other links will be tracked.</li></ul> |
| `ltr_whitelist` |  <ul><li>Whitelist</li><li>String/Array</li><li>A list of CSS classes that should be tracked by the link click tracker.</li><li>All other links will be ignored.</li></ul> |
| `ltr_filter` |  <ul><li>Filter</li><li>A function (or function reference) which should return either `true` or `false`.</li><li>All items returning `true` will be tracked.</li></ul> |
| `ltr_pseudoClicks` |  <ul><li>Pseudo Clicks</li><li>Set whether middle clicks should be recognized as a click event.</li><li>Default value is `false`.</li><li>Value Options are `true` or `false`.</li></ul> |
| `ltr_clickContent` |  <ul><li>Click Content</li><li>Set whether click events should capture the innerHTML of the link.</li><li>Value Options are `true` or `false`</li></ul> |
|`ltr_url`|  <ul><li>URL</li><li>For manually-tracked events.</li><li>Set the target URL.</li></ul> |
| `ltr_elementId` |  <ul><li>Element ID</li><li>For manually-tracked events.</li><li>Set the link ID for the element.</li></ul> |
| `ltr_elementClasses` |  <ul><li>Element Classes</li><li>Array</li><li>For manually-tracked events.</li><li>Set the link classes for the element.</li></ul> |
| `ltr_elementTarget` |  <ul><li>Element Target</li><li>For manually-tracked events.</li><li>Set the link target for the element.</li></ul> |
|`ltr_elementClickContent`|  <ul><li>Element Click Content</li><li>Array</li><li>For manually-tracked events.</li><li>Set the link content for the element.</li></ul> |
| `ltr_schema` |  <ul><li>Context Schema</li><li>String</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
| `ltr_context.data` |  <ul><li>Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `ltr_context.data` with the name associated with your value when mapping.</li></ul> |
| `ltr_contextObj` |  <ul><li>User-Defined Context</li><li>A custom context object with schema and data properties.</li></ul> |

### Ad Tracking

|**Destination Name**| **Description**|
|---| ---|
|`adtracking`|  <ul><li>Ad Tracking</li><li>Set the type of ad being tracked.</li><li>Ad events will only fire if this is populated.</li><li>Value Options are `impression`, `click`, or `conversion`.</li></ul> |
| `ad_impressionId` |  <ul><li>Impression ID</li><li>Set the identifier for the current impression instance.</li></ul> |
| `ad_costModel` |  <ul><li>Cost Model</li><li>Set the cost model for your campaign.</li><li>Value Options: `cpc`, `cpm`, or `cpa`</li></ul> |
| `ad_cost` |  <ul><li>Cost</li><li>Set the cost for the ad.</li></ul> |
|`ad_targetUrl`|  <ul><li>Target URL</li><li>Set the destination URL for the ad.</li></ul> |
|`ad_bannerId`|  <ul><li>Banner ID</li><li>Set the `adserver` identifier for the ad.</li></ul> |
| `ad_zoneId` |  <ul><li>Zone ID</li><li>Set the `adserver` identifier for the zone where the ad is located.</li></ul> |
| `ad_advertiserId` |  <ul><li>Advertiser ID</li><li>Array</li><li>Set the `adserver` identifier for the advertiser the campaign belongs to.</li></ul> |
| `ad_campaignId` |  <ul><li>Campaign ID</li><li>Set the `adserver` identifier for the campaign the banner belongs to.</li></ul> |
| `ad_clickId` |  <ul><li>Click ID</li><li>Set the identifier for the current click instance.</li></ul> |
| `ad_conversionId` |  <ul><li>Conversion ID</li><li>Set the identifier for the current conversion instance.</li></ul> |
| `ad_category` |  <ul><li>Category</li><li>Set the category for the conversion.</li></ul> |
| `ad_action` |  <ul><li>Action</li><li>Set the type of user interaction for the conversion.</li></ul> |
| `ad_property` |  <ul><li>Property</li><li>Set the object description for the conversion.</li></ul> |
| `ad_initialValue` |  <ul><li>Initial Value</li><li>Set the initial worth of the conversion.</li></ul> |
| `ad_schema` |  <ul><li>Context Schema</li><li>String</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
| `ad_context.data` |  <ul><li>Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `ad_context.data` with the name associated with your value when mapping.</li></ul> |
| `ad_contextObj` |  <ul><li>User-Defined Context</li><li>A custom context object with schema and data properties.</li></ul> |

### Page View Custom Context

|**Destination Name**| **Description**|
|---| ---|
| `cc_schema` |  <ul><li>Context Schema</li><li>String</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
|`cc_context.data`|  <ul><li>Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `cc_context.data` with the name associated with your value when mapping.</li></ul> |
| `cc_contextObj` |  <ul><li>User-Defined Context</li><li>A custom context object with schema and data properties.</li></ul> |

### Social Tracking

|**Destination Name**| **Description**|
|---| ---|
| `sot_action` |  <ul><li>Action</li><li>The action performed by the user.</li></ul> |
| `sot_network` |  <ul><li>Social Network</li><li>The network the user interacted with.</li></ul> |
| `sot_target` |  <ul><li>Target</li><li>The object the performed action is on.</li></ul> |
| `sot_schema` |  <ul><li>Context Schema</li><li>String</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
| `sot_context.data` |  <ul><li>Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `sot_context.data` with the name associated with your value when mapping.</li></ul> |
| `sot_contextObj` |  <ul><li>User-Defined Context</li><li>A custom context object with schema and data properties.</li></ul> |

### Form Tracking

|**Destination Name**| **Description**|
|---| ---|
| `enableFormTracking` |  <ul><li>Enable Form Tracking</li><li>Set whether form changes and submissions should be tracked.</li><li>Value Options are `true` or `false`.</li></ul> |
| `ftr_formBlacklist` |  <ul><li>Forms Custom Blacklist</li><li>Array</li><li>A list of form CSS classes that should be ignored by the form tracker.</li><li>All other links will be tracked.</li><li>Examples: login form, request form</li></ul> |
| `ftr_formWhitelist` |  <ul><li>Forms Custom Whitelist</li><li>Array</li><li>A list of form CSS classes that should be tracked by the form tracker.</li><li>All other links will be ignored.</li><li>Examples: login form, request form</li></ul> |
| `ftr_fieldBlacklist` |  <ul><li>Fields Custom Blacklist</li><li>Array</li><li>A list of field CSS classes that should be ignored by the form tracker.</li><li>All other links will be tracked.</li><li>Examples: password field, email field</li></ul> |
| `ftr_fieldWhitelist` |  <ul><li>Fields Custom Whitelist</li><li>Array</li><li>A list of field CSS classes that should be tracked by the form tracker.</li><li>All other links will be ignored.</li><li>Examples: password field, email field</li></ul> |
| `ftr_filterForm` |  <ul><li>Custom Form Filter Function</li><li>A function (or function reference) which should return either `true` or `false`.</li><li>All items returning `true` will be tracked.</li></ul> |
| `ftr_filterField` |  <ul><li>Custom Field Filter Function</li><li>A function (or function reference) which should return either `true` or `false`.</li><li>All items returning `true` will be tracked.</li></ul> |
| `ftr_ctmConfig` |  <ul><li>User-Defined Config</li><li>A custom configuration object with the above properties.</li><li>Use in place of the individual properties.</li></ul> |

### Cart Tracking

|**Destination Name**| **Description**|
|---| ---|
| `cartTracking` |  <ul><li>Cart Tracking</li><li>Set the type of cart event being tracked.</li><li>Cart events will only fire if this is populated.</li><li>Value Options are `cart_add` or `cart_remove`.</li></ul> |
| `cart_sku` |  <ul><li>Cart Item SKU</li><li>The SKU of the item being moved in the cart.</li></ul> |
| `cart_name` |  <ul><li>Cart Item Name</li><li>The name of the item being moved in the cart.</li></ul> |
| `cart_category` |  <ul><li>Cart Item Category</li><li>The category of the item being moved in the cart.</li></ul> |
| `cart_price` |  <ul><li>Cart Item Unit Price</li><li>The price of the item being moved in the cart.</li></ul> |
| `cart_quantity` |  <ul><li>Cart Item Quantity</li><li>The quantity of the item being moved in the cart.</li></ul> |
| `cart_currency` |  <ul><li>Cart Item Currency</li><li>The currency of the item being moved in the cart.</li></ul> |
| `cart_schema` |  <ul><li>Context Schema</li><li>String</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
| `cart_context.data` |  <ul><li>Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `cart_context.data` with the name associated with your value when mapping.</li></ul> |
| `cart_contextObj` |  <ul><li>User-Defined Context</li><li>A custom context object with schema and data properties.</li></ul> |

### Site Search Tracking

|**Destination Name**| **Description**|
|---| ---|
| `sst_terms` |  <ul><li>Search Terms</li><li>Array</li><li>A list of terms used in the site search.</li><li>Search events will only fire if this is populated.</li></ul> |
|`sst_filters`|  <ul><li>Search Filters</li><li>A JSON object defining the filter types and terms.</li></ul> |
| `sst_totalResults` |  <ul><li>Total Results Found</li><li>The total number of results found for the search</li></ul> |
| `sst_pageResults` |  <ul><li>First Page Results</li><li>The number of results displayed on the first page.</li></ul> |
| `sst_schema` |  <ul><li>Context Schema</li><li>String</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
| `sst_context.data` |  <ul><li>Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `sst_context.data` with the name associated with your value when mapping.</li></ul> |
| `sst_contextObj` |  <ul><li>User-Defined Context</li><li>A custom context object with schema and data properties.</li></ul> |

### Structured Event

|**Destination Name**| **Description**|
|---| ---|
| `stctCat` |  <ul><li>Category</li><li>The name of the group of objects you are tracking.</li></ul> |
| `stctActn` |  <ul><li>Action Name</li><li>The name of the user interaction for the objects you are tracking.</li></ul> |
| `stctLabel` |  <ul><li>Label</li><li>An additional name which identifies the specific object you are tracking.</li></ul> |
| `stctProp` |  <ul><li>Property</li><li>An additional item describing the object or action performed on it.</li></ul> |
| `stctVal` |  <ul><li>Value</li><li>An additional decimal number describing the user interaction.</li></ul> |
| `stc_schema` |  <ul><li>Context schema</li><li>String</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
|`stc_context.data`|  <ul><li>Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `stc_context.data` with the name associated with your value when mapping.</li></ul> |
| `stc_contextObj` |  <ul><li>User-Defined Context</li><li>A custom context object with schema and data properties.</li></ul> |

### Unstructured Event

|**Destination Name**| **Description**|
|---| ---|
| `unstctDataSchema` |  <ul><li>Schema</li><li>The JSON schema describing the event. Must be present in an Iglu library.</li></ul> |
| `unstctData.data` |  <ul><li>User-Defined Data</li><li>Data values to be tracked by the event.</li><li>Replace the `data` in `unstctData.data` with the name associated with your value when mapping.</li></ul> |
| `unstctDataObj` |  <ul><li>User-Defined Data Object</li><li>A custom configuration object with the above properties.</li><li>Use in place of the individual properties.</li></ul> |
| `stc_schema` |  <ul><li>Context Schema</li><li>String</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
| `nstc_context.data` |  <ul><li>Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `unstc_context.data` with the name associated with your value when mapping.</li></ul> |
| `unstc_contextObj` |  <ul><li>User-Defined Context</li><li>A custom context object with schema and data properties.</li></ul> |

### Consent Tracking

|**Destination Name**| **Description**|
|---| ---|
| `consentGranted` |  <ul><li>User Granted Consent</li><li>Used to track a user opting into data collection.</li><li>A consent document context is attached to the event if at least the `id` and `version` arguments are supplied.</li></ul> |
| `consentWithdrawn` |  <ul><li>User Withdrew Some Consent</li><li>Used to track a user withdrawing consent for data collection.</li><li>A consent document context is attached to the event if at least the `id` and `version` arguments are supplied.</li></ul> |
| `allConsentWithdrawn` |  <ul><li>User Withdrew All Consent</li><li>Specifies whether all consent should be withdrawn.</li></ul> |
| `con_documentId` |  <ul><li>Consent Document ID</li><li>The consent document is a custom context storing the arguments supplied to the method (in both granted and withdrawn events, this is: `id`, `version`, `name`, and `description`).</li><li>In either consent method, additional documents can be appended to the event by passing an array of consent document self-describing JSONs in the context argument.</li></ul> |
| `con_documentVer` |  <ul><li>Consent Document Version</li><li>Required</li><li>Version of the document granting consent</li></ul> |
| `con_documentName` |  <ul><li>Consent Document Name</li><li>Name of the consent document.</li></ul> |
| `con_documentDesc` |  <ul><li>Consent Document Description</li><li>Description of the consent document.</li></ul> |
| `con_documentExpiry` |  <ul><li>Consent Document Expiration</li><li>Specifies that the user consents to the attached documents until the date-time provided, after which the consent is no longer valid.</li></ul> |
| `unstc_schema` |  <ul><li>Context Schema</li><li>String</li><li>The JSON schema describing the context.</li><li>Must be present in an Iglu library.</li></ul> |
| `nstc_context.data` |  <ul><li>Context Data</li><li>Data values to be tracked by the context.</li><li>Replace the `data` in `unstc_context.data` with the name associated with your value when mapping.</li></ul> |
| `con_contextObj` |  <ul><li>User-Defined Context</li><li>A custom context object with schema and data properties.</li></ul> |

## Vendor Documentation

* [SnowPlow Javascript Tracker documentation](https://docs.snowplowanalytics.com/docs/collecting-data/collecting-from-own-applications/javascript-trackers/)
