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

The Braze Web SDK Tag supports tag template versions 3.3 and older. For best tag performance and functionality, we recommend updating to the most recent tag template.

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

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

After adding the tag, configure the following settings:

* **Code Version**
  * Enter the major.minor version of the Braze Web SDK version you want to use.
  * For example, to deploy version 4.8.1, enter 4.8.
  * Code versions 4.0&#43; no longer support Internet Explorer.
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

[Load Rules]() determine when and where to load an instance of this tag on your site.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. ([Learn more](/iq-tag-management/data-mappings/manage/))

The destination variables for the Braze Web SDK tag are built into the Data Mapping tab for the tag. The following tables list the available destination categories and describe each destination name.

### Standard

| **Destination Name**              | **Description**                                                                                                                                                                                                        |
|:----------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `api_key`                                | &lt;ul&gt;&lt;li&gt;API Key&lt;/li&gt;&lt;li&gt;Your unique API key, available in the Braze dashboard under &lt;strong&gt;Manage App Group&lt;/strong&gt; settings.&lt;/li&gt;&lt;/ul&gt;                                                                         |
| `code_version`                           | &lt;ul&gt;&lt;li&gt;Code Version&lt;/li&gt;&lt;li&gt;The major.minor version of the Braze Web SDK to load.&lt;/li&gt;&lt;li&gt;For example, enter &lt;code&gt;6.8&lt;/code&gt; to deploy the latest 6.8.x release.&lt;/li&gt;&lt;/ul&gt;                                     |
| `initOpt.allow_crawler`           | &lt;ul&gt;&lt;li&gt;Allow Crawlers&lt;/li&gt;&lt;li&gt;All activity from web crawlers to be recorded by Braze.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                                                |
| `initOpt.app_ver`                 | &lt;ul&gt;&lt;li&gt;App Version&lt;/li&gt;&lt;li&gt;The version of your app to associate data with.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                  |
| `initOpt.base_url`                | &lt;ul&gt;&lt;li&gt;Base URL&lt;/li&gt;&lt;li&gt;Full URL to your Braze-provided custom endpoint.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                    |
| `initOpt.no_cookies`              | &lt;ul&gt;&lt;li&gt;No Cookies&lt;/li&gt;&lt;li&gt;Prevent Braze from storing user information in cookies.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                                                    |
| `initOpt.no_fntawsm`              | &lt;ul&gt;&lt;li&gt;No Font Awesome&lt;/li&gt;&lt;li&gt;Prevent Braze from loading `FontAwesome`.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                                                             |
| `initOpt.enable_htmlmsgs`         | &lt;ul&gt;&lt;li&gt;Enable HTML in Messages&lt;/li&gt;&lt;li&gt;Allow Braze users to send HTML through in-app messages.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                                           |
| `initOpt.enable_logging`          | &lt;ul&gt;&lt;li&gt;Enable Logging&lt;/li&gt;&lt;li&gt;Allow Braze error messages in the web console to display.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                                              |
| `initOpt.localization`            | &lt;ul&gt;&lt;li&gt;Localization&lt;/li&gt;&lt;li&gt;An ISO 639-1 Language Code used to override the browser default language.&lt;/li&gt;&lt;/ul&gt;                                                                                                       |
| `initOpt.min_trggrinterval`       | &lt;ul&gt;&lt;li&gt;Minimum Interval Between Actions&lt;/li&gt;&lt;li&gt;The time, in seconds, before another trigger action can occur.&lt;/li&gt;&lt;li&gt;Default value is `30`.&lt;/li&gt;&lt;/ul&gt;                                                               |
| `initOpt.msg_innewtab`            | &lt;ul&gt;&lt;li&gt;Open In App Messages In New Tab&lt;/li&gt;&lt;li&gt;Force in-app message links to open in a new tab or window.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                            |
| `initOpt.card_innewtab`           | &lt;ul&gt;&lt;li&gt;Open News Feed Cards In New Tab&lt;/li&gt;&lt;li&gt;Force news feed card links to open in a new tab or window.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                            |
| `initOpt.explicit_dissmisal`      | &lt;ul&gt;&lt;li&gt;Require Explicit Dismissal&lt;/li&gt;&lt;li&gt;Force user to click a button to dismiss messages.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                                          |
| `initOpt.safari_pushid`           | &lt;ul&gt;&lt;li&gt;Safari Website Push ID&lt;/li&gt;&lt;li&gt;The ID from your Safari push certificate.&lt;/li&gt;&lt;/ul&gt;                                                                                                                             |
| `initOpt.srvcewrkr_location`      | &lt;ul&gt;&lt;li&gt;Service Worker Location&lt;/li&gt;&lt;li&gt;Path to your `service-worker.js` file if it is not in the root directory.&lt;/li&gt;&lt;/ul&gt;                                                                                            |
| `initOpt.session_timeout`         | &lt;ul&gt;&lt;li&gt;Session Timeout&lt;/li&gt;&lt;li&gt;Time until the session will time out, in minutes.&lt;/li&gt;&lt;li&gt;Default: value is `30`.&lt;/li&gt;&lt;/ul&gt;                                                                                            |
| `initOpt.devicePropertyAllowlist`        | &lt;ul&gt;&lt;li&gt;Device Property Allow List&lt;/li&gt;&lt;li&gt;An array of device properties to collect.&lt;/li&gt;&lt;li&gt;Properties not in the list are excluded from collection.&lt;/li&gt;&lt;/ul&gt;                                                  |
| `initOpt.enableSdkAuthentication`        | &lt;ul&gt;&lt;li&gt;Enable SDK Authentication&lt;/li&gt;&lt;li&gt;Appends the current user&#39;s last known JSON web token to network requests made to Braze servers.&lt;/li&gt;&lt;li&gt;This setting is available in versions 3.5 and higher.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
| `initOpt.sdk_auth_signature`             | &lt;ul&gt;&lt;li&gt;SDK Authentication Signature&lt;/li&gt;&lt;li&gt;The JSON web token used to authenticate SDK requests when SDK Authentication is enabled.&lt;/li&gt;&lt;li&gt;This setting is available in versions 3.5 and higher.&lt;/li&gt;&lt;/ul&gt;    |
| `initOpt.allow_user_supplied_javascript` | &lt;ul&gt;&lt;li&gt;Allow User Supplied Javascript&lt;/li&gt;&lt;li&gt;Allows user-supplied JavaScript to run in in-app messages.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                       |
| `initOpt.content_security_nonce`         | &lt;ul&gt;&lt;li&gt;Content Security Nonce&lt;/li&gt;&lt;li&gt;A nonce string to include in Braze SDK script tags for Content Security Policy compliance.&lt;/li&gt;&lt;/ul&gt;                                                                      |
| `initOpt.disable_push_token_maintenance` | &lt;ul&gt;&lt;li&gt;Disable Push Token Maintenance&lt;/li&gt;&lt;li&gt;Disables automatic push token refresh on session start.&lt;/li&gt;&lt;li&gt;Options are `true` or `false`.&lt;/li&gt;&lt;/ul&gt;                                                          |
| `initOpt.in_app_message_zindex`          | &lt;ul&gt;&lt;li&gt;In App Message Zindex&lt;/li&gt;&lt;li&gt;Overrides the default z-index for the in-app message overlay.&lt;/li&gt;&lt;/ul&gt;                                                                                                    |

### E-Commerce

The Braze Web SDK tag is e-commerce enabled and will therefore automatically use the default E-Commerce extension mappings. Manually mapping in this category is generally not needed unless you want to override any extension mappings or an e-commerce variable is not offered in the extension.

| **Destination Name** | **Description**                                                                 |
|:---------------------|:--------------------------------------------------------------------------------|
| `order_id`           | &lt;ul&gt;&lt;li&gt;Order Id&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt;                         |
| `order_subtotal`     | &lt;ul&gt;&lt;li&gt;Sub Total&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt;                     |
| `order_currency`     | &lt;ul&gt;&lt;li&gt;Currency&lt;/li&gt;&lt;li&gt;Overrides `_ccurrency`.&lt;/li&gt;&lt;/ul&gt;                      |
| `customer_id`        | &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`.&lt;/li&gt;&lt;/ul&gt;                     |
| `customer_city`      | &lt;ul&gt;&lt;li&gt;Customer City&lt;/li&gt;&lt;li&gt;Overrides `_ccity`.&lt;/li&gt;&lt;/ul&gt;                     |
| `customer_country`   | &lt;ul&gt;&lt;li&gt;Customer Country&lt;/li&gt;&lt;li&gt;Overrides `_ccountry`.&lt;/li&gt;&lt;/ul&gt;               |
| `product_id`         | &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
| `product_quantity`   | &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt;  |

### Event

Map to these destinations for triggering specific events on a page.

Use the following steps to trigger an event:

1. Select an event from the drop-down list.
  * You can select from the predefined list or create a custom event.
  * For a custom event, enter a name with which to identify it.

1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the **&#43;** button and repeat Steps 1 and 2.
1. Click **Apply**.

The following table lists the event triggers when the supplied value is found in the data layer.

| **Destination Name**     | **Description**                                                                                                                                                     |
|:-------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Purchase`               | &lt;ul&gt;&lt;li&gt;Log Purchase&lt;/li&gt;&lt;li&gt;An In-App purchase is made by the current user.&lt;/li&gt;&lt;li&gt;The Purchase event is automatically set when an Order ID is present.&lt;/li&gt;&lt;/ul&gt; |
| `Alias`                  | &lt;ul&gt;&lt;li&gt;Add User Alias&lt;/li&gt;&lt;li&gt;A new alias is added for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                 |
| `addToSubscriptionGroup` | &lt;ul&gt;&lt;li&gt;Adds a user to an email or SMS subscription group.&lt;/li&gt;&lt;li&gt;This setting is available in versions 3.5 and higher.&lt;/li&gt;&lt;/ul&gt;                                  |
| `AddAtt`                 | &lt;ul&gt;&lt;li&gt;Add Custom Attribute to Array&lt;/li&gt;&lt;li&gt;A new attribute is added to the custom attribute array.&lt;/li&gt;&lt;/ul&gt;                                                     |
| `IncAtt`                 | &lt;ul&gt;&lt;li&gt;Increment Custom Attribute&lt;/li&gt;&lt;li&gt;Increments an attribute currently in the custom attribute array.&lt;/li&gt;&lt;/ul&gt;                                               |
| `RmvAtt`                 | &lt;ul&gt;&lt;li&gt;Remove Custom Attribute from Array&lt;/li&gt;&lt;li&gt;Removes an attribute from the custom attribute array.&lt;/li&gt;&lt;/ul&gt;                                                  |
| `SetAtt`                 | &lt;ul&gt;&lt;li&gt;Set User Attribute&lt;/li&gt;&lt;li&gt;Sets a new custom attribute for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                      |
| `SetAvatar`              | &lt;ul&gt;&lt;li&gt;Set Avatar&lt;/li&gt;&lt;li&gt;Sets the avatar URL for the current user.&lt;/li&gt;&lt;li&gt;Not available in versions 4.0 and higher.&lt;/li&gt;&lt;/ul&gt;                                    |
| `SetLoc`                 | &lt;ul&gt;&lt;li&gt;Set Last Location&lt;/li&gt;&lt;li&gt;Sets the last known location of the current user.&lt;/li&gt;&lt;/ul&gt;                                                                       |
| `SetDOB`                 | &lt;ul&gt;&lt;li&gt;Set Date of Birth&lt;/li&gt;&lt;li&gt;Sets the day, month and year of birth for the current user.&lt;/li&gt;&lt;/ul&gt;                                                             |
| `SetEmail`               | &lt;ul&gt;&lt;li&gt;Set Email&lt;/li&gt;&lt;li&gt;Sets the email for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                            |
| `SetEmailSub`            | &lt;ul&gt;&lt;li&gt;Set Email Subscription Type&lt;/li&gt;&lt;li&gt;Sets the notification type for email subscription for the current user.&lt;/li&gt;&lt;/ul&gt;                                       |
| `SetPushSub`             | &lt;ul&gt;&lt;li&gt;Set Push Subscription Type&lt;/li&gt;&lt;li&gt;Sets the notification type for push notifications for the current user.&lt;/li&gt;&lt;/ul&gt;                                        |
| `SetFirst`               | &lt;ul&gt;&lt;li&gt;Set First Name&lt;/li&gt;&lt;li&gt;Sets the first name for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                  |
| `SetLast`                | &lt;ul&gt;&lt;li&gt;Set Last Name&lt;/li&gt;&lt;li&gt;Sets the last name for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                    |
| `SetCity`                | &lt;ul&gt;&lt;li&gt;Set Home City&lt;/li&gt;&lt;li&gt;Sets the city for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                         |
| `SetCountry`             | &lt;ul&gt;&lt;li&gt;Set Country&lt;/li&gt;&lt;li&gt;Sets the country for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                        |
| `SetLang`                | &lt;ul&gt;&lt;li&gt;Set Language&lt;/li&gt;&lt;li&gt;Sets the language for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                      |
| `SetPhone`               | &lt;ul&gt;&lt;li&gt;Set Phone Number&lt;/li&gt;&lt;li&gt;Sets the phone number for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                              |
| `SetGender`              | &lt;ul&gt;&lt;li&gt;Set Gender&lt;/li&gt;&lt;li&gt;Sets the gender for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                          |
| `removeFromSubscriptionGroup` | &lt;ul&gt;&lt;li&gt;Remove From Subscription Group&lt;/li&gt;&lt;li&gt;Removes the current user from an email or SMS subscription group.&lt;/li&gt;&lt;li&gt;This setting is available in versions 3.5 and higher.&lt;/li&gt;&lt;/ul&gt; |
| `setCustomLocationAttribute` | &lt;ul&gt;&lt;li&gt;Set Custom Location Attribute&lt;/li&gt;&lt;li&gt;Sets a custom location attribute (key, latitude, longitude) for the current user.&lt;/li&gt;&lt;/ul&gt;                          |
| `SetLineId`              | &lt;ul&gt;&lt;li&gt;Set LINE ID&lt;/li&gt;&lt;li&gt;Sets the LINE messaging app ID for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                          |
| `Ecommerce`              | &lt;ul&gt;&lt;li&gt;Log Ecommerce Event&lt;/li&gt;&lt;li&gt;Logs a structured ecommerce event for the current user.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt; |
| `WipeData`               | &lt;ul&gt;&lt;li&gt;Wipe Data (delete local SDK data)&lt;/li&gt;&lt;li&gt;Deletes all locally stored SDK data and disables the SDK.&lt;/li&gt;&lt;li&gt;The SDK must be explicitly re-enabled before further data collection resumes.&lt;/li&gt;&lt;/ul&gt; |
| `RefreshFeatureFlags`    | &lt;ul&gt;&lt;li&gt;Refresh Feature Flags&lt;/li&gt;&lt;li&gt;Requests a refresh of feature flags for the current user from Braze.&lt;/li&gt;&lt;/ul&gt;                                                |
| `LogFeatureFlagImpression` | &lt;ul&gt;&lt;li&gt;Log Feature Flag Impression&lt;/li&gt;&lt;li&gt;Logs an impression event for the specified feature flag.&lt;/li&gt;&lt;/ul&gt;                                                    |
| `RefreshContentCards`    | &lt;ul&gt;&lt;li&gt;Refresh Content Cards&lt;/li&gt;&lt;li&gt;Requests a refresh of the Content Cards feed from Braze.&lt;/li&gt;&lt;/ul&gt;                                                            |
| `ShowContentCards`       | &lt;ul&gt;&lt;li&gt;Show Content Cards&lt;/li&gt;&lt;li&gt;Displays the Content Cards feed.&lt;/li&gt;&lt;/ul&gt;                                                                                       |
| `LogContentCardImpressions` | &lt;ul&gt;&lt;li&gt;Log Content Card Impressions&lt;/li&gt;&lt;li&gt;Logs impression events for an array of Content Cards.&lt;/li&gt;&lt;/ul&gt;                                                     |
| `LogContentCardClick`    | &lt;ul&gt;&lt;li&gt;Log Content Card Click&lt;/li&gt;&lt;li&gt;Logs a click event for a specific Content Card.&lt;/li&gt;&lt;/ul&gt;                                                                    |
| `RequestPushPermission`  | &lt;ul&gt;&lt;li&gt;Request Push Permission&lt;/li&gt;&lt;li&gt;Prompts the user to grant push notification permission.&lt;/li&gt;&lt;/ul&gt;                                                           |
| `UnregisterPush`         | &lt;ul&gt;&lt;li&gt;Unregister Push&lt;/li&gt;&lt;li&gt;Unregisters the current device from push notifications.&lt;/li&gt;&lt;/ul&gt;                                                                   |
| `FlushData`              | &lt;ul&gt;&lt;li&gt;Flush Data&lt;/li&gt;&lt;li&gt;Immediately sends queued analytics data to Braze servers.&lt;/li&gt;&lt;/ul&gt;                                                                      |
| `RefreshBanners`         | &lt;ul&gt;&lt;li&gt;Refresh Banners&lt;/li&gt;&lt;li&gt;Requests a refresh of Braze Banners for the specified placement IDs.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt; |
| `LogBannerImpressions`   | &lt;ul&gt;&lt;li&gt;Log Banner Impressions&lt;/li&gt;&lt;li&gt;Logs impression events for an array of Banner placement IDs.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt; |
| `LogBannerClick`         | &lt;ul&gt;&lt;li&gt;Log Banner Click&lt;/li&gt;&lt;li&gt;Logs a click event for a specific Banner.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt;                  |
| `InsertBanner`           | &lt;ul&gt;&lt;li&gt;Insert Banner&lt;/li&gt;&lt;li&gt;Retrieves a Banner for the specified placement ID and inserts it into the specified parent element.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt; |
| `Custom`                 | &lt;ul&gt;&lt;li&gt;Custom&lt;/li&gt;&lt;li&gt;Sends a custom event made by the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                     |

### Parameter

Map to these destinations to pass data to the events mapped earlier. Parameters are only used with predefined Events. See the Custom Event Data section below to learn how to pass a parameter with a custom event.

Use the following steps to pass a parameter to a predefined event:

1. In the Event field, select an event from the drop-down list.
1. In the Parameter field, select a parameter from the drop-down list.
1. For a custom parameter, enter a name to identify the custom event.
1. Click **&#43; Add**.

| **Destination Name**  | **Description**                                                                                                                                                                                                                                    |
|:----------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `product_id`          | &lt;ul&gt;&lt;li&gt;Product ID&lt;/li&gt;&lt;li&gt;The unique ID for the in-app product purchased.&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                   |
| `product_quantity`    | &lt;ul&gt;&lt;li&gt;Product Quantity&lt;/li&gt;&lt;li&gt;The quantity of the in-app product purchased.&lt;/li&gt;&lt;li&gt;This overrides the e-commerce value `_cquan`.&lt;/li&gt;&lt;/ul&gt;                                                                                                     |
| `order_id`            | &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;The unique ID for the in-app purchase.&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                             |
| `order_subtotal`      | &lt;ul&gt;&lt;li&gt;Order Subtotal&lt;/li&gt;&lt;li&gt;The subtotal for the in-app purchase.&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                     |
| `order_currency`      | &lt;ul&gt;&lt;li&gt;Order Currency&lt;/li&gt;&lt;li&gt;The ISO 4217 currency code for the in-app purchase.&lt;/li&gt;&lt;li&gt;Overrides `_ccurrency`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                        |
| `purchase_properties` | &lt;ul&gt;&lt;li&gt;Purchase Properties&lt;/li&gt;&lt;li&gt;An object of additional properties for the in-app purchase.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                          |
| `alias`               | &lt;ul&gt;&lt;li&gt;User Alias&lt;/li&gt;&lt;li&gt;An identifier for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                           |
| `label`               | &lt;ul&gt;&lt;li&gt;Alias Label&lt;/li&gt;&lt;li&gt;A label for the alias, such as the source of the alias.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                      |
| `key`                 | &lt;ul&gt;&lt;li&gt;Custom Attribute Key&lt;/li&gt;&lt;li&gt;The identifier for the custom attribute.&lt;/li&gt;&lt;li&gt;Enter the name of the parameter to send.&lt;/li&gt;&lt;/ul&gt;                                                                                                           |
| `value`               | &lt;ul&gt;&lt;li&gt;Custom Attribute Value&lt;/li&gt;&lt;li&gt;The value for the custom attribute.&lt;/li&gt;&lt;li&gt;Enter the name of the parameter to send.&lt;/li&gt;&lt;/ul&gt;                                                                                                              |
| `inc_value`           | &lt;ul&gt;&lt;li&gt;Custom Attribute Incrementation Value&lt;/li&gt;&lt;li&gt;The value by which to increment a custom user attribute.&lt;/li&gt;&lt;li&gt;Enter the name of the parameter to send.&lt;/li&gt;&lt;li&gt;Use negative numbers to decrement.&lt;/li&gt;&lt;li&gt;Default value is `1`.&lt;/li&gt;&lt;/ul&gt; |
| `custom_attributes`   | &lt;ul&gt;&lt;li&gt;Custom Attribute Object&lt;/li&gt;&lt;li&gt;An object of custom attribute key-value pairs to set on the current user in a single call.&lt;/li&gt;&lt;/ul&gt;                                                                                                       |
| `line_id`             | &lt;ul&gt;&lt;li&gt;User&#39;s LINE ID&lt;/li&gt;&lt;li&gt;The LINE messaging app ID for the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                          |
| `feature_flag_id`     | &lt;ul&gt;&lt;li&gt;Feature Flag ID&lt;/li&gt;&lt;li&gt;The unique identifier of the feature flag to log an impression for.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                     |
| `banner_placement_ids` | &lt;ul&gt;&lt;li&gt;Banner Placement IDs (Array or comma-separated)&lt;/li&gt;&lt;li&gt;An array or comma-separated string of Banner placement IDs to refresh or log impressions for.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt;            |
| `banner_placement_id` | &lt;ul&gt;&lt;li&gt;Banner Placement ID&lt;/li&gt;&lt;li&gt;The unique identifier for a single Banner placement to retrieve and insert.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt;                                                           |
| `banner_click_id`     | &lt;ul&gt;&lt;li&gt;Banner Click ID&lt;/li&gt;&lt;li&gt;The click tracking ID of the Banner that was clicked.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt;                                                                                     |
| `banner_parent_selector` | &lt;ul&gt;&lt;li&gt;Banner Parent Selector (CSS)&lt;/li&gt;&lt;li&gt;A CSS selector string identifying the parent element into which the Banner is inserted.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt;                                   |
| `content_cards`       | &lt;ul&gt;&lt;li&gt;Content Cards Array&lt;/li&gt;&lt;li&gt;An array of Content Card objects to log impressions for.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                            |
| `content_card`        | &lt;ul&gt;&lt;li&gt;Content Card Object&lt;/li&gt;&lt;li&gt;A single Content Card object to log a click for.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                    |
| `ecommerce_event_name` | &lt;ul&gt;&lt;li&gt;Ecommerce Event Name&lt;/li&gt;&lt;li&gt;The name of the ecommerce event to log.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt;                                                                                             |
| `ecommerce_properties` | &lt;ul&gt;&lt;li&gt;Ecommerce Properties&lt;/li&gt;&lt;li&gt;An object of properties for the ecommerce event.&lt;/li&gt;&lt;li&gt;Supports a &lt;code&gt;source&lt;/code&gt; field that defaults to &lt;code&gt;&#34;tealium&#34;&lt;/code&gt;.&lt;/li&gt;&lt;li&gt;This setting is available in versions 6.0 and higher.&lt;/li&gt;&lt;/ul&gt; |
| `avatar_url`          | &lt;ul&gt;&lt;li&gt;Avatar Image URL&lt;/li&gt;&lt;li&gt;URL for the current user&#39;s selected avatar.&lt;/li&gt;&lt;li&gt;Not available in versions 4.0 and higher.&lt;/li&gt;&lt;/ul&gt;                                                                                                           |
| `longitude`           | &lt;ul&gt;&lt;li&gt;User&#39;s Longitude&lt;/li&gt;&lt;li&gt;The validated longitude of the user&#39;s location, in degrees.&lt;/li&gt;&lt;li&gt;Values are from `-180` to `180`&lt;/li&gt;&lt;/ul&gt;                                                                                                     |
| `latitude`            | &lt;ul&gt;&lt;li&gt;User&#39;s Latitude&lt;/li&gt;&lt;li&gt;The validated latitude of the user&#39;s location, in degrees.&lt;/li&gt;&lt;li&gt;Values are from `-90` to `90`&lt;/li&gt;&lt;/ul&gt;                                                                                                         |
| `accuracy`            | &lt;ul&gt;&lt;li&gt;Location Accuracy&lt;/li&gt;&lt;li&gt;The accuracy of the user&#39;s longitude and latitude, in meters.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                          |
| `altitude`            | &lt;ul&gt;&lt;li&gt;User&#39;s Altitude&lt;/li&gt;&lt;li&gt;The altitude of the user&#39;s location, in meters.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                          |
| `altitude_accuracy`   | &lt;ul&gt;&lt;li&gt;Altitude Accuracy&lt;/li&gt;&lt;li&gt;The accuracy of the user&#39;s altitude, in meters.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                        |
| `year`                | &lt;ul&gt;&lt;li&gt;User&#39;s Birth Year&lt;/li&gt;&lt;li&gt;The year associated with the current user&#39;s birthday.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                  |
| `month`               | &lt;ul&gt;&lt;li&gt;User&#39;s Birth Month&lt;/li&gt;&lt;li&gt;The month associated with the current user&#39;s birthday.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                |
| `day`                 | &lt;ul&gt;&lt;li&gt;User&#39;s Birth Day&lt;/li&gt;&lt;li&gt;The day associated with the current user&#39;s birthday.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                    |
| `email`               | &lt;ul&gt;&lt;li&gt;User&#39;s Email&lt;/li&gt;&lt;li&gt;The validated email address of the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                            |
| `notification_type`   | &lt;ul&gt;&lt;li&gt;Notification Subscription Type&lt;/li&gt;&lt;li&gt;Selected notification type for the current user.&lt;/li&gt;&lt;li&gt;Options: `opted_in`, `subscribed`, `unsubscribed`&lt;/li&gt;&lt;/ul&gt;                                                                                |
| `first_name`          | &lt;ul&gt;&lt;li&gt;User&#39;s First Name&lt;/li&gt;&lt;li&gt;The first name of the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                    |
| `subscriptionGroupId` | &lt;ul&gt;&lt;li&gt;Subscription group ID.&lt;/li&gt;&lt;li&gt;The unique identifier of the subscription group.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                  |
| `last_name`           | &lt;ul&gt;&lt;li&gt;User&#39;s Last Name&lt;/li&gt;&lt;li&gt;The last name of the current user.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                      |
| `gender`              | &lt;ul&gt;&lt;li&gt;User&#39;s Gender&lt;/li&gt;&lt;li&gt;Gender code for the current user.&lt;/li&gt;&lt;li&gt;Options are male (`m`), female (`f`), or other `o`.&lt;/li&gt;&lt;/ul&gt;                                                                                                              |
| `customer_city`       | &lt;ul&gt;&lt;li&gt;User&#39;s Home City&lt;/li&gt;&lt;li&gt;The home city of the current user.&lt;/li&gt;&lt;li&gt;Overrides `_ccity`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                          |
| `customer_country`    | &lt;ul&gt;&lt;li&gt;User&#39;s Country&lt;/li&gt;&lt;li&gt;The country of the current user.&lt;/li&gt;&lt;li&gt;Overrides `_ccountry`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                           |
| `localization`        | &lt;ul&gt;&lt;li&gt;User&#39;s Language&lt;/li&gt;&lt;li&gt;The ISO 639-1 Language Code for the current user&#39;s display language.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                     |
| `phone_number`        | &lt;ul&gt;&lt;li&gt;User&#39;s Phone Number&lt;/li&gt;&lt;li&gt;The phone number for the current user.&lt;/li&gt;&lt;li&gt;Allows only numbers, spaces, and the `&#43;`, `.`, `-`, ` ( `, and `)` characters&lt;/li&gt;&lt;/ul&gt;                                                                         |

### Custom Event Data

Map to custom event data destinations if you want to pass a custom parameter with a custom event that you previously mapped in the Events tab.

Use the following steps to map a custom event data variable:

1. For **Event Name**, enter the name of the custom event, exactly as specified in the **Events** tab.
1. For **Parameter**, enter the name of the parameter you want to send.
1. Click **&#43; Add**.

### Cookie Consent

Map to the Cookie Consent destination to control whether the Braze SDK is enabled or disabled based on a user&#39;s consent state. Consent gating runs before SDK initialization.

| **Value** | **Description**                                                                                          |
|:----------|:---------------------------------------------------------------------------------------------------------|
| `grant`   | Enables the SDK and allows data collection to proceed. The SDK initializes and opens a session normally. |
| `revoke`  | Disables the SDK before initialization. No data is collected and no session is opened.                   |

## Vendor Documentation

* [Braze Web SDK](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/initial_sdk_setup/)
