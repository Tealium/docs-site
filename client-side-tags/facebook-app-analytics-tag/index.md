---
title: Facebook App Analytics Tag Setup Guide
description: This article describes how to set up the Facebook App Analytics tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/facebook-app-analytics-tag/
---
## Tag Tips

* Facebook Developer documentation
  * [API v2.12](https://developers.facebook.com/docs/marketing-api/app-event-api/v2.12)
  * [Application Activities](https://developers.facebook.com/docs/graph-api/reference/application/activities/)

* Tag Configuration
  * These can be found on your dashboard
  * API Version
  * APP ID
  * APP Token (APP Secret)

## Tag Configuration

First, go to Tealium's tag marketplace and add the Facebook App Analytics tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Application Id**: An integer value (for example, `123456`)
* **Access Token (App Secret)**: An integer value (for example, `123456`)
* **Event Name**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Description| Parameter|
|---| ---|
|App Id| `app_id`|
|Access Token| `access_token`|
|Event Name| `event_name`|
|Advertiser Id| `advertiser_id`|
|Attribution| `attribution`|
|Advertiser Tracking Enabled| `advertiser_tracking_enabled`|
|Application Tracking Enabled| `application_tracking_enabled`|
|Custom Events (`custom_events`)| `custom_events` [Array of Objects]|
|Event List (`event_list`)| `event_list` [Array of Objects]|

### Mobile

|Variable| Description|
|---| ---|
|Bundle ID| Overrides `app_rdns`|
|Bundle Version|
|Bundle Short Version| Overrides `app_version`|

### Events

|Parameter| Description |
|---| ---|
|`fb_mobile_level_achieved`| Level achieved|
|`fb_mobile_activate_app`| Active app|
|`fb_mobile_add_payment_info`| Add payment info|
|`fb_mobile_add_to_cart`| Add to cart|
|`fb_mobile_add_to_wishlist`| Add to wish list|
|`fb_mobile_complete_registration`| Complete registration|
|`fb_mobile_tutorial_completion`| Tutorial completion|
|`fb_mobile_initiated_checkout`| Initiated checkout|
|`fb_mobile_purchase`| Purchase|
|`fb_mobile_rate`| Rate|
|`fb_mobile_search`| Ssearch|
|`fb_mobile_spent_credits`| Spent credits|
|`fb_mobile_achievement_unlocked`| Achievement unlocked|
|`fb_mobile_content_view`| Content view|
|Custom| Custom|

### Parameters

|Description| Parameter|
|---| ---|
|Log Time ( `int` )| `_logTime`|
|App Version | `_appVersion`|
|Value to Sum ( `float` )| `_valueToSum`|
|Content ID ( `string` )| `fb_content_id`|
|Content Type ( `string` )| `fb_content_type`|
|Currency ( `string` )| `fb_currency`|
|Description ( `string` )| `fb_description`|
|Level ( `string` )| `fb_level`|
|Max Rating Value ( `int` )| `fb_max_rating_value`|
|Number of Items ( `int` )| `fb_num_items`|
|Payment Info Available ( `1` or `0` )| `fb_payment_info_available`|
|Registration Method ( `string` )| `fb_registration_method`|
|Search String ( `string` )| `fb_search_string`|
|Success( `1` or `0` )| `fb_success`|
|Custom| Custom|

### Limited Data Use

|Variable| Description|
|---| ---|
| `lmt_data.use_ldu` (Use LDU) |  <ul><li>If `true`, use Facebook’s Limited Data Use option </li><li>If `false`, do not use Facebook’s Limited Data Use option</li></ul> |
| `lmt_data.ldu_types.geolocate` (LDU should Geolocate) |  <ul><li>If `true`, the LDU geolocates the user.</li><li>If `false`, the LDU does not geolocate the user. If **Use LDU** is enabled, then **LDU should Geolocate** is also enabled by default.</li></ul> |
| `lmt_data.ldu_types.california` (LDU is California) |  <ul><li>If `true`, sets the state and country California-specific values inside the template. Only enable this option if the user is located in California and needs to be processed with Limited Data Use.</li><li>If `false`, does not set the user’s state and country California-specific values inside the template.</li></ul> |
