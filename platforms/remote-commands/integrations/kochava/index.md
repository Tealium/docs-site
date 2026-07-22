---
title: Remote Command: Kochava
description: Tealium remote command integration for Kochava on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/kochava/
---
## Requirements

* [Kochava App GUID](https://support.kochava.com/reference-information/locating-an-app-guid/)
* One of these mobile libraries:
  * [Tealium for Android-Kotlin](https://docs.tealium.com/platforms/android-kotlin/) (1.0.0+)
  * [Tealium for Android-Java](https://docs.tealium.com/platforms/android-java/) (5.9.0+)
  * [Tealium for iOS-Swift](https://docs.tealium.com/platforms/ios-swift/) (2.1.0+)
* One of these remote command integrations:
  * [Kochava Remote Command JSON File](https://docs.tealium.com/platforms/remote-commands/integrations/kochava/#json-template) (Requires Android-Kotlin 1.0.0+ or iOS-Swift 2.1.0+)
  * [Kochava Remote Command tag](https://docs.tealium.com/kochava-mobile-remote-command-tag/) in Tealium iQ Tag Management

## How It Works

The Kochava integration uses three items:

1. The Kochava native SDK
2. The remote commands module that wraps the Kochava methods
3. Either the JSON configuration file or Remote Command tag that translates event tracking into native Kochava calls

Adding the Kochava remote command module to your app automatically installs and builds the required Kochava libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Kochava SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File > Add Packages... > Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-kochava-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumKochava` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumKochava` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumKochava` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumKochava` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General > Frameworks, Libraries & Embedded Content** and  select the `TealiumKochava` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod "KochavaTrackeriOS"` if they already exist your Podfile. The dependency for `tealium-swift` is already included in the `TealiumKochava` framework.

2. Add the following dependency to your Podfile:
      ```ruby
      pod "TealiumKochava"
      ```
      The `TealiumKochava` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. Import the modules `TealiumSwift` and `TealiumKochava` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Kochava Remote Command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumKochava` framework.

2.  Add the following dependency to your Cartfile:  
      ```bash
      github "tealium/tealium-ios-kochava-remote-command"
      ```


<blockquote>
Tealium for Swift SDK (version 1.6.5+) requires the `TealiumDelegate` module to be included with your installation.
</blockquote>






1. Install [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) and add the Tealium Maven URL to your project’s top-level `build.gradle` file, if you haven't done so already.

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

2. Import both the Kochava SDK and Tealium-Kochava remote commands by adding the following dependencies in your app project's `build.gradle` file:  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:kochava:1.0.0'
      }
      ```





### Manual Installation




The manual installation for Kochava remote commands requires the [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/) library to be installed. To install the Kochava remote commands for your iOS project:

1. Install the [Kochava SDK](https://support.kochava.com/sdk-integration/ios-sdk-integration/), if you haven't already done so.

2. Clone the [Tealium iOS Kochava remote command](https://github.com/tealium/tealium-ios-kochava-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Set the [`remoteAPIEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true.`




The manual installation for Kochava remote commands requires [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) to be installed.

To install the Kochava remote commands for your Android project:

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

2. Add `tealium-kochava.aar` to `<PROJECT_ROOT>/<MODULE>/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:

      ```groovy
      dependencies {
            implementation(name:'tealium-kochava', ext:'aar')
      }
      ```



## Initialize

For all Tealium libraries, register the Kochava mobile remote commands when you initialize.




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
    let kochava = KochavaRemoteCommand() 

    // Local JSON
    //let kochava = KochavaRemoteCommand(type: .local(file: "kochava"))

    // Remote JSON 
    //let kochava = KochavaRemoteCommand(type: .remote(url: "https://some.domain.com/kochava.json")) 

    remoteCommands.add(kochava)
}
```




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's Kotlin library:
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val kochava = KochavaRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(kochava); 

    // Local JSON
    //remoteCommands?.add(kochava, filename = "kochava.json"); 

    // Remote JSON
    //remoteCommands?.add(kochava, remoteUrl = "https://some.domain.com/kochava.json"); 
}
```




Initialize remote commands with the Remote Command tag for Tealium's Android (Java) library:

```java
RemoteCommand kochava = new KochavaRemoteCommand(application);
teal.addRemoteCommand(kochava);
```



## JSON Template

If you are configuring remote commands using a [JSON configuration file](https://docs.tealium.com/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard installation. Edit the mappings as needed.


```json
{
  "config": {
    "app_guid": "test app guid",
    "log_level": "debug",
    "app_tracking_transparency_enabled": false,
    "limit_ad_tracking": true,
    "identity_link_ids": {
        "userID": "CUST123",
        "userName": "Bob"
    }
  },
  "mappings": {
      "event_title": "custom_event_name",
      "achievement_id": "custom.achievement_id",
      "ad_network_name": "custom.ad_network_name",
      "campaign_id": "event.ad_campaign_id",
      "campaign": "event.ad_campaign_name",
      "cart_add_location": "event.item_added_from",
      "checkout_option": "custom.checkout_option",
      "checkout_step": "custom.checkout_step",
      "content": "event.content_id",
      "content_type": "event.content_type",
      "coupon": "custom.coupon",
      "currency_code": "event.currency",
      "customer_id": "event.user_id,identity_link_ids.userID",
      "device_type": "event.ad_device_type",
      "end_date": "event.end_date",
      "flight_number": "custom.flight_number",
      "game_character": "custom.character",
      "group_name": "event.ad_group_name",
      "guest_checkout": "event.checkout_as_guest",
      "level": "event.level",
      "number_nights": "custom.number_nights",
      "number_pax": "custom.number_passengers",
      "number_rooms": "custom.number_rooms",
      "order_id": "event.order_id",
      "order_shipping_amount": "custom.shipping",
      "order_tax_amount": "custom.tax",
      "order_total": "custom.total",
      "product_brand": "custom.brand",
      "product_category": "custom.category",
      "product_id": "custom.product_id",
      "product_name": "event.name",
      "product_quantity": "event.quantity",
      "product_unit_price": "event.price",
      "rating": "event.rating_value",
      "score": "event.score",
      "search_keyword": "event.search_term",
      "search_results": "event.results",
      "signup_method": "event.registration_method",
      "start_date": "event.start_date",
      "travel_destination": "event.destination",
      "travel_class": "custom.travel_class",
      "travel_origin": "event.origin",
      "username": "event.user_name,identity_link_ids.userName"
    },
  "commands": {
      "launch": "initialize",
      "user_login": "custom,sendidentitylink",
      "user_register": "registrationcomplete",
      "share": "custom",
      "show_offers": "adclick,adview",
      "join_group": "custom",
      "travel_order": "purchase",
      "unlock_achievement": "achievement",
      "level_up": "levelcomplete",
      "stop_tutorial": "tutorialcomplete",
      "record_score": "custom",
      "category": "view",
      "product": "view",
      "cart_add": "addtocart",
      "wishlist_add": "addtowishlist",
      "checkout": "checkoutstart",
      "rating": "rating",
      "search": "search",
      "screen_veiw": "view",
      "email_signup": "subscribe",
      "order": "purchase",
      "disable_analytics": "sleeptracker,invalidate"
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

For more information about Kochava's push message tracking, see the [Kochava iOS push notification ](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-push-notification/) documentation.

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

For more information about Kochava's enhanced deep linking, see the [Kochava iOS](http://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/) documentation.

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


<blockquote>
For iOS, the `KVAEvent.deepLink` event needs to be sent in the `AppDelegate` using either the native `KVAEvent.send()` method or the [`TealiumDeepLinkable` protocol](https://docs.tealium.com/platforms/remote-commands/integrations/kochava/#enhanced-deeplinking-ios).
</blockquote>


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
| Retrieve Attribution Data | `retrieve_attribution_data`  | Boolean for setting a delegate/listener that gets the attribution data when ready. In `TealiumKochava` the `attributionDictionary` is set to [Volatile Storage](https://docs.tealium.com/platforms/getting-started-mobile/mobile-concepts/#volatile-storage), and sent a `track` call with a `tealium_event` of `attribution`. The delegate/listener method may be added in `TealiumKochavaTracker` (Learn more about [retrieving attribution](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_6))| `Bool` |
| Identity Link IDs | `identity_link_ids`  | Links different identities together in the form of key-value pairs (Learn more about [identity linking](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_5)) | `Int` |
| Limit Ad Tracking | `limit_ad_tracking`  | Limits ad tracking at the application level if enabled (Default: `false`) | `Bool` |
| Enable App Tracking Transparency (iOS 14+) | `app_tracking_transparency_enabled`  | Enables Kochava's automatic implementation of App Tracking Transparency (iOS 14+) if enabled. (Default: `false`) | `Bool` |

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
