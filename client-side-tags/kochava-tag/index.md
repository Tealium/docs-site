---
title: Kochava Tag Setup Guide
description: This article describes how to set up the Kochava tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/kochava-tag/
---
Kochava enables people-based marketers to establish and enrich user identities, segment and activate audiences, and measure and optimize their campaigns across all connected devices.

## Tag Tips

* Use mappings to:
  * Override standard configuration values and set custom parameters.
  * Trigger standard and custom events.

* Autopage — Set to `true` to send a page event automatically on every page load. Set to `false` to send a page load only on manual calls to the page function.
* Cache — Set to `true` to allow browsers to cache the SDK code. Set to `false` to force the SDK code to be loaded with every page load.
* Verbose — Set to `true` for Verbose logging to the console. Set to `false` to suppress all logging.
* Cookie Collection — Set to `true` to drop Cookie on the website to track a device across sub-domains. Set to `false` to not drop the Cookie and rely only on local storage for tracking.

## Tag Configuration

First, go to the tag marketplace and add the Kochava tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Kochava App GUID**
* **Autopage**
* **Cache**
* **Verbose**
* **Cookie Collection**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Configuration Parameters

|Variable| Description|
|---| ---|
|App ID| (`app_guid`)|
|App Tracking Transparency Enabled (`app_tracking_transparency_enabled`)| [`true`/`false`]|
|Identity Link IDs| (`identity_link_ids`)|
|Log Level| (`log_level`)|

### Events

|Variable| Description|
|---| ---|
|Ad Click| `adclick`|
|Ad View| `adview`|
|Add to Cart| `addtocart`|
|Add to Wish List| `addtowishlist`|
|Achievement| `achievement`|
|Checkout Start| `checkoutstart`|
|Tutorial Complete| `tutorialcomplete`|
|Level Complete| `levelcomplete`|
|Purchase| `purchase`|
|Rating| `rating`|
|Registration Complete| `registrationcomplete`|
|Search| `search`|
|Start Trial| `starttrial`|
|Subscribe| `subscribe`|
|View| `view`|
|QSS. (Quality Steaming Session &gt;5mins)| `qss`|
|First_Video_View| `first_video_view`|
|Share_with_friend| `share_with_friend`|
|Authentication_Success| `authentication_success`|
|Watch_later| `watch_later`|
|Custom| `custom`|

### All Parameters

|Variable| Description|
|---| ---|
|Action| (`action`)|
|Background| (`background`)|
|Checkout as Guest| (`checkout_as_guest`)|
|Completed| (`completed`)|
|Content ID| (`content_id`)|
|Content Type| (`content_type`)|
|Currency| (`currency`)|
|Date| (`now_date`)|
|Description| (`description`)|
|Destination| (`destination`)|
|Duration| (`duration`)|
|End Date| (`end_date`)|
|Item Added From| (`item_added_from`)|
|Level| (`level`)|
|Ad Campaign ID| (`ad_campaign_id`)|
|Ad Campaign Name| (`ad_campaign_name`)|
|Ad Group ID| (`ad_group_id`)|
|Ad Group Name| (`ad_group_name`)|
|Ad Mediation Name| (`ad_mediation_name`)|
|Ad Network Name| (`ad_network_name`)|
|Placement| (`placement`)|
|Ad Size| (`ad_size`)|
|Ad Type| (`ad_type`)|
|Max Rating Value| (`max_rating_value`)|
|Name| (`name`)|
|Order ID| (`order_id`)|
|Origin| (`origin`)|
|Price| (`price`)|
|Quantity| (`quantity`)|
|Rating Value| (`rating_value`)|
|Receipt ID| (`receipt_id`)|
|Referral From| (`referral_from`)|
|Registration Method| (`registration_method`)|
|Results| (`results`)|
|Score| (`score`)|
|Search Term| (`search_term`)|
|Spatial X| (`spatial_x`)|
|Spatial Y| (`spatial_y`)|
|Spatial Z| (`spatial_z`)|
|Start Date| (`start_date`)|
|Success| (`success`)|
|User ID| (`user_id`)|
|User Name| (`user_name`)|
|URI| (`uri`)|
|Validated| (`validated`)|

### Event Parameters

|Variable| Description|
|---| ---|
|Ad Click| `adclick`|
|Ad View| `adview`|
|Add to Cart| `addtocart`|
|Add to Wish List| `addtowishlist`|
|Achievement| `achievement`|
|Checkout Start| `checkoutstart`|
|Tutorial Complete| `tutorialcomplete`|
|Level Complete| `levelcomplete`|
|Purchase| `purchase`|
|Rating| `rating`|
|Registration Complete| `registrationcomplete`|
|Search| `search`|
|Start Trial| `starttrial`|
|Subscribe| `subscribe`|
|View| `view`|
|QSS. (Quality Steaming Session &gt;5mins)| `qss`|
|First_Video_View| `first_video_view`|
|Share_with_friend| `share_with_friend`|
|Authentication_Success| `authentication_success`|
|Watch_later| `watch_later`|
|Custom| `custom`|
