---
title: Remote Command: Adjust
description: Tealium remote command integration for Adjust on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/adjust/
---
## Requirements

* Adjust [App Token](https://help.adjust.com/en/article/app-settings#view-your-app-token)
* One of these mobile libraries:
  * [Tealium for Android-Kotlin](/platforms/android-kotlin/) (1.0.0&#43;)
  * [Tealium for Android-Java](/platforms/android-java/) (5.9.0&#43;)
  * [Tealium for iOS-Swift](/platforms/ios-swift/)
* One of these remote command integrations:
  * [Adjust Remote Command JSON File](/platforms/remote-commands/integrations/adjust/#json-template) (Requires Android-Kotlin 1.0.0&#43; or iOS-Swift 2.1.0&#43;)
  * [Adjust Remote Command tag in Tealium iQ Tag Management]()

## How It Works

The Adjust integration uses three items:

1. The Adjust native SDK
2. The remote commands module that wraps the Adjust methods
3. Either the JSON configuration file or Remote Command tag that translates event tracking into native Adjust calls

Adding the Adjust remote command module to your app automatically installs and builds the required Adjust libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Adjust SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](/platforms/remote-commands/how-it-works/#vendor-integrations).

iOS: For Adjust version 4.23.0&#43;, the SDK automatically adds the following native frameworks: `AdSupport.framework`, `iAd.framework` and `AppTrackingTransparaceny.framework`. Learn more in the [Adjust iOS SKAdNetwork integration](https://help.adjust.com/en/article/app-tracking-transparency-att-framework) guide.

## Install

### Dependency Manager




1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-adjust-remote-command`
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumAdjust` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumAdjust` module to install, and select the app target you want the module to be installed in.
5. If you are using any additional modules from the Tealium Swift library, follow [the Swift Package Manager instructions](/platforms/ios-swift/install/#swift-package-manager-recommended) to add them.

If your project has more than one app target and needs `TealiumAdjust` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumAdjust` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and  select the `TealiumAdjust` module to add it to your app target.




1. Remove `pod &#34;tealium-swift&#34;` and `pod &#34;Adjust&#34;` if they exist in your Podfile. The dependency for `tealium-swift` is already included in the `TealiumAdjust` framework.

2. Add the following dependency to your Podfile:  
      ```ruby
      pod &#34;TealiumAdjust&#34;
      ```  
      The `TealiumAdjust` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      &#34;tealium-swift/Core&#34;
      &#34;tealium-swift/RemoteCommands&#34;
      ```

3. Include a dispatcher pod in your installation, either `tealium-swift/Collect` or `tealium-swift/TagManagement`, and include any other individual sub modules in your podfile. For example:   
      ```ruby
      pod &#34;TealiumAdjust&#34;
      pod &#34;tealium-swift/Collect&#34;
      pod &#34;tealium-swift/Lifecycle&#34;
      pod &#34;tealium-swift/Attribution&#34;
      ```

4. Import the modules `TealiumSwift` and `TealiumAdjust` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Adjsut remote command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumAdjust` framework.

2. Remove the following line if it exists in your Cartfile:  
      ```bash
      github &#34;adjust/ios_sdk&#34;
      ```

3.  Add the following dependency to your Cartfile:  
      ```bash
      github &#34;tealium/tealium-ios-adjust-remote-command&#34;
      ```






1. Install [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) and add the Tealium Maven URL to your project’s top-level `build.gradle` file, if you haven&#39;t done so already.

      ```groovy
      allprojects {
        repositories {
          mavenCentral()
          maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
          }
        }
      }
      ```

2. Import both the Adjust SDK and Tealium-Adjust remote commands by adding the following dependencies in your app project&#39;s `build.gradle` file:  
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:adjust:1.0.0&#39;
      }
      ```



1. Navigate to the root of your React Native project.

2. Download and install the `tealium-react-adjust` package with the following command:  
    ```bash
    yarn add tealium-react-adjust
    ```
3. React Native Autolinking is enabled in version 1.0.7 of the NPM package and is no longer needed to run `react-native link` if using version 0.60&#43; of React Native.




### Manual Installation




The manual installation for Adjust remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the Adjust remote commands for your iOS project:

1. Install the [Adjust SDK](https://github.com/adjust/ios_sdk), if you haven&#39;t already done so.

2. Clone the [Tealium iOS Adjust remote command](https://github.com/tealium/tealium-ios-adjust-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`





The manual installation for Adjust remote commands requires [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) to be installed. To install the Adjust remote commands for your Android project:

1. Add `flatDir` to your project root `build.gradle` file:  
      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              flatDir {
                  dirs &#39;libs&#39;
              }
            }
      }
      ```

2. Add `tealium-adjust.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:  
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-adjust&#39;, ext:&#39;aar&#39;)
      }
      ```



## Initialize

For all Tealium libraries, register the Adjust Remote Command when you initialize.




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s iOS (Swift) library:
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webview Tag
    let adjust = AdjustRemoteCommand()

    // Local JSON
    //let adjust = AdjustRemoteCommand(type: .local(file: &#34;adjust&#34;)) 

    // Remote JSON
    //let adjust = AdjustRemoteCommand(type: .remote(url: &#34;https://some.domain.com/adjust.json&#34;))

    remoteCommands.add(adjust)
}
```



Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s Android (Kotlin) library:
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val adjust = AdjustRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(adjust); 

    // Local JSON
    //remoteCommands?.add(adjust, filename = &#34;adjust.json&#34;);

    // Remote JSON
    //remoteCommands?.add(adjust, remoteUrl = &#34;https://some.domain.com/adjust.json&#34;); 
}
```



Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s Android (Java) library:
```java
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// New code to add the Adjust Remote Command
AdjustRemoteCommand adjustRemoteCommand = new AdjustRemoteCommand(application)
teal.addRemoteCommand(adjustRemoteCommand);
```




Initialize remote commands with a JSON configuration file or the Remote Command tag for React Native:
```javascript
import AdjustRemoteCommand from &#39;tealium-react-adjust&#39;;
AdjustRemoteCommand.initialize();

// Webview Tag
let adjust = { id: AdjustRemoteCommand.name } 

// Local JSON
//let adjust = { id: AdjustRemoteCommand.name, path: &#34;adjust.json&#34; }

// Remote JSON
//let adjust = { id: AdjustRemoteCommand.name, url: &#34;https://some.domain.com/adjust.json&#34; }

let config = TealiumConfig {
    // ...
    remoteCommands: [adjust]
}
```




## JSON Template

If you are configuring remote commands using a [JSON configuration file](/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
  &#34;config&#34;: {
    &#34;api_token&#34;: &#34;YOUR_API_TOKEN&#34;,
    &#34;sandbox&#34;: true,
    &#34;settings&#34;: {
      &#34;log_level&#34;: &#34;verbose&#34;,
      &#34;allow_iad&#34;: true,
      &#34;allow_ad_services&#34;: true,
      &#34;allow_idfa&#34;: true,
      &#34;event_buffering_enabled&#34;: false,
      &#34;send_in_background&#34;: true
    }
  },
  &#34;mappings&#34;: {
    &#34;event_token&#34;: &#34;event_token&#34;,
    &#34;order_total&#34;: &#34;revenue,callback.orderTotal&#34;,
    &#34;order_currency&#34;: &#34;currency&#34;,
    &#34;order_id&#34;: &#34;order_id,callback.orderId&#34;,
    &#34;conversion_value&#34;: &#34;conversion_value&#34;,
    &#34;sales_region&#34;: &#34;sales_region&#34;,
    &#34;callback_id&#34;: &#34;callback_id&#34;,
    &#34;ad_revenue_source&#34;: &#34;ad_revenue_source&#34;,
    &#34;campaign&#34;: &#34;ad_revenue_payload.campaignId&#34;,
    &#34;ad_uuid&#34;: &#34;ad_revenue_payload.adId&#34;,
    &#34;appstore_receipt_data&#34;: &#34;receipt&#34;,
    &#34;purchase_timestamp&#34;: &#34;purchase_time&#34;,
    &#34;product_sku&#34;: &#34;sku&#34;,
    &#34;purchase_signature&#34;: &#34;signature&#34;,
    &#34;purchase_token&#34;: &#34;purchase_token&#34;,
    &#34;deeplink_url&#34;: &#34;deeplink_open_url&#34;,
    &#34;push_token&#34;: &#34;push_token&#34;,
    &#34;favorite_color&#34;: &#34;callback.color,session_callback.color&#34;,
    &#34;num_of_pets&#34;: &#34;partner.pets,session_partner.pets&#34;,
    &#34;customer_id&#34;: &#34;callback.customerId&#34;,
    &#34;customer_is_member&#34;: &#34;partner.isMember&#34;,
    &#34;global_params&#34;: &#34;global_callback,global_partner&#34;,
    &#34;remove_global_params&#34;: &#34;remove_global_callback_params,remove_global_partner_params&#34;,
    &#34;reset_global_params&#34;: &#34;reset_global_callback_params,reset_global_partner_params&#34;,
    &#34;consent_granted&#34;: &#34;measurement_consent&#34;,
    &#34;enabled&#34;: &#34;enabled&#34;
  },
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;initialize&#34;,
    &#34;track_deeplink&#34;: &#34;appwillopenurl&#34;,
    &#34;purchase&#34;: &#34;trackevent,updateconversionvalue&#34;,
    &#34;event&#34;: &#34;trackevent&#34;,
    &#34;contact&#34;: &#34;trackevent,addglobalcallbackparams,addglobalpartnerparams&#34;,
    &#34;ad_revenue&#34;: &#34;trackadrevenue&#34;,
    &#34;subscribe&#34;: &#34;trackevent,tracksubscription&#34;,
    &#34;received_push_token&#34;: &#34;setpushtoken&#34;,
    &#34;add_global_parameters&#34;: &#34;addglobalcallbackparams,addglobalpartnerparams&#34;,
    &#34;remove_global_parameters&#34;: &#34;removeglobalcallbackparams,removeglobalpartnerparams&#34;,
    &#34;reset_global_parameters&#34;: &#34;resetglobalcallbackparams,resetglobalpartnerparams&#34;,
    &#34;consent_revoked&#34;: &#34;gdprforgetme,trackmeasurementconsent&#34;,
    &#34;consent_granted&#34;: &#34;trackmeasurementconsent&#34;,
    &#34;set_enabled&#34;: &#34;setenabled&#34;,
    &#34;offline&#34;: &#34;setofflinemode&#34;
  }
}

```

## Supported Methods

We map a command to each Adjust method. To trigger an Adjust method, pass the corresponding command in the specified format.

| Remote Command | Adjust Method |
| :-- | :-- |
| `initialize` | `initialize()` |
| `sendEvent` | `trackEvent()` |
| `trackSubscription` | `trackSubscription()` |
| `requestTrackingAuthorization`* | `requestTrackingAuthorization()` |
| `updateConversionValue`* | `updateConversionValue()`|
| `appWillOpen` | `appWillOpen()` |
| `trackAdRevenue` | `trackAdRevenue()` |
| `setPushToken` | `setPushToken()` |
| `setEnabled` | `enable()`/`disable()` |
| `setOfflineMode` | `switchToOfflineMode()`/`switchBackToOnlineMode()` |
| `gdprForgetMe` | `gdprForgetMe()` |
| `trackThirdPartySharing` | `trackThirdPartySharing()` |
| `trackMeasurementConsent` | `trackMeasurementConsent()` |
| `addSessionCallbackParams` (deprecated) | `addSessionCallbackParams()` |
| `removeSessionCallbackParams` (deprecated) | `removeSessionCallbackParams()` |
| `resetSessionCallbackParams` (deprecated) | `resetSessionCallbackParams()` |
| `addSessionPartnerParams` (deprecated) | `addSessionPartnerParams()` |
| `removeSessionPartnerParams` (deprecated) | `removeSessionPartnerParams()` |
| `resetSessionPartnerParams` (deprecated) | `resetSessionPartnerParams()` |
| `addGlobalCallbackParams` | `addGlobalCallbackParams()` |
| `removeGlobalCallbackParams` | `removeGlobalCallbackParams()` |
| `resetGlobalCallbackParams` | `resetGlobalCallbackParams()` |
| `addGlobalPartnerParams` | `addGlobalPartnerParams()` |
| `removeGlobalPartnerParams` | `removeGlobalPartnerParams()` |
| `resetGlobalPartnerParams` | `resetGlobalPartnerParams()` |

 Only supported in iOS as part of the `AppTrackingTransparency.framework`.  Learn more in the [Adjust iOS SKAdNetwork integration](https://help.adjust.com/en/article/app-tracking-transparency-att-framework) guide.


### SDK Setup

#### Initialize

The Adjust SDK is initialized automatically upon launch. The Adjust API key is set in the tag configuration.  

| Remote Command | Adjust Method |
|---|---|
| `initialize`  | `initialize()` |

Adjust Developer Guide: Initial SDK Setup

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration)
- [Android](https://dev.adjust.com/en/sdk/android/configuration)

There are several configuration options available in the Adjust Remote Command tag. If any of the below are set on launch, they are sent during the `initialize()` method.

##### Configuration Options

| Name | iQ variable mapping | Type |
|---|---|---|
| `environment`  | `sandbox` | `Bool` |
| `logLevel`| `logLevel`  | `String` |
| `delayStart` (deprecated) | `delay_start` | `Double` |
| `allowiAdInfoReading`* | `allow_iad` | `Bool` |
| `allowAdServicesInfoReading`* | `allow_ad_services` | `Bool` |
| `allowIdfaReading`* | `allow_idfa` | `Bool` |
| `appSecret` (deprecated) | `app_secret` | `String` |
| `appSecretInfo1` (deprecated) | `app_secret_info_1` | `String` |
| `appSecretInfo2` (deprecated) | `app_secret_info_2` | `String` |
| `appSecretInfo3` (deprecated) | `app_secret_info_3` | `String` |
| `appSecretInfo4` (deprecated) | `app_secret_info_4` | `String` |
| `defaultTracker`| `default_tracker` | `String` |
| `externalDeviceId`| `external_device_id` | `String` |
| `eventBufferingEnabled`| `event_buffering_enabled` | `String` |
| `sendInBackground`| `send_in_background` | `String` |
| `setPreinstallTrackingEnabled`** | `preinstall_tracking` | `String` |
| `eventDeduplicationIdsMaxSize`| `deduplication_id_max_size` | `Int` |
| `urlStrategy`| `url_strategy` | `String` |
| `domains`| `url_strategy_domains` | `[String]` |
| `useSubdomains`| `url_strategy_use_subdomains` | `Bool` |
| `isResidency`| `url_strategy_is_residency` | `Bool` |

Note that `url_strategy` must be one of the v4 url strategies or, in alternative, you can provide all of the three parameters domains/useSubdomains/isResidency to create another strategy that is added in the future.

 iOS and Android only

#### Track Event

| Remote Command | Adjust Method |
|---|---|
| `sendevent`  | `trackEvent()` |

|  Parameter | Type |
|---|---|
|  `event_token` (required) | `String` |
|  `order_id` | `String` |
|  `deduplication_id` | `String` |
|  `revenue` | `Double` |
|  `currency` | `String` |
|  `callback` | `Dictionary` or `Map` |
|  `partner` | `Dictionary` or `Map` |
|  `callback_id` | `String` |


Adjust Developer Guide: Track Events

- [iOS](https://dev.adjust.com/en/sdk/ios/features/events)
- [Android](https://dev.adjust.com/en/sdk/android/features/events)

#### Track Subscription

| Remote Command | Adjust Method |
| :--- | :---|
| `tracksubscription`  | `trackAppStoreSubscription()` |

|  Parameter | Type |
|---|---|
|  `revenue` (required) | `Double` |
|  `currency` (required) | `String ` |
|  `order_id` (required) | `String` |
|  `deduplication_id` | `String` |
|  `receipt` (deprecated) | `Data` |
|  `sku` (required for Android only) | `String` |
|  `signature` (required for Android only) | `String` |
|  `purchase_token` (required for Android only) | `String` |
|  `purchase_time` | `Date` |
|  `sales_region` | `String` |
|  `callback` | `Dictionary` or `Map` |
|  `partner` | `Dictionary` or `Map` |

Adjust API Reference: Subscription Tracking

- [iOS](https://dev.adjust.com/en/sdk/ios/features/subscriptions)
- [Android](https://dev.adjust.com/en/sdk/android/features/subscriptions)

#### Request Tracking Authorization (iOS)

The Adjust SDK automatically requests tracking authorization from the user. To set a completion use the `Adjust.trackingAuthorizationCompletion()` method and then add the remote command.

Example:

```swift
tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

	let adjustRemoteCommand = AdjustRemoteCommand()
	adjustRemoteCommand.trackingAuthorizationCompletion = { status in
            switch status {
            case 0: print(&#34;ATTrackingManagerAuthorizationStatusNotDetermined&#34;)
            case 1: print(&#34;ATTrackingManagerAuthorizationStatusRestricted&#34;)
            case 2: print(&#34;ATTrackingManagerAuthorizationStatusDenied&#34;)
            case 3: print(&#34;ATTrackingManagerAuthorizationStatusAuthorized&#34;)
            default:
                break;
            }
        }
	remoteCommands.add(adjustRemoteCommand)
}
```

Adjust API Reference: App-tracking Authorization Wrapper

- [iOS](https://dev.adjust.com/en/sdk/ios/features/att)

#### Update Conversion Value (iOS Only)

| Remote Command | Adjust Method |
|---|---|
| `updateconversionvalue`  | `updateConversionValue()` |

|  Parameter | Type |
|---|---|
|  `conversion_value` (required) | `Int` |
|  `coarse_value` | `low`, `medium`, `high` |
|  `lock_window` | `Bool` |

Adjust API Reference: Update SKAdNetwork Conversion Value

- [iOS](https://dev.adjust.com/en/sdk/ios/features/skad)


#### App Will Open

|  Remote Command | Adjust Method |
|---|---|
| `appwillopen`  | `appWillOpen()` |

|  Parameter | Type |
|----|---|
| `deeplink_open_url` (required) | `String` |


Adjust API Reference: Reattribution Via Deep Links

- [iOS](https://dev.adjust.com/en/sdk/ios/features/deep-links/)
- [Android](https://dev.adjust.com/en/sdk/android/features/deep-links/)

#### Track Ad Revenue

|  Remote Command | Adjust Method |
|---|---|
| `trackadrevenue`  | `trackAdRevenue()` |

|  Parameter | Type |
|----|---|
| `ad_revenue_source` (required) | `String` |
| `ad_revenue_payload` | `Dictionary` or `Map` |

The payload is formed by the following parameters:

|  Parameter | Type |
|----|---|
|  `unit` | `String` |
|  `network` | `String` |
|  `amount` | `Double` |
|  `currency` | `String` |
|  `placement` | `String` |
|  `impression_count` | `Int32` |
|  `callback` | `Dictionary` or `Map` |
|  `partner` | `Dictionary` or `Map` |

Adjust API Reference: Ad Revenue Tracking

- [iOS](https://dev.adjust.com/en/sdk/ios/features/ad-revenue)
- [Android](https://dev.adjust.com/en/sdk/android/features/ad-revenue)

#### Set Push Token

|  Remote Command | Adjust Method |
|---|---|
| `setpushtoken`  | `setPushToken()` |

|  Parameter | Type |
|----|---|
| `push_token` (required) | `String` |

Adjust Additional APIs: Set Push Token

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration/#set-push-tokens)
- [Android](https://dev.adjust.com/en/sdk/android/configuration/#set-push-tokens)

#### Set Offline Mode

|  Remote Command | Adjust Method |
|---|---|
| `setofflinemode`  | `switchToOfflineMode()`/`switchBackToOnlineMode()` |


|  Parameter | Type |
|----|---|
| `offline` (required) | Bool |

Adjust Additional APIs: Set Offline Mode

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration/#activate-offline-mode)
- [Android](https://dev.adjust.com/en/sdk/android/configuration/#activate-offline-mode)

### Callback Parameters

Adjust Additional APIs: Callback Parameters

- [iOS](https://dev.adjust.com/en/sdk/ios/features/session-parameters)
- [Android](https://dev.adjust.com/en/sdk/android/features/session-parameter)

#### Add Global Callback Parameters

|  Remote Command | Adjust Method |
|---|---|
| `addsessioncallbackparams` (deprecated) | `addGlobalCallbackParams()` |
| `addglobalcallbackparams` | `addGlobalCallbackParams()` |

|  Parameter | Type |
|----|---|
| `session_callback` (deprecated) | `Dictionary` or `Map` |
| `global_callback` (required) | `Dictionary` or `Map` |


#### Add Global Partner Parameters

|  Remote Command | Adjust Method |
|---|---|
| `addsessionpartnerparams` (deprecated) | `addGlobalPartnerParams()` |
| `addglobalpartnerparams` | `addGlobalPartnerParams()` |

|  Parameter | Type |
|----|---|
| `session_partner` (deprecated) | `Dictionary` or `Map` |
| `global_partner` (required) | `Dictionary` or `Map` |


#### Remove Global Callback Parameters

|  Remote Command | Adjust Method |
|---|---|
| `removesessioncallbackparams` (deprecated) | `removeGlobalCallbackParams()` |
| `removeglobalcallbackparams` | `removeGlobalCallbackParams()` |

|  Parameter | Type |
|----|---|
| `remove_session_callback_params` (deprecated) | `[String]` |
| `remove_global_callback_params` (required) | `[String]` |


#### Remove Global Partner Parameters

|  Remote Command | Adjust Method |
|---|---|
| `removesessionpartnerparams` (deprecated) | `removeGlobalPartnerParams()` |
| `removeglobalpartnerparams` | `removeGlobalPartnerParams()` |

|  Parameter | Type |
|----|---|
| `remove_session_partner_params` (deprecated) | `[String]` |
| `remove_global_partner_params` (required) | `[String]` |


#### Reset Session Callback Parameters

|  Remote Command | Adjust Method |
|---|---|
| `resetsessioncallbackparams` (deprecated) | `resetGlobalCallbackParams()` |
| `resetglobalcallbackparams` | `resetGlobalCallbackParams()` |


#### Reset Session Partner Parameters

|  Remote Command | Adjust Method |
|---|---|
| `resetsessionpartnerparams` (deprecated) | `resetGlobalPartnerParams()` |
| `resetglobalpartnerparams` | `resetGlobalPartnerParams()` |

### Consent Options

#### Forget Me

|  Remote Command | Adjust Method |
|---|---|
| `gdprforgetme`  | `gdprForgetMe()` |

Adjust Additional APIs: GDPR Right to be Forgotten

- [iOS](https://dev.adjust.com/en/sdk/ios/features/privacy/#send-erasure-request)
- [Android](https://dev.adjust.com/en/sdk/android/features/privacy/#send-erasure-request)

#### Set Enabled

| Remote Command | Adjust Property |
|---|---|
| `setenabled`  | `enable()`/`disable()` |

|  Parameter | Type |
|---|---|
|  `enabled` (required) | `Bool` |

Adjust API Reference: Disable Tracking

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration#disable-the-sdk)
- [Android](https://dev.adjust.com/en/sdk/android/configuration#disable-the-sdk)

#### Track Measurement Consent

|  Remote Command | Adjust Method |
|---|---|
| `trackmeasurementconsent`  | `trackMeasurementConsent()` |


|  Parameter | Type |
|----|---|
| `measurement_consent` (required) | Bool |

Adjust Additional APIs: Consent Measurement

- [iOS](https://dev.adjust.com/en/sdk/ios/features/privacy#consent-measurement-for-specific-users)
- [Android](https://dev.adjust.com/en/sdk/android/features/privacy#consent-measurement-for-specific-users)

#### Track Third Party Sharing

|  Remote Command | Adjust Method |
|---|---|
| `trackthirdpartysharing`  | `trackThirdPartySharing()` |

|  Parameter | Type |
|----|---|
| `enabled` (required) | Bool |

Adjust Additional APIs: Enable Third Party Sharing

- [iOS](https://dev.adjust.com/en/sdk/ios/features/privacy#third-party-sharing-for-specific-users)
- [Android](https://dev.adjust.com/en/sdk/android/features/privacy#third-party-sharing-for-specific-users)
