---
title: Remote Command: Firebase
description: Tealium remote command integration for Firebase on Android and Swift/iOS
url: https://docs.tealium.com/platforms/remote-commands/integrations/firebase/
---
## Requirements

* One of the following libraries:
  * [Tealium for Android-Kotlin](https://docs.tealium.com/platforms/android-kotlin/) (1.0.0 and later)
  * [Tealium for Android-Java](https://docs.tealium.com/platforms/android-java/) (5.9.0 or later for Firebase 2.0.0+, or 5.9.0 or earlier for previous versions)
  * [Tealium for iOS-Swift](https://docs.tealium.com/platforms/ios-swift/)
* One of the following remote command integrations:
  * [Firebase Remote Command JSON File](https://docs.tealium.com/platforms/remote-commands/integrations/firebase/#json-template) (Requires Android-Kotlin 1.0.0 and later or iOS-Swift 2.1.0 and later)
  * [Firebase Remote Command tag](https://docs.tealium.com/firebase-remote-command-tag/) in Tealium iQ Tag Management

## How It Works

The Firebase integration uses three items:

1. The Firebase native SDK
1. The remote commands module that wraps the Firebase methods
1. Either the JSON configuration file or Remote Command tag that translates event tracking into native Firebase calls

Adding the Firebase remote command module to your app automatically installs and builds the required Firebase libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Firebase SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If you are using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager





1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumFirebase` framework.

1. Remove the following line if it exists in your Cartfile:  
      ```bash
      binary "https://dl.google.com/dl/firebase/ios/carthage/FirebaseAnalyticsBinary.json"
      ```

1. Add the following dependency to your Cartfile:  
      ```bash
      github "tealium/tealium-ios-firebase-remote-command"
      ```


<blockquote>
The `TealiumFirebase` module cannot be built as an `xcframework` when using the Carthage `--use-xcframeworks` flag because Firebase uses a Carthage binary installation. We recommend using the Carthage official [Xcode 12 workaround](https://github.com/Carthage/Carthage/blob/master/Documentation/Xcode12Workaround.md) to build the dependencies.
</blockquote>






1. Remove the following line if it exists in your Podfile:  
      ```bash
      pod "Firebase/Analytics"
      ```  

1. Add the following dependency to your Podfile:  
      ```swift
      pod "TealiumFirebase"
      ```  
      The `TealiumFirebase` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      ```

1. Import the modules `TealiumSwift` and `TealiumFirebase` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Firebase remote command.





To install the Tealium Firebase library for Cordova, run the following command in your Cordova app project:

```
cordova plugin add tealium-cordova-firebase-plugin
```





To install the Tealium Firebase library for Flutter, run the following commands:

```
flutter pub add tealium_firebase
import 'package:tealium_firebase/tealium_firebase.dart';
```





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

1. Add the following dependency your `build.gradle` file:

      ```groovy
      dependencies {
          implementation 'com.tealium.remotecommands:firebase:1.2.0'
      }
      ```





1. Navigate to the root of your React Native project.

1. Download and install the `tealium-react-firebase` package with the following command:  
    ```bash
    yarn add tealium-react-firebase
    ```
1. React Native Autolinking is enabled in version 1.0.7 of the NPM package and is no longer needed to run `react-native link` if using version 0.60+ of React Native.





1. In your Xcode project, select **File > Add Packages... > Add Package Dependency**.
1. Enter the repository URL: `https://github.com/tealium/tealium-ios-firebase-remote-command`.
1. Configure the version rules. Typically, we recommend `Up to next major`. If the current `TealiumFirebase` version does not appear in the list, then reset your Swift package cache.
1. Select the `TealiumFirebase` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumFirebase` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumFirebase` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
1. In your Xcode project, select the app target under the **TARGETS** section.
1. Navigate to **General > Frameworks, Libraries & Embedded Content** and  select the `TealiumFirebase` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.





Install the Tealium Firebase library for Xamarin directly from Visual Studio using the built-in NuGet package manager.

[NuGet Package: Tealium.RemoteCommands.Firebase.Xamarin](https://www.nuget.org/packages/Tealium.RemoteCommands.Firebase.Xamarin)




### Manual Installation




The manual installation for Firebase remote commands requires the [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/) library to be installed. To install the Firebase remote commands for your iOS project:

1. Install the [Firebase SDK](https://firebase.google.com/docs/ios/setup), if you haven't already done so.

1. Clone the [Tealium iOS Firebase remote command](https://github.com/tealium/tealium-ios-firebase-remote-command) repo and drag the files within the `Sources` folder into your project.

1. Set the [`remoteAPIEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true.`




The manual installation for Firebase remote commands requires [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) to be installed.

To install the Firebase remote commands for your Android project:

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

1. Add `tealium-firebase.aar` to `<PROJECT_ROOT>/<MODULE>/libs`.

1. Add the Tealium library dependency to your `build.gradle` file:

      ```groovy
      dependencies {
            implementation(name:'tealium-firebase', ext:'aar')
      }
      ```




## Initialize

For all Tealium libraries, register the Firebase mobile remote commands when you initialize.





Initialize remote commands with the Remote Command tag for Tealium's Android (Java) library:
```java
RemoteCommand firebase = new FirebaseRemoteCommand(application);
teal.addRemoteCommand(firebase);
```




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's Kotlin library:
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val firebase = FirebaseRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(firebase); 

    // Local JSON
    //remoteCommands?.add(firebase, filename = "firebase.json"); 

    // Remote JSON
    //remoteCommands?.add(firebase, remoteUrl = "https://some.domain.com/firebase.json"); 
}
```






```javascript
    let Environment = tealium.utils.Environment;
    let Dispatchers = tealium.utils.Dispatchers;

    // Webview Tag
    let firebase = window.tealium.remotecommands.firebase.create() 

    // Local JSON
    //let firebase = window.tealium.remotecommands.firebase.create().setPath("firebase.json") 

    // Remote JSON
    //let firebase = window.tealium.remotecommands.firebase.create().setUrl("https://some.domain.com/firebase.json") 
    
    let config = { 
        account: ACCOUNT_NAME, 
        profile: PROFILE_NAME, 
        environment: Environment.dev, 
        dispatchers: [
            Dispatchers.TagManagement, 
            Dispatchers.RemoteCommands
        ],
        remoteCommands: [
            
        ]
    };

    window.tealium.initialize(config, function(success) {
        console.log("Init was: " + success)
    })
```





Add a `Google-Servives.json` or `.plist` file to the platform object with the following contents:

```json
// WebView remote command
var webViewFirebase = RemoteCommand(TealiumFirebase.commandName)

// Local JSON mappings
var localFirebase = RemoteCommand(
  TealiumFirebase.commandName, 
  path: "firebase.json"
)

// Remote JSON mappings
var remoteFirebase = RemoteCommand(
  TealiumFirebase.commandName, 
  url: "https://some.domain.com/firebase.json"
)

var config = TealiumConfig(
  // ...
  remoteCommands: [
    webViewFirebase // or `localFirebase`, or `remoteFirebase`
  ])
```





```javascript
import FirebaseRemoteCommand from 'tealium-react-firebase';
FirebaseRemoteCommand.initialize();

// Webview Tag
let firebase = { id: FirebaseRemoteCommand.name } 

// Local JSON
//let firebase = { id: FirebaseRemoteCommand.name, path: "firebase.json" } 

// Remote JSON
//let firebase = { id: FirebaseRemoteCommand.name, url: "https://some.domain.com/firebase.json" } 
let config = TealiumConfig {
    // ...
    remoteCommands: [firebase]
}
```




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
    let firebase = FirebaseRemoteCommand() 

    // Local JSON
    //let firebase = FirebaseRemoteCommand(type: .local(file: "firebase")) 

    // Remote JSON
    //let firebase = FirebaseRemoteCommand(type: .remote(url: "https://some.domain.com/firebase.json")) 
    
    remoteCommands.add(firebase)
}
```





```csharp

// Webview Tag
var firebase = new FirebaseRemoteCommandDroid(this.Application, null, null); 

// Local JSON
//var firebase = new FirebaseRemoteCommandDroid(this.Application, "firebase.json", null); 

// Remote JSON
//var firebase = new FirebaseRemoteCommandDroid(this.Application, null, "https://some.domain.com/firebase.json"); 

var commands = new List<IRemoteCommand> {
    firebase
};
TealiumConfig config = new TealiumConfig(ACCOUNT_NAME,
                                          PROFILE_NAME,
                                          ENVIRONMENT,
                                          new List<Dispatchers> {
                                              Dispatchers.RemoteCommands, Dispatchers.TagManagement
                                          },
                                          new List<Collectors> {},
                                          remoteCommands: commands
                                          );
```




```csharp

// Webview Tag
var firebase = new FirebaseRemoteCommandIOS(new RemoteCommandTypeWrapper()); 

// Local JSON
//var firebase = new FirebaseRemoteCommandIOS(new RemoteCommandTypeWrapper("firebase", NSBundle.MainBundle));

// Remote JSON
//var firebase = new FirebaseRemoteCommandIOS(new RemoteCommandTypeWrapper("https://some.domain.com/firebase.json")); 

var commands = new List<IRemoteCommand> {
    firebase
};
TealiumConfig config = new TealiumConfig(ACCOUNT_NAME,
                                          PROFILE_NAME,
                                          ENVIRONMENT,
                                          new List<Dispatchers> {
                                              Dispatchers.RemoteCommands, Dispatchers.TagManagement
                                          },
                                          new List<Collectors> {},
                                          remoteCommands: commands
                                          );
```



## JSON Template

If you are configuring remote commands using a [JSON configuration file](https://docs.tealium.com/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
    "config": {
        "firebase_analytics_enabled": "true",
        "firebase_session_timeout_seconds": "30",
        "firebase_log_level": "max",
        "firebase_session_minimum_seconds": "100"
    },
    "mappings": {
        "achievement_id": "event.param_achievement_id",
        "ad_network_click_id": "event.param_ad_network_click_id",
        "affiliation": "event.param_affiliation",
        "campaign_keywords": "event.param_cp1",
        "campaign": "event.param_campaign",
        "game_character": "event.param_character",
        "checkout_option": "event.param_checkout_option",
        "checkout_step": "event.param_checkout_step",
        "content": "event.param_content",
        "content_type": "event.param_content_type",
        "coupon": "event.param_coupon",
        "creative_name": "event.param_creative_name",
        "creative_slot": "event.param_creative_slot",
        "currency_code": "event.param_currency",
        "travel_destination": "event.param_destination",
        "end_date": "event.param_end_date",
        "flight_number": "event.param_flight_number",
        "group_id": "event.param_group_id",
        "current_index": "param_index",
        "product_brand": "items.param_item_brand",
        "product_category": "items.param_item_category",
        "product_id": "items.param_item_id",
        "product_unit_price": "items.param_price",
        "product_quantity": "items.param_quantity",
        "product_list": "items.param_item_list",
        "product_location_id": "items.param_item_location_id",
        "product_name": "items.param_item_name",
        "product_variant": "items.param_item_variant",
        "current_level": "event.param_level",
        "most_recent_location": "event.param_location",
        "campaign_medium": "event.param_medium",
        "number_nights": "event.param_number_nights",
        "number_pax": "event.param_number_pax",
        "number_rooms": "event.param_number_rooms",
        "travel_origin": "event.param_origin",
        "score": "event.param_score",
        "search_keyword": "event.param_search_term",
        "order_shipping_amount": "event.param_shipping",
        "signup_method": "event.param_signup_method",
        "campaign_source": "event.param_source",
        "start_date": "event.param_start_date",
        "order_tax_amount": "event.param_tax",
        "product_term": "event.param_term",
        "order_id": "event.param_transaction_id",
        "travel_class": "event.param_travel_class",
        "order_total": "event.param_value",
        "currency_type": "event.param_virtual_currency_name",
        "user_signup_method": "event.param_user_signup_method",
        "event_title": "firebase_event_name",
        "screen_name": "firebase_screen_name",
        "screen_class": "firebase_screen_class",
        "customer_property": "firebase_property_name",
        "customer_value": "firebase_property_value",
        "customer_id": "firebase_user_id",
        "consent_ad_storage": "firebase_consent_settings.ad_storage",
        "consent_analytics_storage": "firebase_consent_settings.analytics_storage",
        "consent_ad_user_data": "firebase_consent_settings.ad_user_data",
        "consent_ad_personalization": "firebase_consent_settings.ad_personalization"
    },
    "commands": {
        "launch": "config",
        "user_login": "logevent",
        "user_register": "logevent,setuserproperty",
        "share": "logevent",
        "show_offers": "logevent",
        "join_group": "logevent",
        "travel_order": "logevent",
        "earn_currency": "logevent",
        "spend_currency": "logevent",
        "unlock_achievement": "logevent",
        "level_up": "logevent",
        "start_tutorial": "logevent",
        "stop_tutorial": "logevent",
        "record_score": "logevent",
        "category": "logevent,setscreenname",
        "product": "logevent,setscreenname",
        "cart_add": "logevent",
        "wishlist_add": "logevent",
        "checkout": "logevent,setscreenname",
        "checkout_progress": "logevent",
        "email_signup": "logevent",
        "order": "logevent,setscreenname",
        "setconsent": "setconsent",
        "initiateconversionmeasurement": "initiateconversionmeasurement",
        "resetanalyticsdata": "resetdata"
    }
}
```

## Supported Methods

We map a command to each Firebase method. To trigger a Firebase method, pass the corresponding command in the specified format.

|Remote Command|Firebase Method|
|--------------|------------|
| `config` | `configure()` |
| `logevent` | `logEvent(name, parameters)` |
| `setscreenname` | `logEvent(name (AnalyticsEventScreenView), parameters)` |
| `setdefaultparameters` | `setDefaultEventParameters(parameters)` |
| `setuserproperty` | `setUserProperty(value, name)` |
| `setuserid` | `setUserId(id)` |
| `initiateconversionmeasurement` (iOS) |`initiateOnDeviceConversionMeasurement(emailAddress)` |
| `setconsent` | `setConsent(consentSettings)` |
| `resetdata` | `resetAnalyticsData` |

### SDK Set up

### Configure

| Remote Command | Firebase Method |
|---|---|
| `config` | `configure()` |

The following parameters are used to set up the SDK:

| Parameter | Type | Description |
|---|---|---|
| `firebase_session_timeout_seconds` |  `String` | A string representation of the length of the session in seconds. |
| `firebase_analytics_enabled` |  `String` | A string representation of a boolean to enable or disable analytics (default `true`). |
| `firebase_log_level` (iOS) |  `String` | The log level min|max|error|debug|notice|warning|info (default `min`). |

### Track

Events triggered by basic interactions with your app are tracked automatically. For more information, see [GA4: Automatically collected events](https://support.google.com/firebase/answer/6317485?hl=en).

#### Log Event

Log an event with parameters and, optionally, an array of items.

| Remote Command | Firebase Method |
|---|---|
| `logevent` | `logEvent(name, parameters)` |

| Parameter | Type | Description |
|---|---|---|
| `firebase_event_name` |  `String` | (Required) The event name, mapped to a list of Firebase event names. |
| `event` (JSON) |  `[String:Any]` | An object containing all of the parameters for this event, mapped to a list of firebase parameters. |
| `firebase_event_params` (Tag) | `[String:Any]` | An object containing all the parameters for this event (used by the tag), mapped to a list of Firebase parameters. |
| `items` (JSON) |  `[String:[Any]]` | An object contining array of items for this event. All arrays contain the same number of elements, and all elements can be normalized into a single array of items. |
| `param_items` (Tag) | `[[String:Any]]` | An array of items for this event (used by the tag). |

#### Set screen name

This command is a specific log event that is added as a utility.

| Remote Command | Firebase Method (iOS) | Firebase Method (Android) |
|---|---|---|
| `setscreenname` | `logEvent(name (AnalyticsEventScreenView), parameters)` | `setCurrentScreen(currentActivity, screenName, screenClass)` |

| Parameter | Type | Description |
|---|---|---|
| `firebase_screen_name` |  `String` | (Required) The name of the current screen. |
| `firebase_screen_class` |  `String` | The class of the current screen. |

#### Set Default Parameters

This command sets parameters that are sent on every log event.

| Remote Command | Firebase Method |
|---|---|
| `setdefaultparameters` | `setDefaultEventParameters(parameters)` |

| Parameter | Type | Description |
|---|---|---|
| `default` (JSON) |  `[String:Any]` | An object with key-value default parameters. |
| `firebase_default_params` (Tag) |  `String` | An object with key-value default parameters (used by the tag). |

### Mapping

Parameters and events sent in `logEvent` methods are mapped from Tealium values to Firebase constant names.

The following table lists available keys mapped to constants in iOS and Android. If a parameter is missing from Tealium's mapping, you can directly use the Firebase constant value.

#### Events mapping

| Tealium Key | Firebase Event (iOS) | Firebase Event (Android) |
|---|---|---|
| `event_ad_impression` | `AnalyticsEventAdImpression` | `AD_IMPRESSION` |
| `event_add_payment_info` | `AnalyticsEventAddPaymentInfo` | `ADD_PAYMENT_INFO` |
| `event_add_shipping_info` | `AnalyticsEventAddShippingInfo` | `ADD_SHIPPING_INFO` |
| `event_add_to_cart` | `AnalyticsEventAddToCart` | `ADD_TO_CART` |
| `event_add_to_wishlist` | `AnalyticsEventAddToWishlist` | `ADD_TO_WISHLIST` |
| `event_app_open` | `AnalyticsEventAppOpen` | `APP_OPEN` |
| `event_begin_checkout` | `AnalyticsEventBeginCheckout` | `BEGIN_CHECKOUT` |
| `event_campaign_details` | `AnalyticsEventCampaignDetails` | `CAMPAIGN_DETAILS` |
| `event_earn_virtual_currency` | `AnalyticsEventEarnVirtualCurrency` | `EARN_VIRTUAL_CURRENCY` |
| `event_generate_lead` | `AnalyticsEventGenerateLead` | `GENERATE_LEAD` |
| `event_join_group` | `AnalyticsEventJoinGroup` | `JOIN_GROUP` |
| `event_level_end` | `AnalyticsEventLevelEnd` | `LEVEL_END` |
| `event_level_start` | `AnalyticsEventLevelStart` | `LEVEL_START` |
| `event_level_up` | `AnalyticsEventLevelUp` | `LEVEL_UP` |
| `event_login` | `AnalyticsEventLogin` | `LOGIN` |
| `event_post_score` | `AnalyticsEventPostScore` | `POST_SCORE` |
| `event_purchase` | `AnalyticsEventPurchase` | `PURCHASE` |
| `event_refund` | `AnalyticsEventRefund` | `REFUND` |
| `event_remove_cart` | `AnalyticsEventRemoveFromCart` | `REMOVE_FROM_CART` |
| `event_screen_view` | `AnalyticsEventScreenView` | `SCREEN_VIEW` |
| `event_search` | `AnalyticsEventSearch` | `SEARCH` |
| `event_select_content` | `AnalyticsEventSelectContent` | `SELECT_CONTENT` |
| `event_select_item` | `AnalyticsEventSelectItem` | `SELECT_ITEM` |
| `event_select_promotion` | `AnalyticsEventSelectPromotion` | `SELECT_PROMOTION` |
| `event_share` | `AnalyticsEventShare` | `SHARE` |
| `event_signup` | `AnalyticsEventSignUp` | `SIGN_UP` |
| `event_spend_virtual_currency` | `AnalyticsEventSpendVirtualCurrency` | `SPEND_VIRTUAL_CURRENCY` |
| `event_tutorial_begin` | `AnalyticsEventTutorialBegin` | `TUTORIAL_BEGIN` |
| `event_tutorial_complete` | `AnalyticsEventTutorialComplete` | `TUTORIAL_COMPLETE` |
| `event_unlock_achievement` | `AnalyticsEventUnlockAchievement` | `UNLOCK_ACHIEVEMENT` |
| `event_view_cart` | `AnalyticsEventViewCart` | `VIEW_CART` |
| `event_view_item` | `AnalyticsEventViewItem` | `VIEW_ITEM` |
| `event_view_item_list` | `AnalyticsEventViewItemList` | `VIEW_ITEM_LIST` |
| `event_view_promotion` | `AnalyticsEventViewPromotion` | `VIEW_PROMOTION` |
| `event_view_search_results` | `AnalyticsEventViewSearchResults` | `VIEW_SEARCH_RESULTS` |

#### Parameters mapping

| Tealium Key | Firebase Parameter (iOS) | Firebase Parameter (Android) |
|---|---|---|
| `param_achievement_id` | `AnalyticsParameterAchievementID` | `ACHIEVEMENT_ID` |
| `param_ad_format` | `AnalyticsParameterAdFormat` | `AD_FORMAT` |
| `param_ad_network_click_id` | `AnalyticsParameterAdNetworkClickID` | `ACLID` |
| `param_ad_platform` | `AnalyticsParameterAdPlatform` | `AD_PLATFORM` |
| `param_ad_source` | `AnalyticsParameterAdSource` | `AD_SOURCE` |
| `param_ad_unit_name` | `AnalyticsParameterAdUnitName` | `AD_UNIT_NAME` |
| `param_affiliation` | `AnalyticsParameterAffiliation` | `AFFILIATION` |
| `param_cp1` | `AnalyticsParameterCP1` | `CP1` |
| `param_campaign` | `AnalyticsParameterCampaign` | `CAMPAIGN` |
| `param_campaign_id` | `AnalyticsParameterCampaignID` | N/A |
| `param_character` | `AnalyticsParameterCharacter` | `CHARACTER` |
| `param_content` | `AnalyticsParameterContent` | `CONTENT` |
| `param_content_type` | `AnalyticsParameterContentType` | `CONTENT_TYPE` |
| `param_coupon` | `AnalyticsParameterCoupon` | `COUPON` |
| `param_creative_format` | `AnalyticsParameterCreativeFormat` | N/A |
| `param_creative_name` | `AnalyticsParameterCreativeName` | `CREATIVE_NAME` |
| `param_creative_slot` | `AnalyticsParameterCreativeSlot` | `CREATIVE_SLOT` |
| `param_currency` | `AnalyticsParameterCurrency` | `CURRENCY` |
| `param_destination` | `AnalyticsParameterDestination` | `DESTINATION` |
| `param_discount` | `AnalyticsParameterDiscount` | `DISCOUNT` |
| `param_end_date` | `AnalyticsParameterEndDate` | `END_DATE` |
| `param_extend_session` | `AnalyticsParameterExtendSession` | `EXTEND_SESSION` |
| `param_flight_number` | `AnalyticsParameterFlightNumber` | `FLIGHT_NUMBER` |
| `param_group_id` | `AnalyticsParameterGroupID` | `GROUP_ID` |
| `param_index` | `AnalyticsParameterIndex` | `INDEX` |
| `param_item_brand` | `AnalyticsParameterItemBrand` | `ITEM_BRAND` |
| `param_item_category` | `AnalyticsParameterItemCategory` | `ITEM_CATEGORY` |
| `param_item_category2` | `AnalyticsParameterItemCategory2` | `ITEM_CATEGORY2` |
| `param_item_category3` | `AnalyticsParameterItemCategory3` | `ITEM_CATEGORY3` |
| `param_item_category4` | `AnalyticsParameterItemCategory4` | `ITEM_CATEGORY4` |
| `param_item_category5` | `AnalyticsParameterItemCategory5` | `ITEM_CATEGORY5` |
| `param_item_id` | `AnalyticsParameterItemID` | `ITEM_ID` |
| `param_item_list_id` | `AnalyticsParameterItemListID` | `ITEM_LIST_ID` |
| `param_item_list_name` | `AnalyticsParameterItemListName` | `ITEM_LIST_NAME` |
| `param_item_name` | `AnalyticsParameterItemName` | `ITEM_NAME` |
| `param_item_variant` | `AnalyticsParameterItemVariant` | `ITEM_VARIANT` |
| `param_items` | `AnalyticsParameterItems` | `ITEMS` |
| `param_level` | `AnalyticsParameterLevel` | `LEVEL` |
| `param_level_name` | `AnalyticsParameterLevelName` | `LEVEL_NAME` |
| `param_location` | `AnalyticsParameterLocation` | `LOCATION` |
| `param_location_id` | `AnalyticsParameterLocationID` | `LOCATION_ID` |
| `param_marketing_tactic` | `AnalyticsParameterMarketingTactic` | N/A |
| `param_medium` | `AnalyticsParameterMedium` | `MEDIUM` |
| `param_method` | `AnalyticsParameterMethod` | `METHOD` |
| `param_number_nights` | `AnalyticsParameterNumberOfNights` | `NUMBER_OF_NIGHTS` |
| `param_number_pax` | `AnalyticsParameterNumberOfPassengers` | `NUMBER_OF_PASSENGERS` |
| `param_number_rooms` | `AnalyticsParameterNumberOfRooms` | `NUMBER_OF_ROOMS` |
| `param_origin` | `AnalyticsParameterOrigin` | `ORIGIN` |
| `param_payment_type` | `AnalyticsParameterPaymentType` | `PAYMENT_TYPE` |
| `param_price` | `AnalyticsParameterPrice` | `PRICE` |
| `param_promotion_id` | `AnalyticsParameterPromotionID` | `PROMOTION_ID` |
| `param_promotion_name` | `AnalyticsParameterPromotionName` | `PROMOTION_NAME` |
| `param_quantity` | `AnalyticsParameterQuantity` | `QUANTITY` |
| `param_score` | `AnalyticsParameterScore` | `SCORE` |
| `param_search_term` | `AnalyticsParameterSearchTerm` | `SEARCH_TERM` |
| `param_shipping` | `AnalyticsParameterShipping` | `SHIPPING` |
| `param_shipping_tier` | `AnalyticsParameterShippingTier` | `SHIPPING_TIER` |
| `param_screen_name` | `AnalyticsParameterScreenName` | `SCREEN_NAME` |
| `param_screen_class` | `AnalyticsParameterScreenClass` | `SCREEN_CLASS` |
| `param_source` | `AnalyticsParameterSource` | `SOURCE` |
| `param_source_platform` | `AnalyticsParameterSourcePlatform` | N/A |
| `param_start_date` | `AnalyticsParameterStartDate` | `START_DATE` |
| `param_success` | `AnalyticsParameterSuccess` | `SUCCESS` |
| `param_tax` | `AnalyticsParameterTax` | `TAX` |
| `param_term` | `AnalyticsParameterTerm` | `TERM` |
| `param_transaction_id` | `AnalyticsParameterTransactionID` | `TRANSACTION_ID` |
| `param_travel_class` | `AnalyticsParameterTravelClass` | `TRAVEL_CLASS` |
| `param_value` | `AnalyticsParameterValue` | `VALUE` |
| `param_virtual_currency_name` | `AnalyticsParameterVirtualCurrencyName` | `VIRTUAL_CURRENCY_NAME` |
| `param_user_signup_method` | `AnalyticsUserPropertySignUpMethod` | N/A |
| `param_user_allow_ad_personalization_signals` | `AnalyticsUserPropertyAllowAdPersonalizationSignals` | N/A |

### Set User

#### Set User property

This command sets a single or list of user property names and values.

| Remote Command | Firebase Method |
|---|---|
| `setuserproperty` | `setUserProperty(value, name)` |

| Parameter | Type | Description |
|---|---|---|
| `firebase_property_name` |  `String\|[String]` | (Required) The property name or an array of property names |
| `firebase_property_value` |  `String\|[String]]` | (Required) The property value or an array of property values. If this parameter is an array, it must match the `firebase_property_name` array length and item order. |

#### Set User ID

This command sets the user ID.

| Remote Command | Firebase Method |
|---|---|
| `setuserid` | `setUserId(id)` |

| Parameter | Type | Description |
|---|---|---|
| `firebase_user_id`|  `String` | (Required) The user ID to set |

### Conversion Measurement (iOS)

This command initiates Conversion Measurement.

| Remote Command | Firebase Method |
|---|---|
| `initiateconversionmeasurement` | `initiateOnDeviceConversionMeasurement()` |

| Parameter | Type | Description |
|---|---|---|
| `param_hashed_email_address` | `String` | The hashed user email address |
| `param_hashed_phone_number` | `String` | The hashed user phone number |
| `param_email_address` | `String` | The user email address |
| `param_phone_number` | `String` | The user phone number |


<blockquote>
If you are sending the parameter hashed, you need to follow the [Firebase documentation on Measure iOS Ads conversions](https://firebase.google.com/docs/tutorials/ads-ios-on-device-measurement/step-3) to normalize and hash it. Tealium still needs to receive a `String` in the parameter. It will be converted to `Data` as a final step before passing it to `Firebase`.
</blockquote>


### Consent

This command sets consent modes.

| Remote Command | Firebase Method |
|---|---|
| `setconsent` | `setConsent(consentSettings)` |

| Parameter | Type | Description |
|---|---|---|
| `firebase_consent_settings` |  `[String:String]` | (Required) An object containing the consent settings. Keys are consent types, values are `granted` or `denied` |

#### Supported Consent Types

| Consent Type | Minimum Firebase iOS Version | Minimum Firebase Android Version |
|---|---|---|
| `ad_storage`| 10.7.0 | 18.0.0 |
| `analytics_storage` | 10.7.0 | 18.0.0 |
| `ad_personalization`| 10.17.0 | 21.5.0 |
| `ad_user_data` | 10.17.0 | 21.5.0 |

For more information, see [Firebase: Mobile Remote Command Tag setup](https://docs.tealium.com/firebase-remote-command-tag/).

### Reset Analytics Data

Clears all analytics data for this instance from the device and resets the app instance ID.

| Remote Command | Firebase Method |
|---|---|
| `resetdata` | `resetAnalyticsData()` |
