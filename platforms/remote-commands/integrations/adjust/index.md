---
title: Remote Command: Adjust
description: Tealium remote command integration for Adjust on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/adjust/
---
## Requirements

* Adjust [App Token](https://help.adjust.com/en/article/app-settings#view-your-app-token)
* One of these mobile libraries:
  * [Tealium for Android-Kotlin](https://docs.tealium.com/platforms/android-kotlin/) (1.0.0+)
  * [Tealium for Android-Java](https://docs.tealium.com/platforms/android-java/) (5.9.0+)
  * [Tealium for iOS-Swift](https://docs.tealium.com/platforms/ios-swift/)
* One of these remote command integrations:
  * [Adjust Remote Command JSON File](https://docs.tealium.com/platforms/remote-commands/integrations/adjust/#json-template) (Requires Android-Kotlin 1.0.0+ or iOS-Swift 2.1.0+)
  * [Adjust Remote Command tag in Tealium iQ Tag Management](https://docs.tealium.com/adjust-mobile-remote-command-tag/)

## How It Works

The Adjust integration uses three items:

1. The Adjust native SDK
2. The remote commands module that wraps the Adjust methods
3. Either the JSON configuration file or Remote Command tag that translates event tracking into native Adjust calls

Adding the Adjust remote command module to your app automatically installs and builds the required Adjust libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Adjust SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-integrations).


<blockquote>
iOS: For Adjust version 4.23.0+, the SDK automatically adds the following native frameworks: `AdSupport.framework`, `iAd.framework` and `AppTrackingTransparaceny.framework`. Learn more in the [Adjust iOS SKAdNetwork integration](https://help.adjust.com/en/article/app-tracking-transparency-att-framework) guide.
</blockquote>


## Install

### Dependency Manager




1. In your Xcode project, select **File > Add Packages... > Add Package Dependency**
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-adjust-remote-command`
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumAdjust` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumAdjust` module to install, and select the app target you want the module to be installed in.
5. If you are using any additional modules from the Tealium Swift library, follow [the Swift Package Manager instructions](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) to add them.

If your project has more than one app target and needs `TealiumAdjust` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumAdjust` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General > Frameworks, Libraries & Embedded Content** and  select the `TealiumAdjust` module to add it to your app target.




1. Remove `pod "tealium-swift"` and `pod "Adjust"` if they exist in your Podfile. The dependency for `tealium-swift` is already included in the `TealiumAdjust` framework.

2. Add the following dependency to your Podfile:  
      ```ruby
      pod "TealiumAdjust"
      ```  
      The `TealiumAdjust` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      "tealium-swift/Core"
      "tealium-swift/RemoteCommands"
      ```

3. Include a dispatcher pod in your installation, either `tealium-swift/Collect` or `tealium-swift/TagManagement`, and include any other individual sub modules in your podfile. For example:   
      ```ruby
      pod "TealiumAdjust"
      pod "tealium-swift/Collect"
      pod "tealium-swift/Lifecycle"
      pod "tealium-swift/Attribution"
      ```

4. Import the modules `TealiumSwift` and `TealiumAdjust` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Adjsut remote command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumAdjust` framework.

2. Remove the following line if it exists in your Cartfile:  
      ```bash
      github "adjust/ios_sdk"
      ```

3.  Add the following dependency to your Cartfile:  
      ```bash
      github "tealium/tealium-ios-adjust-remote-command"
      ```






1. Install [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) and add the Tealium Maven URL to your project’s top-level `build.gradle` file, if you haven't done so already.

      ```groovy
      allprojects {
        repositories {
          mavenCentral()
          maven {
            url "https://maven.tealiumiq.com/android/releases/"
          }
        }
      }
      ```

2. Import both the Adjust SDK and Tealium-Adjust remote commands by adding the following dependencies in your app project's `build.gradle` file:  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:adjust:1.0.0'
      }
      ```



1. Navigate to the root of your React Native project.

2. Download and install the `tealium-react-adjust` package with the following command:  
    ```bash
    yarn add tealium-react-adjust
    ```
3. React Native Autolinking is enabled in version 1.0.7 of the NPM package and is no longer needed to run `react-native link` if using version 0.60+ of React Native.




### Manual Installation




The manual installation for Adjust remote commands requires the [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/) library to be installed. To install the Adjust remote commands for your iOS project:

1. Install the [Adjust SDK](https://github.com/adjust/ios_sdk), if you haven't already done so.

2. Clone the [Tealium iOS Adjust remote command](https://github.com/tealium/tealium-ios-adjust-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Set the [`remoteAPIEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`





The manual installation for Adjust remote commands requires [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) to be installed. To install the Adjust remote commands for your Android project:

1. Add `flatDir` to your project root `build.gradle` file:  
      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              flatDir {
                  dirs 'libs'
              }
            }
      }
      ```

2. Add `tealium-adjust.aar` to `<PROJECT_ROOT>/<MODULE>/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:  
      ```groovy
      dependencies {
            implementation(name:'tealium-adjust', ext:'aar')
      }
      ```



## Initialize

For all Tealium libraries, register the Adjust Remote Command when you initialize.




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's iOS (Swift) library:
```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webview Tag
    let adjust = AdjustRemoteCommand()

    // Local JSON
    //let adjust = AdjustRemoteCommand(type: .local(file: "adjust")) 

    // Remote JSON
    //let adjust = AdjustRemoteCommand(type: .remote(url: "https://some.domain.com/adjust.json"))

    remoteCommands.add(adjust)
}
```



Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's Android (Kotlin) library:
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val adjust = AdjustRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(adjust); 

    // Local JSON
    //remoteCommands?.add(adjust, filename = "adjust.json");

    // Remote JSON
    //remoteCommands?.add(adjust, remoteUrl = "https://some.domain.com/adjust.json"); 
}
```



Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's Android (Java) library:
```java
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// New code to add the Adjust Remote Command
AdjustRemoteCommand adjustRemoteCommand = new AdjustRemoteCommand(application)
teal.addRemoteCommand(adjustRemoteCommand);
```




Initialize remote commands with a JSON configuration file or the Remote Command tag for React Native:
```javascript
import AdjustRemoteCommand from 'tealium-react-adjust';
AdjustRemoteCommand.initialize();

// Webview Tag
let adjust = { id: AdjustRemoteCommand.name } 

// Local JSON
//let adjust = { id: AdjustRemoteCommand.name, path: "adjust.json" }

// Remote JSON
//let adjust = { id: AdjustRemoteCommand.name, url: "https://some.domain.com/adjust.json" }

let config = TealiumConfig {
    // ...
    remoteCommands: [adjust]
}
```




## JSON Template

If you are configuring remote commands using a [JSON configuration file](https://docs.tealium.com/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
  "config": {
    "api_token": "YOUR_API_TOKEN",
    "sandbox": true,
    "settings": {
      "log_level": "verbose",
      "allow_iad": true,
      "allow_ad_services": true,
      "allow_idfa": true,
      "event_buffering_enabled": false,
      "send_in_background": true
    }
  },
  "mappings": {
    "event_token": "event_token",
    "order_total": "revenue,callback.orderTotal",
    "order_currency": "currency",
    "order_id": "order_id,callback.orderId",
    "conversion_value": "conversion_value",
    "sales_region": "sales_region",
    "callback_id": "callback_id",
    "ad_revenue_source": "ad_revenue_source",
    "campaign": "ad_revenue_payload.campaignId",
    "ad_uuid": "ad_revenue_payload.adId",
    "appstore_receipt_data": "receipt",
    "purchase_timestamp": "purchase_time",
    "product_sku": "sku",
    "purchase_signature": "signature",
    "purchase_token": "purchase_token",
    "deeplink_url": "deeplink_open_url",
    "push_token": "push_token",
    "favorite_color": "callback.color,session_callback.color",
    "num_of_pets": "partner.pets,session_partner.pets",
    "customer_id": "callback.customerId",
    "customer_is_member": "partner.isMember",
    "global_params": "global_callback,global_partner",
    "remove_global_params": "remove_global_callback_params,remove_global_partner_params",
    "reset_global_params": "reset_global_callback_params,reset_global_partner_params",
    "consent_granted": "measurement_consent",
    "enabled": "enabled"
  },
  "commands": {
    "launch": "initialize",
    "track_deeplink": "appwillopenurl",
    "purchase": "trackevent,updateconversionvalue",
    "event": "trackevent",
    "contact": "trackevent,addglobalcallbackparams,addglobalpartnerparams",
    "ad_revenue": "trackadrevenue",
    "subscribe": "trackevent,tracksubscription",
    "received_push_token": "setpushtoken",
    "add_global_parameters": "addglobalcallbackparams,addglobalpartnerparams",
    "remove_global_parameters": "removeglobalcallbackparams,removeglobalpartnerparams",
    "reset_global_parameters": "resetglobalcallbackparams,resetglobalpartnerparams",
    "consent_revoked": "gdprforgetme,trackmeasurementconsent",
    "consent_granted": "trackmeasurementconsent",
    "set_enabled": "setenabled",
    "offline": "setofflinemode"
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


<blockquote>
Only supported in iOS as part of the `AppTrackingTransparency.framework`.  Learn more in the [Adjust iOS SKAdNetwork integration](https://help.adjust.com/en/article/app-tracking-transparency-att-framework) guide.
</blockquote>


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


<blockquote>
iOS and Android only
</blockquote>


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
            case 0: print("ATTrackingManagerAuthorizationStatusNotDetermined")
            case 1: print("ATTrackingManagerAuthorizationStatusRestricted")
            case 2: print("ATTrackingManagerAuthorizationStatusDenied")
            case 3: print("ATTrackingManagerAuthorizationStatusAuthorized")
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
