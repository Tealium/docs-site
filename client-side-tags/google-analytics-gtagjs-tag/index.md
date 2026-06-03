---
title: Google Analytics (gtag.js) Tag Setup Guide
description: This article describes how to set up the Google Analytics (gtag.js) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-analytics-gtagjs-tag/
---
Google Analytics provides APIs to collect, configure, and report on user-interactions with your online content. Using gtag.js lets you benefit from the latest tracking features and integrations as they become available.

## Tag tips

* Use mappings to:
  * Dynamically override the E-Commerce extension values.
  * Setup event triggers.
  * Add custom Metrics, Dimensions, and Content Groups.
* Replace `cst` in custom event variables with the event name you want.
* Supports the following E-Commerce extension values:
  * Order ID
  * Order Total
  * Shipping Amount
  * Tax Amount
  * Store
  * Promo Code
  * Customer ID
  * List of Product IDs
  * List of Names
  * List of Brands
  * List of Categories
  * List of Prices
  * List of Quantities
  * List of Discounts

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Tracking ID**
  * Tracking ID of the Google Analytics property to which you want to send data  
  * Example: `UA-XXXXXX-13`  
  * Use a comma-separated list to send data for multiple properties.
Enable [App &#43; Web](https://developers.google.com/analytics/devguides/collection/app-web/basic-tag) by including the measurement ID in the Tracking ID value. For example; `UA-XXXXXX-13,G-XXXXXXXXXX`
* **Global Object**
  * The name of the Global Object used for the event queue.
  * If not specified, &#34;gtag&#34; is used.
  * Not required for most implementations.
* **Cross-Tracking Domains**
  * A comma-separated list of domains to use with Cross-Domain Tracking (`setAllowLinker`).
  * To use this list, Cross-Domain Tracking must be set to **true**.
  * Should be the top level domain, such as **tealiumiq.com**.
* **Cross-Domain Tracking**
  * Sets the value for `setAllowLinker` and enables the cross-domain tracking plug-in.
  * To use this feature, one or more domains must be specified in the &#34;Cross-Tracking Domains&#34; field or be mapped to `crossDomainTrack`.
* **Transport Type**
  * Specifies the transport mechanism with which hits are sent.
* **Allow Advertising Features**
  * Enables Google Analytics to collect data about your traffic through the Google Ad Manager (DoubleClick) cookie, in addition to data collected through the standard Google Analytics implementation.
  * Setting this to **Off** disables all advertising, reporting, and remarketing features, overrides any property settings established in the Google Analytics user interface.
* **Enhanced Link Attribution**
  * If unsure, use the default value (**false**).
  * Google Analytics provides enhanced link attribution to improve the accuracy of report data by automatically differentiating between multiple links to the same URL on a single page and using link element IDs.
* **Track Screen Views**
  * Enables App/Screen tracking.
  * When enabled, a separate screenview request is sent after the initial pageview.
* **Anonymize IP**
  * Tells Google Analytics to anonymize the information sent by the tracker objects by removing the last octet of the IP address prior to its storage.
  * Slightly reduces the accuracy of geographic reporting.
* **Clear Vars**
  * Clears items usually set for the lifetime of the tracker after each tracking request.
* **Optimize Container ID**
  * Sets the `optimize_id` and enables the Google Optimize plug-in.
  * This ID is found in your Optimize accounts page.
  * Example: **GTM-XXXXXX**
* **Use AMP Client ID**
  * The Google AMP Client ID lets you uniquely identify users that engage with your content on AMP and non-AMP pages.
  * If you opt-in, Google Analytics uses the AMP Client ID to determine that multiple site events belong to the same user when those users visit AMP pages through a Google AMP viewer.
* **Data Layer Name**
  * By default, the data layer initiated and referenced by the global site tag is named `dataLayer`.
  * Only rename the data layer if your project requires a separate name.
* **Allow Anchor**
  * When true, the `_ga` parameter is added to the query portion of the URL rather than the anchor portion (&#34;#&#34;).

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tracking_id`|  &lt;ul&gt;&lt;li&gt;Tracking ID&lt;/li&gt;&lt;li&gt;Tracking ID of the Google Analytics property to which you want to send data&lt;/li&gt;&lt;li&gt;Example: `UA-XXXXXX-13`&lt;/li&gt;&lt;li&gt;Use a comma-separated list to send data for multiple properties.&lt;/li&gt;&lt;/ul&gt; |
|`transport_type`|  &lt;ul&gt;&lt;li&gt;Transport type&lt;/li&gt;&lt;/ul&gt; |
|`page_title`|  &lt;ul&gt;&lt;li&gt;Page Title&lt;/li&gt;&lt;/ul&gt; |
|`page_location`|  &lt;ul&gt;&lt;li&gt;Page Location&lt;/li&gt;&lt;/ul&gt; |
| `page_path` |  &lt;ul&gt;&lt;li&gt;Page Path&lt;/li&gt;&lt;/ul&gt; |
|`cookie_name`|  &lt;ul&gt;&lt;li&gt;Cookie Name&lt;/li&gt;&lt;/ul&gt; |
| `cookie_domain` |  &lt;ul&gt;&lt;li&gt;Cookie Domain&lt;/li&gt;&lt;/ul&gt; |
| `cookie_expires` |  &lt;ul&gt;&lt;li&gt;Cookie Expires&lt;/li&gt;&lt;/ul&gt; |
|`cookie_prefix`|  &lt;ul&gt;&lt;li&gt;Cookie prefix&lt;/li&gt;&lt;/ul&gt; |
|`cookie_update`|  &lt;ul&gt;&lt;li&gt;Cookie update&lt;/li&gt;&lt;/ul&gt; |
|`config.allow_google_signals`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Allow advertising features.&lt;/li&gt;&lt;/ul&gt; |
|`allow_ad_personalization_signals`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Allow ad personalization signals.&lt;/li&gt;&lt;li&gt;Enables Google Analytics to collect data about your traffic through the Google Ad Manager (DoubleClick) cookie, in addition to data collected through the standard Google Analytics implementation.&lt;/li&gt;&lt;/ul&gt; |
|`config.link_attribution.cookie_name`|  &lt;ul&gt;&lt;li&gt;Link Attribution Cookie Name&lt;/li&gt;&lt;/ul&gt; |
|`config.link_attribution.cookie_expires`|  &lt;ul&gt;&lt;li&gt;Link Attribution Cookie Expiration&lt;/li&gt;&lt;/ul&gt; |
|`config.link_attribution.levels`|  &lt;ul&gt;&lt;li&gt;Link Attribution Levels&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.id`|  &lt;ul&gt;&lt;li&gt;Campaign ID&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.name`|  &lt;ul&gt;&lt;li&gt;Campaign Name&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.source`|  &lt;ul&gt;&lt;li&gt;Campaign Source&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.medium`|  &lt;ul&gt;&lt;li&gt;Campaign Medium&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.content`|  &lt;ul&gt;&lt;li&gt;Campaign Content&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.term`|  &lt;ul&gt;&lt;li&gt;Campaign Term/Keyword&lt;/li&gt;&lt;/ul&gt; |
|`config.anonymize_ip`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Anonymize IP&lt;/li&gt;&lt;li&gt;Tells Google Analytics to anonymize the information sent by the tracker objects by removing the last octet of the IP address prior to its storage.&lt;/li&gt;&lt;li&gt;Slightly reduces the accuracy of geographic reporting.&lt;/li&gt;&lt;/ul&gt; |
|`clear_global_vars`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Clear Vars&lt;/li&gt;&lt;li&gt;Clears items usually set for the lifetime of the tracker after each tracking request.&lt;/li&gt;&lt;/ul&gt; |
|`config.optimize_id`|  &lt;ul&gt;&lt;li&gt;Optimize Container ID&lt;/li&gt;&lt;li&gt;Sets the `optimize_id` and enables the Google Optimize plugin.&lt;/li&gt;&lt;li&gt;This ID is found in your Optimize accounts page.&lt;/li&gt;&lt;li&gt;Example: **GTM-XXXXXX**&lt;/li&gt;&lt;/ul&gt; |
|`config.use_amp_client_id`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Use AMP Client ID&lt;/li&gt;&lt;li&gt;The Google AMP Client ID lets you uniquely identify users that engage with your content on AMP and non-AMP pages.&lt;/li&gt;&lt;li&gt;If you opt-in, Google Analytics uses the AMP Client ID to determine that multiple site events belong to the same user when those users visit AMP pages through a Google AMP viewer.&lt;/li&gt;&lt;/ul&gt; |
| `config.sample_rate` |  &lt;ul&gt;&lt;li&gt;Sample Rate&lt;/li&gt;&lt;/ul&gt; |
|`config.site_speed_sample_rate`|  &lt;ul&gt;&lt;li&gt;Site Speed Sample Rate&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;User ID&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`&lt;/li&gt;&lt;/ul&gt; |
|`config.client_id`|  &lt;ul&gt;&lt;li&gt;Client ID&lt;/li&gt;&lt;/ul&gt; |

### Event

|Variable| Description|
|---| ---|
| `event_name` |  &lt;ul&gt;&lt;li&gt;Event Action&lt;/li&gt;&lt;/ul&gt; |
| `event.event_category` |  &lt;ul&gt;&lt;li&gt;Event Category&lt;/li&gt;&lt;/ul&gt; |
| `event.event_label` |  &lt;ul&gt;&lt;li&gt;Event Label&lt;/li&gt;&lt;/ul&gt; |
| `event.value` |  &lt;ul&gt;&lt;li&gt;Event / Timing Value&lt;/li&gt;&lt;/ul&gt; |
| `event.name` |  &lt;ul&gt;&lt;li&gt;Timing Variable Name&lt;/li&gt;&lt;/ul&gt; |
| `event.description` |  &lt;ul&gt;&lt;li&gt;Exception Description&lt;/li&gt;&lt;/ul&gt; |
| `event.non_interaction` |  &lt;ul&gt;&lt;li&gt;Non-Interaction&lt;/li&gt;&lt;/ul&gt; |
|`event.fatal`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Fatal Error&lt;/li&gt;&lt;/ul&gt; |
| `event.search_term` |  &lt;ul&gt;&lt;li&gt;Search Term&lt;/li&gt;&lt;/ul&gt; |
| `event.method` |  &lt;ul&gt;&lt;li&gt;Method&lt;/li&gt;&lt;/ul&gt; |
| `event.content_type` |  &lt;ul&gt;&lt;li&gt;Content Type&lt;/li&gt;&lt;/ul&gt; |
| `event.content_id` |  &lt;ul&gt;&lt;li&gt;Content ID&lt;/li&gt;&lt;/ul&gt; |
| `event.destination` |  &lt;ul&gt;&lt;li&gt;Destination&lt;/li&gt;&lt;/ul&gt; |
|`event.start_date`|  &lt;ul&gt;&lt;li&gt;Start Date&lt;/li&gt;&lt;li&gt;Date format is YYYYMMDD.&lt;/li&gt;&lt;/ul&gt; |
|`event.end_date`|  &lt;ul&gt;&lt;li&gt;End Date&lt;/li&gt;&lt;li&gt;Date format is YYYYMMDD.&lt;/li&gt;&lt;/ul&gt; |
| `event.custom` |  &lt;ul&gt;&lt;li&gt;Custom Event Data&lt;/li&gt;&lt;/ul&gt; |
|`event.anonymize_ip`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Anonymize IP&lt;/li&gt;&lt;li&gt;Tells Google Analytics to anonymize the information sent by the tracker objects by removing the last octet of the IP address prior to its storage.&lt;/li&gt;&lt;li&gt;Slightly reduces the accuracy of geographic reporting.&lt;/li&gt;&lt;/ul&gt; |
| `event.send_to` |  &lt;ul&gt;&lt;li&gt;Override Default Routing&lt;/li&gt;&lt;/ul&gt; |
| `event.event_callback` |  &lt;ul&gt;&lt;li&gt;Event callback&lt;/li&gt;&lt;/ul&gt; |

### App / Screen tracking

|Variable| Description|
|---| ---|
|`screen_view`|  &lt;ul&gt;&lt;li&gt;Boolean.&lt;/li&gt;&lt;li&gt;Values accepted to activate: &#34;true&#34;, &#34;on&#34;)&lt;/li&gt;&lt;li&gt;Track Screen Views&lt;/li&gt;&lt;li&gt;Enables App/Screen tracking.&lt;/li&gt;&lt;li&gt;When enabled, a separate screenview request is sent after the initial pageview.&lt;/li&gt;&lt;/ul&gt; |
| `event.screen_name` |  &lt;ul&gt;&lt;li&gt;Screen Name&lt;/li&gt;&lt;/ul&gt; |
| `config.app_name` |  &lt;ul&gt;&lt;li&gt;Application Name&lt;/li&gt;&lt;/ul&gt; |
| `config.app_id` |  &lt;ul&gt;&lt;li&gt;Application ID&lt;/li&gt;&lt;/ul&gt; |
| `config.app_version` |  &lt;ul&gt;&lt;li&gt;Application Version&lt;/li&gt;&lt;/ul&gt; |
|`IDconfig.app_installer_id`|  &lt;ul&gt;&lt;li&gt;Application Installer&lt;/li&gt;&lt;/ul&gt; |

### Content groups

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
|`checkout_step`|  &lt;ul&gt;&lt;li&gt;Number&lt;/li&gt;&lt;li&gt;Checkout step.&lt;/li&gt;&lt;/ul&gt; |
| `checkout_option` |  &lt;ul&gt;&lt;li&gt;Checkout Option.&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;Currency&lt;/li&gt;&lt;li&gt;Overrides `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|`order_id`|  &lt;ul&gt;&lt;li&gt;Transaction ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;Value/Order Total&lt;/li&gt;&lt;li&gt;Overrides `_ctotal`.&lt;/li&gt;&lt;/ul&gt; |
| `order_shipping` |  &lt;ul&gt;&lt;li&gt;Shipping Amount&lt;/li&gt;&lt;li&gt;Overrides `_cship`.&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;Tax Amount&lt;/li&gt;&lt;li&gt;Overrides `_ctax`.&lt;/li&gt;&lt;/ul&gt; |
|`order_store`|  &lt;ul&gt;&lt;li&gt;Affiliation/Store&lt;/li&gt;&lt;li&gt;Overrides `_cstore`.&lt;/li&gt;&lt;/ul&gt; |
| `order_coupon_code` |  &lt;ul&gt;&lt;li&gt;Promo Code/Coupon&lt;/li&gt;&lt;li&gt;Overrides `_cpromo`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;User ID&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of IDs&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Names&lt;/li&gt;&lt;li&gt;`Overrides _cprodname`.&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Brands&lt;/li&gt;&lt;li&gt;Overrides `_cbrand`.&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Categories&lt;/li&gt;&lt;li&gt;Overrides `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|`product_variant`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Variants&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_discount`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Discounts&lt;/li&gt;&lt;li&gt;Overrides `_cdisc`.&lt;/li&gt;&lt;/ul&gt; |
|`product_promo_code`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Promo Codes/Coupons&lt;/li&gt;&lt;/ul&gt; |
|`product_action_list`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Action List&lt;/li&gt;&lt;/ul&gt; |
|`product_list_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Name&lt;/li&gt;&lt;/ul&gt; |
|`product_list_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product List ID&lt;/li&gt;&lt;/ul&gt; |
|`product_list_position`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Position&lt;/li&gt;&lt;/ul&gt; |
|`product_location_id`|  &lt;ul&gt;&lt;li&gt;Product Location ID&lt;/li&gt;&lt;/ul&gt; |

### Enh E-Comm engagement

|Variable| Description|
|---| ---|
|`impression_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression ID&lt;/li&gt;&lt;/ul&gt; |
|`impression_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Name&lt;/li&gt;&lt;/ul&gt; |
| `impression_category` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Category&lt;/li&gt;&lt;/ul&gt; |
|`impression_brand`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Brand&lt;/li&gt;&lt;/ul&gt; |
|`impression_variant`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Variant&lt;/li&gt;&lt;/ul&gt; |
|`impression_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Price&lt;/li&gt;&lt;/ul&gt; |
|`impression_list_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression List&lt;/li&gt;&lt;/ul&gt; |
|`impression_item_list_id`|  &lt;ul&gt;&lt;li&gt;Product Impression List ID&lt;/li&gt;&lt;/ul&gt; |
|`impression_list_position`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Product Impression Position&lt;/li&gt;&lt;/ul&gt; |
|```promo_id```|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion ID&lt;/li&gt;&lt;/ul&gt; |
|`promo_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion Name&lt;/li&gt;&lt;/ul&gt; |
|`promo_creative_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion Creative&lt;/li&gt;&lt;/ul&gt; |
| `promo_creative_slot` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion Position&lt;/li&gt;&lt;/ul&gt; |
| `promo_location_id` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Promotion Location&lt;/li&gt;&lt;/ul&gt; |

### App&#43;Web travel

|Variable| Description|
|---| ---|
|`event.trip_type`|  &lt;ul&gt;&lt;li&gt;Trip Type&lt;/li&gt;&lt;/ul&gt; |
|`start_date`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Start Date&lt;/li&gt;&lt;/ul&gt; |
|`end_date`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;End Date&lt;/li&gt;&lt;/ul&gt; |
|`origin`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Origin&lt;/li&gt;&lt;/ul&gt; |
|`destination`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Destination&lt;/li&gt;&lt;/ul&gt; |
|`flight_number`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Flight Number&lt;/li&gt;&lt;/ul&gt; |
|`travel_class`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Travel Class&lt;/li&gt;&lt;/ul&gt; |
|`fare_product`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Fare Product&lt;/li&gt;&lt;/ul&gt; |
|`booking_code`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Booking Code&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.total`|  &lt;ul&gt;&lt;li&gt;Total Number of Passengers&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.adult`|  &lt;ul&gt;&lt;li&gt;Number of Adult Passengers&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.child`|  &lt;ul&gt;&lt;li&gt;Number of Child Passengers&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.infant_in_lap`|  &lt;ul&gt;&lt;li&gt;Number of Infant Passengers in Lap&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.infant_in_seat`|  &lt;ul&gt;&lt;li&gt;Number of Infant Passengers in Seat&lt;/li&gt;&lt;/ul&gt; |

### App&#43;Web game

|Variable| Description|
|---| ---|
|`event.achievement_id`|  &lt;ul&gt;&lt;li&gt;Achievement ID&lt;/li&gt;&lt;/ul&gt; |
|`event.character`|  &lt;ul&gt;&lt;li&gt;Character&lt;/li&gt;&lt;/ul&gt; |
|`event.group_id`|  &lt;ul&gt;&lt;li&gt;Group ID&lt;/li&gt;&lt;/ul&gt; |
|`event.item_name`|  &lt;ul&gt;&lt;li&gt;Item Name&lt;/li&gt;&lt;/ul&gt; |
|`event.level`|  &lt;ul&gt;&lt;li&gt;Level&lt;/li&gt;&lt;/ul&gt; |
|`event.level_name`|  &lt;ul&gt;&lt;li&gt;Level Name&lt;/li&gt;&lt;/ul&gt; |
|`event.score`|  &lt;ul&gt;&lt;li&gt;Score&lt;/li&gt;&lt;/ul&gt; |
|`event.success`|  &lt;ul&gt;&lt;li&gt;Success&lt;/li&gt;&lt;/ul&gt; |
|`event.virtual_currency_name`|  &lt;ul&gt;&lt;li&gt;Virtual Currency Name&lt;/li&gt;&lt;/ul&gt; |

### IAB Transparency and Consent Framework v2

|Variable| Description|
|---| ---|
|`gtag_enable_tcf_support`|  &lt;ul&gt;&lt;li&gt;Enable TCF Support&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |

## Google Analytics 4 support

Google Analytics 4 (GA4) is currently supported through the App and Web mappings for this tag.
