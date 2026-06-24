---
title: Firebase dispatcher
description: Add and configure the Firebase dispatcher to your Prism SDK app.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/firebase-dispatcher/
---

## Configuration

When adding the module, configure the following settings:

* **Session Timeout**: Firebase session timeout in seconds. Default value is 1800 seconds (30 minutes).
* **Analytics Collection Enabled**: Enable/disable analytics data collection.
* **Log Level**: Internal Firebase logging verbosity.

## Rules

The module dispatches (or collects for) any event. For more information, see [Rules](/platforms/prism-mobile/rules/).

## Data mappings

Mapping is the process of sending the value of an event variable to the corresponding destination variable in the vendor module.

The available categories are:

### Firebase Config

| Variable | Type  |
|:---------|:-----|
| `firebase_session_timeout_seconds` | Integer as String | 
| `firebase_analytics_collection_enabled` | Boolean as String | 
| `firebase_log_level` | String | 


### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `param_achievement_id` | `String` | Achievement ID |
| `param_ad_network_click_id` | `String` | Ad Network Click ID |
| `param_affiliation` | `String` | Affiliation |
| `param_cp1` | `String` | CP1 |
| `param_campaign` | `String` | Campaign |
| `param_character` | `String` | Character |
| `param_content` | `String` | Content |
| `param_content_type` | `String` | Content Type |
| `param_coupon` | `String` | Coupon |
| `param_creative_name` | `String` | Creative Name |
| `param_creative_slot` | `String` | Creative Slot |
| `param_currency` | `String` | Currency |
| `param_destination` | `String` | Destination |
| `param_end_date` | `String` | End Date |
| `param_flight_number` | `String` | Flight Number |
| `param_group_id` | `String` | Group ID |
| `param_index` | `String` | Index |
| `param_item_brand` | `String` | Item Brand |
| `param_item_category` | `String` | Item Category |
| `param_item_id` | `String` | Item ID |
| `param_item_list` | `String` | Item List |
| `param_item_name` | `String` | Item Name |
| `param_item_variant` | `String` | Item Variant |
| `param_level` | `Long` | Level |
| `param_location` | `Long` | Location |
| `param_medium` | `String` | Medium |
| `param_number_nights` | `Long` | Number Of Nights |
| `param_number_pax` | `Long` | Number Of Passengers |
| `param_number_rooms` | `Long` | Number Of Rooms |
| `param_origin` | `String` | Origin |
| `param_price` | `Double` | Price |
| `param_quantity` | `Long` | Quantity |
| `param_screen_name` | `String` | Screen Name |
| `param_screen_class` | `String` | Screen Class |
| `param_score` | `Long` | Score |
| `param_search_term` | `String` | Search Term |
| `param_shipping` | `Double` | Shipping |
| `param_method` | `String` | Method |
| `param_source` | `String` | Source |
| `param_travel_class` | `String` | Travel Class |
| `param_virtual_currency_name` | `String` | Virtual Currency Name |
| `param_start_date` | `String` | Start Date |
| `param_term` | `String` | Term |
| `param_tax` | `Double` | Tax |
| `param_transaction_id` | `String` | Transaction ID |
| `param_value` | `Long or Double` | Value |
| `param_level_name` | `String` | Level Name |
| `param_success` | `String` | Success |
| `param_ad_format` | `String` | Ad Format |
| `param_ad_platform` | `String` | Ad Platform |
| `param_ad_source` | `String` | Ad Source |
| `param_ad_unit_name` | `String` | Ad Unit Name |
| `param_campaign_id` | `String` | Campaign ID |
| `param_creative_format` | `String` | Creative Format |
| `param_discount` | `String` | Discount |
| `param_extend_session` | `String` | Extend Session |
| `param_item_category2` | `String` | Item Category2 |
| `param_item_category3` | `String` | Item Category3 |
| `param_item_category4` | `String` | Item Category4 |
| `param_item_category5` | `String` | Item Category5 |
| `param_item_list_id` | `String` | Item List ID |
| `param_item_list_name` | `String` | Item List Name |
| `param_items` | `Array` | Items |
| `param_level_name` | `String` | Level Name |
| `param_location_id` | `String` | Location ID |
| `param_marketing_tactic` | `String` | Marketing Tactic |
| `param_payment_type` | `String` | Payment Type |
| `param_promotion_id` | `String` | Promotion ID |
| `param_promotion_name` | `String` | Promotion Name |
| `param_shipping_tier` | `String` | Shipping Tier |
| `param_source_platform` | `String` | Source Platform |
| `param_travel_class` | `String` | Travel Class |
| `param_virtual_currency_name` | `String` | Virtual Currency Name |
| `param_user_signup_method` | `String` | User Signup Method |
| `param_user_allow_ad_personalization_signals` | `String` | User Allow Ad Personalization Signals |
| `param_email_address` | `String` | Email Address |
| `param_phone_number` | `String` | Phone Number |
| `param_hashed_email_address` | `String` | Hashed Email Address |
| `param_hashed_phone_number` | `String` | Hashed Phone Number |


### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `order_id` | `String` | Order ID |
| `order_total` | `Long or Double` | Order Total |
| `order_shipping` | `Double` | Shipping Amount |
| `order_tax` | `Double` | Tax Amount |
| `order_currency` | `String` | Currency |
| `order_coupon_code` | `String` | Promo Code |
| `product_id` | `Array` | List of Product IDs |
| `product_name` | `Array` | List of Names |
| `product_brand` | `Array` | List of Brands |
| `product_category` | `Array` | List of Categories |
| `product_quantity` | `Array` | List of Quantities |
| `product_unit_price` | `Array` | List of Prices |
| `param_item_list` | `Array` | List of Presentation Lists |
| `param_item_variant` | `Array` | List of Variants |
| `param_index` | `Array` | List of Indexes |


### Consent Settings

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `ad_storage` | `String` | Ad Storage |
| `analytics_storage` | `String` | Analytics Storage |
| `ad_user_data` | `String` | Ad User Data |
| `ad_personalization` | `String` | Ad Personalization |


### Events
To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `config` | Config |
| `setScreenName` | Set Screen Name |
| `setUserProperty` | Set User Property |
| `setUserId` | Set User Id |
| `logEvent` | Log Event |
| `resetData` | Reset Data |
| `event_add_payment_info` | Add Payment Info |
| `event_add_to_cart` | Add To Cart |
| `event_add_to_wishlist` | Add To Wishlist |
| `event_app_open` | App Open |
| `event_begin_checkout` | Begin Checkout |
| `event_campaign_details` | Campaign Detail |
| `event_earn_virtual_currency` | Earn Virtual Currency |
| `event_generate_lead` | Generate Lead |
| `event_join_group` | Join Group |
| `event_level_up` | Level Up |
| `event_level_start` | Level Start |
| `event_level_end` | Level End |
| `event_login` | Login |
| `event_post_score` | Post Score |
| `event_remove_cart` | Remove From Cart |
| `event_screen_view` | Screen View |
| `event_search` | Search |
| `event_select_content` | Select Content |
| `event_share` | Share |
| `event_signup` | Sign Up |
| `event_spend_virtual_currency` | Spend Virtual Currency |
| `event_tutorial_begin` | Tutorial Begin |
| `event_tutorial_complete` | Tutorial End |
| `event_unlock_achievement` | Unlock Achievement |
| `event_view_item` | View Item |
| `event_view_item_list` | View Item List |
| `event_view_search_results` | View Search Results |
| `event_ad_impression` | Ad Impression |
| `event_add_shipping_info` | Add Shipping Info |
| `purchase` | Purchase |
| `event_refund` | Refund |
| `event_select_item` | Select Item |
| `event_select_promotion` | Select Promotion |
| `event_view_cart` | View Cart |
| `event_view_promotion` | View Promotion |
| `initiateconversionmeasurement` | Initiate Conversion Measurement |
| `resetdata` | Reset Data |
| `setConsent` | Set Consent |


### Parameters

| Event | Description |
|:------|:------------|
| `param_ad_format` | Ad Format |
| `param_ad_platform` | Ad Platform |
| `param_ad_source` | Ad Source |
| `param_ad_unit_name` | Ad Unit Name |
| `param_campaign_id` | Campaign ID |
| `param_creative_format` | Creative Format |
| `param_discount` | Discount |
| `param_extend_session` | Extend Session |
| `param_item_category2` | Item Category2 |
| `param_item_category3` | Item Category3 |
| `param_item_category4` | Item Category4 |
| `param_item_category5` | Item Category5 |
| `param_item_list_id` | Item List ID |
| `param_item_list_name` | Item List Name |
| `param_items` | Items |
| `param_level_name` | Level Name |
| `param_location_id` | Location ID |
| `param_marketing_tactic` | Marketing Tactic |
| `param_payment_type` | Payment Type |
| `param_promotion_id` | Promotion ID |
| `param_promotion_name` | Promotion Name |
| `param_shipping_tier` | Shipping Tier |
| `param_source_platform` | Source Platform |
| `param_travel_class` | Travel Class |
| `param_virtual_currency_name` | Virtual Currency Name |
| `param_user_signup_method` | User Signup Method |
| `param_email_address` | Email Address |
| `param_phone_number` | Phone Number |
| `param_hashed_email_address` | Hashed Email Address |
| `param_hashed_phone_number` | Hashed Phone Number |
| `param_user_allow_ad_personalization_signals` | User Allow Ad Personalization Signals |
| `ad_storage` | Ad Storage |
| `analytics_storage` | Analytics Storage |
| `ad_user_data` | Ad User Data |
| `ad_personalization` | Ad Personalization |

    