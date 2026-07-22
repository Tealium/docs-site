---
title: Braze Web SDK Tag Setup Guide
description: This article describes how to set up the Braze Web SDK tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/braze-web-sdk-tag/
---
## Supported Versions

* 6.8
* 5.5
* 4.8
* 3.5


<blockquote>
The Braze Web SDK Tag supports tag template versions 3.3 and older. For best tag performance and functionality, we recommend updating to the most recent tag template.
</blockquote>


## Tag Tips

* The Purchase Event fires when an Order ID is present.
* Supports these E-Commerce extension parameters:
  * Customer ID (Overrides `_ccustid`)
  * City (Overrides `_ccity`)
  * Country (Overrides `_ccountry`)
  * Order ID (Overrides `_corder`)
  * Sub Total (Overrides `_csubtotal`)
  * Currency (Overrides `_ccurrency`)
  * Product IDs (Overrides `_cprod`)
  * Product Quantities (Overrides `_cquan`)

* Use mapping to dynamically override the standard configuration values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

After adding the tag, configure the following settings:

* **Code Version**
  * Enter the major.minor version of the Braze Web SDK version you want to use.
  * For example, to deploy version 4.8.1, enter 4.8.
  * Code versions 4.0+ no longer support Internet Explorer.
  * To find the latest version of the Braze Web SDK, see the [changelog](https://github.com/Appboy/appboy-web-sdk/blob/master/CHANGELOG.md).

* **API Key**
  * Your unique API key, available on your Braze dashboard in the **Manage App Group** settings.

* **Base URL**
  * The API endpoint pointing to the Braze Cluster you are assigned.
  * Example for 4.0: `https://js.appboycdn.com/web-sdk/4.0/braze.no-amd.min.js`
  * Example for versions 3.5 and older: `https://js.appboycdn.com/web-sdk/3.5/appboy.no-amd.min.js`
  * For a list of options, see [Braze SDK Endpoints](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints/).

* **Enable Logging**
  * When enabled, this will log debugging information in the web console.

## Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. ([Learn more](https://docs.tealium.com/iq-tag-management/data-mappings/manage/))

The destination variables for the Braze Web SDK tag are built into the Data Mapping tab for the tag. The following tables list the available destination categories and describe each destination name.

### Standard

| **Destination Name**              | **Description**                                                                                                                                                                                                        |
|:----------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `api_key`                                | <ul><li>API Key</li><li>Your unique API key, available in the Braze dashboard under <strong>Manage App Group</strong> settings.</li></ul>                                                                         |
| `code_version`                           | <ul><li>Code Version</li><li>The major.minor version of the Braze Web SDK to load.</li><li>For example, enter <code>6.8</code> to deploy the latest 6.8.x release.</li></ul>                                     |
| `initOpt.allow_crawler`           | <ul><li>Allow Crawlers</li><li>All activity from web crawlers to be recorded by Braze.</li><li>Options are `true` or `false`.</li></ul>                                                                                |
| `initOpt.app_ver`                 | <ul><li>App Version</li><li>The version of your app to associate data with.</li></ul>                                                                                                                                  |
| `initOpt.base_url`                | <ul><li>Base URL</li><li>Full URL to your Braze-provided custom endpoint.</li></ul>                                                                                                                                    |
| `initOpt.no_cookies`              | <ul><li>No Cookies</li><li>Prevent Braze from storing user information in cookies.</li><li>Options are `true` or `false`.</li></ul>                                                                                    |
| `initOpt.no_fntawsm`              | <ul><li>No Font Awesome</li><li>Prevent Braze from loading `FontAwesome`.</li><li>Options are `true` or `false`.</li></ul>                                                                                             |
| `initOpt.enable_htmlmsgs`         | <ul><li>Enable HTML in Messages</li><li>Allow Braze users to send HTML through in-app messages.</li><li>Options are `true` or `false`.</li></ul>                                                                           |
| `initOpt.enable_logging`          | <ul><li>Enable Logging</li><li>Allow Braze error messages in the web console to display.</li><li>Options are `true` or `false`.</li></ul>                                                                              |
| `initOpt.localization`            | <ul><li>Localization</li><li>An ISO 639-1 Language Code used to override the browser default language.</li></ul>                                                                                                       |
| `initOpt.min_trggrinterval`       | <ul><li>Minimum Interval Between Actions</li><li>The time, in seconds, before another trigger action can occur.</li><li>Default value is `30`.</li></ul>                                                               |
| `initOpt.msg_innewtab`            | <ul><li>Open In App Messages In New Tab</li><li>Force in-app message links to open in a new tab or window.</li><li>Options are `true` or `false`.</li></ul>                                                            |
| `initOpt.card_innewtab`           | <ul><li>Open News Feed Cards In New Tab</li><li>Force news feed card links to open in a new tab or window.</li><li>Options are `true` or `false`.</li></ul>                                                            |
| `initOpt.explicit_dissmisal`      | <ul><li>Require Explicit Dismissal</li><li>Force user to click a button to dismiss messages.</li><li>Options are `true` or `false`.</li></ul>                                                                          |
| `initOpt.safari_pushid`           | <ul><li>Safari Website Push ID</li><li>The ID from your Safari push certificate.</li></ul>                                                                                                                             |
| `initOpt.srvcewrkr_location`      | <ul><li>Service Worker Location</li><li>Path to your `service-worker.js` file if it is not in the root directory.</li></ul>                                                                                            |
| `initOpt.session_timeout`         | <ul><li>Session Timeout</li><li>Time until the session will time out, in minutes.</li><li>Default: value is `30`.</li></ul>                                                                                            |
| `initOpt.devicePropertyAllowlist`        | <ul><li>Device Property Allow List</li><li>An array of device properties to collect.</li><li>Properties not in the list are excluded from collection.</li></ul>                                                  |
| `initOpt.enableSdkAuthentication`        | <ul><li>Enable SDK Authentication</li><li>Appends the current user's last known JSON web token to network requests made to Braze servers.</li><li>This setting is available in versions 3.5 and higher.</li><li>Options are `true` or `false`.</li></ul> |
| `initOpt.sdk_auth_signature`             | <ul><li>SDK Authentication Signature</li><li>The JSON web token used to authenticate SDK requests when SDK Authentication is enabled.</li><li>This setting is available in versions 3.5 and higher.</li></ul>    |
| `initOpt.allow_user_supplied_javascript` | <ul><li>Allow User Supplied Javascript</li><li>Allows user-supplied JavaScript to run in in-app messages.</li><li>Options are `true` or `false`.</li></ul>                                                       |
| `initOpt.content_security_nonce`         | <ul><li>Content Security Nonce</li><li>A nonce string to include in Braze SDK script tags for Content Security Policy compliance.</li></ul>                                                                      |
| `initOpt.disable_push_token_maintenance` | <ul><li>Disable Push Token Maintenance</li><li>Disables automatic push token refresh on session start.</li><li>Options are `true` or `false`.</li></ul>                                                          |
| `initOpt.in_app_message_zindex`          | <ul><li>In App Message Zindex</li><li>Overrides the default z-index for the in-app message overlay.</li></ul>                                                                                                    |

### E-Commerce

The Braze Web SDK tag is e-commerce enabled and will therefore automatically use the default E-Commerce extension mappings. Manually mapping in this category is generally not needed unless you want to override any extension mappings or an e-commerce variable is not offered in the extension.

| **Destination Name** | **Description**                                                                 |
|:---------------------|:--------------------------------------------------------------------------------|
| `order_id`           | <ul><li>Order Id</li><li>Overrides `_corder`.</li></ul>                         |
| `order_subtotal`     | <ul><li>Sub Total</li><li>Overrides `_csubtotal`.</li></ul>                     |
| `order_currency`     | <ul><li>Currency</li><li>Overrides `_ccurrency`.</li></ul>                      |
| `customer_id`        | <ul><li>Customer ID</li><li>Overrides `_ccustid`.</li></ul>                     |
| `customer_city`      | <ul><li>Customer City</li><li>Overrides `_ccity`.</li></ul>                     |
| `customer_country`   | <ul><li>Customer Country</li><li>Overrides `_ccountry`.</li></ul>               |
| `product_id`         | <ul><li>Array</li><li>List of Product IDs</li><li>Overrides `_cprod`.</li></ul> |
| `product_quantity`   | <ul><li>Array</li><li>List of Quantities</li><li>Overrides `_cquan`.</li></ul>  |

### Event

Map to these destinations for triggering specific events on a page.

Use the following steps to trigger an event:

1. Select an event from the drop-down list.
  * You can select from the predefined list or create a custom event.
  * For a custom event, enter a name with which to identify it.

1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the **+** button and repeat Steps 1 and 2.
1. Click **Apply**.

The following table lists the event triggers when the supplied value is found in the data layer.

| **Destination Name**     | **Description**                                                                                                                                                     |
|:-------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Purchase`               | <ul><li>Log Purchase</li><li>An In-App purchase is made by the current user.</li><li>The Purchase event is automatically set when an Order ID is present.</li></ul> |
| `Alias`                  | <ul><li>Add User Alias</li><li>A new alias is added for the current user.</li></ul>                                                                                 |
| `addToSubscriptionGroup` | <ul><li>Adds a user to an email or SMS subscription group.</li><li>This setting is available in versions 3.5 and higher.</li></ul>                                  |
| `AddAtt`                 | <ul><li>Add Custom Attribute to Array</li><li>A new attribute is added to the custom attribute array.</li></ul>                                                     |
| `IncAtt`                 | <ul><li>Increment Custom Attribute</li><li>Increments an attribute currently in the custom attribute array.</li></ul>                                               |
| `RmvAtt`                 | <ul><li>Remove Custom Attribute from Array</li><li>Removes an attribute from the custom attribute array.</li></ul>                                                  |
| `SetAtt`                 | <ul><li>Set User Attribute</li><li>Sets a new custom attribute for the current user.</li></ul>                                                                      |
| `SetAvatar`              | <ul><li>Set Avatar</li><li>Sets the avatar URL for the current user.</li><li>Not available in versions 4.0 and higher.</li></ul>                                    |
| `SetLoc`                 | <ul><li>Set Last Location</li><li>Sets the last known location of the current user.</li></ul>                                                                       |
| `SetDOB`                 | <ul><li>Set Date of Birth</li><li>Sets the day, month and year of birth for the current user.</li></ul>                                                             |
| `SetEmail`               | <ul><li>Set Email</li><li>Sets the email for the current user.</li></ul>                                                                                            |
| `SetEmailSub`            | <ul><li>Set Email Subscription Type</li><li>Sets the notification type for email subscription for the current user.</li></ul>                                       |
| `SetPushSub`             | <ul><li>Set Push Subscription Type</li><li>Sets the notification type for push notifications for the current user.</li></ul>                                        |
| `SetFirst`               | <ul><li>Set First Name</li><li>Sets the first name for the current user.</li></ul>                                                                                  |
| `SetLast`                | <ul><li>Set Last Name</li><li>Sets the last name for the current user.</li></ul>                                                                                    |
| `SetCity`                | <ul><li>Set Home City</li><li>Sets the city for the current user.</li></ul>                                                                                         |
| `SetCountry`             | <ul><li>Set Country</li><li>Sets the country for the current user.</li></ul>                                                                                        |
| `SetLang`                | <ul><li>Set Language</li><li>Sets the language for the current user.</li></ul>                                                                                      |
| `SetPhone`               | <ul><li>Set Phone Number</li><li>Sets the phone number for the current user.</li></ul>                                                                              |
| `SetGender`              | <ul><li>Set Gender</li><li>Sets the gender for the current user.</li></ul>                                                                                          |
| `removeFromSubscriptionGroup` | <ul><li>Remove From Subscription Group</li><li>Removes the current user from an email or SMS subscription group.</li><li>This setting is available in versions 3.5 and higher.</li></ul> |
| `setCustomLocationAttribute` | <ul><li>Set Custom Location Attribute</li><li>Sets a custom location attribute (key, latitude, longitude) for the current user.</li></ul>                          |
| `SetLineId`              | <ul><li>Set LINE ID</li><li>Sets the LINE messaging app ID for the current user.</li></ul>                                                                          |
| `Ecommerce`              | <ul><li>Log Ecommerce Event</li><li>Logs a structured ecommerce event for the current user.</li><li>This setting is available in versions 6.0 and higher.</li></ul> |
| `WipeData`               | <ul><li>Wipe Data (delete local SDK data)</li><li>Deletes all locally stored SDK data and disables the SDK.</li><li>The SDK must be explicitly re-enabled before further data collection resumes.</li></ul> |
| `RefreshFeatureFlags`    | <ul><li>Refresh Feature Flags</li><li>Requests a refresh of feature flags for the current user from Braze.</li></ul>                                                |
| `LogFeatureFlagImpression` | <ul><li>Log Feature Flag Impression</li><li>Logs an impression event for the specified feature flag.</li></ul>                                                    |
| `RefreshContentCards`    | <ul><li>Refresh Content Cards</li><li>Requests a refresh of the Content Cards feed from Braze.</li></ul>                                                            |
| `ShowContentCards`       | <ul><li>Show Content Cards</li><li>Displays the Content Cards feed.</li></ul>                                                                                       |
| `LogContentCardImpressions` | <ul><li>Log Content Card Impressions</li><li>Logs impression events for an array of Content Cards.</li></ul>                                                     |
| `LogContentCardClick`    | <ul><li>Log Content Card Click</li><li>Logs a click event for a specific Content Card.</li></ul>                                                                    |
| `RequestPushPermission`  | <ul><li>Request Push Permission</li><li>Prompts the user to grant push notification permission.</li></ul>                                                           |
| `UnregisterPush`         | <ul><li>Unregister Push</li><li>Unregisters the current device from push notifications.</li></ul>                                                                   |
| `FlushData`              | <ul><li>Flush Data</li><li>Immediately sends queued analytics data to Braze servers.</li></ul>                                                                      |
| `RefreshBanners`         | <ul><li>Refresh Banners</li><li>Requests a refresh of Braze Banners for the specified placement IDs.</li><li>This setting is available in versions 6.0 and higher.</li></ul> |
| `LogBannerImpressions`   | <ul><li>Log Banner Impressions</li><li>Logs impression events for an array of Banner placement IDs.</li><li>This setting is available in versions 6.0 and higher.</li></ul> |
| `LogBannerClick`         | <ul><li>Log Banner Click</li><li>Logs a click event for a specific Banner.</li><li>This setting is available in versions 6.0 and higher.</li></ul>                  |
| `InsertBanner`           | <ul><li>Insert Banner</li><li>Retrieves a Banner for the specified placement ID and inserts it into the specified parent element.</li><li>This setting is available in versions 6.0 and higher.</li></ul> |
| `Custom`                 | <ul><li>Custom</li><li>Sends a custom event made by the current user.</li></ul>                                                                                     |

### Parameter

Map to these destinations to pass data to the events mapped earlier. Parameters are only used with predefined Events. See the Custom Event Data section below to learn how to pass a parameter with a custom event.

Use the following steps to pass a parameter to a predefined event:

1. In the Event field, select an event from the drop-down list.
1. In the Parameter field, select a parameter from the drop-down list.
1. For a custom parameter, enter a name to identify the custom event.
1. Click **+ Add**.

| **Destination Name**  | **Description**                                                                                                                                                                                                                                    |
|:----------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `product_id`          | <ul><li>Product ID</li><li>The unique ID for the in-app product purchased.</li><li>Overrides `_cprod`.</li></ul>                                                                                                                                   |
| `product_quantity`    | <ul><li>Product Quantity</li><li>The quantity of the in-app product purchased.</li><li>This overrides the e-commerce value `_cquan`.</li></ul>                                                                                                     |
| `order_id`            | <ul><li>Order ID</li><li>The unique ID for the in-app purchase.</li><li>Overrides `_corder`.</li></ul>                                                                                                                                             |
| `order_subtotal`      | <ul><li>Order Subtotal</li><li>The subtotal for the in-app purchase.</li><li>Overrides `_csubtotal`.</li></ul>                                                                                                                                     |
| `order_currency`      | <ul><li>Order Currency</li><li>The ISO 4217 currency code for the in-app purchase.</li><li>Overrides `_ccurrency`.</li></ul>                                                                                                                        |
| `purchase_properties` | <ul><li>Purchase Properties</li><li>An object of additional properties for the in-app purchase.</li></ul>                                                                                                                                          |
| `alias`               | <ul><li>User Alias</li><li>An identifier for the current user.</li></ul>                                                                                                                                                                           |
| `label`               | <ul><li>Alias Label</li><li>A label for the alias, such as the source of the alias.</li></ul>                                                                                                                                                      |
| `key`                 | <ul><li>Custom Attribute Key</li><li>The identifier for the custom attribute.</li><li>Enter the name of the parameter to send.</li></ul>                                                                                                           |
| `value`               | <ul><li>Custom Attribute Value</li><li>The value for the custom attribute.</li><li>Enter the name of the parameter to send.</li></ul>                                                                                                              |
| `inc_value`           | <ul><li>Custom Attribute Incrementation Value</li><li>The value by which to increment a custom user attribute.</li><li>Enter the name of the parameter to send.</li><li>Use negative numbers to decrement.</li><li>Default value is `1`.</li></ul> |
| `custom_attributes`   | <ul><li>Custom Attribute Object</li><li>An object of custom attribute key-value pairs to set on the current user in a single call.</li></ul>                                                                                                       |
| `line_id`             | <ul><li>User's LINE ID</li><li>The LINE messaging app ID for the current user.</li></ul>                                                                                                                                                          |
| `feature_flag_id`     | <ul><li>Feature Flag ID</li><li>The unique identifier of the feature flag to log an impression for.</li></ul>                                                                                                                                     |
| `banner_placement_ids` | <ul><li>Banner Placement IDs (Array or comma-separated)</li><li>An array or comma-separated string of Banner placement IDs to refresh or log impressions for.</li><li>This setting is available in versions 6.0 and higher.</li></ul>            |
| `banner_placement_id` | <ul><li>Banner Placement ID</li><li>The unique identifier for a single Banner placement to retrieve and insert.</li><li>This setting is available in versions 6.0 and higher.</li></ul>                                                           |
| `banner_click_id`     | <ul><li>Banner Click ID</li><li>The click tracking ID of the Banner that was clicked.</li><li>This setting is available in versions 6.0 and higher.</li></ul>                                                                                     |
| `banner_parent_selector` | <ul><li>Banner Parent Selector (CSS)</li><li>A CSS selector string identifying the parent element into which the Banner is inserted.</li><li>This setting is available in versions 6.0 and higher.</li></ul>                                   |
| `content_cards`       | <ul><li>Content Cards Array</li><li>An array of Content Card objects to log impressions for.</li></ul>                                                                                                                                            |
| `content_card`        | <ul><li>Content Card Object</li><li>A single Content Card object to log a click for.</li></ul>                                                                                                                                                    |
| `ecommerce_event_name` | <ul><li>Ecommerce Event Name</li><li>The name of the ecommerce event to log.</li><li>This setting is available in versions 6.0 and higher.</li></ul>                                                                                             |
| `ecommerce_properties` | <ul><li>Ecommerce Properties</li><li>An object of properties for the ecommerce event.</li><li>Supports a <code>source</code> field that defaults to <code>"tealium"</code>.</li><li>This setting is available in versions 6.0 and higher.</li></ul> |
| `avatar_url`          | <ul><li>Avatar Image URL</li><li>URL for the current user's selected avatar.</li><li>Not available in versions 4.0 and higher.</li></ul>                                                                                                           |
| `longitude`           | <ul><li>User's Longitude</li><li>The validated longitude of the user's location, in degrees.</li><li>Values are from `-180` to `180`</li></ul>                                                                                                     |
| `latitude`            | <ul><li>User's Latitude</li><li>The validated latitude of the user's location, in degrees.</li><li>Values are from `-90` to `90`</li></ul>                                                                                                         |
| `accuracy`            | <ul><li>Location Accuracy</li><li>The accuracy of the user's longitude and latitude, in meters.</li></ul>                                                                                                                                          |
| `altitude`            | <ul><li>User's Altitude</li><li>The altitude of the user's location, in meters.</li></ul>                                                                                                                                                          |
| `altitude_accuracy`   | <ul><li>Altitude Accuracy</li><li>The accuracy of the user's altitude, in meters.</li></ul>                                                                                                                                                        |
| `year`                | <ul><li>User's Birth Year</li><li>The year associated with the current user's birthday.</li></ul>                                                                                                                                                  |
| `month`               | <ul><li>User's Birth Month</li><li>The month associated with the current user's birthday.</li></ul>                                                                                                                                                |
| `day`                 | <ul><li>User's Birth Day</li><li>The day associated with the current user's birthday.</li></ul>                                                                                                                                                    |
| `email`               | <ul><li>User's Email</li><li>The validated email address of the current user.</li></ul>                                                                                                                                                            |
| `notification_type`   | <ul><li>Notification Subscription Type</li><li>Selected notification type for the current user.</li><li>Options: `opted_in`, `subscribed`, `unsubscribed`</li></ul>                                                                                |
| `first_name`          | <ul><li>User's First Name</li><li>The first name of the current user.</li></ul>                                                                                                                                                                    |
| `subscriptionGroupId` | <ul><li>Subscription group ID.</li><li>The unique identifier of the subscription group.</li></ul>                                                                                                                                                  |
| `last_name`           | <ul><li>User's Last Name</li><li>The last name of the current user.</li></ul>                                                                                                                                                                      |
| `gender`              | <ul><li>User's Gender</li><li>Gender code for the current user.</li><li>Options are male (`m`), female (`f`), or other `o`.</li></ul>                                                                                                              |
| `customer_city`       | <ul><li>User's Home City</li><li>The home city of the current user.</li><li>Overrides `_ccity`.</li></ul>                                                                                                                                          |
| `customer_country`    | <ul><li>User's Country</li><li>The country of the current user.</li><li>Overrides `_ccountry`.</li></ul>                                                                                                                                           |
| `localization`        | <ul><li>User's Language</li><li>The ISO 639-1 Language Code for the current user's display language.</li></ul>                                                                                                                                     |
| `phone_number`        | <ul><li>User's Phone Number</li><li>The phone number for the current user.</li><li>Allows only numbers, spaces, and the `+`, `.`, `-`, ` ( `, and `)` characters</li></ul>                                                                         |

### Custom Event Data

Map to custom event data destinations if you want to pass a custom parameter with a custom event that you previously mapped in the Events tab.

Use the following steps to map a custom event data variable:

1. For **Event Name**, enter the name of the custom event, exactly as specified in the **Events** tab.
1. For **Parameter**, enter the name of the parameter you want to send.
1. Click **+ Add**.

### Cookie Consent

Map to the Cookie Consent destination to control whether the Braze SDK is enabled or disabled based on a user's consent state. Consent gating runs before SDK initialization.

| **Value** | **Description**                                                                                          |
|:----------|:---------------------------------------------------------------------------------------------------------|
| `grant`   | Enables the SDK and allows data collection to proceed. The SDK initializes and opens a session normally. |
| `revoke`  | Disables the SDK before initialization. No data is collected and no session is opened.                   |

## Vendor Documentation

* [Braze Web SDK](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/initial_sdk_setup/)
