---
title: Remote Command: Facebook
description: Tealium remote command integration for Facebook on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/facebook/
---
## Requirements

* One of these mobile libraries:
  * [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/) (1.0.0+).
  * [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/) (5.9.0+ for Facebook 1.0.0+ or <5.9.0 for previous versions).
  * [Tealium for iOS (Swift)](https://docs.tealium.com/platforms/ios-swift/).
* One of these remote command integrations:
  * [Facebook Remote Command JSON File](https://docs.tealium.com/platforms/remote-commands/integrations/facebook/.#json-template) (Requires Android-Kotlin 1.0.0+ or iOS-Swift 2.1.0+).
  * Facebook Remote Command tag in Tealium iQ Tag Management.

The following are requirements for iOS and Android:  




Add the following keys to your `app/src/main/res/values/strings.xml` file. Replace `[APP_ID]` with your Facebook App ID and `[CLIENT_TOKEN]` with your Facebook Client Token:
```xml
<string name="facebook_app_id">[APP_ID]</string>
<string name="fb_login_protocol_scheme">fb[APP_ID]</string>
<string name="facebook_client_token">[CLIENT_TOKEN]</string>
```

The following `meta-data` element is required in the `AndroidManifest.xml` file:
```xml
<application android:label="@string/app_name" ...>
    ...
    <meta-data
      android:name="com.facebook.sdk.ApplicationId"
      android:value="@string/facebook_app_id" />
    <meta-data 
        android:name="com.facebook.sdk.ClientToken"
        android:value="@string/facebook_client_token" />
    ...
</application>
```

Learn more: [Facebook Android Getting Started - Integrate the Facebook SDK in Your Android App](https://developers.facebook.com/docs/app-events/getting-started-app-events-android).




Add the following keys to your `Info.plist` file. Replace `[APP_ID]` with your Facebook App ID, `[APP_NAME]` with your app name, and `[CLIENT_TOKEN]` with your Facebook Client Token:  
```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
  <key>CFBundleURLSchemes</key>
  <array>
    <string>fb[APP_ID]</string>
  </array>
  </dict>
</array>
<key>FacebookAppID</key>
<string>[APP_ID]</string>
<key>FacebookDisplayName</key>
<string>[APP_NAME]</string>
<key>FacebookClientToken</key>
<string>[CLIENT_TOKEN]</string>
```
Learn more: [Facebook iOS Getting Started - Configure Your Property List](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios/#plist-config).

Update the `AppDelegate` code as follows:

1. Import `FBSDKCoreKit`.
2. In the `didFinishLaunchingWithOptions` method add the following:  
      ```swift
      ApplicationDelegate.shared.application(
            application, 
            didFinishLaunchingWithOptions: launchOptions)
      ```
3. Add the following function in your `AppDelegate.swift` (or Objective-C equivalent):
      ```swift
      func application(
            _ app: UIApplication,
            open url: URL,
            options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        let handled = ApplicationDelegate.shared.application(
            app,
            open: url,
            options: options)
      }
      ```
Learn more: [Facebook iOS Getting Started - Set Up Your Development Environment](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios/#dev-env-setup).




## How It Works

The Facebook integration uses three items:

1. The Facebook native SDK.
2. The remote commands module that wraps the Facebook methods.
3. Either the JSON configuration file or Remote Command tag that translates event tracking into native Facebook calls.

Adding the Facebook remote command module to your app automatically installs and builds the required Facebook libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Facebook SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File > Add Packages... > Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-facebook-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumFacebook` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumFacebook` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumFacebook` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumFacebook` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General > Frameworks, Libraries & Embedded Content** and  select the `TealiumFacebook` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod "FBSDKCoreKit"` if they already exist your Podfile. The dependency for `tealium-swift` is already included in the `TealiumFacebook` framework.

2. Add the following dependency to your Podfile:
      ```ruby
      pod "TealiumFacebook"
      ```
      The `TealiumFacebook` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. Import the modules `TealiumSwift` and `TealiumFacebook` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Facebook Remote Command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumFacebook` framework.

2. Remove the following line if it exists in your Cartfile:  
      ```bash
      github "facebook/facebook-ios-sdk"
      ```

3.  Add the following dependency to your Cartfile:  
      ```bash
      github "tealium/tealium-ios-facebook-remote-command"
      ```


<blockquote>
Tealium for Swift SDK (version 2.12+) is required for the latest Facebook Remote Command integration.
</blockquote>






1. Install [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) and add the Tealium Maven URL to your project's top-level `build.gradle` file, if you haven't done so already.


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

2. Import both the Facebook SDK and Tealium-Facebook remote command by adding the following dependencies in your app project's `build.gradle` file:  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:facebook:3.0.0'
      }
      ```




### Manual Installation




The manual installation for Facebook remote commands requires the [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/) library to be installed. To install the Facebook remote commands for your iOS project:

1. Install the [Facebook SDK](https://github.com/facebook/facebook-ios-sdk/tree/master/FBSDKCoreKit), if you haven't already done so.

2. Clone the [Tealium iOS Facebook remote command](https://github.com/tealium/tealium-ios-facebook-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Add `Dispatchers.RemoteCommands` as a dispatcher.

4. Set the [`remoteAPIEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true.`




The manual installation for Facebook remote commands requires [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) to be installed.

To install the Facebook remote commands for your Android project:

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

2. Add `tealium-facebook.aar` to `<PROJECT_ROOT>/<MODULE>/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:  
      ```groovy
      dependencies {
            implementation(name:'tealium-facebook', ext:'aar')
      }
      ```



## Initialize

For all Tealium libraries, register the Facebook Remote Command when you initialize.





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
    let facebook = FacebookRemoteCommand(launchOptions: launchOptions) 

    // Local JSON
    //let facebook = FacebookRemoteCommand(type: .local(file: "facebook"), launchOptions: launchOptions) 

    // Remote JSON
    //let facebook = FacebookRemoteCommand(type: .remote(url: "https://some.domain.com/facebook.json"), launchOptions: launchOptions) 

    remoteCommands.add(facebook)
}
```



Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's Kotlin library:
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val facebook = FacebookRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Webview Tag
    remoteCommands?.add(facebook); 

    // Local JSON
    //remoteCommands?.add(facebook, filename = "facebook.json"); 

    // Remote JSON
    //remoteCommands?.add(facebook, remoteUrl = "https://some.domain.com/facebook.json"); 
}
```



Initialize remote commands with the Remote Command tag for Tealium's Android (Java) library:   
```java
import com.tealium.remotecommands.facebook.FacebookRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

FacebookRemoteCommand facebook = new FacebookRemoteCommand(this);

// register the command
teal.addRemoteCommand(facebook);
```




## JSON Template

If you are configuring remote commands using a [JSON configuration file](https://docs.tealium.com/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
  "config": {
    "applicationid": "YOUR_APP_ID",
    "clienttoken": "YOUR_CLIENT_TOKEN",
    "accesstoken": "YOUR_ACCESS_TOKEN",
    "userid": "YOUR_USER_ID",
    "auto_log": true,
    "auto_log_events_enabled": true,
    "auto_initialized": true,
    "advertiser_id_collection_enabled": true,
    "advertiser_collection": true,
    "debug": true
  },
  "mappings": {
    "achievement_type": "event.fb_description",
    "ad_type": "event.ad_type",
    "content": "event.fb_content",
    "content_type": "event.fb_content_type",
    "currency_code": "event.fb_currency",
    "event_name": "event.fb_description",
    "current_level": "event.fb_level",
    "pet_count": "event.fb_max_rating_value",
    "number_of_items": "event.fb_num_items",
    "order_id": "event.fb_order_id",
    "payment_info_available": "event.fb_payment_info_available",
    "signup_method": "event.fb_registration_method",
    "search_keyword": "event.fb_search_string",
    "success": "event.fb_success",
    "customer_email": "user.em",
    "customer_first_name": "user.fn",
    "customer_last_name": "user.ln",
    "customer_phone": "user.ph",
    "customer_dob": "user.dob",
    "customer_gender": "user.ge",
    "customer_city": "user.ct",
    "customer_state": "user.st",
    "customer_zip": "user.zp",
    "customer_country": "user.country",
    "customer_id": "fb_user_id",
    "user_value": "fb_user_value",
    "user_key": "fb_user_key",
    "product_id": "product.fb_product_item_id,event.fb_content_id",
    "product_availability": "product.fb_product_availability",
    "product_condition": "product.fb_product_condition",
    "product_description": "product.fb_product_description,event.fb_product_description",
    "product_image_link": "product.fb_product_image_link",
    "product_link": "product.fb_product_link",
    "product_name": "product.fb_product_title",
    "product_variant": "product.fb_product_gtin",
    "product_brand": "product.fb_product_brand",
    "product_price": "product.fb_product_price_amount,event.fb_value_to_sum",
    "product_currency": "product.fb_product_price_currency",
    "product_alias": "product_parameters.product_alias",
    "product_color": "product_parameters.product_color",
    "order_total": "purchase.fb_purchase_amount",
    "order_currency": "purchase.fb_purchase_currency",
    "customer_status": "purchase_parameters.customer_status",
    "coupon": "purchase_parameters.coupon",
    "push_action": "push.fb_push_action",
    "push_payload": "push.fb_push_payload",
    "tealium_event": "command_name"
  },
  "commands": {
    "launch": "initialize,setautologappeventsenabled,setautoinitenabled,enableadvertiseridcollection",
    "user_login": "setuser,setuserid",
    "email_signup": "updateuservalue",
    "level_up": "achievedlevel",
    "user_register": "completedregistration",
    "unlock_achievement": "unlockedachievement",
    "cart_add": "addedtocart",
    "custom_attribute": "rated",
    "wishlist_add": "addedtowishlist",
    "payment": "initiatedcheckout",
    "product": "logproductitem",
    "order": "logpurchase",
    "flush": "flush",
    "customfbevent": "customfbevent"
  }
}
```

## Push Message Tracking (iOS)

The Tealium Swift library includes a `TealiumRegistration` protocol for handling push message tracking through Tealium and the Facebook Remote Command. We conform to this protocol in the wrapper class `FacebookInstance`, which is used to send push message authorization events, push message open events, and to uninstall tracking. We recommend taking advantage of the push message tracking capability.

The following steps integrate push message tracking for your iOS project:

1. In the `TealiumHelper.swift` file, initialize an empty array of objects that conform to the `TealiumRegistration` protocol. For example:  
      ```swift
      var pushMessagingHelpers = [TealiumRegistration]()
      ```
2. Initialize the `FacebookInstance` before the `FacebookRemoteCommand.`
3. Append the `FacebookInstance` to the array described above.

The following is an example of the push message tracking integration:
```swift
var pushMessagingHelpers = [TealiumRegistration]()

//...

teal = Tealium(config: config) { responses in
      guard let remoteCommands = self.tealium?.remoteCommands() else {
            return
      }
      let facebookInstance = FacebookInstance()
      let facebookRemoteCommand = FacebookRemoteCommand(facebookInstance: facebookInstance)
      remoteCommands.add(facebookRemoteCommand)
      self.pushMessagingHelpers.append(facebookInstance)
}
```

To see the entire `TealiumHelper.swift` file, explore the [Facebook Remote Command sample apps](https://github.com/Tealium/tealium-ios-facebook-remote-command/tree/master/Examples). To send an event to Facebook once a user has registered for notifications, opened a push message, or uninstalled the app, see the file `AppDelegate.swift`.

## Supported Methods

We map a command to each Facebook method. To trigger a Facebook method, pass the corresponding command in the specified format.

| Remote Command | Facebook Method | Supported Platforms |
| -------------- | --------------- | ------------------- |
| `clearuser`(ios)/`clearuserdata`(android) | `clearUserData()` | iOS, Android |
| `clearuserid` | `clearUserId()` | iOS, Android |
| `enableadvertiseridcollection` | `setAdvertiserIDCollectionEnabled()` | iOS, Android |
| `flush` | `flush()` | iOS, Android |
| `initialize` | `initialize()` | iOS, Android |
| `logproductitem` | `logProductItem()` | iOS, Android |
| `logpurchase` | `logPurchase()` | iOS, Android |
| `setautoinitenabled` | `setAutoInitEnabled()` | Android |
| `setautologappeventsenabled` | `setAutoLogAppEventsEnabled()` | iOS, Android |
| `setflushbehavior` | `setFlushBehavior()` | iOS, Android |
| `setpushregistrationid` | `setPushNotificationsRegistrationId()` | Android only |
| `setuser`(ios, android)/`updateUserValue`(ios) | `setUserData()` | iOS, Android |
| `setuserid` | `setUserId()` | iOS, Android |
| Any of the below event names | `logEvent()` | iOS, Android |

### Standard Event Names

The following is a list of standard event names supported with the `logEvent` method. If any of the below command names are sent, they are automatically triggered in the Facebook SDK. This is assuming all the required variables are also mapped and defined for that particular event. Learn about [recording in-app events](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios/#manually-log-events).

| Remote Command               | Facebook Event Name                                |
| :--------------------------- | :------------------------------------------------ |
| `activatedapp`               | `FBSDKAppEventNameActivatedApp`                   |
| `achievedlevel`              | `FBSDKAppEventNameAchievedLevel`                  |
| `adclick`                    | `FBSDKAppEventNameAdClick`                        |
| `adimpression`               | `FBSDKAppEventNameAdImpression`                   |
| `addedpaymentinfo`           | `FBSDKAppEventNameAddedPaymentInfo`               |
| `addedtocart`                | `FBSDKAppEventNameAddedToCart`                    |
| `addedtowishlist`            | `FBSDKAppEventNameAddedToWishlist`                |
| `completedregistration`      | `FBSDKAppEventNameCompletedRegistration`          |
| `completedtutorial`          | `FBSDKAppEventNameCompletedTutorial`              |
| `contact`                    | `FBSDKAppEventNameContact`                        |
| `customizeproduct`           | `FBSDKAppEventNameCustomizeProduct`               |
| `deactivatedapp`             | `FBSDKAppEventNameDeactivatedApp`                 |
| `donate`                     | `FBSDKAppEventNameDonate`                         |
| `findlocation`               | `FBSDKAppEventNameFindLocation`                   |
| `initiatedcheckout`          | `FBSDKAppEventNameInitiatedCheckout`              |
| `livestreamingstart`         | `FBSDKAppEventNameLiveStreamingStart`             |
| `livestreamingstop`          | `FBSDKAppEventNameLiveStreamingStop`              |
| `livestreamingpause`         | `FBSDKAppEventNameLiveStreamingPause`             |
| `livestreamingresume`        | `FBSDKAppEventNameLiveStreamingResume`            |
| `livestreamingerror`         | `FBSDKAppEventNameLiveStreamingError`             |
| `livestreamingupdatestatus`  | `FBSDKAppEventNameLiveStreamingUpdateStatus`      |
| `productcatalogupdate`       | `FBSDKAppEventNameProductCatalogUpdate`           |
| `pushtokenobtained`          | `FBSDKAppEventNamePushTokenObtained`              |
| `rated`                      | `FBSDKAppEventNameRated`                          |
| `schedule`                   | `FBSDKAppEventNameSchedule`                       |
| `searched`                   | `FBSDKAppEventNameSearched`                       |
| `sessioninterruptions`       | `FBSDKAppEventNameSessionInterruptions`           |
| `spentcredits`               | `FBSDKAppEventNameSpentCredits`                   |
| `starttrial`                 | `FBSDKAppEventNameStartTrial`                     |
| `submitapplication`          | `FBSDKAppEventNameSubmitApplication`              |
| `subscribe`                  | `FBSDKAppEventNameSubscribe`                      |
| `timebetweensessions`        | `FBSDKAppEventNameTimeBetweenSessions`            |
| `unlockedachievement`        | `FBSDKAppEventNameUnlockedAchievement`            |
| `viewedcontent`              | `FBSDKAppEventNameViewedContent`                  |



<blockquote>
Since the Facebook SDK is installed alongside the Tealium SDK, you are able to trigger any native Facebook functionality given the corresponding tag configuration.
</blockquote>


### Clear User

Clears the current user data.

| Event Name  | Required | Optional | Type |
| ----------- | -------- | -------- | ---- |
| `clearuser` |          |          |      |

- [Facebook iOS SDK Integration - clearUserData](https://github.com/facebook/facebook-ios-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L800)
- [Facebook Android SDK Integration - clearUserData](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L708)

### Clear User ID

Clears the currently set user ID.

| Event Name     | Required | Optional | Type |
| -------------- | -------- | -------- | ---- |
| `clearuserid`  |          |          |      |

- [Facebook iOS SDK Integration - clearUserId](https://github.com/facebook/facebook-ios-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L761)
- [Facebook Android SDK Integration - clearUserId](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L629)


### Set Advertiser ID Collection

Sets the advertiserID collection flag for the application.

| Event Name                     | Required                                | Optional | Type   |
| ------------------------------ | --------------------------------------- | -------- | ------ |
| `enableadvertiseridcollection` | `advertiser_collection`(android)        |          | `bool` |
|                                | `advertiser_id_collection_enabled`(ios) |          |          |        |

- [Facebook iOS SDK Integration - setAdvertiserIDCollectionEnabled](https://github.com/facebook/facebook-ios-sdk/blob/ae94c9c7489fd8b080a965d9551758eadf419a06/FBSDKCoreKit/FBSDKCoreKit/Settings.swift#L155)
- [Facebook Android SDK Integration - setAdvertiserIDCollectionEnabled](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/FacebookSdk.kt#L1011)

### Flush

Explicitly kick off flushing of events to Facebook. This is an asynchronous method, but it does initiate an immediate kick off. Server failures are reported through the NotificationCenter with notification ID `FBSDKAppEventsLoggingResultNotification`.

| Event Name | Required | Optional | Type |
| ---------- | -------- | -------- | ---- |
| `flush`    |          |          |      |

- [Facebook iOS SDK Integration - flush](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L730)
- [Facebook Android SDK Integration - flush](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L560)

### Initialize

Initializes the Facebook SDK with application credentials.

| Event Name   | Required        | Optional      | Type      |
| ------------ | --------------- | ------------- | --------- |
| `initialize` | `applicationid` |               | `String`  |
|              |                 | `clienttoken` | `String`  |
|              |                 | `debug`       | `Boolean` |

### Log Product Item

Uploads product catalog product item as an app event.

| Event Name     | Required                  | Optional           | Type                                       |
| -------------- | ------------------------- | ------------------ | ------------------------------------------ |
| `logProductItem` | `fb_product_item_id`        |                  | `String`                                     |
|                | `fb_product_availability`   |                    | `Int` (See lookup below)                     |
|                | `fb_product_condition`      |                    | `Int` (See lookup below)                     |
|                | `fb_product_description`    |                    | `String`                                     |
|                | `fb_product_image_link`     |                    | `String`                                     |
|                | `fb_product_link`           |                    | `String`                                     |
|                | `fb_product_title`          |                    | `String`                                     |
|                | `fb_product_price_amount`   |                    | `Double/Decimal`                             |
|                | `fb_product_price_currency` |                    | `String`                                     |
|                | `fb_product_parameters`     |                    | `[String: Any]` - JavaScript Object if in iQ |
|                |                           | `fb_product_gtin`  | `String`                                     |
|                |                           | `fb_product_mpn` | `String`                                     |
|                |                           | `fb_product_brand` | `String`                                     |


<blockquote>
Either `gtin`, `mpn` or `brand` is required. Product parameters are optional fields for deep link specification.
</blockquote>


| Product Availability Input | Product Availability Lookup              |
| -------------------------- | ---------------------------------------- |
| `0`                          | In Stock - Item ships immediately        |
| `1`                          | Out of stock - No plan to restock        |
| `2`                          | Preorder - Available in future           |
| `3`                          | Available for order - Ships in 1-2 weeks |
| `4`                          | Discontinued - Discontinued              |

| Product Condition Input | Product Condition Lookup |
| ----------------------- | ------------------------ |
| `0`                       | New                      |
| `1`                       | Refurbished              |
| `2`                       | Used                     |

- [Facebook iOS SDK Integration - logProductItem](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L642)
- [Facebook Android SDK Integration - logProductItem](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L524)

### Log Purchase

 Log a purchase of the specified amount, in the specified currency, also optionally providing a set of additional characteristics describing the purchase.

 Arbitrary parameter dictionary of characteristics. The keys to this dictionary must
 be `NSString`'s, and the values are expected to be `NSString` or `NSNumber`. Limitations on the number of
 parameters and name construction are given in the [FBSDKAppEvents](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios#event-names) documentation. Commonly used parameter names
 are provided in [FBSDKAppEventParameterName](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios#event-params) constants.

| Event Name  | Required             | Optional               | Type                                     |
| ----------- | -------------------- | ---------------------- | ---------------------------------------- |
| `logPurchase` | `fb_purchase_amount`   |                        | `Decimal/Double` (iOS) / `Double` (Android)  |
|             | `fb_purchase_currency` |                        | `String`                                   |
|             |                      | `fb_purchase_parameters` | `[String: Any]` - Javascript object in iQ |

- [Facebook iOS SDK Integration - logPurchase](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L547)
- [Facebook Android SDK Integration - logPurchase](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L440)

### Set Auto Init Enabled

Sets the auto init SDK flag for the application.

| Event Name           | Required           | Optional | Type      |
| ---------------------| ------------------ | -------- | --------- |
| `setautoinitenabled` | `auto_initialized` |          | `Boolean` |

- [Facebook Android SDK Integration - setAutoInitEnabled](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/FacebookSdk.kt#L957)

### Set Auto Log App Events Enabled

Sets the auto logging events flag for the application.

| Event Name                   | Required                       | Optional | Type      |
| -----------------------------| ------------------------------ | -------- | --------- |
| `setautologappeventsenabled` | `auto_log`(android)            |          | `Boolean` |

- [Facebook iOS SDK Integration - setAutoLogAppEventsEnabled](https://github.com/facebook/facebook-ios-sdk/blob/ae94c9c7489fd8b080a965d9551758eadf419a06/FBSDKCoreKit/FBSDKCoreKit/Settings.swift#L83)
- [Facebook Android SDK Integration - setAutoLogAppEventsEnabled](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/FacebookSdk.kt#L981)

### Set Flush Behavior

Sets when Facebook SDK should flush app events to the server.

| Event Name        | Required          | Optional | Type   |
| ----------------- | ----------------- | -------- | ------ |
| `setFlushBehavior` | `flush_behavior` |          | `String` |

- [Facebook iOS SDK Integration - setFlushBehavior](https://github.com/facebook/facebook-ios-sdk/blob/ae94c9c7489fd8b080a965d9551758eadf419a06/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.m#L1752)
- [Facebook Android SDK Integration - setFlushBehavior](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L348)

### Set Push Notifications Registration Id (Android)

Additional push notification methods available on Android platform.

| Event Name                  | Required          | Optional | Type     |
| --------------------------- | ----------------- | -------- | -------- |
| `setPushRegistrationId`     | `registration_id` |          | `String` |

Available flush behavior values:
- `auto` - Events are flushed automatically (default)
- `explicit_only` - Events are only flushed when explicitly called

- [Facebook Android SDK Integration - setPushNotificationsRegistrationId](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.kt#L453)

### Set User

Sets custom user data to associate with all app events. All user data is hashed and used to match Facebook users from this instance of an application. The user data is persisted between application instances.

| Event Name | Required | Optional | Type          |
| ---------- | -------- | -------- | ------------- |
| `setUser`    | `user`     |          | `[String: Any]` |

| User Dictionary Properties | Optional |
| -------------------------- | -------- |
| `em`                         | `String`   |
| `fn`                         | `String`   |
| `ln`                         | `String`   |
| `dob`                        | `String`   |
| `ge`                         | `String`   |
| `ct`                         | `String`   |
| `st`                         | `String`   |
| `zp`                         | `String`   |
| `country`                    | `String`   |

- [Facebook iOS SDK setUser](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L764)
- [Facebook Android SDK Integration - setUserData](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L674)

### Set User ID

Sets the user ID to associate with all app events. This ID will be used to measure cross-device conversions and for setting up Custom Audiences.

| Event Name  | Required     | Optional | Type     |
| ----------- | ------------ | -------- | -------- |
| `setUserId` | `fb_user_id` |          | `String` |

### Update User Value

Updates a user value for a type/key. All user data is hashed and used to match Facebook users from this instance of an application. The user data is persisted between application instances.

| Event Name      | Required      | Optional | Type   |
| --------------- | ------------- | -------- | ------ |
| `updateUserValue` | `fb_user_value` |          | `String` |
|                 | `fb_user_key`   |          | `String` |

- [Facebook iOS SDK Integration - setUserData](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L803)
- [Facebook Android SDK Integration - updateUserProperties](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L712)

### Log Event

The following are [Facebook Standard Events](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L118) and accept a number of optional [parameters](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195) in the payload.

- `activatedapp`
- `achievedlevel`
- `adclick`
- `adimpression`
- `addedpaymentinfo`
- `addedtocart`
- `addedtowishlist`
- `completedregistration`
- `completedtutorial`
- `contact`
- `customizeproduct`
- `deactivatedapp`
- `donate`
- `findlocation`
- `initiatedcheckout`
- `livestreamingstart`
- `livestreamingstop`
- `livestreamingpause`
- `livestreamingresume`
- `livestreamingerror`
- `livestreamingupdatestatus`
- `productcatalogupdate`
- `pushtokenobtained`
- `rated`
- `schedule`
- `searched`
- `sessioninterruptions`
- `spentcredits`
- `starttrial`
- `submitapplication`
- `subscribe`
- `timebetweensessions`
- `unlockedachievement`
- `viewedcontent`


<blockquote>
Because the Facebook SDK is installed alongside the Tealium SDK, all native Facebook functionality is available.
</blockquote>


Arbitrary parameter dictionary of characteristics. The keys to this dictionary must
be `NSString`'s, and the values are expected to be `NSString` or `NSNumber`.  Limitations on the number of
parameters and name construction are given in the [FBSDKAppEvents](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L118s) documentation. Commonly used parameter names
are provided in [FBSDKAppEventParameterName](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195) constants.

| Event Name                          | Required                                           | Optional                                                                                                                                                                          | Type                                    |
| ----------------------------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
|                                     | `command_name` (one of the event names listed above) |                                                                                                                                                                                   |                                         |
| Any of the event names listed above |                                                    | [See parameters list](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195) | Multiple                                |
|                                     |                                                    | `fb_value_to_sum`                                                                                                                                                                   | `Double/Decimal` (iOS) / `Double` (Android) |

- [Facebook iOS SDK Integration - logEvent](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L456)
- [Facebook Android SDK Integration - logEvent](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L362)