---
title: AppsFlyer Mobile Remote Command Tag
description: This article describes how to set up the AppsFlyer Mobile Remote Command tag.
url: https://docs.tealium.com/client-side-tags/appsflyer-mobile-remote-command-tag/
---
## Tag tips

* The initialize and launch commands are automatically sent on first load if initialize is not found in the event list or `b.lifecycle_type` is set to launch.
* If the appropriate data is provided the login event can also, automatically, send a `setcustomerid` event.
* `af_content_id` will automatically use the first item in the `product_id` if it is available and no value is mapped.
* Supports the following E-Commerce extension values: 
  * Order ID
  * Order Total
  * Order Currency
  * Order Coupon Code
  * List of IDs
  * List of Quantities
  * List of Prices

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **App ID**:  The application ID.
* **SDK Dev Key**: The Software Development Kit developer's key.
* **Enable Debug Mode**: The default is `False`.
* **Enable Purchase Autotracking**: The default is `False`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration

| Variable | Type | Description |
|:---------|:------------|:------------|
| `command_name`  | String | Command Name  |
|  `app_id`  | String  |  App ID|
|  `app_dev_key`  | String | App Development Key |
|  `debug`  | Boolean | Debug |
|  `disable_ad_tracking`  | Boolean | Disable Ad Tracking |
|  `disable_apple_ad_tracking`  | Boolean | Disable Apple Ad Tracking |
|  `time_between_sessions`  | Integer | Time Between Sessions |
|  `anonymize_user`  | Boolean | Anonymize User |
|  `collect_device_name`  | Boolean | Collect Device Name |
|  `custom_data`  | [JSON Object] | Custom Data|
|  `resolve_deep_links`  | [Array of Strings] | Resolve Deep Links |
|  `stop_tracking`  | Boolean | Stop Tracking |
|  `customer_emails`  | [Array of Strings] | Customer Emails |
|  `email_hash_type`  | Integer |  Email Hash Type|
|  `host`  | String | Host |
|  `host_prefix`  | String | Host Prefix|

### Standard

| Variable | Type | Description |
|:---------|:------------| :------------|
|  `af_achievement_id`  | String | Achievement ID|
|  `af_adrev_ad_type`  | String | Ad Type |
|  `af_city`  | String | City|
|  `af_class`  | String | Class|
|  `af_content`  | [JSON Encoded String] | Content|
|  `af_content_id`  | String | Content ID |
|  `af_content_type`  | String | Content Type |
|  `af_country`  | String | Country|
|  `af_customer_segment`  | String | Customer Segment|
|  `af_customer_user_id`  | String | Customer User ID |
|  `af_date_a`  | [String Date] | Date A | 
|  `af_date_b`  | [String Date] | Date B |
|  `af_deep_link`  | String | Deep Link |
|  `af_departing_arrival_date`  | [String Date] | Departing Arrival Date | 
|  `af_departing_departure_date`  | [String Date] | Departing Departure Date | 
|  `af_description`  | String | Description |
|  `af_destination_a`  | String | Destination A |
|  `af_destination_b`  | String | Destination B |
|  `af_destination_list`  | [Array of Strings] | Destination List |
|  `af_event_end`  | String | Event End |
|  `af_event_start`  | String | Event Start |
|  `af_hotel_score`  | Float | Hotel Score |
|  `af_lat`  | Integer | Latitude |
|  `af_level`  | Integer | Level |
|  `af_long`  | Integer | Longitude |
|  `af_max_rating_value`  | Float | Max Rating Value |
|  `af_new_version`  | String | New Version |
|  `af_num_adults`  | Integer | Number of Adults |
|  `af_num_children`  | Integer | Number of Children|
|  `af_num_infants`  | Integer | Number of Infants|
|  `af_old_version`  | String | Old Version| 
|  `af_preferred_neighborhoods`  | [Array of Strings] | Preferred Neighborhoods |
| `af_preferred_num_stops`  | [Array of Integers] | Preferred Number of Stops |
|  `af_preferred_price_range`  | [Array of Integers] | Preferred Price Range|
|  `af_preferred_star_ratings`  | [Array of Integers] | Preferred Star Ratings |
|  `af_rating_value`  | Float | Rating Value |
|  `af_receipt_id`  | String | Receipt ID |
|  `af_region`  | String |Region|
|  `af_registration_method`  | String | Registration Method |
|  `af_returning_arrival_date`  | [String Date] | Returning Arrival Date |
|  `af_returning_departure_date`  | [String Date] | Returning Departure Date |
|  `af_review_text`  | String | Review Text |
|  `af_score`  | Integer | Score |
|  `af_search_string`  | String | Search String|
|  `af_success`  | Boolean | Success|
|  `af_suggested_destinations`  | [Array of Strings] | Suggested Destinations |
|  `af_suggested_hotels`  | [Array of Strings] | Suggested Hotels|
|  `af_travel_end`  | String | Travel End|
|  `af_travel_start`  | String | Travel Start |
|  `af_tutorial_id`  | String | Tutorial ID|
|  `af_user_score`  | Float | User Score|
|  `af_validated`  | String | Validated|
|  `af_virtual_currency_name`  | String | Virtual Currency Name | 
|  `af_param_1`  | String |Parameter 1|
|   `af_param_2`  | String |Parameter 2|
|   `af_param_3`  | String |Parameter 3|
|   `af_param_4`  | String |Parameter 4|
|   `af_param_5`  | String |Parameter 5|
|   `af_param_6`  | String |Parameter 6|
|   `af_param_7`  | String |Parameter 7|
|  `af_param_8`  | String |Parameter 8|
|   `af_param_9`  | String |Parameter 9|
|   `af_param_10`  | String |Parameter 10|

### E-Commerce

| Variable | Type| Description |
|:---------|:------------|:------------|
| `order_id`  | String | Order ID (Overrides `_corder`) 
 | `order_total`  | String | Order Total/Revenue (Overrides `_ctotal`)
| `af_payment_info_available`  | Boolean | Payment Info Available  |
| `af_purchase_currency`  | String | Purchase Currency |
 | `order_currency`  | String | Currency (Overrides `_ccurrency`) |
 | `order_coupon_code`  | String | Promo Code/ Coupon Code (Overrides `_cpromo`) |
| `product_id`  | Array |  List of Product IDs/Content ID  (Overrides `_cprod`) |
| `product_quantity` | Array | List of Quantities/Quantity (Overrides `_cquan`)  |
| `product_unit_price` | Array | List of Prices/Price  (Overrides `_cprice`)  |

### Events
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/manage-data-mappings/)

| Variable | Description |
|:---------|:------------|
|   `initialize` | Initialize |
|  `launch` | Launch |
|   `tracklocation` | Track Location |
|   `sethost` | Set Host | 
|   `setuseremails` |Set User Emails |
|   `setcurrencycode` | Set Currency Code |
|  `setcustomerid` | Set Customer ID |
|  `disabletracking` | Disable Tracking |
| `resolvedeeplinkurls` | Resolve Deep Link Urls |
| `achievelevel` | Achieve Level  |
| `adclick` | Ad Click |
|`adview` | Ad View |
|   `addpaymentinfo` | Add Payment Info |
|  `addtocart` | Add To Cart |
|  `addtowishlist` | Add to wish list |
|  `completeregistration` | Complete Registration |
| `completetutorial` | Complete Tutorial |
| `rate` |  Rate |
|  `starttrial` | Start Trial |
|   `subscribe` | Subscribe |
|   `unlockachievement` | Unlock Achievement |
|  `spentcredits` | Spent Credits |
|  `listview` | List View |
|   `share` | Share |
|  `invite` | Invite |
|   `reengage` | Re-Engage |
|   `update` | Update|
|  `login` |Login|
|   `search` | Search|
|   `initiatecheckout` | Initiate Checkout |
|  `purchase` | Purchase |
|  `viewedcontent` | Viewed Content |
|  `travelbooking` | Travel Booking |
| `customersegment` | Customer Segment |

### Parameters
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/manage-data-mappings/)

| Variable | Description |
|:---------|:------------|
|  `command_name` | Command Name |
|  `app_id` | App ID |
|  `app_dev_key` | App Development Key | 
|   `debug` | Debug | 
|   `disable_ad_tracking` | Disable Ad Tracking | 
|   `disable_apple_ad_tracking` | Disable Apple Ad Tracking | 
|   `time_between_sessions` | Time Between Sessions |
|  `anonymize_user` | Anonymize User | 
|  `collect_device_name` | Collect Device Name |
|   `custom_data` | Custom Data |
|   `resolve_deep_links` | Resolve Deep Links |
|  `stop_tracking` | Stop Tracking |
|   `customer_emails` | Customer Emails |
|   `email_hash_type` | Email Hash Type |
|  `host` | Host |
|   `host_prefix` | Host Prefix |
|  `af_achievement_id` | Achievement ID |
| `af_adrev_ad_type` | Ad Type |
|  `af_city` | City |
|   `af_class` | Class |
|   `af_content` | Content |
| `af_content_id` | Content ID |
|  `af_content_type` | Content Type |
|  `af_country` | Country |
|  `af_customer_segment` | Customer Segment |
| `af_customer_user_id` | Customer User ID |
|   `af_date_a` | Date A |
| `af_date_b` | Date B |
|  `af_deep_link` | Deep Link|
| `af_departing_arrival_date` | Departing Arrival Date  |
|   `af_departing_departure_date` | Departing Departure Date |
|  `af_description` | Description |
|  `af_destination_a` | Destination A |
|   `af_destination_b` | Destination B |
|   `af_destination_list` | Destination List |
|   `af_event_end` | Event End |
|   `af_event_start` | Event Start |
|  `af_hotel_score` |Hotel Score |
|   `af_lat` |  Latitude |
|  `af_level` | Level |
|  `af_long` | Longitude |
| `af_max_rating_value` | Max Rating Value |
| `af_new_version` | New Version |
| `af_num_adults` | Number of Adults |
| `af_num_children` | Number of Children |
| `af_num_infants` | Number of Infants |
| `af_old_version` | Old Version  |
| `af_preferred_neighborhoods` | Preferred Neighborhoods |
| `af_preferred_num_stops` | Preferred Number of Stops |
| `af_preferred_price_range` | Preferred Price Range |
| `af_preferred_star_ratings` | Preferred Star Ratings |
| `af_rating_value` | Rating Value |
| `af_receipt_id` | Receipt ID |
| `af_region` | Region |
| `af_registration_method` | Registration Method |
| `af_returning_arrival_date` | Returning Arrival Date |
| `af_returning_departure_date` | Returning Departure Date |
| `af_review_text` | Review Text |
| `af_score` | Score |
| `af_search_string` | Search String |
| `af_success` | Success |
| `af_suggested_destinations` | Suggested Destinations |
| `af_suggested_hotels` | Suggested Hotels |
| `af_travel_end` | Travel End |
| `af_travel_start` | Travel Start  |
| `af_tutorial_id` | Tutorial ID |
| `af_user_score` | User Score |
| `af_validated` | Validated |
| `af_virtual_currency_name` | Virtual Currency Name |
| `af_param_1` |Parameter 1 |
| `af_param_2` |Parameter 2 |
| `af_param_3` |Parameter 3 |
| `af_param_4` |Parameter 4 |
| `af_param_5` |Parameter 5 |
| `af_param_6` |Parameter 6 |
| `af_param_7` |Parameter 7 |
| `af_param_8` | Parameter 8 |
| `af_param_9` |  Parameter 9 |
| `af_param_10` | Parameter 10 (`af_param_10`) 
| `af_order_id` | Order ID (Overrides `_corder`) 
| `af_revenue` | Order Total/ Revenue (Overrides `_ctotal`)
| `af_payment_info_available` | Payment Info Available |
| `af_purchase_currency` | Purchase Currency  |
| `af_currency` | Currency (Overrides `_ccurrency`) |
| `af_coupon_code` | Promo Code/ Coupon Code  (Overrides `_cpromo`)  |
|  `af_content_list` | [Array] List of Product IDs/ Content ID (Overrides `_cprod`) |
| `af_quantity` | [Array]  List of Quantities/ Quantity (Overrides `_cquan`)  |
| `af_price` | [Array] List of Prices/ Price (Overrides `_cprice`) |
|  `custom` |Custom |

    