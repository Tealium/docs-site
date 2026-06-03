---
title: Remote Command: Kochava
description: Tealium remote command integration for Kochava on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/kochava/
---
## Requirements

* [Kochava App GUID](https://support.kochava.com/reference-information/locating-an-app-guid/)
* One of these mobile libraries:
  * [Tealium for Android-Kotlin](/platforms/android-kotlin/) (1.0.0&#43;)
  * [Tealium for Android-Java](/platforms/android-java/) (5.9.0&#43;)
  * [Tealium for iOS-Swift](/platforms/ios-swift/) (2.1.0&#43;)
* One of these remote command integrations:
  * [Kochava Remote Command JSON File](/platforms/remote-commands/integrations/kochava/#json-template) (Requires Android-Kotlin 1.0.0&#43; or iOS-Swift 2.1.0&#43;)
  * [Kochava Remote Command tag]() in Tealium iQ Tag Management

## How It Works

The Kochava integration uses three items:

1. The Kochava native SDK
2. The remote commands module that wraps the Kochava methods
3. Either the JSON configuration file or Remote Command tag that translates event tracking into native Kochava calls

Adding the Kochava remote command module to your app automatically installs and builds the required Kochava libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Kochava SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-kochava-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumKochava` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumKochava` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumKochava` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumKochava` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and  select the `TealiumKochava` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod &#34;KochavaTrackeriOS&#34;` if they already exist your Podfile. The dependency for `tealium-swift` is already included in the `TealiumKochava` framework.

2. Add the following dependency to your Podfile:
      ```ruby
      pod &#34;TealiumKochava&#34;
      ```
      The `TealiumKochava` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      &#39;tealium-swift/TagManagement&#39;
      ```

3. Import the modules `TealiumSwift` and `TealiumKochava` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Kochava Remote Command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumKochava` framework.

2.  Add the following dependency to your Cartfile:  
      ```bash
      github &#34;tealium/tealium-ios-kochava-remote-command&#34;
      ```

Tealium for Swift SDK (version 1.6.5&#43;) requires the `TealiumDelegate` module to be included with your installation.





1. Install [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) and add the Tealium Maven URL to your project’s top-level `build.gradle` file, if you haven&#39;t done so already.

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

2. Import both the Kochava SDK and Tealium-Kochava remote commands by adding the following dependencies in your app project&#39;s `build.gradle` file:  
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:kochava:1.0.0&#39;
      }
      ```





### Manual Installation




The manual installation for Kochava remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the Kochava remote commands for your iOS project:

1. Install the [Kochava SDK](https://support.kochava.com/sdk-integration/ios-sdk-integration/), if you haven&#39;t already done so.

2. Clone the [Tealium iOS Kochava remote command](https://github.com/tealium/tealium-ios-kochava-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true.`




The manual installation for Kochava remote commands requires [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) to be installed.

To install the Kochava remote commands for your Android project:

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

2. Add `tealium-kochava.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:

      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kochava&#39;, ext:&#39;aar&#39;)
      }
      ```



## Initialize

For all Tealium libraries, register the Kochava mobile remote commands when you initialize.




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
    let kochava = KochavaRemoteCommand() 

    // Local JSON
    //let kochava = KochavaRemoteCommand(type: .local(file: &#34;kochava&#34;))

    // Remote JSON 
    //let kochava = KochavaRemoteCommand(type: .remote(url: &#34;https://some.domain.com/kochava.json&#34;)) 

    remoteCommands.add(kochava)
}
```




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s Kotlin library:
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val kochava = KochavaRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(kochava); 

    // Local JSON
    //remoteCommands?.add(kochava, filename = &#34;kochava.json&#34;); 

    // Remote JSON
    //remoteCommands?.add(kochava, remoteUrl = &#34;https://some.domain.com/kochava.json&#34;); 
}
```




Initialize remote commands with the Remote Command tag for Tealium&#39;s Android (Java) library:

```java
RemoteCommand kochava = new KochavaRemoteCommand(application);
teal.addRemoteCommand(kochava);
```



## JSON Template

If you are configuring remote commands using a [JSON configuration file](/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard installation. Edit the mappings as needed.


```json
{
  &#34;config&#34;: {
    &#34;app_guid&#34;: &#34;test app guid&#34;,
    &#34;log_level&#34;: &#34;debug&#34;,
    &#34;app_tracking_transparency_enabled&#34;: false,
    &#34;limit_ad_tracking&#34;: true,
    &#34;identity_link_ids&#34;: {
        &#34;userID&#34;: &#34;CUST123&#34;,
        &#34;userName&#34;: &#34;Bob&#34;
    }
  },
  &#34;mappings&#34;: {
      &#34;event_title&#34;: &#34;custom_event_name&#34;,
      &#34;achievement_id&#34;: &#34;custom.achievement_id&#34;,
      &#34;ad_network_name&#34;: &#34;custom.ad_network_name&#34;,
      &#34;campaign_id&#34;: &#34;event.ad_campaign_id&#34;,
      &#34;campaign&#34;: &#34;event.ad_campaign_name&#34;,
      &#34;cart_add_location&#34;: &#34;event.item_added_from&#34;,
      &#34;checkout_option&#34;: &#34;custom.checkout_option&#34;,
      &#34;checkout_step&#34;: &#34;custom.checkout_step&#34;,
      &#34;content&#34;: &#34;event.content_id&#34;,
      &#34;content_type&#34;: &#34;event.content_type&#34;,
      &#34;coupon&#34;: &#34;custom.coupon&#34;,
      &#34;currency_code&#34;: &#34;event.currency&#34;,
      &#34;customer_id&#34;: &#34;event.user_id,identity_link_ids.userID&#34;,
      &#34;device_type&#34;: &#34;event.ad_device_type&#34;,
      &#34;end_date&#34;: &#34;event.end_date&#34;,
      &#34;flight_number&#34;: &#34;custom.flight_number&#34;,
      &#34;game_character&#34;: &#34;custom.character&#34;,
      &#34;group_name&#34;: &#34;event.ad_group_name&#34;,
      &#34;guest_checkout&#34;: &#34;event.checkout_as_guest&#34;,
      &#34;level&#34;: &#34;event.level&#34;,
      &#34;number_nights&#34;: &#34;custom.number_nights&#34;,
      &#34;number_pax&#34;: &#34;custom.number_passengers&#34;,
      &#34;number_rooms&#34;: &#34;custom.number_rooms&#34;,
      &#34;order_id&#34;: &#34;event.order_id&#34;,
      &#34;order_shipping_amount&#34;: &#34;custom.shipping&#34;,
      &#34;order_tax_amount&#34;: &#34;custom.tax&#34;,
      &#34;order_total&#34;: &#34;custom.total&#34;,
      &#34;product_brand&#34;: &#34;custom.brand&#34;,
      &#34;product_category&#34;: &#34;custom.category&#34;,
      &#34;product_id&#34;: &#34;custom.product_id&#34;,
      &#34;product_name&#34;: &#34;event.name&#34;,
      &#34;product_quantity&#34;: &#34;event.quantity&#34;,
      &#34;product_unit_price&#34;: &#34;event.price&#34;,
      &#34;rating&#34;: &#34;event.rating_value&#34;,
      &#34;score&#34;: &#34;event.score&#34;,
      &#34;search_keyword&#34;: &#34;event.search_term&#34;,
      &#34;search_results&#34;: &#34;event.results&#34;,
      &#34;signup_method&#34;: &#34;event.registration_method&#34;,
      &#34;start_date&#34;: &#34;event.start_date&#34;,
      &#34;travel_destination&#34;: &#34;event.destination&#34;,
      &#34;travel_class&#34;: &#34;custom.travel_class&#34;,
      &#34;travel_origin&#34;: &#34;event.origin&#34;,
      &#34;username&#34;: &#34;event.user_name,identity_link_ids.userName&#34;
    },
  &#34;commands&#34;: {
      &#34;launch&#34;: &#34;initialize&#34;,
      &#34;user_login&#34;: &#34;custom,sendidentitylink&#34;,
      &#34;user_register&#34;: &#34;registrationcomplete&#34;,
      &#34;share&#34;: &#34;custom&#34;,
      &#34;show_offers&#34;: &#34;adclick,adview&#34;,
      &#34;join_group&#34;: &#34;custom&#34;,
      &#34;travel_order&#34;: &#34;purchase&#34;,
      &#34;unlock_achievement&#34;: &#34;achievement&#34;,
      &#34;level_up&#34;: &#34;levelcomplete&#34;,
      &#34;stop_tutorial&#34;: &#34;tutorialcomplete&#34;,
      &#34;record_score&#34;: &#34;custom&#34;,
      &#34;category&#34;: &#34;view&#34;,
      &#34;product&#34;: &#34;view&#34;,
      &#34;cart_add&#34;: &#34;addtocart&#34;,
      &#34;wishlist_add&#34;: &#34;addtowishlist&#34;,
      &#34;checkout&#34;: &#34;checkoutstart&#34;,
      &#34;rating&#34;: &#34;rating&#34;,
      &#34;search&#34;: &#34;search&#34;,
      &#34;screen_veiw&#34;: &#34;view&#34;,
      &#34;email_signup&#34;: &#34;subscribe&#34;,
      &#34;order&#34;: &#34;purchase&#34;,
      &#34;disable_analytics&#34;: &#34;sleeptracker,invalidate&#34;
  }
}
```

## Push Message Tracking (iOS)

The Tealium Swift library includes a `TealiumRegistration` protocol for handling push message tracking through Tealium and the Kochava Remote Command. We conform to this protocol in the wrapper class `KochavaInstance` which is used to send push message authorization events, push message open events, and to uninstall tracking. We recommend taking advantage of the push message tracking capability.

The following steps integrate push message tracking for your iOS project:

1. In the `TealiumHelper.swift` file, initialize an empty array of objects that conform to the `TealiumRegistration` protocol. For example:  
      ```swift
      var pushMessagingHelpers = [TealiumRegistration]()
      ```
2. Initialize the `KochavaInstance` before the `KochavaRemoteCommand`
3. Append the `KochavaInstance` to the array described above

The following is an example of the push message tracking integration:  

```swift
var pushMessagingHelpers = [TealiumRegistration]()

//...

teal = Tealium(config: config) { responses in
  guard let remoteCommands = self.tealium?.remoteCommands() else {
        return
  }
  let kochavaInstance = KochavaInstance()
  let kochavaRemoteCommand = KochavaRemoteCommand(kochavaInstance: kochavaInstance)
  remoteCommands.add(kochavaRemoteCommand)
  self.pushMessagingHelpers.append(kochavaInstance)
}
```

To see the entire `TealiumHelper.swift` file, explore the [Kochava Remote Command Example App](https://github.com/Tealium/tealium-ios-kochava-remote-command/tree/master/TealiumKochavaExample). To send an event to Kochava once a user has registered for notifications, opened a push message, or uninstalled the app, see the file [`AppDelegate.swift`](https://github.com/Tealium/tealium-ios-kochava-remote-command/blob/master/TealiumKochavaExample/TealiumKochavaExample/AppDelegate.swift).

For more information about Kochava&#39;s push message tracking, see the [Kochava iOS push notification ](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-push-notification/) documentation.

## Enhanced Deep Linking (iOS)

The Tealium Swift Library includes a `TealiumDeepLinkable` protocol for handling your deep links through Tealium and the Kochava Remote Command. We conform to this protocol in wrapper class `KochavaInstance` which is used to send `.deepLink` events before rerouting your user to the location you want.

The following steps integrate enhanced deep linking for your iOS project:

1. In the `TealiumHelper.swift` file, initialize an empty array of objects that conform to the `TealiumDeepLinkable ` protocol. For example:  
      ```swift
      var deepLinkHelpers = [TealiumDeepLinkable]()
      ```
2. Initialize the `KochavaInstance` before the `KochavaRemoteCommand`
3. Append the `KochavaInstance` to the array described above.

The following is full example of the enhanced deep linking integration:  
      ```swift
      var deepLinkHelpers = [TealiumDeepLinkable]()

      //...

      teal = Tealium(config: config) { responses in
        guard let remoteCommands = self.tealium?.remoteCommands() else {
          return
        }
        let kochavaInstance = KochavaInstance()
        let kochavaRemoteCommand = KochavaRemoteCommand(kochavaInstance: kochavaInstance)
        remoteCommands.add(kochavaRemoteCommand)
        self.deepLinkHelpers.append(kochavaInstance)
      }
      ```

To see the entire `TealiumHelper.swift` file, explore the [Kochava Remote Command Example App](https://github.com/Tealium/tealium-ios-kochava-remote-command/tree/master/TealiumKochavaExample).

To send an event to Kochava once a user has registered for notifications, opened a push message, or uninstalled the app, see the file [`AppDelegate.swift`](https://github.com/Tealium/tealium-ios-kochava-remote-command/blob/master/TealiumKochavaExample/TealiumKochavaExample/AppDelegate.swift).

For more information about Kochava&#39;s enhanced deep linking, see the [Kochava iOS](http://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/) documentation.

## Supported Methods

We map a command to each Kochava method. To trigger a Kochava method, pass the corresponding command in the specified format.

#### iOS Remote Commands

| iOS Remote Command | Kochava Method |
| :-- | :-- |
| `initialize` | `start()` |
| `sleepTracker` | `sleepTracker (property on the KochavaTracker.shared object)` |
| `invalidate` | `invalidate()` |
| Any of the below event names | `sendEvent()` |
| `sendIdentityLink` | `sendIdentityLink()` |
| Called manually in `AppDelegate` within `didReceiveRemoteNotification` | `sendEvent() - event type: .pushOpened` |
| Called manually in `AppDelegate` within `didRegisterForRemoteNotificationsWithDeviceToken` using `TealiumRegistration` protocol (`registerPushToken()` method) | `addRemoteNotificationsDeviceToken()` |
| Called manually in `AppDelegate` within `continue userActivity` using `TealiumDeeplinkable` protocol | `KVADeeplink.process()` and/or `sendEvent() - event type: .deepLink` |

#### Android Remote Commands

| Android Remote Command | Kochava Method |
| :-- | :-- |
| `configure` | `configure()` |
| `setsleep` | `setSleep()` |
| Any of the below event names | `sendEvent()` |

### Standard Event Names

The following standard event command names are supported with the `trackEvent` method. When a command is sent, and all required variables are mapped and defined for the event, then the command is automatically triggered in the Kochava SDK.

| Remote Command | Kochava Event Name (iOS)| Kochava Event Name (Andriod)
| :-- | :-- | :-- |
|`achievement`| `KVAEventType.achievement`| `Commands.ACHIEVEMENT` |
|`addToCart`| `KVAEventType.addToCart`| `Commands.ADD_TO_CART` |
|`addToWishlist`| `KVAEventType.addToWishList`| `Commands.Add_TO_WISH_LIST` |
|`registrationComplete`| `KVAEventType.registrationComplete`| `Commands.REGISTRATION_COMPLETE` |
|`tutorialComplete`| `KVAEventType.tutorialComplete`| `Commands.TUTORIAL_COMPLETE` |
|`levelComplete`| `KVAEventType.levelComplete`| `Commands.LEVEL_COMPLETE` |
|`checkoutStart`| `KVAEventType.checkoutStart`| `Commands.CHECKOUT_START` |
|`purchase`| `KVAEventType.purchase`| `Commands.PURCHASE` |
|`subscribe`| `KVAEventType.subscribe`| `Commands.SUBSCRIBE` |
|`startTrial`| `KVAEventType.startTrial`| `Commands.START_TRIAL` |
|`rating`| `KVAEventType.rating`| `Commands.RATING` |
|`search`| `KVAEventType.search`| `Commands.SEARCH` |
|`adView`| `KVAEventType.adView`| `Commands.AD_VIEW` |
|`view`| `KVAEventType.view`| `Commands.VIEW` |
|`pushOpened`| `KVAEventType.pushOpened`| requires `customEventNameString` in mappings |
|`pushRecieved`| `KVAEventType.pushReceived`| requires `customEventNameString` in mappings |
|`consentGranted`| `KochavaEventTypeEnumConsentGranted`| requires `customEventNameString` in mappings |
|`adClick`| `KVAEventType.adClick`| requires `customEventNameString` in mappings |
|`custom`| `KVAEventType.custom` (`customEventNameString` required in mappings)| requires `customEventNameString` in mappings |

For iOS, the `KVAEvent.deepLink` event needs to be sent in the `AppDelegate` using either the native `KVAEvent.send()` method or the [`TealiumDeepLinkable` protocol](/platforms/remote-commands/integrations/kochava/#enhanced-deeplinking-ios).

### SDK Setup

Learn more about the Kochava SDK Setup:

  - [Kochava iOS SDK](https://support.kochava.com/sdk-integration/ios-sdk-integration/)
  - [Kochava Android SDK](https://support.kochava.com/sdk-integration/android-sdk-integration/)

#### Initialize

The Kochava SDK is initialized automatically upon launch. The Kochava App GUID is set in the Tealium remote command configuration.

| Remote Command | Kochava Method |
|---|---|
| `initialize`  | `start()` |

There are several configuration options available for the Kochava Remote Command tag. If any of the below are set on launch, they are sent during the `configure()` method.

##### Configuration Options

| Name | TiQ Variable Mapping | Description | Type |
|---|---|---|---|
| Log Level  | `log_level` | The log level for Kochava output in the console: `none`, `error`, `warn`, `info`, `debug`, `trace` (Learn more about [log levels](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_10)) | `String` |
| Retrieve Attribution Data | `retrieve_attribution_data`  | Boolean for setting a delegate/listener that gets the attribution data when ready. In `TealiumKochava` the `attributionDictionary` is set to [Volatile Storage](/platforms/getting-started-mobile/mobile-concepts/#volatile-storage), and sent a `track` call with a `tealium_event` of `attribution`. The delegate/listener method may be added in `TealiumKochavaTracker` (Learn more about [retrieving attribution](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_6))| `Bool` |
| Identity Link IDs | `identity_link_ids`  | Links different identities together in the form of key-value pairs (Learn more about [identity linking](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_5)) | `Int` |
| Limit Ad Tracking | `limit_ad_tracking`  | Limits ad tracking at the application level if enabled (Default: `false`) | `Bool` |
| Enable App Tracking Transparency (iOS 14&#43;) | `app_tracking_transparency_enabled`  | Enables Kochava&#39;s automatic implementation of App Tracking Transparency (iOS 14&#43;) if enabled. (Default: `false`) | `Bool` |

#### Sleep Tracker

| Remote Command | Kochava Method |
|---|---|
| `sleeptracker` (iOS) | `sleepTracker` (`KochavaTracker.shared` object property) |
| `setsleep` (Android) | `setSleep()` |

|  Parameter | Type |
|---|---|
|  `sleep` (required) | `Bool` |


#### Invalidate (iOS)

| Remote Command | Kochava Method |
| :--- | :---|
| `invalidate`  | `invalidate()` |


#### Send Identity Link (iOS)

|  Remote Command | Kochava Method |
|---|---|
| `sendidentitylink`  | `sendIdentityLink()` |

|  Parameter | Type |
|---|---|
|  `identityLinkIds` (required) | Key-value pairs |

#### Send Custom Event (iOS)

|  Remote Command | Kochava Method |
|---|---|
| [Standard Event Names](#standard-event-names) | `send()` |

|  Parameter | Type |
|---|---|
|  `event_parameters` (optional) | Key-value pairs |

#### Send Custom Event (iOS)

|  Remote Command | Kochava Method |
|---|---|
| `custom`  | `sendCustom()` |

|  Parameter | Type |
|---|---|
|  `custom_event_name` (required) | `String` |
|  `info_dictionary` (optional) | Key-value pairs |
