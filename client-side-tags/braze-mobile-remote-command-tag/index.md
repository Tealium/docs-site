---
title: Braze Mobile Remote Command Tag Setup Guide
description: This article describes how to set up the Braze Mobile Remote Command tag.
url: https://docs.tealium.com/client-side-tags/braze-mobile-remote-command-tag/
---
## Tag Tips

* Use mappings to override standard config values and set custom parameters.
* This is a Mobile Remote Command companion tag for the native mobile app SDK.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Braze Mobile Remote Command tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **API Key**: Your application's API Key from the Braze Dashboard
* **Auto Initialize**: Automatically send the Initialize command.
* **Firebase Enabled**
* **ADM Enabled**
* **Automatic Deep Link Opening**
* **Disable Automatic Location Collection**
* **Enable News Feed Unread Indicator**
* **Firebase Sender ID**
* **Custom Endpoint**
* **Session Timeout (seconds)**
* **Notification Background Color** (For example, `0xFFf33e3e`)
* **Interval (in seconds) Between Triggers**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Commands (Command Triggers)

Map a trigger to one or more of the following events:

|Variable| Description|
|---| ---|
|`initSDK`|  <ul><li>SDK Set Up</li></ul> |
|`disableSDK`|  <ul><li>Disable Data Collection</li></ul> |
|`changeUser`|  <ul><li>Identify User</li></ul> |
|`addAlias`|  <ul><li>Set User Alias</li></ul> |
|`logPurchase`|  <ul><li>Purchase Event</li></ul> |
|`facebookUser`|  <ul><li>Facebook User</li></ul> |
|`twitterUser`|  <ul><li>X User</li></ul> |
|`addToSubscriptionGroup`|  <ul><li>Add user to email or SMS subscription group</li></ul> |
|`removeFromSubscriptionGroup`|  <ul><li>Remove user to email or SMS subscription group</li></ul> |

### Location

|Variable| Description|
|---| ---|
|`location_latitude`|  <ul><li>Double</li><li>Latitude</li></ul> |
|`location_longitude`|  <ul><li>Double</li><li>Longitude</li></ul> |
|`location_latitude`|  <ul><li>Double</li><li>Altitude</li></ul> |
|`location_horizontal_accuracy`|  <ul><li>Double</li><li>Horizontal Accuracy</li></ul> |
| `location_vertical_accuracy` |  <ul><li>Double</li><li>Vertical Accuracy</li></ul> |
| `enable_automatic_geofences` | <ul><li>Boolean</li><li>Sets whether Braze Geofences are automatically requested by the Braze SDK. The default value is `true`.</li></ul> | 

### Subscriptions

|Variable| Description|
|---| ---|
|`email_notification`|  <ul><li>Email Subscription</li><li>Set Email Subscription Type</li><li>Sets the notification type for email subscription for the current user.</li></ul> |
|`push_notification`|  <ul><li>Push Subscription</li><li>Set Push Subscription Type</li><li>Sets the notification type for push notifications for the current user.</li></ul> |
|`subscription_group_id`|  <ul><li>The unique identifier of the subscription group.</li></ul> |

### Social Data Tracking

|Variable| Description|
|---| ---|
|`twitterFollowingCount`|  <ul><li>Integer</li><li>X Following Count</li></ul> |
|`twitterProfileImageUrl`|  <ul><li>X Profile Image URL</li></ul> |

### User Attributes

|Variable| Description|
|---| ---|
|`user_id`|  <ul><li>User ID</li></ul> |
| `alias_name` |  <ul><li>Alias Name</li><li>An identifier for the current user.</li></ul> |
| `alias_label` |  <ul><li>User Alias Label</li><li>A label for the alias, such as the source of the alias.</li></ul> |
| `first_name` |  <ul><li>First Name</li></ul> |
| `last_name` |  <ul><li>Last name</li></ul> |
|`gender`|  <ul><li>Gender</li></ul> |
|`language`|  <ul><li>Language</li><li>ISO 639-1 Language Code for the display language.</li></ul> |
|`email`|  <ul><li>Email</li></ul> |
|`home_city`|  <ul><li>Home City</li></ul> |
|`country`|  <ul><li>Country</li></ul> |
| `date_of_birth` |  <ul><li>Date of Birth</li></ul> |
| `phone` | <ul><li>String</li><li>The phone number of the user. A null value unsets the phone number for this user.</li></ul> |
|`unset_custom_attribute`|  <ul><li>Array</li><li>Unset Custom Attribute</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_currency`|  <ul><li>Currency</li><li>Overrides `_ccurrency`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs</li><li>Overrides `_cprod`.</li></ul> |
|`product_qty`|  <ul><li>Array</li><li>List of Quantities</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices</li><li>Overrides `_cprice`.</li></ul> |
| `purchase_properties.foo` |  <ul><li>Custom Purchase Properties</li></ul> |

### Initialization

|Variable| Description|
|---| ---|
|`api_key`|  <ul><li>API Key</li></ul> |
| `sdk_authentication_signature` | <ul><li>String</li><li>SDK Authentication signature</li></ul> |
| `ad_tracking_enabled` | <ul><li>Boolean</li><li>Google Advertising ID's limit ad-tracking field. Note that when "limit ad tracking" is enabled on the Google Advertising ID, it means that ad tracking should be disabled.</li></ul> |
| `is_sdk_authentication_enabled` | <ul><li>Boolean</li><li>The default value is `true`.</li></ul> |
|`firebase_enabled`|  <ul><li>Boolean</li><li>Firebase is enabled</li></ul> |
|`adm_enabled`|  <ul><li>Boolean</li><li>Adm Enabled</li></ul> |
|`auto_push_deep_links`|  <ul><li>Boolean</li><li>Auto Push Deep Links</li></ul> |
|`enable_automatic_location`|  <ul><li>Boolean</li><li>Disable Location</li></ul> |
|`firebase_sender_id`|  <ul><li>String</li><li>Firebase Sender ID</li></ul> |
| `small_notification_icon` |  <ul><li>String</li><li>Small Notification Icon</li></ul> |
|`large_notification_icon`|  <ul><li>String</li><li>Large Notification Icon</li></ul> |
|`custom_endpoint`|  <ul><li>String</li><li>Custom Endpoint</li></ul> |
|`session_timeout`|  <ul><li>Integer</li><li>Session Timeout</li></ul> |
| `default_notification_color` |  <ul><li>Integer</li><li>Default Notification Color</li></ul> |
|`bad_network_interval`|  <ul><li>Integer</li><li>Bad Network Interval</li></ul> |
| `good_network_interval` |  <ul><li>Integer</li><li>Good Network Interval</li></ul> |
|`great_network_interval`|  <ul><li>Integer</li><li>Great Network Interval</li></ul> |
|`trigger_interval_seconds`|  <ul><li>Integer</li><li>Trigger Interval Seconds</li></ul> |
|`push_token`|  <ul><li>String</li><li>Push Token</li></ul> |
|`enable_geofences`|  <ul><li>Boolean</li><li>Enable Geofences</li></ul> |
| `request_processing_policy` |  <ul><li>Integer</li><li>Request Processing Policy</li></ul> |
|`flush_interval`|  <ul><li>Double</li><li>Flush Interval</li></ul> |
|`device_options`|  <ul><li>Integer</li><li>Device Options</li></ul> |
|`push_story_identifier`|  <ul><li>String</li><li>Push Story Identifier</li></ul> |
| `backstack_activity_enabled` |  <ul><li>Boolean</li><li>Backstack Activity Enabled</li></ul> |
|`backstack_activity_class`|  <ul><li>String</li><li>Backstack Activity Class</li></ul> |
