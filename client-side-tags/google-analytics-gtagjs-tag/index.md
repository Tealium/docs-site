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

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Tracking ID**
  * Tracking ID of the Google Analytics property to which you want to send data  
  * Example: `UA-XXXXXX-13`  
  * Use a comma-separated list to send data for multiple properties.

<blockquote>
Enable [App + Web](https://developers.google.com/analytics/devguides/collection/app-web/basic-tag) by including the measurement ID in the Tracking ID value. For example; `UA-XXXXXX-13,G-XXXXXXXXXX`
</blockquote>

* **Global Object**
  * The name of the Global Object used for the event queue.
  * If not specified, "gtag" is used.
  * Not required for most implementations.
* **Cross-Tracking Domains**
  * A comma-separated list of domains to use with Cross-Domain Tracking (`setAllowLinker`).
  * To use this list, Cross-Domain Tracking must be set to **true**.
  * Should be the top level domain, such as **tealiumiq.com**.
* **Cross-Domain Tracking**
  * Sets the value for `setAllowLinker` and enables the cross-domain tracking plug-in.
  * To use this feature, one or more domains must be specified in the "Cross-Tracking Domains" field or be mapped to `crossDomainTrack`.
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
  * When true, the `_ga` parameter is added to the query portion of the URL rather than the anchor portion ("#").

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tracking_id`|  <ul><li>Tracking ID</li><li>Tracking ID of the Google Analytics property to which you want to send data</li><li>Example: `UA-XXXXXX-13`</li><li>Use a comma-separated list to send data for multiple properties.</li></ul> |
|`transport_type`|  <ul><li>Transport type</li></ul> |
|`page_title`|  <ul><li>Page Title</li></ul> |
|`page_location`|  <ul><li>Page Location</li></ul> |
| `page_path` |  <ul><li>Page Path</li></ul> |
|`cookie_name`|  <ul><li>Cookie Name</li></ul> |
| `cookie_domain` |  <ul><li>Cookie Domain</li></ul> |
| `cookie_expires` |  <ul><li>Cookie Expires</li></ul> |
|`cookie_prefix`|  <ul><li>Cookie prefix</li></ul> |
|`cookie_update`|  <ul><li>Cookie update</li></ul> |
|`config.allow_google_signals`|  <ul><li>Boolean</li><li>Allow advertising features.</li></ul> |
|`allow_ad_personalization_signals`|  <ul><li>Boolean</li><li>Allow ad personalization signals.</li><li>Enables Google Analytics to collect data about your traffic through the Google Ad Manager (DoubleClick) cookie, in addition to data collected through the standard Google Analytics implementation.</li></ul> |
|`config.link_attribution.cookie_name`|  <ul><li>Link Attribution Cookie Name</li></ul> |
|`config.link_attribution.cookie_expires`|  <ul><li>Link Attribution Cookie Expiration</li></ul> |
|`config.link_attribution.levels`|  <ul><li>Link Attribution Levels</li></ul> |
|`config.campaign.id`|  <ul><li>Campaign ID</li></ul> |
|`config.campaign.name`|  <ul><li>Campaign Name</li></ul> |
|`config.campaign.source`|  <ul><li>Campaign Source</li></ul> |
|`config.campaign.medium`|  <ul><li>Campaign Medium</li></ul> |
|`config.campaign.content`|  <ul><li>Campaign Content</li></ul> |
|`config.campaign.term`|  <ul><li>Campaign Term/Keyword</li></ul> |
|`config.anonymize_ip`|  <ul><li>Boolean</li><li>Anonymize IP</li><li>Tells Google Analytics to anonymize the information sent by the tracker objects by removing the last octet of the IP address prior to its storage.</li><li>Slightly reduces the accuracy of geographic reporting.</li></ul> |
|`clear_global_vars`|  <ul><li>Boolean</li><li>Clear Vars</li><li>Clears items usually set for the lifetime of the tracker after each tracking request.</li></ul> |
|`config.optimize_id`|  <ul><li>Optimize Container ID</li><li>Sets the `optimize_id` and enables the Google Optimize plugin.</li><li>This ID is found in your Optimize accounts page.</li><li>Example: **GTM-XXXXXX**</li></ul> |
|`config.use_amp_client_id`|  <ul><li>Boolean</li><li>Use AMP Client ID</li><li>The Google AMP Client ID lets you uniquely identify users that engage with your content on AMP and non-AMP pages.</li><li>If you opt-in, Google Analytics uses the AMP Client ID to determine that multiple site events belong to the same user when those users visit AMP pages through a Google AMP viewer.</li></ul> |
| `config.sample_rate` |  <ul><li>Sample Rate</li></ul> |
|`config.site_speed_sample_rate`|  <ul><li>Site Speed Sample Rate</li></ul> |
|`customer_id`|  <ul><li>User ID</li><li>Overrides `_ccustid`</li></ul> |
|`config.client_id`|  <ul><li>Client ID</li></ul> |

### Event

|Variable| Description|
|---| ---|
| `event_name` |  <ul><li>Event Action</li></ul> |
| `event.event_category` |  <ul><li>Event Category</li></ul> |
| `event.event_label` |  <ul><li>Event Label</li></ul> |
| `event.value` |  <ul><li>Event / Timing Value</li></ul> |
| `event.name` |  <ul><li>Timing Variable Name</li></ul> |
| `event.description` |  <ul><li>Exception Description</li></ul> |
| `event.non_interaction` |  <ul><li>Non-Interaction</li></ul> |
|`event.fatal`|  <ul><li>Boolean</li><li>Fatal Error</li></ul> |
| `event.search_term` |  <ul><li>Search Term</li></ul> |
| `event.method` |  <ul><li>Method</li></ul> |
| `event.content_type` |  <ul><li>Content Type</li></ul> |
| `event.content_id` |  <ul><li>Content ID</li></ul> |
| `event.destination` |  <ul><li>Destination</li></ul> |
|`event.start_date`|  <ul><li>Start Date</li><li>Date format is YYYYMMDD.</li></ul> |
|`event.end_date`|  <ul><li>End Date</li><li>Date format is YYYYMMDD.</li></ul> |
| `event.custom` |  <ul><li>Custom Event Data</li></ul> |
|`event.anonymize_ip`|  <ul><li>Boolean</li><li>Anonymize IP</li><li>Tells Google Analytics to anonymize the information sent by the tracker objects by removing the last octet of the IP address prior to its storage.</li><li>Slightly reduces the accuracy of geographic reporting.</li></ul> |
| `event.send_to` |  <ul><li>Override Default Routing</li></ul> |
| `event.event_callback` |  <ul><li>Event callback</li></ul> |

### App / Screen tracking

|Variable| Description|
|---| ---|
|`screen_view`|  <ul><li>Boolean.</li><li>Values accepted to activate: "true", "on")</li><li>Track Screen Views</li><li>Enables App/Screen tracking.</li><li>When enabled, a separate screenview request is sent after the initial pageview.</li></ul> |
| `event.screen_name` |  <ul><li>Screen Name</li></ul> |
| `config.app_name` |  <ul><li>Application Name</li></ul> |
| `config.app_id` |  <ul><li>Application ID</li></ul> |
| `config.app_version` |  <ul><li>Application Version</li></ul> |
|`IDconfig.app_installer_id`|  <ul><li>Application Installer</li></ul> |

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
|`checkout_step`|  <ul><li>Number</li><li>Checkout step.</li></ul> |
| `checkout_option` |  <ul><li>Checkout Option.</li></ul> |
|`order_currency`|  <ul><li>Currency</li><li>Overrides `_ccurrency`.</li></ul> |
|`order_id`|  <ul><li>Transaction ID</li><li>Overrides `_corder`.</li></ul> |
|`order_total`|  <ul><li>Value/Order Total</li><li>Overrides `_ctotal`.</li></ul> |
| `order_shipping` |  <ul><li>Shipping Amount</li><li>Overrides `_cship`.</li></ul> |
|`order_tax`|  <ul><li>Tax Amount</li><li>Overrides `_ctax`.</li></ul> |
|`order_store`|  <ul><li>Affiliation/Store</li><li>Overrides `_cstore`.</li></ul> |
| `order_coupon_code` |  <ul><li>Promo Code/Coupon</li><li>Overrides `_cpromo`.</li></ul> |
|`customer_id`|  <ul><li>User ID</li><li>Overrides `_ccustid`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of IDs</li><li>Overrides `_cprod`.</li></ul> |
|`product_name`|  <ul><li>Array</li><li>List of Names</li><li>`Overrides _cprodname`.</li></ul> |
|`product_brand`|  <ul><li>Array</li><li>List of Brands</li><li>Overrides `_cbrand`.</li></ul> |
|`product_category`|  <ul><li>Array</li><li>List of Categories</li><li>Overrides `_ccat`.</li></ul> |
|`product_variant`|  <ul><li>Array</li><li>List of Variants</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices</li><li>Overrides `_cprice`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities</li><li>Overrides `_cquan`.</li></ul> |
|`product_discount`|  <ul><li>Array</li><li>List of Discounts</li><li>Overrides `_cdisc`.</li></ul> |
|`product_promo_code`|  <ul><li>Array</li><li>List of Promo Codes/Coupons</li></ul> |
|`product_action_list`|  <ul><li>Array</li><li>Product Action List</li></ul> |
|`product_list_name`|  <ul><li>Array</li><li>Product Name</li></ul> |
|`product_list_id`|  <ul><li>Array</li><li>Product List ID</li></ul> |
|`product_list_position`|  <ul><li>Array</li><li>Product Position</li></ul> |
|`product_location_id`|  <ul><li>Product Location ID</li></ul> |

### Enh E-Comm engagement

|Variable| Description|
|---| ---|
|`impression_id`|  <ul><li>Array</li><li>Product Impression ID</li></ul> |
|`impression_name`|  <ul><li>Array</li><li>Product Impression Name</li></ul> |
| `impression_category` |  <ul><li>Array</li><li>Product Impression Category</li></ul> |
|`impression_brand`|  <ul><li>Array</li><li>Product Impression Brand</li></ul> |
|`impression_variant`|  <ul><li>Array</li><li>Product Impression Variant</li></ul> |
|`impression_price`|  <ul><li>Array</li><li>Product Impression Price</li></ul> |
|`impression_list_name`|  <ul><li>Array</li><li>Product Impression List</li></ul> |
|`impression_item_list_id`|  <ul><li>Product Impression List ID</li></ul> |
|`impression_list_position`|  <ul><li>Array</li><li>Product Impression Position</li></ul> |
|```promo_id```|  <ul><li>Array</li><li>Promotion ID</li></ul> |
|`promo_name`|  <ul><li>Array</li><li>Promotion Name</li></ul> |
|`promo_creative_name`|  <ul><li>Array</li><li>Promotion Creative</li></ul> |
| `promo_creative_slot` |  <ul><li>Array</li><li>Promotion Position</li></ul> |
| `promo_location_id` |  <ul><li>Array</li><li>Promotion Location</li></ul> |

### App+Web travel

|Variable| Description|
|---| ---|
|`event.trip_type`|  <ul><li>Trip Type</li></ul> |
|`start_date`|  <ul><li>Array</li><li>Start Date</li></ul> |
|`end_date`|  <ul><li>Array</li><li>End Date</li></ul> |
|`origin`|  <ul><li>Array</li><li>Origin</li></ul> |
|`destination`|  <ul><li>Array</li><li>Destination</li></ul> |
|`flight_number`|  <ul><li>Array</li><li>Flight Number</li></ul> |
|`travel_class`|  <ul><li>Array</li><li>Travel Class</li></ul> |
|`fare_product`|  <ul><li>Array</li><li>Fare Product</li></ul> |
|`booking_code`|  <ul><li>Array</li><li>Booking Code</li></ul> |
|`event.passengers.total`|  <ul><li>Total Number of Passengers</li></ul> |
|`event.passengers.adult`|  <ul><li>Number of Adult Passengers</li></ul> |
|`event.passengers.child`|  <ul><li>Number of Child Passengers</li></ul> |
|`event.passengers.infant_in_lap`|  <ul><li>Number of Infant Passengers in Lap</li></ul> |
|`event.passengers.infant_in_seat`|  <ul><li>Number of Infant Passengers in Seat</li></ul> |

### App+Web game

|Variable| Description|
|---| ---|
|`event.achievement_id`|  <ul><li>Achievement ID</li></ul> |
|`event.character`|  <ul><li>Character</li></ul> |
|`event.group_id`|  <ul><li>Group ID</li></ul> |
|`event.item_name`|  <ul><li>Item Name</li></ul> |
|`event.level`|  <ul><li>Level</li></ul> |
|`event.level_name`|  <ul><li>Level Name</li></ul> |
|`event.score`|  <ul><li>Score</li></ul> |
|`event.success`|  <ul><li>Success</li></ul> |
|`event.virtual_currency_name`|  <ul><li>Virtual Currency Name</li></ul> |

### IAB Transparency and Consent Framework v2

|Variable| Description|
|---| ---|
|`gtag_enable_tcf_support`|  <ul><li>Enable TCF Support</li><li>Values are **true** or **false**.</li></ul> |

## Google Analytics 4 support

Google Analytics 4 (GA4) is currently supported through the App and Web mappings for this tag.
