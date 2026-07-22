---
title: Remote Command: AppsFlyer
description: Tealium remote command integration for AppsFlyer on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/appsflyer/
---
## Requirements

* AppsFlyer [app ID](https://support.appsflyer.com/hc/en-us/articles/207377436#available-in-the-app-store-google-play-store-windows-phone-store) and [dev key](https://support.appsflyer.com/hc/en-us/articles/211719806-App-Settings#sdk-dev-key)
* One of these mobile libraries:
  * [Tealium for Android-Kotlin](https://docs.tealium.com/platforms/android-kotlin/) (1.0.0 or later)
  * [Tealium for Android-Java](https://docs.tealium.com/platforms/android-java/) (5.9.0 or later for AppsFlyer 1.0.0 or later, or 5.9.0 or earlier for previous versions)
  * [Tealium for iOS-Swift](https://docs.tealium.com/platforms/ios-swift/)
  * [Tealium for React Native](https://docs.tealium.com/platforms/react-native/)
* One of these remote command integrations:
  * [AppsFlyer Remote Command JSON File](https://docs.tealium.com/platforms/remote-commands/integrations/appsflyer/#json-template) (Requires Android-Kotlin 1.0.0 or later, or iOS-Swift 2.1.0 or later)
  * AppsFlyer Remote Command tag in Tealium iQ Tag Management

## How It Works

The AppsFlyer integration uses three items:

1. The AppsFlyer native SDK
1. The remote commands module that wraps the AppsFlyer methods
1. Either the JSON configuration file or the Remote Command tag that translates event tracking into native AppsFlyer calls

Adding the AppsFlyer remote command module to your app automatically installs and builds the required AppsFlyer libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the AppsFlyer SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File > Add Packages... > Add Package Dependency**.
1. Enter the repository URL: `https://github.com/tealium/tealium-ios-appsflyer-remote-command`.
1. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumAppsFlyer` version does not appear in the list, then reset your Swift package cache.
1. Select the `TealiumAppsFlyer` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumAppsFlyer` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumAppsFlyer` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
1. In your Xcode project, select the app target under the **TARGETS** section.
1. Navigate to **General > Frameworks, Libraries & Embedded Content** and select the `TealiumAppsFlyer` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod "AppsFlyerFramework"` if they exist in your Podfile. The dependency for `tealium-swift` is already included in the `TealiumAppsFlyer` framework.
2. Add the following dependency to your Podfile:  
      ```ruby
      pod "TealiumAppsFlyer"
      ```  
      The `TealiumAppsFlyer` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      ```

3. Import the modules `TealiumSwift` and `TealiumAppsFlyer` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the AppsFlyer remote command.




To install AppsFlyer remote commands for iOS using Carthage:

1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumAppsFlyer` framework.
2. Remove the following line if it exists in your Cartfile:  
      ```bash
      `binary "https://raw.githubusercontent.com/AppsFlyerSDK/AppsFlyerFramework/master/AppsFlyerLib.json"`
      ```

3.  Add the following dependency to your Cartfile:  
      ```bash
      github "tealium/tealium-ios-appsflyer-remote-command"
      ```


<blockquote>
Tealium for Swift SDK (version 1.x) and `TealiumAppsFlyer` version 1.x requires the `TealiumDelegate` module to be included with your installation.
</blockquote>








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

2. Import both the AppsFlyer SDK and Tealium-AppsFlyer remote commands by adding the following dependencies in your app project's `build.gradle` file:  
      ```groovy
      dependencies {
      implementation 'com.tealium.remotecommands:appsflyer:1.0.0'
      }
      ```



Follow the installation instructions for the main [Tealium React Native library](https://docs.tealium.com/platforms/react-native) installation. Ensure you have installed version 2.2.0 or newer.

Navigate to the root of your React Native project.

Download and install the `tealium-react-appsflyer` package with the following command:

Install the AppsFlyer Remote Command package
```yarn add tealium-react-appsflyer```




### Manual Installation




The manual installation for AppsFlyer remote commands requires the [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/) library to be installed. To install the AppsFlyer remote commands for your iOS project:

1. Install the [AppsFlyer SDK](https://github.com/AppsFlyerSDK/AppsFlyerFramework), if you haven't already done so.
1. Clone the [Tealium iOS AppsFlyer remote command](https://github.com/tealium/tealium-ios-appsflyer-remote-command) repo and drag the files within the `Sources` folder into your project.
1. Set the [`remoteAPIEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`.




The manual installation for AppsFlyer remote commands requires [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) to be installed. To install the AppsFlyer remote commands for your Android project:

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

2. Add `tealium-appsflyer.aar` to `<PROJECT_ROOT>/<MODULE>/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:  
      ```groovy
      dependencies {
            implementation(name:'tealium-appsflyer', ext:'aar')
      }
      ```




## Initialize

For all Tealium libraries, register the AppsFlyer Remote Command when you initialize.




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's iOS (Swift) library:
```swift
// Sets up a config object and creates a Tealium instance
    let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT")
    
    // Webview Tag
    let appsFlyerRemoteCommand = AppsFlyerRemoteCommand()

    // Local JSON
    //let appsFlyerRemoteCommand = AppsFlyerRemoteCommand(type: .local(file: "appsflyer"))

    // Remote JSON
    //let appsFlyerRemoteCommand = AppsFlyerRemoteCommand(type: .remote(url: "https://some.domain.com/path/to/appsflyer.json"))

    config.remoteAPIEnabled = true
    config.collectors = [Collectors.Lifecycle]
    config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
    
    config.addRemoteCommand(appsFlyerRemoteCommand)
    
    var tealium = Tealium(config: config)
```


Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's Android (Kotlin) library:  
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val appsFlyer = AppsFlyerRemoteCommand(applicationm, appsFlyerDevKey = devKey);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(appsFlyer); 

    // Local JSON
    //remoteCommands?.add(appsFlyer, filename = "appsFlyer.json");

    // Remote JSON
    //remoteCommands?.add(appsFlyer, remoteUrl = "https://some.domain.com/appsFlyer.json");
}
```



Initialize remote commands with the Remote Command tag for Tealium's Android (Java) library:  
```java
// Sets up a config object and creates a Tealium instance
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// New code to add the AppsFlyer Remote Command
AppsFlyerRemoteCommand appsFlyer = new AppsFlyerRemoteCommand(application, appsFlyerDevKey = devKey)
teal.addRemoteCommand(appsFlyer);
```


```js
import AppsflyerRemoteCommand from 'tealium-react-appsflyer';

AppsflyerRemoteCommand.initialize();

let config = TealiumConfig {
    // ...
    remoteCommands: [{
        id: AppsflyerRemoteCommand.name,
        // Optional - path to local JSON mappings
        // path: "appsflyer.json"
        // Optional - path to remote JSON mappings
        // url: "https://some.domain.com/appsflyer.json"
    }]
}
Tealium.initialize(config, success => {});
```



## Push Message Tracking (iOS)

In TealiumAppsFlyer SDK for iOS version 3.0.0, we removed support for the `TealiumRegistration` framework that was previously used to generalize and uniform push messaging for different remote commands. Push notifications are handled directly with the underlying `AppsFlyerLib` framework. For more informatiom, see the [AppsFlyer push notificatiom documentation](https://dev.appsflyer.com/hc/docs/push-notifications).

## JSON Template

If you are configuring remote commands using a [JSON configuration file](https://docs.tealium.com/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
    "config": {
        "app_id": "YOUR_APP_ID",
        "app_dev_key": "YOUR_APPSFLYER_DEV_KEY",
        "settings": {
            "custom_data": {"custom_key": "custom_value"},
            "debug": true,
            "disable_ad_tracking": false,
            "disable_apple_ad_tracking": false,
            "time_between_sessions": 30,
            "anonymize_user": false,
            "collect_device_name": false
        }
    },
    "mappings": {
        "latitude": "af_lat",
        "longitude": "af_long",
        "customer_email": "customer_emails",
        "hash_type": "email_hash_type",
        "currency_code": "af_currency",
        "customer_id": "af_customer_user_id",
        "signup_method": "event.signup_method",
        "achievement_id": "event.achievement_id",
        "checkout_option": "event.checkout_option",
        "checkout_step": "event.checkout_step",
        "content": "event.content",
        "content_type": "event.content_type",
        "coupon": "event.coupon",
        "product_brand": "event.product_brand",
        "product_category": "event.product_category",
        "product_id": "event.af_content_id",
        "product_list": "event.product_list",
        "product_location_id": "event.product_location_id",
        "product_name": "event.product_name",
        "product_variant": "event.product_variant",
        "product_unit_price": "event.af_price",
        "product_quantity": "event.af_quantity",
        "current_level": "event.level",
        "score": "event.score",
        "search_keyword": "event.search_keyword",
        "order_shipping_amount": "event.order_shipping",
        "order_tax_amount": "event.order_tax",
        "order_id": "event.af_order_id",
        "order_total": "event.af_revenue",
        "currency_type": "event.currency_type",
    },
    "commands": {
        "launch": "initialize,launch",
        "geofence_entered": "tracklocation",
        "geofence_exited": "tracklocation",
        "user_login": "login",
        "user_register": "setuseremails,setcustomerid,completeregistration",
        "show_offers": "adclick",
        "cart_add": "addtocart",
        "wishlist_add": "addtowishlist",
        "payment": "addpaymentinfo",
        "unlock_achievement": "unlockachievement",
        "level_up": "achievelevel,customersegment",
        "email_signup": "subscribe",
        "product": "viewedcontent",
        "category": "listview",
        "share": "share",
        "search": "search",
        "checkout": "initiatecheckout",
        "order":"purchase"
    }
}
```

## Supported Methods

We map a command to each AppsFlyer method. To trigger an AppsFlyer method, pass the corresponding command in the specified format.

| Remote Command | AppsFlyer Method |
| :-- | :-- |
| `initialize` | `initialize()` |
| `trackLaunch` | `trackLaunch()` |
| Any of the below event names | `trackEvent()` |
| `setHost` | `setHost()` |
| `setUserEmails` | `setUserEmails()` |
| `setCurrencyCode` | `currencyCode (property on the AppsFlyerTracker.shared object)`|
| `setCustomerId` | `customerUserID (property on the AppsFlyerTracker.shared object)` |
| `disableDeviceTracking` | `setDeviceTrackingDisabled` |
| `disableTracking` | `isStopTracking (property on the AppsFlyerTracker.shared object)` |
| `resolveDeeplinkUrls` | `resolveDeepLinkURLs (property on the AppsFlyerTracker.shared object)` |

### Standard Event Names

The following is a list of standard event names supported with the `trackEvent` method. If any of the below command names are sent, they are automatically triggered in the AppsFlyer SDK. This is assuming all the required variables are also mapped and defined for that particular event. Learn more about [recording in-app events](https://support.appsflyer.com/hc/en-us/articles/207032066#core-apis-5-recording-inapp-events) and the see the full list of [recommended in-app events per vertical](https://support.appsflyer.com/hc/en-us/articles/115005544169#Verticals).

| Remote Command | AppsFlyer Event Name |
| :-- | :-- |
|`achievedLevel`| `"af_level_achieved"`|
|`addPaymentInfo`| `"af_add_payment_info"`|
|`addToCart`| `"af_add_to_cart"`|
|`addToWishlist`| `"af_add_to_wishlist"`|
|`completeRegistration`| `"af_complete_registration"`|
|`completeTutorial`| `"af_tutorial_completion"`|
|`initiateCheckout`| `"af_initiated_checkout"`|
|`purchase`| `"af_purchase"`|
|`subscribe`| `"af_subscribe"`|
|`startTrial`| `"af_start_trial"`|
|`rate`| `"af_rate"`|
|`search`| `"af_search"`|
|`spentCredits`| `"af_spent_credits"`|
|`unlockAchievement`| `"af_achievement_unlocked"`|
|`contentView`| `"af_content_view"`|
|`listView`| `"af_list_view"`|
|`adClick`| `"af_ad_click"`|
|`adView`| `"af_ad_view"`|
|`travelBooking`| `"af_travel_booking"`|
|`share`| `"af_share`"|
|`invite`| `"af_invite"`|
|`reEngage`| `"af_re_engage"`|
|`update`| `"af_update"`|
|`login`| `"af_login"`|
|`customerSegment`| `"af_customer_segment"`|
|`pushNotificationOpened`| `"af_opened_from_push_notification"`|


<blockquote>
Because the AppsFlyer SDK is installed alongside the Tealium SDK, you are able to trigger any native AppsFlyer functionality given the corresponding tag configuration.
</blockquote>


### SDK Setup

#### Initialize

The AppsFlyer SDK is initialized automatically upon launch. The AppsFlyer API key is set in the tag configuration.  

| Remote Command | AppsFlyer Method |
|---|---|
| `initialize`  | `initialize()` |

AppsFlyer Developer Guide: Initial SDK Setup

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#integration-33-initializing-the-sdk)

There are several configuration options available that can be configured in the AppsFlyer Remote Command tag. If any of the below are set on launch, they are sent during the initialize method.

##### Configuration Options

| Name | iQ variable mapping | Type |
|---|---|---|
| `debug`  | `debug` | `Bool` |
| `disableIAdTracking`| `disable_apple_ad_tracking`  | `Bool` |
| `minTimeBetweenSessions` | `time_between_sessions` | `Int` |
| `anonymizeUser`| `anonymize_user` | `Bool` |
| `shouldCollectDeviceName`| `collect_device_name` | `Bool` |
| `customData`| `custom_data` | `Dictionary` or `Map` |

AppsFlyer Developer Guide: Additional APIs

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#additional-apis)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#additional-apis)

##### OnReady (iOS)

Use this method when you need to use the `AppsFlyerLib` but you don't know if it has been initialized yet.
The completion will be called immediately, if `AppsFlyerLib` has already been initialized, or it will wait until it is initialized.

This can be useful when a client is using the remote command configuration to initialize the library and, therefore, the `AppsFlyerLib` is initialized asynchronously. 

Example:

```swift
appsFlyerRemoteCommand.onReady { appsFlyer in
    appsFlyer.registerUninstall(deviceToken)
}
```

### Location

#### Track Location

| Remote Command | AppsFlyer Method |
| :--- | :---|
| `tracklocation`  | `trackEvent()` - event name `af_location_coordinates` |

|  Parameter | Type |
|---|---|
|  `latitude` (required) | `Bool` |
|  `longitude` (required) | `Bool` |


<blockquote>
If you have the location module installed, the latitude and longitude are sent with every event.
</blockquote>


AppsFlyer API Reference: Location Tracking

- [iOS](https://github.com/AppsFlyerSDK/AppsFlyerFramework/blob/19ab52e9133ae86626c013e8cf0ed34aaf3721f0/iOS/AppsFlyerLib.framework/Versions/A/Headers/AppsFlyerTracker.h#L443)

### Other Options

#### Set Host

|  Remote Command | AppsFlyer Method |
|---|---|
| `sethost`  | `setHost` |

|  Parameter | Type |
|---|---|
|  `host` (required) | `String` |
|  `hostPrefix` (required) | `String` |

AppsFlyer API Reference: Set Host

- [iOS](https://github.com/AppsFlyerSDK/AppsFlyerFramework/blob/19ab52e9133ae86626c013e8cf0ed34aaf3721f0/iOS/AppsFlyerLib.framework/Versions/A/Headers/AppsFlyerTracker.h#L534)

#### Set User Emails

|  Remote Command | AppsFlyer Method |
|---|---|
| `setsermails`  | `setUserEmails` |

|  Parameter | Type |
|----|---|
| `emails` (required) | `[String]` |
| `cryptType` (required) | `Int` |

##### Crypt Type Reference

|  Value | Type |
|---|---|
| `0` | `None` |
| `1` | `SHA1` |
| `2` | `MD5` |
| `3` | `SHA256` |

AppsFlyer API Reference: Set User Email

- [iOS](https://github.com/AppsFlyerSDK/AppsFlyerFramework/blob/19ab52e9133ae86626c013e8cf0ed34aaf3721f0/iOS/AppsFlyerLib.framework/Versions/A/Headers/AppsFlyerTracker.h#L361)

#### Set Currency Code

|  Remote Command | AppsFlyer Property |
|---|---|
| `setcurrencycode`  | `currencyCode` |

|  Parameter | Type |
|----|---|
| `currency` (required) | `String` |

AppsFlyer API Reference: Set Currency Code

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#api-reference-currencycode)

#### Set Customer ID

|  Remote Command | AppsFlyer Property |
|---|---|
| `setcustomerid`  | `customerUserID` |

|  Parameter | Type |
|----|---|
| `customerId` (required) | `String` |

- AppsFlyer Additional APIs: Set Customer ID
- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#additional-apis-set-customer-user-id)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#api-reference-setcustomeruserid)

#### Resolve Deep Link Urls

| Remote Command | AppsFlyer Property |
|---|---|
| resolvedeeplinkurls  | `resolveDeepLinkURLs` |

|  Parameter | Type |
|---|---|
|  `deepLinkUrls` (required) | `[String]` |

AppsFlyer API Reference: Resolve Deep Link URLs

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#api-reference-resolvedeeplinkurls)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#api-reference-setresolvedeeplinkurls)


### Consent Options

#### Disable Tracking

|  Remote Command | AppsFlyer Property |
|---|---|
| disabletracking  | `isStopTracking` |

|  Parameter | Type |
|----|---|
| `stopTracking` (required) | Bool |

AppsFlyer Additional APIs: Stop Tracking (Opt-out)

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#additional-apis-optout)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#additional-apis-optout)
