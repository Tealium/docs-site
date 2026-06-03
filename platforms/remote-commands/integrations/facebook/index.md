---
title: Remote Command: Facebook
description: Tealium remote command integration for Facebook on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/facebook/
---
## Requirements

* One of these mobile libraries:
  * [Tealium for Android (Kotlin)](/platforms/android-kotlin/) (1.0.0&#43;).
  * [Tealium for Android (Java)](/platforms/android-java/) (5.9.0&#43; for Facebook 1.0.0&#43; or &lt;5.9.0 for previous versions).
  * [Tealium for iOS (Swift)](/platforms/ios-swift/).
* One of these remote command integrations:
  * [Facebook Remote Command JSON File](/platforms/remote-commands/integrations/facebook/.#json-template) (Requires Android-Kotlin 1.0.0&#43; or iOS-Swift 2.1.0&#43;).
  * Facebook Remote Command tag in Tealium iQ Tag Management.

The following are requirements for iOS and Android:  




Add the following keys to your `app/src/main/res/values/strings.xml` file. Replace `[APP_ID]` with your Facebook App ID and `[CLIENT_TOKEN]` with your Facebook Client Token:
```xml
&lt;string name=&#34;facebook_app_id&#34;&gt;[APP_ID]&lt;/string&gt;
&lt;string name=&#34;fb_login_protocol_scheme&#34;&gt;fb[APP_ID]&lt;/string&gt;
&lt;string name=&#34;facebook_client_token&#34;&gt;[CLIENT_TOKEN]&lt;/string&gt;
```

The following `meta-data` element is required in the `AndroidManifest.xml` file:
```xml
&lt;application android:label=&#34;@string/app_name&#34; ...&gt;
    ...
    &lt;meta-data
      android:name=&#34;com.facebook.sdk.ApplicationId&#34;
      android:value=&#34;@string/facebook_app_id&#34; /&gt;
    &lt;meta-data 
        android:name=&#34;com.facebook.sdk.ClientToken&#34;
        android:value=&#34;@string/facebook_client_token&#34; /&gt;
    ...
&lt;/application&gt;
```

Learn more: [Facebook Android Getting Started - Integrate the Facebook SDK in Your Android App](https://developers.facebook.com/docs/app-events/getting-started-app-events-android).




Add the following keys to your `Info.plist` file. Replace `[APP_ID]` with your Facebook App ID, `[APP_NAME]` with your app name, and `[CLIENT_TOKEN]` with your Facebook Client Token:  
```xml
&lt;key&gt;CFBundleURLTypes&lt;/key&gt;
&lt;array&gt;
  &lt;dict&gt;
  &lt;key&gt;CFBundleURLSchemes&lt;/key&gt;
  &lt;array&gt;
    &lt;string&gt;fb[APP_ID]&lt;/string&gt;
  &lt;/array&gt;
  &lt;/dict&gt;
&lt;/array&gt;
&lt;key&gt;FacebookAppID&lt;/key&gt;
&lt;string&gt;[APP_ID]&lt;/string&gt;
&lt;key&gt;FacebookDisplayName&lt;/key&gt;
&lt;string&gt;[APP_NAME]&lt;/string&gt;
&lt;key&gt;FacebookClientToken&lt;/key&gt;
&lt;string&gt;[CLIENT_TOKEN]&lt;/string&gt;
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
            options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -&gt; Bool {
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

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-facebook-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumFacebook` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumFacebook` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumFacebook` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumFacebook` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and  select the `TealiumFacebook` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod &#34;FBSDKCoreKit&#34;` if they already exist your Podfile. The dependency for `tealium-swift` is already included in the `TealiumFacebook` framework.

2. Add the following dependency to your Podfile:
      ```ruby
      pod &#34;TealiumFacebook&#34;
      ```
      The `TealiumFacebook` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      &#39;tealium-swift/TagManagement&#39;
      ```

3. Import the modules `TealiumSwift` and `TealiumFacebook` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Facebook Remote Command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumFacebook` framework.

2. Remove the following line if it exists in your Cartfile:  
      ```bash
      github &#34;facebook/facebook-ios-sdk&#34;
      ```

3.  Add the following dependency to your Cartfile:  
      ```bash
      github &#34;tealium/tealium-ios-facebook-remote-command&#34;
      ```

Tealium for Swift SDK (version 2.12&#43;) is required for the latest Facebook Remote Command integration.





1. Install [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) and add the Tealium Maven URL to your project&#39;s top-level `build.gradle` file, if you haven&#39;t done so already.


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

2. Import both the Facebook SDK and Tealium-Facebook remote command by adding the following dependencies in your app project&#39;s `build.gradle` file:  
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:facebook:3.0.0&#39;
      }
      ```




### Manual Installation




The manual installation for Facebook remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the Facebook remote commands for your iOS project:

1. Install the [Facebook SDK](https://github.com/facebook/facebook-ios-sdk/tree/master/FBSDKCoreKit), if you haven&#39;t already done so.

2. Clone the [Tealium iOS Facebook remote command](https://github.com/tealium/tealium-ios-facebook-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Add `Dispatchers.RemoteCommands` as a dispatcher.

4. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true.`




The manual installation for Facebook remote commands requires [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) to be installed.

To install the Facebook remote commands for your Android project:

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

2. Add `tealium-facebook.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:  
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-facebook&#39;, ext:&#39;aar&#39;)
      }
      ```



## Initialize

For all Tealium libraries, register the Facebook Remote Command when you initialize.





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
    let facebook = FacebookRemoteCommand(launchOptions: launchOptions) 

    // Local JSON
    //let facebook = FacebookRemoteCommand(type: .local(file: &#34;facebook&#34;), launchOptions: launchOptions) 

    // Remote JSON
    //let facebook = FacebookRemoteCommand(type: .remote(url: &#34;https://some.domain.com/facebook.json&#34;), launchOptions: launchOptions) 

    remoteCommands.add(facebook)
}
```



Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s Kotlin library:
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val facebook = FacebookRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Webview Tag
    remoteCommands?.add(facebook); 

    // Local JSON
    //remoteCommands?.add(facebook, filename = &#34;facebook.json&#34;); 

    // Remote JSON
    //remoteCommands?.add(facebook, remoteUrl = &#34;https://some.domain.com/facebook.json&#34;); 
}
```



Initialize remote commands with the Remote Command tag for Tealium&#39;s Android (Java) library:   
```java
import com.tealium.remotecommands.facebook.FacebookRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

FacebookRemoteCommand facebook = new FacebookRemoteCommand(this);

// register the command
teal.addRemoteCommand(facebook);
```




## JSON Template

If you are configuring remote commands using a [JSON configuration file](/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
  &#34;config&#34;: {
    &#34;applicationid&#34;: &#34;YOUR_APP_ID&#34;,
    &#34;clienttoken&#34;: &#34;YOUR_CLIENT_TOKEN&#34;,
    &#34;accesstoken&#34;: &#34;YOUR_ACCESS_TOKEN&#34;,
    &#34;userid&#34;: &#34;YOUR_USER_ID&#34;,
    &#34;auto_log&#34;: true,
    &#34;auto_log_events_enabled&#34;: true,
    &#34;auto_initialized&#34;: true,
    &#34;advertiser_id_collection_enabled&#34;: true,
    &#34;advertiser_collection&#34;: true,
    &#34;debug&#34;: true
  },
  &#34;mappings&#34;: {
    &#34;achievement_type&#34;: &#34;event.fb_description&#34;,
    &#34;ad_type&#34;: &#34;event.ad_type&#34;,
    &#34;content&#34;: &#34;event.fb_content&#34;,
    &#34;content_type&#34;: &#34;event.fb_content_type&#34;,
    &#34;currency_code&#34;: &#34;event.fb_currency&#34;,
    &#34;event_name&#34;: &#34;event.fb_description&#34;,
    &#34;current_level&#34;: &#34;event.fb_level&#34;,
    &#34;pet_count&#34;: &#34;event.fb_max_rating_value&#34;,
    &#34;number_of_items&#34;: &#34;event.fb_num_items&#34;,
    &#34;order_id&#34;: &#34;event.fb_order_id&#34;,
    &#34;payment_info_available&#34;: &#34;event.fb_payment_info_available&#34;,
    &#34;signup_method&#34;: &#34;event.fb_registration_method&#34;,
    &#34;search_keyword&#34;: &#34;event.fb_search_string&#34;,
    &#34;success&#34;: &#34;event.fb_success&#34;,
    &#34;customer_email&#34;: &#34;user.em&#34;,
    &#34;customer_first_name&#34;: &#34;user.fn&#34;,
    &#34;customer_last_name&#34;: &#34;user.ln&#34;,
    &#34;customer_phone&#34;: &#34;user.ph&#34;,
    &#34;customer_dob&#34;: &#34;user.dob&#34;,
    &#34;customer_gender&#34;: &#34;user.ge&#34;,
    &#34;customer_city&#34;: &#34;user.ct&#34;,
    &#34;customer_state&#34;: &#34;user.st&#34;,
    &#34;customer_zip&#34;: &#34;user.zp&#34;,
    &#34;customer_country&#34;: &#34;user.country&#34;,
    &#34;customer_id&#34;: &#34;fb_user_id&#34;,
    &#34;user_value&#34;: &#34;fb_user_value&#34;,
    &#34;user_key&#34;: &#34;fb_user_key&#34;,
    &#34;product_id&#34;: &#34;product.fb_product_item_id,event.fb_content_id&#34;,
    &#34;product_availability&#34;: &#34;product.fb_product_availability&#34;,
    &#34;product_condition&#34;: &#34;product.fb_product_condition&#34;,
    &#34;product_description&#34;: &#34;product.fb_product_description,event.fb_product_description&#34;,
    &#34;product_image_link&#34;: &#34;product.fb_product_image_link&#34;,
    &#34;product_link&#34;: &#34;product.fb_product_link&#34;,
    &#34;product_name&#34;: &#34;product.fb_product_title&#34;,
    &#34;product_variant&#34;: &#34;product.fb_product_gtin&#34;,
    &#34;product_brand&#34;: &#34;product.fb_product_brand&#34;,
    &#34;product_price&#34;: &#34;product.fb_product_price_amount,event.fb_value_to_sum&#34;,
    &#34;product_currency&#34;: &#34;product.fb_product_price_currency&#34;,
    &#34;product_alias&#34;: &#34;product_parameters.product_alias&#34;,
    &#34;product_color&#34;: &#34;product_parameters.product_color&#34;,
    &#34;order_total&#34;: &#34;purchase.fb_purchase_amount&#34;,
    &#34;order_currency&#34;: &#34;purchase.fb_purchase_currency&#34;,
    &#34;customer_status&#34;: &#34;purchase_parameters.customer_status&#34;,
    &#34;coupon&#34;: &#34;purchase_parameters.coupon&#34;,
    &#34;push_action&#34;: &#34;push.fb_push_action&#34;,
    &#34;push_payload&#34;: &#34;push.fb_push_payload&#34;,
    &#34;tealium_event&#34;: &#34;command_name&#34;
  },
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;initialize,setautologappeventsenabled,setautoinitenabled,enableadvertiseridcollection&#34;,
    &#34;user_login&#34;: &#34;setuser,setuserid&#34;,
    &#34;email_signup&#34;: &#34;updateuservalue&#34;,
    &#34;level_up&#34;: &#34;achievedlevel&#34;,
    &#34;user_register&#34;: &#34;completedregistration&#34;,
    &#34;unlock_achievement&#34;: &#34;unlockedachievement&#34;,
    &#34;cart_add&#34;: &#34;addedtocart&#34;,
    &#34;custom_attribute&#34;: &#34;rated&#34;,
    &#34;wishlist_add&#34;: &#34;addedtowishlist&#34;,
    &#34;payment&#34;: &#34;initiatedcheckout&#34;,
    &#34;product&#34;: &#34;logproductitem&#34;,
    &#34;order&#34;: &#34;logpurchase&#34;,
    &#34;flush&#34;: &#34;flush&#34;,
    &#34;customfbevent&#34;: &#34;customfbevent&#34;
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


Since the Facebook SDK is installed alongside the Tealium SDK, you are able to trigger any native Facebook functionality given the corresponding tag configuration.

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

Either `gtin`, `mpn` or `brand` is required. Product parameters are optional fields for deep link specification.

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
 be `NSString`&#39;s, and the values are expected to be `NSString` or `NSNumber`. Limitations on the number of
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

Because the Facebook SDK is installed alongside the Tealium SDK, all native Facebook functionality is available.

Arbitrary parameter dictionary of characteristics. The keys to this dictionary must
be `NSString`&#39;s, and the values are expected to be `NSString` or `NSNumber`.  Limitations on the number of
parameters and name construction are given in the [FBSDKAppEvents](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L118s) documentation. Commonly used parameter names
are provided in [FBSDKAppEventParameterName](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195) constants.

| Event Name                          | Required                                           | Optional                                                                                                                                                                          | Type                                    |
| ----------------------------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
|                                     | `command_name` (one of the event names listed above) |                                                                                                                                                                                   |                                         |
| Any of the event names listed above |                                                    | [See parameters list](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195) | Multiple                                |
|                                     |                                                    | `fb_value_to_sum`                                                                                                                                                                   | `Double/Decimal` (iOS) / `Double` (Android) |

- [Facebook iOS SDK Integration - logEvent](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L456)
- [Facebook Android SDK Integration - logEvent](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L362)