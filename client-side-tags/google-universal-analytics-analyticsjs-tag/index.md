---
title: Google Universal Analytics (analytics.js) Tag Setup Guide
description: This article describes how to configure the Google Universal Analytics tag in your iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-universal-analytics-analyticsjs-tag/
---

<blockquote>
As of July 1, 2023, Google Universal Analytics properties stopped processing hits. This tag has been deprecated and no longer available in the tag marketplace. For the current tag, see [Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/).
</blockquote>


Google Analytics (analytics.js) introduces a set of features that change the way data is collected and organized in your Google Analytics account.

## Tag tips

* For more information about Google Analytics (analytics.js), see [About Universal Analytics](http://support.google.com/analytics/bin/answer.py?hl=en&answer=2790010&topic=2790009).
* To use the Tealium implementation for this tag, use mapping instead of Google API functions
* For display advertising support information, see [About Advertising Features](http://support.google.com/analytics/answer/3450482).
* Automatically-generated tracker names take the format of `tealium_X` for the number of accounts defined.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Title**
  * (Required) Enter a descriptive title to identify the tag instance.
* **Tracking ID**
  * (Required) Enter the tracking ID of your Google Universal Analytics (GUA) account.
  * Each property you track in Google Analytics has a unique Property Tracking ID.
  * Example: **UA-12345678-1**
  * Use a comma-separated list to send data for multiple properties.
* **Tracker Name**
  * (Optional) Use this configuration if you have, or plan to have, multiple trackers.
  * Each account ID or GUA property you want to send data to needs to have an associated tracker name.
  * Required when you have more than one copy of this tag running per page.
  * Use a comma-separated list for multiple Tracker Names (for multiple account tracking), which should be the same length as the list you entered for Tracking IDs above.
  * Dashes (-) are not supported in Tracker Names.
* **Domain**
  * (Optional) Set this value to only allow tracking for a specific domain.
  * Enter your domain name for your site.
  * Leave this field blank to have Google Analytics auto-detect the domain.
  * This configuration sets the domain of the cookie that GUA uses to identify the site visitor.
  * If you want to enable tracking across shared sub-domains, omit the ‘www.’ prefix of the domain, for example [www.tealium.com](http://www.tealium.com) would be **tealium.com**. If you want to specifically track sub-domains separately, enter the entire domain address. For example: `www.tealium.com`.
* **Global Object**
  * Not required for most implementations.
  * The name of the Global Object used for the event queue,.
  * If not specified "**ga**" is used.
* **Cross-Tracking Domains**
  * (Optional) Cross-Domain Tracking must be set to **true** for this list to be used.
  * A comma-separated list of domains to use with Cross-Domain Tracking (setAllowLinker).
  * You must use the fully-qualified domain name, such as "my.tealiumiq.com", not the top level domain "tealiumiq.com".
* **Cross-Domain Tracking**
  * (Optional) Select **On** to enable cross-domain tracking.
  * A comma-separated list of domains to use with Cross-Domain Tracking (setAllowLinker).
  * Sets the value for "setAllowLinker" and enables the cross-domain tracking plugin.
  * One or more domains must be specified in the "Cross-Tracking Domains" field or mapped to "crossDomainTrack" to use this feature.
* **Transport**
  * Specifies the transport mechanism with which hits are sent.
* **Enhanced Ecommerce**
  * (Optional) Use the default value (**false**) if you are not sure.
  * Setting to **true** enables enhanced e-commerce functionality.
  * Mapping E-Commerce actions are required for the following actions:
    * `product_click`
    * `detail`
    * `add`
    * `remove`
    * `checkout`
    * `checkout_option`
    * `promo_click`
    * `refund`
  * For more information, see the Google [Enhanced E-Commerce](http://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce) documentation.
  * For more information about how to setup enhanced E-Commerce actions through Tealium iQ Tag Management, see [Google Universal Analytics Tag: Enhanced E-Commerce](https://docs.tealium.com/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/).
* **Enhanced Link Attribution**
  * (Optional) When enabled, a request will be made for `linkid.js` on each page.
  * Use the default (**false**) if you are not sure.
  * Setting to **true** enables [enhanced link](https://developers.google.com/analytics/devguides/collection/analyticsjs/advanced#enhancedlink) link-tracking functionality.
* **Display Advertising Features**
  * (Optional) Enables Google Analytics to collect data about your traffic through the DoubleClick cookie in addition to data collected through the standard Google Analytics implementation.
  * Select **On** to enable GUA to collect data about your traffic through the DoubleClick cookie, in addition to data collected through your standard GUA implementation.
* **Track Screen Views**
  * (Optional) Select **On** to enable GUA's [App/Screen tracking](https://developers.google.com/analytics/devguides/collection/analyticsjs/screens) functionality.
  * When enabled, a separate screenview request will be sent after the initial pageview.
  * Enabling allows this tag to track the content that visitors viewed using an app.
* **Anonymize IP**
  * (Optional) Select **On** to set the last portion of the visitor IP address to zeros before sending it to the GUA data collection network, which lets you comply with privacy policies.
  * Tells Google Analytics to anonymize the information sent by the tracker objects by removing the last octet of the IP address prior to its storage.
  * This will slightly reduce the accuracy of geographic reporting.
* **Enable create before Extensions**
  * Optional.
  * Select **On** to enable to initialize a Tracking ID using GA's "create" method before extensions run.
  * Not applicable when Tracking ID is configured with a mapping.
* **Autofill E-Commerce values**
  * (Optional) Populates product name, unit price and quantity, if not defined.
  * If you do not want the E-Commerce mappings to be altered, you may turn OFF this setting.
* **Auto Send Events**
  * (Optional) If enabled, a default custom event is generated for the following Enhanced E-Commerce actions:
    * `product_click`
    * `add`
    * `remove`
    * `checkout_option`
    * `promo_click`
* **Enable Optimizely Integration**
  * (Optional) Enables automatic GA tracking for Optimizely experiments.
  * Select **On** if you want the tag to track your Optimizely experiments.
* **Clear Vars**
  * Clears items, usually set for the lifetime of the tracker, after each tracking request.
  * Applies only to single page applications.
  * The default value is **Off**.
* **Use AMP Client ID**
  * The Google AMP Client ID lets you uniquely identify users that engage with your content on AMP and non-AMP pages.
  * Select **On** to enable.
  * If you opt-in, Google Analytics uses the AMP Client ID to determine that multiple site events belong to the same user when those users visit AMP pages with a Google AMP viewer.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.


<blockquote>
Analytics tags such as Google Universal Analytics are intended to be loaded on all pages, so the default **All Pages** load rule should be selected.
</blockquote>


## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

* If you are tracking e-commerce data, then we recommend that you add and configure the [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/). Mapping to e-commerce destinations in the mapping toolbox overrides the e-commerce extension's mappings.
* For Google Analytics, additional mapping is not required for basic page tracking. The tag automatically tracks basic page data. Event tracking, campaign tracking, social interaction measurement, content groups, and custom variables are not automatically sent; you must map these manually.

For more information on mapping to Google Universal Analytics, see the [Google Universal Analytics Tag: Advanced Mapping](https://docs.tealium.com/client-side-tags/google-universal-analytics-tag-advanced-mapping/) article.

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tid`|  <ul><li>Tracking ID</li><li>Tracking ID of the Google Analytics property to which you want to send data</li><li>Example: **UA-12345678-1**</li><li>Use a comma-separated list to send data for multiple properties.</li><li>Override Default.</li></ul> |
|`name`|  <ul><li>Tracker Name.</li><li>Override Default.</li></ul> |
|`page`|  <ul><li>Page</li></ul> |
|`title`|  <ul><li>Title</li></ul> |
|`location`|  <ul><li>Location</li></ul> |
|`uid`|  <ul><li>UID</li></ul> |
|`transport`|  <ul><li>Transport</li></ul> |
|`cookieDomain`|  <ul><li>Cookie Domain</li><li>Override Default.</li></ul> |
|`cookieExpires`|  <ul><li>Cookie Expires</li></ul> |
|`legacyCookieDomain`|  <ul><li>Legacy Cookie Domain</li></ul> |
|`legacyHistoryImport`|  <ul><li>Legacy History Import</li><li>Values are **true** or **false**.</li></ul> |
|`nonInteraction`|  <ul><li>Non-Interaction</li></ul> |
|`enhancedLinkAttribution`|  <ul><li>Enhanced Link Attribution</li><li>Values are **true** or **false**.</li></ul> |
|`allowLinker`|  <ul><li>Set Allow Linker</li><li>Values are **true** or **false**.</li></ul> |
|`crossDomainTrack`|  <ul><li>Boolean</li><li>Cross-Domain Tracking</li><li>Auto Linking Domains</li><li>Sets the value for `setAllowLinker` and enables the cross-domain tracking plug-in.</li><li>To use this feature, one or more domains must be specified in the "Cross-Tracking Domains" field or be mapped to `crossDomainTrack`.</li><li>Use a comma-separated list for more than one domain.</li></ul> |
|`siteSpeedSampleRate`|  <ul><li>Site Speed Sample Rate</li></ul> |
|`sampleRate`|  <ul><li>Sample Rate</li></ul> |
|`autofill_params`|  <ul><li>Autofill E-Commerce Params</li><li>Values are **true** or **false**.</li></ul> |
|`optimizely`|  <ul><li>Optimizely Integration</li><li>Values are **true** or **false**.</li></ul> |
|`init_before_extensions`|  <ul><li>Initialize Tracker before Extensions</li><li>Values are **true** or **false**.</li></ul> |
|`sessionControl`|  <ul><li>Session control</li><li>Values are **start** or **end**.</li></ul> |
|`anonymizeIp`|  <ul><li>Anonymize IP</li><li>Tells Google Analytics to anonymize the information sent by the tracker objects by removing the last octet of the IP address prior to its storage.</li><li>Slightly reduces the accuracy of geographic reporting.</li><li>Values are **true** or **false**.</li></ul> |
|`dataSource`|  <ul><li>Data Source</li><li>Examples: web, mobile.</li></ul> |
|`clear_global_vars`|  <ul><li>Clear Vars</li><li>Clears items usually set for the lifetime of the tracker after each tracking request.</li><li>Values are **true** or **false**.</li></ul> |
|`clientId`|  <ul><li>Client ID</li></ul> |
|`useAmpClientId`|  <ul><li>Use AMP Client ID</li><li>Values are **true** or **false**.</li></ul> |
|`set.###`|  <ul><li>Custom Set Command</li></ul> |

### Event

|Variable| Description|
|---| ---|
|`eventCategory`|  <ul><li>(Required) Event Category.</li></ul> |
|`eventAction`|  <ul><li>(Required) Event Action.</li></ul> |
|`eventLabel`|  <ul><li>Event Label</li></ul> |
|`eventValue`|  <ul><li>Event Value</li></ul> |
|`ga_events`|  <ul><li>Array</li><li>GA Event Array</li></ul> |
|`global_event_cb`|  <ul><li>Global View Callback</li></ul> |
|`standard_event_cb`|  <ul><li>Standard Event Callback</li></ul> |

### Campaign

|Variable| Description|
|---| ---|
|`campaignId`|  <ul><li>Campaign ID</li></ul> |
|`campaignName`|  <ul><li>Campaign Name</li></ul> |
|`campaignSource`|  <ul><li>Campaign Source</li></ul> |
|`campaignMedium`|  <ul><li>Campaign Medium</li></ul> |
|`campaignContent`|  <ul><li>Campaign Content</li></ul> |
|`campaignKeyword`|  <ul><li>Campaign Keyword</li></ul> |

### Social

|Variable| Description|
|---| ---|
|`socialNetwork`|  <ul><li>Social Network</li></ul> |
|`socialAction`|  <ul><li>Social Action</li></ul> |
|`socialTarget`|  <ul><li>Social Target</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Transaction ID</li></ul> |
|`affiliation`|  <ul><li>Store Name/ID</li></ul> |
|`revenue`|  <ul><li>Grand Total</li></ul> |
|`shipping`|  <ul><li>Shipping</li></ul> |
|`tax`|  <ul><li>Tax</li></ul> |

### App / Screen Tracking

|Variable| Description|
|---| ---|
|`screenView`|  <ul><li>Track Screen Views</li><li>Enables App/Screen tracking.</li><li>When enabled, a separate screenview request is sent after the initial pageview.</li></ul> |
| `appName` |  <ul><li>Application Name</li></ul> |
| `appId` |  <ul><li>Application ID</li></ul> |
| `appVersion` |  <ul><li>Application Version</li></ul> |
|`appInstallerId`|  <ul><li>Application Installer ID</li></ul> |
|`screenName`|  <ul><li>Screen Name</li></ul> |
|`exception_reason`|  <ul><li>Exception description</li></ul> |

### Content Groups

|Variable| Description|
|---| ---|
|`content_group1`| Content Group 1|
|`content_group2`| Content Group 2|
|`content_group3`| Content Group 4|
|`content_group4`| Content Group 4|
|`content_group5`| Content Group 5|

### Dimensions

|Variable| Description|
|---| ---|
|`dimension1`| Dimension 1|
|`dimension2`| Dimension 2|
|`dimension3`| Dimension 3|
|`dimension4`| Dimension 4|
|`dimension5`| Dimension 5|
|`dimension6`| Dimension 6|
|`dimension7`| Dimension 7|
|`dimension8`| Dimension 8|
|`dimension9`| Dimension 9|
|`dimension10`| Dimension 10|
|`dimension11`| Dimension 11|
|`dimension12`| Dimension 12|
|`dimension13`| Dimension 13|
|`dimension14`| Dimension 14|
|`dimension15`| Dimension 15|
|`dimension16`| Dimension 16|
|`dimension17`| Dimension 17|
|`dimension18`| Dimension 18|
|`dimension19`| Dimension 19|
|`dimension20`| Dimension 20|
|-- Premium Dimension--|
|`dimension21` - `dimension200`| Dimension 21 through Dimension 100|

### Metrics

|Variable| Description|
|---| ---|
|`metric1`| Metric 1|
|`metric2`| Metric 2|
|`metric3`| Metric 3|
|`metric4`| Metric 4|
|`metric5`| Metric 5|
|`metric6`| Metric 6|
|`metric7`| Metric 7|
|`metric8`| Metric 8|
|`metric9`| Metric 9|
|`metric10`| Metric 10|
|`metric11`| Metric 11|
|`metric12`| Metric 12|
|`metric13`| Metric 13|
|`metric14`| Metric 14|
|`metric15`| Metric 15|
|`metric16`| Metric 16|
|`metric17`| Metric 17|
|`metric18`| Metric 18|
|`metric19`| Metric 19|
|`metric20`| Metric 20|
|-- Premium Metric--|
|`metric21` - `metric200`| Metric 21 through Metric 200|

### Enhanced E-Commerce

|Variable| Description|
|---| ---|
|`enh_action`|  <ul><li>E-Commerce Action</li></ul> |
| `enh_event_cb` |  <ul><li>E-Commerce Event Callback</li></ul> |
| `enh_checkout_step` |  <ul><li>Checkout step</li></ul> |
| `enh_checkout_option` |  <ul><li>Checkout option</li></ul> |
| `order_id` |  <ul><li>Transaction ID</li><li>Overrides `_corder`.</li></ul> |
| `affiliation` |  <ul><li>Store Name/ID</li><li>Overrides `_cstore`.</li></ul> |
| `revenue` |  <ul><li>Grand Total</li><li>Overrides `_ctotal`.</li></ul> |
| `shipping` |  <ul><li>Shipping</li><li>Overrides `_cship`.</li></ul> |
| `tax` |  <ul><li>Tax</li><li>Overrides `_ctax`.</li></ul> |
| `coupon` |  <ul><li>Coupon</li><li>Overrides `_cpromo`.</li></ul> |
| `product_id` |  <ul><li>Array</li><li>List of IDs</li></ul> |
| `product_name` |  <ul><li>Array</li><li>List of Names</li></ul> |
| `product_category` |  <ul><li>Array</li><li>List of Categories</li></ul> |
| `product_brand` |  <ul><li>Array</li><li>List of Brands</li></ul> |
| `product_variant` |  <ul><li>Array</li><li>List of Variants</li></ul> |
| `product_unit_price` |  <ul><li>Array</li><li>List of Prices</li></ul> |
| `product_quantity` |  <ul><li>Array</li><li>List of Quantities</li></ul> |
| `product_discount` |  <ul><li>Array</li><li>List of Discounts</li></ul> |
| `product_action_list` |  <ul><li>Product Action List</li></ul> |
| `product_position` |  <ul><li>Array</li><li>Product Position</li></ul> |

### Enh E-Comm: Impressions/Promo

|Variable| Description|
|---| ---|
|`enh_impression_id`|  <ul></ul> |
|`enh_impression_name`|  <ul><li>Array</li><li>Product Impression Name</li></ul> |
|`enh_impression_category`|  <ul><li>Array</li><li>Product Impression Category</li></ul> |
|`enh_impression_brand`|  <ul><li>Array</li><li>Product Impression Brand</li></ul> |
|`enh_impression_variant`|  <ul><li>Array</li><li>Product Impression Variant</li></ul> |
|`enh_impression_price`|  <ul><li>Array</li><li>Product Impression Price</li></ul> |
|`enh_impression_list`|  <ul><li>Array</li><li>Product Impression List</li></ul> |
|`enh_impression_position`|  <ul><li>Array</li><li>Product Impression Position</li></ul> |
|`enh_promo_id`|  <ul><li>Array</li><li>Promotion ID</li></ul> |
|`enh_promo_name`|  <ul><li>Array</li><li>Promotion Name</li></ul> |
|`enh_promo_creative`|  <ul><li>Array</li><li>Promotion Creative</li></ul> |
|`enh_promo_position`|  <ul><li>Array</li><li>Promotion Position</li></ul> |

## Vendor documentation

* [Adding analytics.js to Your Site (**Google Analytics** &gt; **Tracking**)](https://developers.google.com/analytics/devguides/collection/analyticsjs/)
