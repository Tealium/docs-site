---
title: Braze Mobile Remote Command Tag Setup Guide
description: This article describes how to set up the Braze Mobile Remote Command tag.
url: https://docs.tealium.com/client-side-tags/braze-mobile-remote-command-tag/
---
## Tag Tips

* Use mappings to override standard config values and set custom parameters.
* This is a Mobile Remote Command companion tag for the native mobile app SDK.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Braze Mobile Remote Command tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **API Key**: Your application&#39;s API Key from the Braze Dashboard
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

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Commands (Command Triggers)

Map a trigger to one or more of the following events:

|Variable| Description|
|---| ---|
|`initSDK`|  &lt;ul&gt;&lt;li&gt;SDK Set Up&lt;/li&gt;&lt;/ul&gt; |
|`disableSDK`|  &lt;ul&gt;&lt;li&gt;Disable Data Collection&lt;/li&gt;&lt;/ul&gt; |
|`changeUser`|  &lt;ul&gt;&lt;li&gt;Identify User&lt;/li&gt;&lt;/ul&gt; |
|`addAlias`|  &lt;ul&gt;&lt;li&gt;Set User Alias&lt;/li&gt;&lt;/ul&gt; |
|`logPurchase`|  &lt;ul&gt;&lt;li&gt;Purchase Event&lt;/li&gt;&lt;/ul&gt; |
|`facebookUser`|  &lt;ul&gt;&lt;li&gt;Facebook User&lt;/li&gt;&lt;/ul&gt; |
|`twitterUser`|  &lt;ul&gt;&lt;li&gt;X User&lt;/li&gt;&lt;/ul&gt; |
|`addToSubscriptionGroup`|  &lt;ul&gt;&lt;li&gt;Add user to email or SMS subscription group&lt;/li&gt;&lt;/ul&gt; |
|`removeFromSubscriptionGroup`|  &lt;ul&gt;&lt;li&gt;Remove user to email or SMS subscription group&lt;/li&gt;&lt;/ul&gt; |

### Location

|Variable| Description|
|---| ---|
|`location_latitude`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;Latitude&lt;/li&gt;&lt;/ul&gt; |
|`location_longitude`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;Longitude&lt;/li&gt;&lt;/ul&gt; |
|`location_latitude`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;Altitude&lt;/li&gt;&lt;/ul&gt; |
|`location_horizontal_accuracy`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;Horizontal Accuracy&lt;/li&gt;&lt;/ul&gt; |
| `location_vertical_accuracy` |  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;Vertical Accuracy&lt;/li&gt;&lt;/ul&gt; |
| `enable_automatic_geofences` | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Sets whether Braze Geofences are automatically requested by the Braze SDK. The default value is `true`.&lt;/li&gt;&lt;/ul&gt; | 

### Subscriptions

|Variable| Description|
|---| ---|
|`email_notification`|  &lt;ul&gt;&lt;li&gt;Email Subscription&lt;/li&gt;&lt;li&gt;Set Email Subscription Type&lt;/li&gt;&lt;li&gt;Sets the notification type for email subscription for the current user.&lt;/li&gt;&lt;/ul&gt; |
|`push_notification`|  &lt;ul&gt;&lt;li&gt;Push Subscription&lt;/li&gt;&lt;li&gt;Set Push Subscription Type&lt;/li&gt;&lt;li&gt;Sets the notification type for push notifications for the current user.&lt;/li&gt;&lt;/ul&gt; |
|`subscription_group_id`|  &lt;ul&gt;&lt;li&gt;The unique identifier of the subscription group.&lt;/li&gt;&lt;/ul&gt; |

### Social Data Tracking

|Variable| Description|
|---| ---|
|`twitterFollowingCount`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;X Following Count&lt;/li&gt;&lt;/ul&gt; |
|`twitterProfileImageUrl`|  &lt;ul&gt;&lt;li&gt;X Profile Image URL&lt;/li&gt;&lt;/ul&gt; |

### User Attributes

|Variable| Description|
|---| ---|
|`user_id`|  &lt;ul&gt;&lt;li&gt;User ID&lt;/li&gt;&lt;/ul&gt; |
| `alias_name` |  &lt;ul&gt;&lt;li&gt;Alias Name&lt;/li&gt;&lt;li&gt;An identifier for the current user.&lt;/li&gt;&lt;/ul&gt; |
| `alias_label` |  &lt;ul&gt;&lt;li&gt;User Alias Label&lt;/li&gt;&lt;li&gt;A label for the alias, such as the source of the alias.&lt;/li&gt;&lt;/ul&gt; |
| `first_name` |  &lt;ul&gt;&lt;li&gt;First Name&lt;/li&gt;&lt;/ul&gt; |
| `last_name` |  &lt;ul&gt;&lt;li&gt;Last name&lt;/li&gt;&lt;/ul&gt; |
|`gender`|  &lt;ul&gt;&lt;li&gt;Gender&lt;/li&gt;&lt;/ul&gt; |
|`language`|  &lt;ul&gt;&lt;li&gt;Language&lt;/li&gt;&lt;li&gt;ISO 639-1 Language Code for the display language.&lt;/li&gt;&lt;/ul&gt; |
|`email`|  &lt;ul&gt;&lt;li&gt;Email&lt;/li&gt;&lt;/ul&gt; |
|`home_city`|  &lt;ul&gt;&lt;li&gt;Home City&lt;/li&gt;&lt;/ul&gt; |
|`country`|  &lt;ul&gt;&lt;li&gt;Country&lt;/li&gt;&lt;/ul&gt; |
| `date_of_birth` |  &lt;ul&gt;&lt;li&gt;Date of Birth&lt;/li&gt;&lt;/ul&gt; |
| `phone` | &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;The phone number of the user. A null value unsets the phone number for this user.&lt;/li&gt;&lt;/ul&gt; |
|`unset_custom_attribute`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Unset Custom Attribute&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_currency`|  &lt;ul&gt;&lt;li&gt;Currency&lt;/li&gt;&lt;li&gt;Overrides `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_qty`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
| `purchase_properties.foo` |  &lt;ul&gt;&lt;li&gt;Custom Purchase Properties&lt;/li&gt;&lt;/ul&gt; |

### Initialization

|Variable| Description|
|---| ---|
|`api_key`|  &lt;ul&gt;&lt;li&gt;API Key&lt;/li&gt;&lt;/ul&gt; |
| `sdk_authentication_signature` | &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;SDK Authentication signature&lt;/li&gt;&lt;/ul&gt; |
| `ad_tracking_enabled` | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Google Advertising ID&#39;s limit ad-tracking field. Note that when &#34;limit ad tracking&#34; is enabled on the Google Advertising ID, it means that ad tracking should be disabled.&lt;/li&gt;&lt;/ul&gt; |
| `is_sdk_authentication_enabled` | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;The default value is `true`.&lt;/li&gt;&lt;/ul&gt; |
|`firebase_enabled`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Firebase is enabled&lt;/li&gt;&lt;/ul&gt; |
|`adm_enabled`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Adm Enabled&lt;/li&gt;&lt;/ul&gt; |
|`auto_push_deep_links`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Auto Push Deep Links&lt;/li&gt;&lt;/ul&gt; |
|`enable_automatic_location`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Disable Location&lt;/li&gt;&lt;/ul&gt; |
|`firebase_sender_id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Firebase Sender ID&lt;/li&gt;&lt;/ul&gt; |
| `small_notification_icon` |  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Small Notification Icon&lt;/li&gt;&lt;/ul&gt; |
|`large_notification_icon`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Large Notification Icon&lt;/li&gt;&lt;/ul&gt; |
|`custom_endpoint`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Custom Endpoint&lt;/li&gt;&lt;/ul&gt; |
|`session_timeout`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;Session Timeout&lt;/li&gt;&lt;/ul&gt; |
| `default_notification_color` |  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;Default Notification Color&lt;/li&gt;&lt;/ul&gt; |
|`bad_network_interval`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;Bad Network Interval&lt;/li&gt;&lt;/ul&gt; |
| `good_network_interval` |  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;Good Network Interval&lt;/li&gt;&lt;/ul&gt; |
|`great_network_interval`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;Great Network Interval&lt;/li&gt;&lt;/ul&gt; |
|`trigger_interval_seconds`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;Trigger Interval Seconds&lt;/li&gt;&lt;/ul&gt; |
|`push_token`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Push Token&lt;/li&gt;&lt;/ul&gt; |
|`enable_geofences`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Enable Geofences&lt;/li&gt;&lt;/ul&gt; |
| `request_processing_policy` |  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;Request Processing Policy&lt;/li&gt;&lt;/ul&gt; |
|`flush_interval`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;Flush Interval&lt;/li&gt;&lt;/ul&gt; |
|`device_options`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;Device Options&lt;/li&gt;&lt;/ul&gt; |
|`push_story_identifier`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Push Story Identifier&lt;/li&gt;&lt;/ul&gt; |
| `backstack_activity_enabled` |  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Backstack Activity Enabled&lt;/li&gt;&lt;/ul&gt; |
|`backstack_activity_class`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Backstack Activity Class&lt;/li&gt;&lt;/ul&gt; |
