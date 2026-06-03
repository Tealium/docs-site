---
title: Google Universal Analytics (analytics.js) Tag Setup Guide
description: This article describes how to configure the Google Universal Analytics tag in your iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-universal-analytics-analyticsjs-tag/
---
 As of July 1, 2023, Google Universal Analytics properties stopped processing hits. This tag has been deprecated and no longer available in the tag marketplace. For the current tag, see [Google Analytics 4](). 

Google Analytics (analytics.js) introduces a set of features that change the way data is collected and organized in your Google Analytics account.

## Tag tips

* For more information about Google Analytics (analytics.js), see [About Universal Analytics](http://support.google.com/analytics/bin/answer.py?hl=en&amp;answer=2790010&amp;topic=2790009).
* To use the Tealium implementation for this tag, use mapping instead of Google API functions
* For display advertising support information, see [About Advertising Features](http://support.google.com/analytics/answer/3450482).
* Automatically-generated tracker names take the format of `tealium_X` for the number of accounts defined.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

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
  * If not specified &#34;**ga**&#34; is used.
* **Cross-Tracking Domains**
  * (Optional) Cross-Domain Tracking must be set to **true** for this list to be used.
  * A comma-separated list of domains to use with Cross-Domain Tracking (setAllowLinker).
  * You must use the fully-qualified domain name, such as &#34;my.tealiumiq.com&#34;, not the top level domain &#34;tealiumiq.com&#34;.
* **Cross-Domain Tracking**
  * (Optional) Select **On** to enable cross-domain tracking.
  * A comma-separated list of domains to use with Cross-Domain Tracking (setAllowLinker).
  * Sets the value for &#34;setAllowLinker&#34; and enables the cross-domain tracking plugin.
  * One or more domains must be specified in the &#34;Cross-Tracking Domains&#34; field or mapped to &#34;crossDomainTrack&#34; to use this feature.
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
  * For more information about how to setup enhanced E-Commerce actions through Tealium iQ Tag Management, see [Google Universal Analytics Tag: Enhanced E-Commerce](/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/).
* **Enhanced Link Attribution**
  * (Optional) When enabled, a request will be made for `linkid.js` on each page.
  * Use the default (**false**) if you are not sure.
  * Setting to **true** enables [enhanced link](https://developers.google.com/analytics/devguides/collection/analyticsjs/advanced#enhancedlink) link-tracking functionality.
* **Display Advertising Features**
  * (Optional) Enables Google Analytics to collect data about your traffic through the DoubleClick cookie in addition to data collected through the standard Google Analytics implementation.
  * Select **On** to enable GUA to collect data about your traffic through the DoubleClick cookie, in addition to data collected through your standard GUA implementation.
* **Track Screen Views**
  * (Optional) Select **On** to enable GUA&#39;s [App/Screen tracking](https://developers.google.com/analytics/devguides/collection/analyticsjs/screens) functionality.
  * When enabled, a separate screenview request will be sent after the initial pageview.
  * Enabling allows this tag to track the content that visitors viewed using an app.
* **Anonymize IP**
  * (Optional) Select **On** to set the last portion of the visitor IP address to zeros before sending it to the GUA data collection network, which lets you comply with privacy policies.
  * Tells Google Analytics to anonymize the information sent by the tracker objects by removing the last octet of the IP address prior to its storage.
  * This will slightly reduce the accuracy of geographic reporting.
* **Enable create before Extensions**
  * Optional.
  * Select **On** to enable to initialize a Tracking ID using GA&#39;s &#34;create&#34; method before extensions run.
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

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

Analytics tags such as Google Universal Analytics are intended to be loaded on all pages, so the default **All Pages** load rule should be selected.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

* If you are tracking e-commerce data, then we recommend that you add and configure the [E-Commerce Extension](). Mapping to e-commerce destinations in the mapping toolbox overrides the e-commerce extension&#39;s mappings.
* For Google Analytics, additional mapping is not required for basic page tracking. The tag automatically tracks basic page data. Event tracking, campaign tracking, social interaction measurement, content groups, and custom variables are not automatically sent; you must map these manually.

For more information on mapping to Google Universal Analytics, see the [Google Universal Analytics Tag: Advanced Mapping](/client-side-tags/google-universal-analytics-tag-advanced-mapping/) article.

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tid`|  &lt;ul&gt;&lt;li&gt;Tracking ID&lt;/li&gt;&lt;li&gt;Tracking ID of the Google Analytics property to which you want to send data&lt;/li&gt;&lt;li&gt;Example: **UA-12345678-1**&lt;/li&gt;&lt;li&gt;Use a comma-separated list to send data for multiple properties.&lt;/li&gt;&lt;li&gt;Override Default.&lt;/li&gt;&lt;/ul&gt; |
|`name`|  &lt;ul&gt;&lt;li&gt;Tracker Name.&lt;/li&gt;&lt;li&gt;Override Default.&lt;/li&gt;&lt;/ul&gt; |
|`page`|  &lt;ul&gt;&lt;li&gt;Page&lt;/li&gt;&lt;/ul&gt; |
|`title`|  &lt;ul&gt;&lt;li&gt;Title&lt;/li&gt;&lt;/ul&gt; |
|`location`|  &lt;ul&gt;&lt;li&gt;Location&lt;/li&gt;&lt;/ul&gt; |
|`uid`|  &lt;ul&gt;&lt;li&gt;UID&lt;/li&gt;&lt;/ul&gt; |
|`transport`|  &lt;ul&gt;&lt;li&gt;Transport&lt;/li&gt;&lt;/ul&gt; |
|`cookieDomain`|  &lt;ul&gt;&lt;li&gt;Cookie Domain&lt;/li&gt;&lt;li&gt;Override Default.&lt;/li&gt;&lt;/ul&gt; |
|`cookieExpires`|  &lt;ul&gt;&lt;li&gt;Cookie Expires&lt;/li&gt;&lt;/ul&gt; |
|`legacyCookieDomain`|  &lt;ul&gt;&lt;li&gt;Legacy Cookie Domain&lt;/li&gt;&lt;/ul&gt; |
|`legacyHistoryImport`|  &lt;ul&gt;&lt;li&gt;Legacy History Import&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`nonInteraction`|  &lt;ul&gt;&lt;li&gt;Non-Interaction&lt;/li&gt;&lt;/ul&gt; |
|`enhancedLinkAttribution`|  &lt;ul&gt;&lt;li&gt;Enhanced Link Attribution&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`allowLinker`|  &lt;ul&gt;&lt;li&gt;Set Allow Linker&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`crossDomainTrack`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Cross-Domain Tracking&lt;/li&gt;&lt;li&gt;Auto Linking Domains&lt;/li&gt;&lt;li&gt;Sets the value for `setAllowLinker` and enables the cross-domain tracking plug-in.&lt;/li&gt;&lt;li&gt;To use this feature, one or more domains must be specified in the &#34;Cross-Tracking Domains&#34; field or be mapped to `crossDomainTrack`.&lt;/li&gt;&lt;li&gt;Use a comma-separated list for more than one domain.&lt;/li&gt;&lt;/ul&gt; |
|`siteSpeedSampleRate`|  &lt;ul&gt;&lt;li&gt;Site Speed Sample Rate&lt;/li&gt;&lt;/ul&gt; |
|`sampleRate`|  &lt;ul&gt;&lt;li&gt;Sample Rate&lt;/li&gt;&lt;/ul&gt; |
|`autofill_params`|  &lt;ul&gt;&lt;li&gt;Autofill E-Commerce Params&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`optimizely`|  &lt;ul&gt;&lt;li&gt;Optimizely Integration&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`init_before_extensions`|  &lt;ul&gt;&lt;li&gt;Initialize Tracker before Extensions&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`sessionControl`|  &lt;ul&gt;&lt;li&gt;Session control&lt;/li&gt;&lt;li&gt;Values are **start** or **end**.&lt;/li&gt;&lt;/ul&gt; |
|`anonymizeIp`|  &lt;ul&gt;&lt;li&gt;Anonymize IP&lt;/li&gt;&lt;li&gt;Tells Google Analytics to anonymize the information sent by the tracker objects by removing the last octet of the IP address prior to its storage.&lt;/li&gt;&lt;li&gt;Slightly reduces the accuracy of geographic reporting.&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`dataSource`|  &lt;ul&gt;&lt;li&gt;Data Source&lt;/li&gt;&lt;li&gt;Examples: web, mobile.&lt;/li&gt;&lt;/ul&gt; |
|`clear_global_vars`|  &lt;ul&gt;&lt;li&gt;Clear Vars&lt;/li&gt;&lt;li&gt;Clears items usually set for the lifetime of the tracker after each tracking request.&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`clientId`|  &lt;ul&gt;&lt;li&gt;Client ID&lt;/li&gt;&lt;/ul&gt; |
|`useAmpClientId`|  &lt;ul&gt;&lt;li&gt;Use AMP Client ID&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`set.###`|  &lt;ul&gt;&lt;li&gt;Custom Set Command&lt;/li&gt;&lt;/ul&gt; |

### Event

|Variable| Description|
|---| ---|
|`eventCategory`|  &lt;ul&gt;&lt;li&gt;(Required) Event Category.&lt;/li&gt;&lt;/ul&gt; |
|`eventAction`|  &lt;ul&gt;&lt;li&gt;(Required) Event Action.&lt;/li&gt;&lt;/ul&gt; |
|`eventLabel`|  &lt;ul&gt;&lt;li&gt;Event Label&lt;/li&gt;&lt;/ul&gt; |
|`eventValue`|  &lt;ul&gt;&lt;li&gt;Event Value&lt;/li&gt;&lt;/ul&gt; |
|`ga_events`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;GA Event Array&lt;/li&gt;&lt;/ul&gt; |
|`global_event_cb`|  &lt;ul&gt;&lt;li&gt;Global View Callback&lt;/li&gt;&lt;/ul&gt; |
|`standard_event_cb`|  &lt;ul&gt;&lt;li&gt;Standard Event Callback&lt;/li&gt;&lt;/ul&gt; |

### Campaign

|Variable| Description|
|---| ---|
|`campaignId`|  &lt;ul&gt;&lt;li&gt;Campaign ID&lt;/li&gt;&lt;/ul&gt; |
|`campaignName`|  &lt;ul&gt;&lt;li&gt;Campaign Name&lt;/li&gt;&lt;/ul&gt; |
|`campaignSource`|  &lt;ul&gt;&lt;li&gt;Campaign Source&lt;/li&gt;&lt;/ul&gt; |
|`campaignMedium`|  &lt;ul&gt;&lt;li&gt;Campaign Medium&lt;/li&gt;&lt;/ul&gt; |
|`campaignContent`|  &lt;ul&gt;&lt;li&gt;Campaign Content&lt;/li&gt;&lt;/ul&gt; |
|`campaignKeyword`|  &lt;ul&gt;&lt;li&gt;Campaign Keyword&lt;/li&gt;&lt;/ul&gt; |

### Social

|Variable| Description|
|---| ---|
|`socialNetwork`|  &lt;ul&gt;&lt;li&gt;Social Network&lt;/li&gt;&lt;/ul&gt; |
|`socialAction`|  &lt;ul&gt;&lt;li&gt;Social Action&lt;/li&gt;&lt;/ul&gt; |
|`socialTarget`|  &lt;ul&gt;&lt;li&gt;Social Target&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Transaction ID&lt;/li&gt;&lt;/ul&gt; |
|`affiliation`|  &lt;ul&gt;&lt;li&gt;Store Name/ID&lt;/li&gt;&lt;/ul&gt; |
|`revenue`|  &lt;ul&gt;&lt;li&gt;Grand Total&lt;/li&gt;&lt;/ul&gt; |
|`shipping`|  &lt;ul&gt;&lt;li&gt;Shipping&lt;/li&gt;&lt;/ul&gt; |
|`tax`|  &lt;ul&gt;&lt;li&gt;Tax&lt;/li&gt;&lt;/ul&gt; |

### App / Screen Tracking

|Variable| Description|
|---| ---|
|`screenView`|  &lt;ul&gt;&lt;li&gt;Track Screen Views&lt;/li&gt;&lt;li&gt;Enables App/Screen tracking.&lt;/li&gt;&lt;li&gt;When enabled, a separate screenview request is sent after the initial pageview.&lt;/li&gt;&lt;/ul&gt; |
| `appName` |  &lt;ul&gt;&lt;li&gt;Application Name&lt;/li&gt;&lt;/ul&gt; |
| `appId` |  &lt;ul&gt;&lt;li&gt;Application ID&lt;/li&gt;&lt;/ul&gt; |
| `appVersion` |  &lt;ul&gt;&lt;li&gt;Application Version&lt;/li&gt;&lt;/ul&gt; |
|`appInstallerId`|  &lt;ul&gt;&lt;li&gt;Application Installer ID&lt;/li&gt;&lt;/ul&gt; |
|`screenName`|  &lt;ul&gt;&lt;li&gt;Screen Name&lt;/li&gt;&lt;/ul&gt; |
|`exception_reason`|  &lt;ul&gt;&lt;li&gt;Exception description&lt;/li&gt;&lt;/ul&gt; |

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
|`enh_action`|  &lt;ul&gt;&lt;li&gt;E-Commerce Action&lt;/li&gt;&lt;/ul&gt; |
| `enh_event_cb` |  &lt;ul&gt;&lt;li&gt;E-Commerce Event Callback&lt;/li&gt;&lt;/ul&gt; |
| `enh_checkout_step` |  &lt;ul&gt;&lt;li&gt;Checkout step&lt;/li&gt;&lt;/ul&gt; |
| `enh_checkout_option` |  &lt;ul&gt;&lt;li&gt;Checkout option&lt;/li&gt;&lt;/ul&gt; |
| `order_id` |  &lt;ul&gt;&lt;li&gt;Transaction ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
| `affiliation` |  &lt;ul&gt;&lt;li&gt;Store Name/ID&lt;/li&gt;&lt;li&gt;Overrides `_cstore`.&lt;/li&gt;&lt;/ul&gt; |
| `revenue` |  &lt;ul&gt;&lt;li&gt;Grand Total&lt;/li&gt;&lt;li&gt;Overrides `_ctotal`.&lt;/li&gt;&lt;/ul&gt; |
| `shipping` |  &lt;ul&gt;&lt;li&gt;Shipping&lt;/li&gt;&lt;li&gt;Overrides `_cship`.&lt;/li&gt;&lt;/ul&gt; |
| `tax` |  &lt;ul&gt;&lt;li&gt;Tax&lt;/li&gt;&lt;li&gt;Overrides `_ctax`.&lt;/li&gt;&lt;/ul&gt; |
| `coupon` |  &lt;ul&gt;&lt;li&gt;Coupon&lt;/li&gt;&lt;li&gt;Overrides `_cpromo`.&lt;/li&gt;&lt;/ul&gt; |
| `product_id` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of IDs&lt;/li&gt;&lt;/ul&gt; |
| `product_name` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Names&lt;/li&gt;&lt;/ul&gt; |
| `product_category` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Categories&lt;/li&gt;&lt;/ul&gt; |
| `product_brand` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Brands&lt;/li&gt;&lt;/ul&gt; |
| `product_variant` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Variants&lt;/li&gt;&lt;/ul&gt; |
| `product_unit_price` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices&lt;/li&gt;&lt;/ul&gt; |
| `product_quantity` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities&lt;/li&gt;&lt;/ul&gt; |
| `product_discount` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Discounts&lt;/li&gt;&lt;/ul&gt; |
| `product_action_list` |  &lt;ul&gt;&lt;li&gt;Product Action List&lt;/li&gt;&lt;/ul&gt; |
| `product_position` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Position&lt;/li&gt;&lt;/ul&gt; |

### Enh E-Comm: Impressions/Promo

|Variable| Description|
|---| ---|
|`enh_impression_id`|  &lt;ul&gt;&lt;/ul&gt; |
|`enh_impression_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Name&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_category`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Category&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_brand`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Brand&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_variant`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Variant&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Price&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_list`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression List&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_position`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Position&lt;/li&gt;&lt;/ul&gt; |
|`enh_promo_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion ID&lt;/li&gt;&lt;/ul&gt; |
|`enh_promo_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion Name&lt;/li&gt;&lt;/ul&gt; |
|`enh_promo_creative`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion Creative&lt;/li&gt;&lt;/ul&gt; |
|`enh_promo_position`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion Position&lt;/li&gt;&lt;/ul&gt; |

## Vendor documentation

* [Adding analytics.js to Your Site (**Google Analytics** &amp;gt; **Tracking**)](https://developers.google.com/analytics/devguides/collection/analyticsjs/)
