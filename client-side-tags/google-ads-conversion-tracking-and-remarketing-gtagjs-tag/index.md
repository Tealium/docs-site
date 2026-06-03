---
title: Google Ads Conversion Tracking and Remarketing (gtag.js) Tag Setup Guide
description: This article describes how to set up the Google Ads Conversion Tracking & Remarketing (gtag.js) tag.
url: https://docs.tealium.com/client-side-tags/google-ads-conversion-tracking-and-remarketing-gtagjs-tag/
---
## Tag tips

* Supports the E-Commerce extension for:
  * Subtotal/conversion value.
  * Order currency/conversion currency.
  * Order ID/transaction ID.
  * List of product IDs.
  * List of categories.
  * List of quantities.
  * List of prices.
* We recommend a hybrid setup using both a tag and a connector. This configuration ensures maximum data resilience, improves event matching with server-side signals, and maintains data flow continuity while retaining real-time client-side signals. For more information, see [Google Ads Enhanced Conversions for Web Connector]().
* Use mapping to dynamically override the standard configuration values and the E-Commerce extension values.
* Pass custom conversion variables by mapping to **Custom Conversion Variable** and replacing `myvar` with your custom variable name.
* [Google: Dynamic Remarketing documentation](https://support.google.com/google-ads/answer/7305793).
* [Google: Google Ads documentation](https://developers.google.com/adwords-remarketing-tag/).
* Use the [Crypto Extension]() to encrypt and populate the **Hashed Email** and **Phone Number** values.

## Enhanced Conversions

Google’s Enhanced Conversions for Web feature can improve the accuracy of your conversion measurements. It supplements your existing conversion tags by sending hashed first-party conversion data from your website in a privacy safe way. 

* Before enabling Enhanced Conversions, you must enable enhanced conversions in your Google Ads account. For more information, see [Google: Set up enhanced conversions for web using the Google tag](https://support.google.com/google-ads/answer/13258081?sjid=1600196321043643540-NC).
* If you are using the server-side Enhanced Conversions for Web connector to supplement this client-side tag, map a unique value, such as `tealium_random`, to **Transaction ID** for non-purchase conversions to enable Google to deduplicate the event. In addition, within the Google Ads configuration for your conversion, set **Implementation Type** to `API`.

 Support for enhanced conversions was added in June, 2022. If you are running an older version of the tag and want to use this feature, you must update the tag template. For more information, see [Managing Tag Templates](). 

## Deduplication

Google uses the transaction ID to deduplicate if the same conversion event is sent from client-side and server-side conversions. The Transaction ID should be unique to each conversion event. The server-side value of this ID should equal the matching client-side event ID. We recommend using `order_ID` for purchases and `tealium_random` for other events. 

## Dynamic Remarketing

The Google Ads Conversion Tracking and Remarketing tag supports dynamic remarketing that lets you personalize ads based on previous visitor activity on your website. To use remarketing features with this tag, set **Enable Remarketing** to **On** in the tag configuration.

When you enable remarketing, this tag automatically pulls in data from the [E-Commerce extension]() to populate the Google Ads **Retail** parameters. To pass the values with a remarketing event, go to **Data Mapping &gt; Event-specific parameters** and map the relevant data layer attribute to the remarketing event attribute.

Google recommends always mapping at least one attribute from one of the remarketing categories (for example, retail, education, flights, hotels and rentals, jobs, local, real estate, and travel) to a remarketing event. If the user interacts with multiple items on your website, like checking out a shopping cart or searching for a travel itinerary, you can map more than one attribute.

For more information about dynamic remarketing events and item parameters, see [Google: Dynamic remarketing events and parameters](https://support.google.com/google-ads/answer/7305793).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Conversion ID**: Unique ID for the conversion. You can find this ID in your Google Ads control panel (for example, `AW-123456789`).
    * Use mapping to dynamically override this value.
    * Use a comma-separated list to send data for multiple properties.
* **Conversion Label**: Set a default label here and use mapping to dynamically override this value.
    * Use a comma-separated list to send data for multiple labels. This list can use a matching number of **Conversion Labels** as **Conversion IDs** or use a single label for all **Conversion IDs**.
* **Conversion Value**: Set a default value here or leave this blank to use the Subtotal value from the E-Commerce extension.
    * Use mapping to dynamically override this value and the E-Commerce extension value.
* **Global Object**: This value is the name of the **Global Object** used for the event queue. If not specified, `gtag` is used.
    * Not required for most implementations.
* **Data Layer Name**: By default, the data layer initiated and referenced by the global site tag is named **dataLayer**. Rename the data layer only if your project requires a separate name.
* **Enable Remarketing**: When Remarketing is enabled, this tag will automatically pull in data from the E-Commerce Extension to populate the Google Ads **Retail** parameters.
    * Mapping directly to the **Retail** tab in the toolbox will override the data pulled in through the E-Commerce Extension.
* **Page Type**: Select a default page type here and use mapping to dynamically override this value.
* **Cross-Tracking Domains**: A comma-separated list of domains to use with Cross-Domain Tracking (`setAllowLinker`).
    * This list should consist of top-level domains, such as `tealiumiq.com`.
* **Enable Enhanced Conversions**
  * Only enable this option if you are sending PII (Personally Identifiable Information) through the tag. 
  * If you are using the server-side **Enhanced Conversions for Web** connector to supplement this client-side tag, map a unique value, such as `tealium_random`, to **Transaction ID** for non-purchase conversions to enable Google to deduplicate the event. In addition, within the Google Ads configuration for your conversion, set **Implementation Type** to `API`.
  * For more information on how to set up this tag to work with the Google Ads Enhanced Conversion connector in EventStream, see [Tealium &#43; Google Enhanced Conversions Integration Guide]().
* **Enable Event Matching for Server-side Enhanced Conversions**
  * Enable event matching to use Automatic Transaction ID in the [Google Ads Enhanced Conversions for Web connector]().

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `conversion_id` | String | Conversion ID.  |
| `conversion_label` |String | Conversion label.  | 
|  `conversion_value` |String | Conversion value.  |
|  `conversion_currency` |String | Conversion currency.  |
|  `user_id` |String | User ID.  |
|  `pagetype` |String | Page type.  |
| `aw_merchant_id` |String | Merchant center ID.  | 
| `aw_feed_country` |String | Feed country.  | 
|  `aw_feed_language` |String | Feed language.  |
|  `config.send_page_view`  | Boolean | Send page view. |
| `conversion_cookie_prefix` |String | Conversion cookie prefix.  | 
| `custom.myvar` |String | Custom conversion variable.  | 
|  `cross_track_domains` | Comma-separated String | Cross-tracking domains.  |
| `config.enable_event_matching_conversions` | Boolean | Enable event matching for server-side enhanced conversions. |

### Retail

| Variable | Type | Description |
|:---------|:------------|:------------|
| `rmkt.retail.id`  | Array | Unique product ID (Overrides `_cprod`).  | 

### Education

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `rmkt.education.id`  | Array | Unique ID.|
|  `rmkt.education.location_id`  | Array | Location ID.|

### Flights

| Variable | Type | Description |
|:---------|:------------|:------------|
| `rmkt.flights.origin`  | Array |  Origin ID.|
|  `rmkt.flights.destination`  | Array | Destination ID.|
|  `rmkt.flights.start_date`  | Array | Start date.|
| `rmkt.flights.end_date`  | Array | End date.  |

### Hotel and Rentals

| Variable | Type | Description |
|:---------|:------------|:------------|
| `rmkt.hotel_rental.id`  | Array | Property ID. |
|  `rmkt.hotel_rental.start_date`  | Array | Start date.|
|  `rmkt.hotel_rental.end_date`  | Array | End date.|

### Jobs

| Variable | Type | Description |
|:---------|:------------|:------------|
| `rmkt.jobs.id`  | Array | Job ID. |
|  `rmkt.jobs.location_id`  | Array | Location ID.|

### Local

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `rmkt.local.id`  | Array | Deal ID.|

### Real Estate

| Variable | Type | Description |
|:---------|:------------|:------------|
| `rmkt.real_estate.id`  | Array |Listing ID. |

### Travel

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `rmkt.travel.origin`  | Array | Origin ID.|
|  `rmkt.travel.destination`  | Array | Destination ID. |
|  `rmkt.travel.start_date`  | Array |Start date.|
|  `rmkt.travel.end_date`  | Array | End date. |

### Custom / Legacy

| Variable |  Description |
|:---------|:------------|
| `rmkt.custom.id`  | Array. Custom ID.  |
|  `rmkt.custom.location_id`  | Array. Custom location ID/ID2 |
|   `ecomm.prodid` |  ecomm.prodid  (Overrides `_cprod`) |
|     `ecomm.totalvalue` | ecomm.totalvalue |
|   `ecomm.category` |  ecomm.category (Overrides `_ccat`) |
|  `ecomm.pvalue`  | ecomm.pvalue (Overrides `_cprice`) |
|  `ecomm.quantity`  |  ecomm.quantity (Overrides `_cquan`) |
| `edu.pid` |  edu.pid  | 
|  `edu.plocid` |  edu.plocid  |
| `flight.originid` | flight.originid  | 
| `flight.destid` | flight.destid  | 
|  `flight.totalvalue` | flight.totalvalue  |
| `flight.startdate` | flight.startdate  | 
|  `flight.enddate` | flight.enddate  |
| `hrental.id` | hrental.id  | 
| `hrental.startdate` | hrental.startdate  | 
| `hrental.enddate` | hrental.enddate  | 
| `hrental.totalvalue` |hrental.totalvalue  | 
| `job.id` |  job.id  | 
| `job.locid`  | job.locid  | 
| `job.totalvalue` |  job.totalvalue  | 
| `local.id` |  local.id  | 
|  `local.totalvalue` | local.totalvalue  |
|  `listing.id` |  listing.id  |
|  `listing.totalvalue` |  listing.totalvalue  |
|  `travel.destid` |  travel.destid  |
|  `travel.originid` |  travel.originid  |
| `travel.startdate` |  travel.startdate  | 
|  `travel.enddate` |  travel.enddate  |
| `travel.totalvalue` |  travel.totalvalue  | 
|  `dynx.itemid` |  dynx.itemid  |
|  `dynx.itemid2` |  dynx.itemid2  |
| `dynx.totalvalue` |  dynx.totalvalue  | 

### Advanced

| Variable | Type | Description |
|:---------|:------------|:------------|
| `custom.ecomm_rec_prodid`| Array  |Recommended product IDs.  | 
|`custom.a` |  Number |Visitor&#39;s age.  |
| `custom.g`| String |Visitor&#39;s gender.  |
|`custom.hasaccount`| Boolean  |Visitor has account.  | 
| `custom.cqs`| Number |Customer quality score.  | 
| `custom.rp`| Boolean  |Repeat purchaser.  | 
| `custom.ly` | Number |Visitor loyalty score. | 
| `custom.hs`| Number |Visitor high spender score. | 
| `custom.myvar`| String  |Custom.  | 

### Phone Conversion

| Variable | Type | Description |
|:---------|:------------|:------------|
| `config.phone_conversion_number` | String | Phone conversion number.  | 
|  `config.phone_conversion_callback`  | Function | Phone conversion callback. |
|  `config.phone_conversion_css_class`  | String | Phone conversion CSS class name. |
|  `config.phone_conversion_options.timeout`  | Number | Phone conversion timeout. |
| `config.phone_conversion_options.cache`  | Boolean | Phone conversion cache.  |

### E-Commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
|   `order_id` (Overrides `_corder`) | String | Order ID. |
|  `order_subtotal` (Overrides `_csubtotal`) | Number | Sub total.  | 
|   `order_currency` (Overrides `_ccurrency`) | String | Currency. |
|  `product_id` (Overrides `_cprod`)  | Array | List of product IDs |
| `product_category` (Overrides `_ccat`)  | Array | List of categories.  |
|  `product_quantity` (Overrides `_cquan`)  | Array | List of quantities. |
| `product_unit_price` (Overrides `_cprice`)  | Array | List of prices.  |
|  `product_discount` (Overrides `_cdisc`)  | Array | List of discounts. |

### Event-specific Parameters

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `gtag_enable_tcf_support` (true/false) | Boolean | Enable TCF support  |
| `user_provided_data` | String | Any mapped event-specific parameters passed in a `user_data` object. |
| `customer_type` | String | Whether the customer in a `purchase` event is a new customer. &lt;ul&gt;&lt;li&gt;`New`: A new customer who hasn&#39;t purchased within 540 days.&lt;/li&gt;&lt;li&gt;`Returning`: A returning customer who has made a purchase within 540 days.&lt;/li&gt;&lt;/ul&gt; |

### IAB Transparency and Consent Framework v2

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `exception` | An exception event is logged when the normal flow of an app&#39;s execution is interrupted. |
| `generate_lead` | A lead has been generated. This variable helps you understand how effective your re-engagement campaigns are. |
| `login` | A user has logged in. |
| `page_view` | A user has viewed a page. |
| `screen_view` | The user transitions to a new screen. |
| `search` | The user has performed a search. You can use this event to contextualize search operations to identify the content that users are searching for on your website or app. For example, you can send this event when a user views a page after performing a search. |
| `share` | Use this event when a user has shared content. |
| `sign_up` | The user registers for the site or service. |
| `timing_complete` | The user completes a process. |
| `view_search_results` | The user has been presented with the results of a search. Note that you can enable the `view_search_results` event for automatic collection through enhanced event measurement in Google Analytics. |
| `cst` | Custom event. |
| `add_payment_info` | A user has submitted their payment information. |
| `add_to_cart` | An item was added to a cart for purchase. |
| `add_to_wishlist` | An item was added to a wish list. Use this event to identify popular gift items in your app. |
| `begin_checkout` | A user has begun a checkout. |
| `checkout_progress` |A user is in the process of checking out. |
| `purchase` | One or more items is purchased by a user. |
| `refund` | One or more items is refunded to a user. |
| `remove_from_cart` | An item was removed from a cart. |
| `product_click` | An item was selected from a list. |
| `promotion_click` | A promotion was selected from a list. |
| `set_checkout_option` | The user selected a checkout option, such as a shipping method. |
| `view_item` | Content was shown to the user. Use this event to discover the most popular items viewed. |
| `view_item_list` | The user has been presented with a list of items of a certain category. |
| `view_promotion` | A promotion was viewed from a list. |

### Enhanced Conversions

| Variable  | Type | Description |
|:---------|:------------|:------------|
|  `config.allow_enhanced_conversions`  | Boolean | Allow enhanced conversions. |
|  `user_data.email` | String |Email address.  |
|  `user_data.sha256_email_address` | String |Hashed email address.  |
|  `user_data.phone_number` | String |Phone number.  |
| `user_data.sha256_phone_number` | String |Hashed phone number.  | 
|  `user_data.address.first_name` | String |First name.  |
| `user_data.address.sha256_first_name` |String | Hashed first name.  | 
|  `user_data.address.last_name` |String |Last name.  | 
| `user_data.address.sha256_last_name` | String |Hashed last name.  | 
| `user_data.address.street` | String |Street address.  | 
|  `user_data.address.city` |String |City.  |
|  `user_data.address.region` | String |Region.  |
| `user_data.address.postal_code` | String |Postal code.  | 
|  `user_data.address.country` | String |Country.  |
|  `transaction_id` |String | (Required) Transaction ID.  |