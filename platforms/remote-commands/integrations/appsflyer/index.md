---
title: Remote Command: AppsFlyer
description: Tealium remote command integration for AppsFlyer on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/appsflyer/
---
## Requirements

* AppsFlyer [app ID](https://support.appsflyer.com/hc/en-us/articles/207377436#available-in-the-app-store-google-play-store-windows-phone-store) and [dev key](https://support.appsflyer.com/hc/en-us/articles/211719806-App-Settings#sdk-dev-key)
* One of these mobile libraries:
  * [Tealium for Android-Kotlin](/platforms/android-kotlin/) (1.0.0 or later)
  * [Tealium for Android-Java](/platforms/android-java/) (5.9.0 or later for AppsFlyer 1.0.0 or later, or 5.9.0 or earlier for previous versions)
  * [Tealium for iOS-Swift](/platforms/ios-swift/)
  * [Tealium for React Native](/platforms/react-native/)
* One of these remote command integrations:
  * [AppsFlyer Remote Command JSON File](/platforms/remote-commands/integrations/appsflyer/#json-template) (Requires Android-Kotlin 1.0.0 or later, or iOS-Swift 2.1.0 or later)
  * AppsFlyer Remote Command tag in Tealium iQ Tag Management

## How It Works

The AppsFlyer integration uses three items:

1. The AppsFlyer native SDK
1. The remote commands module that wraps the AppsFlyer methods
1. Either the JSON configuration file or the Remote Command tag that translates event tracking into native AppsFlyer calls

Adding the AppsFlyer remote command module to your app automatically installs and builds the required AppsFlyer libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the AppsFlyer SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**.
1. Enter the repository URL: `https://github.com/tealium/tealium-ios-appsflyer-remote-command`.
1. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumAppsFlyer` version does not appear in the list, then reset your Swift package cache.
1. Select the `TealiumAppsFlyer` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumAppsFlyer` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumAppsFlyer` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
1. In your Xcode project, select the app target under the **TARGETS** section.
1. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and select the `TealiumAppsFlyer` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod &#34;AppsFlyerFramework&#34;` if they exist in your Podfile. The dependency for `tealium-swift` is already included in the `TealiumAppsFlyer` framework.
2. Add the following dependency to your Podfile:  
      ```ruby
      pod &#34;TealiumAppsFlyer&#34;
      ```  
      The `TealiumAppsFlyer` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      ```

3. Import the modules `TealiumSwift` and `TealiumAppsFlyer` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the AppsFlyer remote command.




To install AppsFlyer remote commands for iOS using Carthage:

1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumAppsFlyer` framework.
2. Remove the following line if it exists in your Cartfile:  
      ```bash
      `binary &#34;https://raw.githubusercontent.com/AppsFlyerSDK/AppsFlyerFramework/master/AppsFlyerLib.json&#34;`
      ```

3.  Add the following dependency to your Cartfile:  
      ```bash
      github &#34;tealium/tealium-ios-appsflyer-remote-command&#34;
      ```

Tealium for Swift SDK (version 1.x) and `TealiumAppsFlyer` version 1.x requires the `TealiumDelegate` module to be included with your installation.







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

2. Import both the AppsFlyer SDK and Tealium-AppsFlyer remote commands by adding the following dependencies in your app project&#39;s `build.gradle` file:  
      ```groovy
      dependencies {
      implementation &#39;com.tealium.remotecommands:appsflyer:1.0.0&#39;
      }
      ```



Follow the installation instructions for the main [Tealium React Native library](/platforms/react-native) installation. Ensure you have installed version 2.2.0 or newer.

Navigate to the root of your React Native project.

Download and install the `tealium-react-appsflyer` package with the following command:

Install the AppsFlyer Remote Command package
```yarn add tealium-react-appsflyer```




### Manual Installation




The manual installation for AppsFlyer remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the AppsFlyer remote commands for your iOS project:

1. Install the [AppsFlyer SDK](https://github.com/AppsFlyerSDK/AppsFlyerFramework), if you haven&#39;t already done so.
1. Clone the [Tealium iOS AppsFlyer remote command](https://github.com/tealium/tealium-ios-appsflyer-remote-command) repo and drag the files within the `Sources` folder into your project.
1. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`.




The manual installation for AppsFlyer remote commands requires [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) to be installed. To install the AppsFlyer remote commands for your Android project:

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

2. Add `tealium-appsflyer.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:  
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-appsflyer&#39;, ext:&#39;aar&#39;)
      }
      ```




## Initialize

For all Tealium libraries, register the AppsFlyer Remote Command when you initialize.




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s iOS (Swift) library:
```swift
// Sets up a config object and creates a Tealium instance
    let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;)
    
    // Webview Tag
    let appsFlyerRemoteCommand = AppsFlyerRemoteCommand()

    // Local JSON
    //let appsFlyerRemoteCommand = AppsFlyerRemoteCommand(type: .local(file: &#34;appsflyer&#34;))

    // Remote JSON
    //let appsFlyerRemoteCommand = AppsFlyerRemoteCommand(type: .remote(url: &#34;https://some.domain.com/path/to/appsflyer.json&#34;))

    config.remoteAPIEnabled = true
    config.collectors = [Collectors.Lifecycle]
    config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
    
    config.addRemoteCommand(appsFlyerRemoteCommand)
    
    var tealium = Tealium(config: config)
```


Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s Android (Kotlin) library:  
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val appsFlyer = AppsFlyerRemoteCommand(applicationm, appsFlyerDevKey = devKey);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(appsFlyer); 

    // Local JSON
    //remoteCommands?.add(appsFlyer, filename = &#34;appsFlyer.json&#34;);

    // Remote JSON
    //remoteCommands?.add(appsFlyer, remoteUrl = &#34;https://some.domain.com/appsFlyer.json&#34;);
}
```



Initialize remote commands with the Remote Command tag for Tealium&#39;s Android (Java) library:  
```java
// Sets up a config object and creates a Tealium instance
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// New code to add the AppsFlyer Remote Command
AppsFlyerRemoteCommand appsFlyer = new AppsFlyerRemoteCommand(application, appsFlyerDevKey = devKey)
teal.addRemoteCommand(appsFlyer);
```


```js
import AppsflyerRemoteCommand from &#39;tealium-react-appsflyer&#39;;

AppsflyerRemoteCommand.initialize();

let config = TealiumConfig {
    // ...
    remoteCommands: [{
        id: AppsflyerRemoteCommand.name,
        // Optional - path to local JSON mappings
        // path: &#34;appsflyer.json&#34;
        // Optional - path to remote JSON mappings
        // url: &#34;https://some.domain.com/appsflyer.json&#34;
    }]
}
Tealium.initialize(config, success =&gt; {});
```



## Push Message Tracking (iOS)

In TealiumAppsFlyer SDK for iOS version 3.0.0, we removed support for the `TealiumRegistration` framework that was previously used to generalize and uniform push messaging for different remote commands. Push notifications are handled directly with the underlying `AppsFlyerLib` framework. For more informatiom, see the [AppsFlyer push notificatiom documentation](https://dev.appsflyer.com/hc/docs/push-notifications).

## JSON Template

If you are configuring remote commands using a [JSON configuration file](/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
    &#34;config&#34;: {
        &#34;app_id&#34;: &#34;YOUR_APP_ID&#34;,
        &#34;app_dev_key&#34;: &#34;YOUR_APPSFLYER_DEV_KEY&#34;,
        &#34;settings&#34;: {
            &#34;custom_data&#34;: {&#34;custom_key&#34;: &#34;custom_value&#34;},
            &#34;debug&#34;: true,
            &#34;disable_ad_tracking&#34;: false,
            &#34;disable_apple_ad_tracking&#34;: false,
            &#34;time_between_sessions&#34;: 30,
            &#34;anonymize_user&#34;: false,
            &#34;collect_device_name&#34;: false
        }
    },
    &#34;mappings&#34;: {
        &#34;latitude&#34;: &#34;af_lat&#34;,
        &#34;longitude&#34;: &#34;af_long&#34;,
        &#34;customer_email&#34;: &#34;customer_emails&#34;,
        &#34;hash_type&#34;: &#34;email_hash_type&#34;,
        &#34;currency_code&#34;: &#34;af_currency&#34;,
        &#34;customer_id&#34;: &#34;af_customer_user_id&#34;,
        &#34;signup_method&#34;: &#34;event.signup_method&#34;,
        &#34;achievement_id&#34;: &#34;event.achievement_id&#34;,
        &#34;checkout_option&#34;: &#34;event.checkout_option&#34;,
        &#34;checkout_step&#34;: &#34;event.checkout_step&#34;,
        &#34;content&#34;: &#34;event.content&#34;,
        &#34;content_type&#34;: &#34;event.content_type&#34;,
        &#34;coupon&#34;: &#34;event.coupon&#34;,
        &#34;product_brand&#34;: &#34;event.product_brand&#34;,
        &#34;product_category&#34;: &#34;event.product_category&#34;,
        &#34;product_id&#34;: &#34;event.af_content_id&#34;,
        &#34;product_list&#34;: &#34;event.product_list&#34;,
        &#34;product_location_id&#34;: &#34;event.product_location_id&#34;,
        &#34;product_name&#34;: &#34;event.product_name&#34;,
        &#34;product_variant&#34;: &#34;event.product_variant&#34;,
        &#34;product_unit_price&#34;: &#34;event.af_price&#34;,
        &#34;product_quantity&#34;: &#34;event.af_quantity&#34;,
        &#34;current_level&#34;: &#34;event.level&#34;,
        &#34;score&#34;: &#34;event.score&#34;,
        &#34;search_keyword&#34;: &#34;event.search_keyword&#34;,
        &#34;order_shipping_amount&#34;: &#34;event.order_shipping&#34;,
        &#34;order_tax_amount&#34;: &#34;event.order_tax&#34;,
        &#34;order_id&#34;: &#34;event.af_order_id&#34;,
        &#34;order_total&#34;: &#34;event.af_revenue&#34;,
        &#34;currency_type&#34;: &#34;event.currency_type&#34;,
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;initialize,launch&#34;,
        &#34;geofence_entered&#34;: &#34;tracklocation&#34;,
        &#34;geofence_exited&#34;: &#34;tracklocation&#34;,
        &#34;user_login&#34;: &#34;login&#34;,
        &#34;user_register&#34;: &#34;setuseremails,setcustomerid,completeregistration&#34;,
        &#34;show_offers&#34;: &#34;adclick&#34;,
        &#34;cart_add&#34;: &#34;addtocart&#34;,
        &#34;wishlist_add&#34;: &#34;addtowishlist&#34;,
        &#34;payment&#34;: &#34;addpaymentinfo&#34;,
        &#34;unlock_achievement&#34;: &#34;unlockachievement&#34;,
        &#34;level_up&#34;: &#34;achievelevel,customersegment&#34;,
        &#34;email_signup&#34;: &#34;subscribe&#34;,
        &#34;product&#34;: &#34;viewedcontent&#34;,
        &#34;category&#34;: &#34;listview&#34;,
        &#34;share&#34;: &#34;share&#34;,
        &#34;search&#34;: &#34;search&#34;,
        &#34;checkout&#34;: &#34;initiatecheckout&#34;,
        &#34;order&#34;:&#34;purchase&#34;
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
|`achievedLevel`| `&#34;af_level_achieved&#34;`|
|`addPaymentInfo`| `&#34;af_add_payment_info&#34;`|
|`addToCart`| `&#34;af_add_to_cart&#34;`|
|`addToWishlist`| `&#34;af_add_to_wishlist&#34;`|
|`completeRegistration`| `&#34;af_complete_registration&#34;`|
|`completeTutorial`| `&#34;af_tutorial_completion&#34;`|
|`initiateCheckout`| `&#34;af_initiated_checkout&#34;`|
|`purchase`| `&#34;af_purchase&#34;`|
|`subscribe`| `&#34;af_subscribe&#34;`|
|`startTrial`| `&#34;af_start_trial&#34;`|
|`rate`| `&#34;af_rate&#34;`|
|`search`| `&#34;af_search&#34;`|
|`spentCredits`| `&#34;af_spent_credits&#34;`|
|`unlockAchievement`| `&#34;af_achievement_unlocked&#34;`|
|`contentView`| `&#34;af_content_view&#34;`|
|`listView`| `&#34;af_list_view&#34;`|
|`adClick`| `&#34;af_ad_click&#34;`|
|`adView`| `&#34;af_ad_view&#34;`|
|`travelBooking`| `&#34;af_travel_booking&#34;`|
|`share`| `&#34;af_share`&#34;|
|`invite`| `&#34;af_invite&#34;`|
|`reEngage`| `&#34;af_re_engage&#34;`|
|`update`| `&#34;af_update&#34;`|
|`login`| `&#34;af_login&#34;`|
|`customerSegment`| `&#34;af_customer_segment&#34;`|
|`pushNotificationOpened`| `&#34;af_opened_from_push_notification&#34;`|

Because the AppsFlyer SDK is installed alongside the Tealium SDK, you are able to trigger any native AppsFlyer functionality given the corresponding tag configuration.

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

Use this method when you need to use the `AppsFlyerLib` but you don&#39;t know if it has been initialized yet.
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

If you have the location module installed, the latitude and longitude are sent with every event.

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
