---
title: Kochava Mobile Remote Command Tag Setup Guide
description: This article describes how to set up the Kochava Mobile Remote Command tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/kochava-mobile-remote-command-tag/
---
## Tag Tips

* Use mappings to:
  * Override standard config values and set custom parameters
  * Trigger standard and custom events

* This is a Mobile Remote Command companion tag for the native mobile app SDK.

## Tag Configuration

First, go to the tag marketplace and add the Kochava Mobile Remote Command tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **App ID**
* **App Tracking Transparency Enabled**

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Configuration Parameters

|Variable| Description|
|---| ---|
|`app_guid`|  &lt;ul&gt;&lt;li&gt;App ID&lt;/li&gt;&lt;/ul&gt; |
|`app_tracking_transparency_enabled`|  &lt;ul&gt;&lt;li&gt;App Tracking Transparency Enabled&lt;/li&gt;&lt;li&gt;Value are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`identity_link_ids`|  &lt;ul&gt;&lt;li&gt;Identity Link IDs&lt;/li&gt;&lt;/ul&gt; |
|`log_level`|  &lt;ul&gt;&lt;li&gt;Log Level&lt;/li&gt;&lt;/ul&gt; |

### Events

|Variable| Description|
|---| ---|
|`adclick`| Ad Click|
|`adview`| Ad View|
|`addtocart`| Add to Cart|
|`addtowishlist`| Add to wish list|
|`achievement`| Achievement|
|`checkoutstart`| Checkout Start|
|`tutorialcomplete`| Tutorial Complete|
|`consentgranted`| Consent Granted|
|`initialize`| Initialize|
|`invalidate`| Invalidate|
|`levelcomplete`| Level Complete|
|`purchase`| Purchase|
|`pushopened`| Push Opened|
|`pushreceived`| Push Received|
|`rating`| Rating|
|`registrationcomplete`| Registration Complete|
|`search`| Search|
|`sendidentitylink`| Send Identity Link|
|`sleeptracker`| Sleep Tracker|
|`setsleep`| Set Sleep|
|`starttrial`| Start Trial|
|`subscribe`| Subscribe|
|`view`| View|
|`custom`| Custom|

### All Parameters

|Variable| Description|
|---| ---|
|`action`| Action|
|`ad_campaign_id`| Ad Campaign ID|
|`ad_campaign_name`| Ad Campaign Name|
|`ad_device_type`| Ad Device Type|
|`ad_group_id`| Ad Group ID|
|`ad_group_name`| Ad Group Name|
|`ad_mediation_name`| Ad Mediation Name|
|`ad_network_name`| Ad Network Name|
|`ad_size`| Ad Size|
|`ad_type`| Ad Type|
|`app_store_receipt_encoded`| App Store Receipt Encoded|
|`apple_watch_id`| Apple Watch ID|
|`background`| Background|
|`checkout_as_guest`| Checkout as Guest|
|`completed`| Completed|
|`content_id`| Content ID|
|`content_type`| Content Type|
|`currency`| Currency|
|`custom_event_name`| Custom Event Name|
|`date_now`| Date|
|`description`| Description|
|`destination`| Destination|
|`duration`| Duration|
|`end_date`| End Date|
|`from_apple_watch`| From Apple Watch|
|`item_added_from`| Item Added From|
|`level`| Level|
|`max_rating_value`| Max Rating Value|
|`name`| Name|
|`order_id`| Order ID|
|`origin`| Origin|
|`placement`| Placement|
|`price`| Price|
|`quantity`| Quantity|
|`rating_value`| Rating Value|
|`receipt_id`| Receipt ID|
|`referral_from`| Referral From|
|`registration_method`| Registration Method|
|`results`| Results|
|`score`| Score|
|`search_term`| Search Term|
|`sleep`| Sleep|
|`spatial_x`| Spatial X|
|`spatial_y`| Spatial Y|
|`spatial_z`| Spatial Z|
|`start_date`| Start Date|
|`success`| Success|
|`user_id`| User ID|
|`user_name`| User Name|
|`uri`| URI|
|`validated`| Validated|
|`custom`| Custom|

### Event Parameters

|Variable| Description|
|---| ---|
|`adclick`| Ad Click|
|`adview`| Ad View|
|`addtocart`| Add to Cart|
|`addtowishlist`| Add to wish list|
|`achievement`| Achievement|
|`checkoutstart`| Checkout Start|
|`completetutorial`| Complete Tutorial|
|`consentgranted`| Consent Granted|
|`initialize`| Initialize|
|`invalidate`| Invalidate|
|`levelcomplete`| Level Complete|
|`purchase`| Purchase|
|`pushopened`| Push Opened|
|`pushreceived`| Push Received|
|`rating`| Rating|
|`registrationcomplete`| Registration Complete|
|`search`| Search|
|`sendidentitylink`| Send Identity Link|
|`setsleep`| Set Sleep|
|`sleeptracker`| Sleep Tracker|
|`starttrial`| Start Trial|
|`subscribe`| Subscribe|
|`view`| View|
|`custom`| Custom|
