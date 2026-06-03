---
title: AppsFlyer App Events Connector Setup Guide
description: This article describes how to set up the AppsFlyer App Events connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/appsflyer-app-events-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Track Install | ✓ | ✓ |
| Track in App Event | ✓ | ✓ |
| Track In App Event (SDK Clients) | ✓ | ✓ |


## Configure Settings

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **App ID**
  * This is the AppsFlyer App ID of the app for which you are passing data.
* **Dev Key**
  * The account dev key taken from the **App Settings** screen in the **AppsFlyer** dashboard.
* **S2S Key**  
The token used to send data using server-to-server calls. For more information, see [AppsFlyer: Managing AppsFlyer tokens](https://support.appsflyer.com/hc/en-us/articles/360004562377-Managing-AppsFlyer-tokens).

S2S Key is used to enable access. For more information, see [AppsFlyer: Managing API and Server-to-server S2S tokens](https://support.appsflyer.com/hc/en-us/articles/360004562377-Managing-API-and-Server-to-server-S2S-tokens).

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Track Install

#### Parameters

The Platform Data parameters are required. The Apple Search Ads and Custom Data parameters are optional.

##### Platform Data

| **Parameter** | **Platform** | **Description** |
|---| ---| ---|
| Ad ID Enabled Flag   | All                 | (Required) Set this parameter to `false` to opt the user out of AppsFlyerAnalytics. Set the flag to `true` to opt in to AppsFlyerAnalytics.                                                                                                                                                                                                                                                                                               |
| App Open Counter      | All                 | (Required) Set this parameter to `1` or `2` for first launch attribution, or set it to `3` or higher for retargeting.                                                                                                                                                                                                                                                             |
| Device Advertising ID | Android or Windows  | (Required) The device&#39;s advertising ID. For example, `caf5555d48f22222d34f03bcd7ab333b`.                                                                                                                                                                                                                                                                                          |
| Device IP Address   | All                 | (Required) The device&#39;s IP address.                                                                                                                                                                                                                                                                                                                                               |
| Device Locale       | All                 | (Required) The device&#39;s locale. For example, `en-US`.                                                                                                                                                                                                                                                                                                                             |
| Device Type/Model    | All                 | (Required) The device&#39;s type or model.                                                                                                                                                                                                                                                                                                                                            |
| Install Date       | All                 | (Required) The first launch date or install date of the application on the device, in ISO 8601 UTC format. For example, `2015-01-22T08:45:33.412`.                                                                                                                                                                                                                                |
| iOS Ad ID          | iOS                 | (Required) The OS ID for Advertisers (`advertisingIdentifier`), which can be SHA1 hashed. For example, `AC9FB4FB-AAAA-BBBB-88E6-2840D9BB17F4`.                                                                                                                                                                                                                                    |
| OS Version         | All                 | (Required) The operating system version.                                                                                                                                                                                                                                                                                                                                          |
| Unique User ID     | All                 | (Required) The unique user ID. For example, `1b1758cd-c22b-461e-924e-ceb0c7f849aa`.                                                                                                                                                                                                                                                                                               |
| User Agent           | All                 | (Required) The application&#39;s user agent.                                                                                                                                                                                                                                                                                                                                          |
| App Bundle ID                    | iOS                 | The app bundle ID. For example, `com.company.appname`.                                                                                                                                                                                                                                                                                                                 |
| Customer User ID                 | IOS and Android     | The customer user ID, as set by the developer. The advertiser&#39;s system will use this as the user identifier. For example, `3d4d05e5-9ae4-4755-9363-8166568f7935`.                                                                                                                                                                                                      |
| Device IMEI                      | Android             | The device&#39;s IMEI (International Mobile Equipment Identity), which can be SHA1 hashed.                                                                                                                                                                                                                                                                                                                           |
| Device Android ID                | Android             | The device&#39;s Android ID, which can be SHA1 hashed.                                                                                                                                                                                                                                                                                                                     |
| Facebook Tracking Cookie Value   | Android and Windows | The Facebook Tracking Cookie&#39;s value.                                                                                                                                                                                                                                                                                                                                  |
| Full DeepLink URL                | All                 | The full DeepLink URL of the tracking call. For example, `myapp://page/1?param1=val1`.                                                                                                                                                                                                                                                                                  |
| Google Play Referrer             | Android             | The referrer received from Google Play receiver, without URL-encoding. For example, `af_tranid=1A4F123KJHG73F0P&amp;c=c1&amp;pid=MediaSource1`.                                                                                                                                                                                                                                |
| Microsoft Store Referrer           | Windows             | The Windows referrer received from Microsoft Store, without URL-encoding. For example, `af_tranid=1A4F123KJHG73F0P`.                                                                                                                                                                                                                                                     |
| iOS Identifier for Vendor        | iOS                 | The iOS identifier for the vendor. For example, `95C9BD22-4A4C-41C8-9548-ED07C5C8C145`.                                                                                                                                                                                                                                                                                |
| App Tracking Transparency        | iOS 14 and above    | Set this parameter to indicate if the user opted out of the use of IDFA:  &lt;ul&gt;&lt;li&gt;`0`: Not determined.&lt;/li&gt;&lt;li&gt;`1`: Restricted.&lt;/li&gt;&lt;li&gt;`2`: Denied.&lt;/li&gt;&lt;li&gt;`3`: Authorized.&lt;/li&gt;&lt;/ul&gt;  For more information, see [Apple: ATTrackingManager.AuthorizationStatus](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus/). |
| App Type                         | iOS                 | If this is an app clip install.                                                                                                                                                                                                                                                                                                                                        |
| Open Anonymous Device Identifier | Android             | The Open Anonymous Device Identifier. For example, `57cfbf44-edfc-9f25-7fcf-7 3fdffc59929`.                                                                                                                                                                                                                                                                            |
| Amazon Advertising ID            | Android             | The unique advertising ID for Amazon devices. For example, `24c5f114-7718-4a12-97d9-1273397be3c6`.                                                                                                                                                                                                                                                                      |
| App Store                        | Android             | The store from which the app was downloaded.                                                                                                                                                                                                                                                                                                                           |

##### App ID Override

Use this field to override the **App ID** set in the connector configuration screen.

##### Dev Key Override

Use this field to override the **Dev Key** set in the connector configuration screen.

##### Apple Search Ads

| **Parameter**       | **Description**          |
|:--------------------|:-------------------------|
| iad-adgroup-id      | Ad ID group ID.          |
| iad-adgroup-name    | Ad ID group name.        |
| iad-attribution     | Ad ID attribution.       |
| iad-campaign-id     | Ad ID campaign ID.       |
| iad-campaign-name   | Ad ID campaign name.     |
| iad-click-date      | Ad ID click date.        |
| iad-conversion-date | Ad ID conversion date.   |
| iad-keyword         | Ad ID keyword.           |
| iad-lineitem-id     | Ad ID line item.         |
| iad-lineitem-name   | Ad ID line item name.    |
| iad-org-name        | Ad ID organization name. |

##### Custom Data

Use this section to add any customized information to the event message.

### Action - Track in App Event

#### Parameters

The **Platform Data** and **Event Data** parameters are required. The **Custom Data** parameters are optional.

##### Platform Data

This action uses the same **Platform Data** parameters as The Track Install action.

##### Event Data

| **Parameter**         | **Description**                                                                                                                                                                      |
|:----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Event Currency        | &lt;ul&gt;&lt;li&gt;The default currency for the event&lt;/li&gt;&lt;li&gt;Only use for `USD`, for all other currencies, map under the **Event Properties** (`event_value`) section using the `af_currency` key.&lt;/li&gt;&lt;/ul&gt; |
| Event Name | (Required) A string describing the event name. For example, `af_purchase`.                                                                                                                      |

##### Custom Data

Use this section to add any customized information to the event message.

### Track In App Event (SDK Clients)

Use this action when you have the AppsFlyer SDK installed and want to send mobile events that occur outside the app.

#### Platform Data

| **Parameter** | **Platform**   |**Description** |
| --- | --- |--- |
| Appsflyer ID | All | (Required) A unique identifier, generated by AppsFlyer, when the app launches for the first time. |
| Advertising ID | Android | The device&#39;s advertising ID. |
| Open Anonymous Device Identifier | Android | The Open Anonymous Device Identifier.  |
| Amazon Advertising ID | Android | Amazon Advertising ID. |
| Device IMEI | Android | The device&#39;s IMEI, which can be SHA1 hashed. |
| iOS Ad ID | IOS | The OS ID for Advertisers (`advertisingIdentifier`), which can be SHA1 hashed. |
| iOS Identifier for Vendor | IOS | The iOS identifier for the vendor. |
| Advertising ID Enabled Flag | IOS | Use this boolean flag to indicate if the user opted out of sharing their advertiser ID. |
| App Tracking Transparency | IOS 14 and later | Set this parameter to indicate if the user opted out of the use of IDFA:  &lt;ul&gt;&lt;li&gt;`0`: Not determined.&lt;/li&gt;&lt;li&gt;`1`: Restricted.&lt;/li&gt;&lt;li&gt;`2`: Denied.&lt;/li&gt;&lt;li&gt;`3`: Authorized.&lt;/li&gt;&lt;/ul&gt;  For more information, see [Apple: ATTrackingManager.AuthorizationStatus](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus/). |
| App Store | All             |If this is an app clip install. |
| App Type | All             |If the user event takes place in an `app_clip`, send the parameter. In all other cases don&#39;t send the parameter. |
| App Version Name | All             |Your named app version. |
| Bundle Identifier | All             |A unique app identifier. In raw data, the parameter populates **Bundle ID**. |
| Customer User ID | All             |Customer user ID, as set by the developer. This is used as the user identifier in the advertiser&#39;s system. |
| Event Time | All             |The time when the event occurred using UTC timezone. If not set, Appsflyer will use the incoming event time. |
| IP Address | All             |The mobile device&#39;s IP address during the event occurrence. If sent, the IP address is used to populate geolocation fields. If not sent, AppsFlyer populates the geolocation fields using the values from the install attribution event. |
| Operating System |  All             |The device operating system version. |
| Sharing Filter |  All             |The sharing filter blocks the sharing of S2S events through postbacks/API with integrated partners and other third-party integrations. Set to `all` to block all partners. Pass an array of partner IDs to block specific partners. |

#### Event Data

| **Parameter** | **Description** |
| --- | --- |
| Event Name | (Required) A string describing the event name. For example, `af_purchase`. |
| Event Currency |  Default currency for the event. For example, `USD`. |
| Custom Data | Use this section to add additional customized information to the event message. |