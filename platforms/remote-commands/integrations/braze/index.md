---
title: Remote Command: Braze
description: Tealium remote command integration for Braze on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/braze/
---
## Requirements

* Braze API key
* One of the following mobile libraries:
  * [Tealium for Android-Kotlin](https://docs.tealium.com/platforms/android-kotlin/) (1.0.0+)
  * [Tealium for Android-Java](https://docs.tealium.com/platforms/android-java/) (5.9.0+ for Braze 1.0.0+ or <5.9.0 for previous versions)
  * [Tealium for iOS-Swift](https://docs.tealium.com/platforms/ios-swift/) (2.8.0+)
* One of the following remote command integrations:
  * [Braze Remote Command JSON File](https://docs.tealium.com/platforms/remote-commands/integrations/braze/#json-template) (Requires Android-Kotlin 1.0.0+ or iOS-Swift 2.1.0+)
  * Braze Remote Command tag in Tealium iQ Tag Management

## How It Works

The Braze integration uses the following items:

1. The Braze native SDK.
2. The remote commands module that wraps the Braze methods.
3. Either the JSON configuration file or the Remote Command tag that translates event tracking into native Braze calls.

Adding the Braze remote command module to your app automatically installs and builds the required Braze libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Braze SDK separately.

There are two remote command options: a JSON configuration file or using iQ Tag Management to configure the mappings. Using a JSON configuration file is recommended for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-integrations).


## Install

### Dependency Manager




1. In your Xcode project, select **File > Add Packages... > Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-braze-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumBraze` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumBraze` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs the `TealiumBraze` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumBraze` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General > Frameworks, Libraries & Embedded Content** and select the `TealiumBraze` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod "BrazeKit"` if they exist in your Podfile. The dependency for `tealium-swift` is already included in the `TealiumBraze` framework.

2. Add the following dependency to your Podfile:  
      ```ruby
      pod "TealiumBraze"
      ```  
      The `TealiumBraze` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      ```

3. Import the `TealiumSwift` and `TealiumBraze` modules in your `TealiumHelper` file, and any other files that access the `Tealium` class or the Braze remote command.





1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumBraze` framework.

2.  Add the following dependency to your Cartfile:  
      ```bash
      github "tealium/tealium-ios-braze-remote-command"
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

2. Import both the Braze SDK and Tealium-Braze remote commands by adding the following dependencies in your app project's `build.gradle` file:  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:braze:3.0.0'
            implementation 'com.braze:android-sdk-ui:29.0.1'
      }
      ```



1. Navigate to the root of your React Native project.

2. Download and install the `tealium-react-braze` package with the following command:  
    ```bash
    yarn add tealium-react-braze
    ```
3. React Native Autolinking is enabled in version 1.0.7 of the NPM package and is no longer needed to run `react-native link` if using version 0.60+ of React Native.



### Manual Installation




The manual installation for Braze remote commands requires the [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/) library to be installed. To install the Braze remote commands for your iOS project:

1. Install the [Braze SDK](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/initial_sdk_setup/initial_sdk_setup/), if you haven't already done so.

2. Clone the [Tealium iOS Braze remote command](https://github.com/tealium/tealium-ios-braze-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Set the [`remoteAPIEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`




The manual installation for Braze remote commands requires [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) to be installed.

To install the Braze remote commands for your Android project:

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

2. Add `tealium-braze.aar` to `<PROJECT_ROOT>/<MODULE>/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:

      ```groovy
      dependencies {
            implementation(name:'tealium-braze', ext:'aar')
      }
      ```




## Initialize



Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium’s iOS (Swift) library:  
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
    let braze = BrazeRemoteCommand(brazeLocation: BrazeLocationProvider()) 

    // Local JSON
    //let braze = BrazeRemoteCommand(type: .local(file: "braze"), brazeLocation: BrazeLocationProvider()) 

    // Remote JSON
    //let braze = BrazeRemoteCommand(type: .remote(url: "https://some.domain.com/braze.json"), brazeLocation: BrazeLocationProvider()) 

    remoteCommands.add(braze)
}
```


Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's Kotlin library:
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
// New code to add the Braze Remote Command
val braze = BrazeRemoteCommand(application,
                            true,
                            sessionHandlingBlacklist,
                            true,
                            inAppMessageBlacklist)

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Optional: Set config options that may not be supported yet by the Tag in Tealium IQ
    //              or simply to override settings locally.
    braze.registerConfigOverride { builder ->
        // builder.setIsLocationCollectionEnabled(true);
        // builder.setGeofencesEnabled(true);
        // builder.setPushDeepLinkBackStackActivityEnabled(true);
        // builder.setPushDeepLinkBackStackActivityClass(UserActivity.class);
    }

    // register the command

    // Webview Tag
    remoteCommands?.add(braze); 

    // Local JSON
    //remoteCommands?.add(braze, filename = "braze.json"); 

    // Remote JSON
    //remoteCommands?.add(braze, remoteUrl = "https://some.domain.com/braze.json"); 
}
```


Initialize remote commands with the Remote Command tag for Tealium's Android (Java) library:  
```java
import com.tealium.remotecommands.BrazeRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

BrazeRemoteCommand braze;
// Initialize with default configuration options.
braze = new BrazeRemoteCommand(config);

// Or alternatively initialize with some additional config options:
Set<Class> sessionHandlingBlacklist = new HashSet<>();
Set<Class> inAppMessageBlacklist = new HashSet<>();
// sessionHandlingBlacklist.add(MainActivity.class);
// inAppMessageBlacklist.add(UserActivity.class);
braze = new BrazeRemoteCommand(config,
        true,                     // sessiongHandlingEnabled
        sessionHandlingBlacklist, // sessionHandlingBlacklist
        true,                     // registerInAppMessageManager
        inAppMessageBlacklist);   // inAppMessageBlackList

// Optional: Set config options that may not be supported yet by the Tag in Tealium IQ
//              or simply to override settings locally.
braze.registerConfigOverride(new BrazeRemoteCommand.ConfigOverrider() {
    @Override
    public void onOverride(AppboyConfig.Builder b) {
        b.setPushDeepLinkBackStackActivityEnabled(true);
        b.setPushDeepLinkBackStackActivityClass(UserActivity.class);
    }
});

// register the command
teal.addRemoteCommand(braze);
```

 

Initialize remote commands with a JSON configuration file or the Remote Command tag for React Native:
```javascript
import BrazeRemoteCommand from 'tealium-react-braze';
BrazeRemoteCommand.initialize();

// Webview Tag
let braze = { id: BrazeRemoteCommand.name } 

// Local JSON
//let braze = { id: BrazeRemoteCommand.name, path: "braze.json" } 

// Remote JSON
//let braze = { id: BrazeRemoteCommand.name, url: "https://some.domain.com/braze.json" } 

let config = TealiumConfig {
    // ...
    remoteCommands: [braze]
}
```





## JSON Template

If you are configuring remote commands using a [JSON configuration file](https://docs.tealium.com/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
    "config": {
        "api_key": "YOUR_API_KEY",
        "custom_endpoint": "sdk.iad-01.braze.com",
        "session_timeout": 30,
        "trigger_interval_seconds": 100,
        "enable_geofences": true,
        "enable_automatic_geofences": true,
        "enable_automatic_location": true,
        "push_story_identifier": "YOUR_IDENTIFIER",
        "use_uuid_as_device_id": true,
        "forward_universal_links": true
    },
    "mappings": {
        "customer_id": "user_id",
        "customer_first_name": "first_name",
        "customer_last_name": "last_name",
        "customer_gender": "gender",
        "customer_language": "language",
        "customer_email": "email",
        "customer_home_city": "home_city",
        "customer_dob": "date_of_birth",
        "customer_alias": "user_alias",
        "customer_alias_label": "alias_label",
        "pet": "set_custom_attribute.pet",
        "pet_count": "set_custom_attribute.pet_count",
        "pet_count_unset": "unset_custom_attribute.pet_count_unset",
        "pet_count_increment": "increment_custom_attribute.pet_count_increment",
        "pet_names": "set_custom_array_attribute.pet_names",
        "pet_names_append": "append_custom_array_attribute.pet_names_append",
        "pet_names_remove": "remove_custom_array_attribute.pet_names_remove",
        "screen_name": "screen_name",
        "email_notification": "email_notification",
        "push_notification": "push_notification",
        "event_name": "event_name",
        "current_level": "event.current_level",
        "start_date": "event.start_date",
        "high_score": "event.high_score",
        "product_id": "product_id",
        "product_quantity": "product_qty",
        "product_unit_price": "product_unit_price",
        "currency_code": "product_currency",
        "rewards_member": "purchase.rewards_member",
        "rewards_points_earned": "purchase.rewards_points_earned",
        "date_joined_program": "purchase.date_joined_program",
        "latitude": "location_latitude",
        "longitude": "location_longitude",
        "horizontal_accuracy": "location_horizontal_accuracy",
        "vertical_accuracy": "location_vertical_accuracy"
    },
    "commands": {
        "launch": "initialize",
        "setengagement": "emailnotification,pushnotification",
        "log_custom_event": "logcustomevent",
        "set_location": "setlastknownlocation",
        "custom_attribute": "setcustomattribute",
        "unset_custom_attribute": "unsetcustomattribute",
        "custom_array_attribute": "appendcustomarrayattribute",
        "append_custom_array_attribute": "appendcustomarrayattribute",
        "remove_custom_array_attribute": "removecustomarrayattribute",
        "increment_custom_attribute": "incrementcustomattribute",
        "log_purchase": "logpurchase",
        "user_attribute": "userattribute,useridentifier,useralias",
        "user_login": "useridentifier,useralias",
        "user_alias": "useralias",
    }
}
```

## Supported Methods

We map a command to each Braze method. To trigger a Braze method, pass the corresponding command in the specified format.

|Remote Command|Braze Method|
|--------------|------------|
| `addtosubscriptiongroup` | `user.addToSubscriptionGroup(id:)` |
| `appendcustomarrayattribute` | `user.addToCustomAttributeArray()` |
| `emailnotification` | `user.set(emailSubscriptionState:)` |
| `enablesdk` | `enabled = true/false` |
| `flush`| `requestImmediateDataFlush()` |
| `incrementcustomattribute` | `user.incrementCustomUserAttribute()` |
| `initialize` | `Braze(configuration:)` |
| `logcustomevent` | `logCustomEvent()` |
| `logpurchase` | `logPurchase()` |
| `pushnotification` | `user.set(pushNotificationSubscriptionState:)` |
| `removefromsubscriptiongroup` | `user.removeFromSubscriptionGroup(id:)` |
| `removecustomarrayattribute` | `user.removeFromCustomAttributeArray()` |
| `setadtrackingenabled` | `set(adTrackingEnabled:)` |
| `setcustomattribute` | `user.setCustomAttribute())` |
| `setcustomarrayattribute` | `user.setCustomAttributeArray()` |
| `setlastknownlocation` | `user.setLastKnownLocation()` |
| `setsdkauthsignature`| `set(sdkAuthenticationSignature:)` |
| `useralias` | `user.add(alias:)` |
| `unsetcustomattribute` | `user.unsetCustomAttribute()` |
| `userattribute` | `user.set()` |
| `useridentifier` | `changeUser()` |
| `wipedata` | `wipeData()` |



<blockquote>
Since the Braze SDK is installed alongside the Tealium SDK, trigger any native Braze functionality given the corresponding tag configuration.
</blockquote>


### SDK Setup

#### Initialize

The Braze API key and the custom endpoint are required and need to be set in the tag configuration.

| Remote Command | Braze Method (iOS) | Braze Method (Android) |
|---|---|---|
| `initialize` | `Braze(configuration:)` | `configure()` |

The following mappings are used to set launch options.

| Parameter | Type | Description |
|---|---|---|
| `api_key` (required) |  `String` | Sets the API Key |
| `custom_endpoint` (required) |  `String` | Sets a custom API endpoint. This gets sent in the format `sdk.api.braze.eu` |
| `device_options` |  `[String]` | A whitelist for device fields that are collected by the Braze SDK (by default, all fields are collected). |
| `enable_automatic_geofences` | `Bool` | Enable automatic collection of geofences (`true` or `false`).  |
| `enable_automatic_location` | `Bool` | Enable collection of location (`true` or `false`).  |
| `enable_geofences` | `Bool` | Enable collection of geofences (`true` or `false`).  |
| `flush_interval` |  `Double` | Sets the data flush interval (in seconds). Values are converted into NSTimeIntervals and must be greater than `1.0`. |
| `is_sdk_authentication_enabled` | `Bool` | Enable SDK authentication, default is `false`. |
| `push_story_identifier` |  `String` | This key is set to a string value representing the app group name for the Push Story Notification Content extension. |
| `request_processing_policy` |  `String` | Possible values for the SDKs request processing (`manual` or `automatic`). Default is `automatic`. |
| `session_timeout` |  `Int` (seconds) | The session timeout in seconds (default is `30` seconds). |
| `trigger_interval_seconds` | `Int` (seconds) | Override the minimum interval between in-app message triggers (default is `30` seconds). |
| `use_uuid_as_device_id` | `Bool` | (iOS) Determines if a randomly generated UUID should be used as the device ID (default is `true`). |
| `forward_universal_links` | `Bool` | Specifies if the SDK should automatically recognize and forward universal links to the system methods (default is `false`). |

Android  

- [Braze Developer Guide: Initial SDK Setup](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/initial_sdk_setup/android_sdk_integration/)

iOS  

- [Braze Developer Guide: Initial SDK Setup](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/initial_sdk_setup/#customizing-braze-on-startup)   
- [Braze Developer Guide: Fine Network Traffic Control](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/advanced_use_cases/fine_network_traffic_control/)  
- [Braze Developer Guide: Locations and Geofences](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/advanced_use_cases/locations_and_geofences/)  
- [Braze Developer Guide: Push Story Setup](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/push_story/)  
- [Braze Developer Guide: Tracking Sessions](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/tracking_sessions/)


#### Set SDK Auth Signature

| Remote Command | Braze Method (iOS) | Braze Method (Android)
|---|---|---|
| `setsdkauthsignature`| `set(sdkAuthenticationSignature:)` | `setSdkAuthenticationSignature` |

| Parameter | Type |
|---|---|
| `sdk_authentication_signature` | `String` |

#### Flush

| Remote Command | Braze Method |
|---|---|
| `flush`| `requestImmediateDataFlush` |


- Braze Developer Guide: Analytics Disabling  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/advanced_use_cases/fine_network_traffic_control/)
### User Tracking

#### Assigning a User ID

| Remote Command | Braze Method |
|---|---|
| `useridentifier`  | `changeUser` |

| Parameter | Type |
|---|---|
| `user_id` (required) | `String` |
| `sdk_authentication_signature` | `String` |


- Braze Developer Guide: Analytics User IDs  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_user_ids/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_user_ids/#assigning-a-user-id)

#### Aliasing Users

| Remote Command | Braze Method |
|---|---|
| `useralias` | `user.add(alias:)` |

| Parameter | Type |
|----|---|
| `user_alias` (required) | `String` |
| `alias_label` (required) | `String` |

- Braze Developer Guide: Analytics Alias Users     
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_user_ids/#aliasing-users)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_user_ids/#aliasing-users)

### User Attributes

#### Standard Attributes

| Event | Braze Method |
|---|---|
| userattribute  | Set fields on the `Braze.User` object |

|  Parameter | Type |
|---|---|
| `first_name` | `String` |
| `last_name` | `String` |
| `email` | `String` |
| `date_of_birth` | `String` |
| `country` | `String` |
| `language` | `String` |
| `home_city` | `String` |
| `phone` | `String` |
| `gender` | `String` |

- Braze Developer Guide: Analytics User Attributes
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#assigning-standard-user-attributes)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-standard-user-attributes)
- [Braze Developer Guide: User Data API](https://www.braze.com/docs/api/endpoints/user_data/?redirected=true#user-attributes-object-specification)

#### Set Custom Attribute

| Remote Command | Braze Method |
|---|---|
| `setcustomattribute` | `user.setCustomAttribute` |


| Parameter | Type |
|---|---|
| `set_custom_attribute.PROPERTY` | `[String: Any]` / `JSONObject` |

- Braze Developer Guide: Analytics Custom Attributes  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#assigning-custom-user-attributes)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### Unset Custom Attribute

| Remote Command | Braze Method |
|---|---|
| `setcustomattribute` | `user.unsetCustomAttribute` |

| Parameter | Type |
|---|---|
| `set_custom_attribute.PROPERTY` | `String` |

- Braze Developer Guide: Analytics Custom Attributes  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#unsetting-a-custom-attribute)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### Increment Custom Attribute

| Remote Command | Braze Method |
|---|---|
| `incrementcustomattribute` | `user.incrementCustomUserAttribute`|

| Parameter | Type |
|---|---|
| `increment_custom_attribute.PROPERTY` | `String` |

- Braze Developer Guide: Analytics Incrementing Attributes
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#incrementingdecrementing-custom-attributes)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### Set Custom Array Attribute

| Remote Command | Braze Method |
|---|---|
| `setcustomarrayattribute` | `user.setCustomAttributeArray` |

| Parameter | Type |
|---|---|
| `set_custom_array_attribute.PROPERTY` | `[String: [Any]]` / `JSONObject` |

- Braze Developer Guide: Analytics Array Attributes  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#custom-attribute-with-an-array-value)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### Append Custom Array Attribute

| Remote Command | Braze Method |
|---|---|
| `appendcustomarrayattribute` | `user.addToCustomAttributeArray` |

| Parameter | Type |
|---|---|
| `append_custom_array_attribute.PROPERTY` | `[String: String]` / `JSONObject` |

- Braze Developer Guide: Analytics Array Attributes  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#custom-attribute-with-an-array-value)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### Remove Custom Array Attribute

| Remote Command | Braze Method |
|---|---|
| `removecustomarrayattribute`| `user.removeFromCustomAttributeArray`|

| Parameter | Type |
|---|---|
| `remove_custom_array_attribute.PROPERTY` | `[String: String]` / `JSONObject` |

- Braze Developer Guide: Analytics Array Attributes  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#custom-attribute-with-an-array-value)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

### Custom Event Tracking

#### Custom Event

| Remote Command | Braze Method |
| --- | --- |
| `logcustomevent`  | `logCustomEvent` |

| Parameter | Type |
|--- | --- |
|  `event_name` (required) | `String` |
|  `event_properties` | `[String: Any]` / `JSONObject` |

- Braze Developer Guide: Analytics Custom Events
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/tracking_custom_events/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/tracking_custom_events/)

### Notifications

#### Email Notifications

| Remote Command | Braze Method |
|---|---|
| `emailnotification` | `setEmailNotificationSubscriptionType` |

| Parameter | Type | Example |
|---|---|---|
| `email_notification` | `String`| [`"optedin"`, `"subscribed"`, `"unsubscribed"`]|

- Braze Developer Guide: Analytics Email Subscriptions   
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#setting-email-subscriptions)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#setting-up-user-subscriptions)

#### Add to subscription group

| Remote Command | Braze Method |
|---|---|
| `addtosubscriptiongroup` | `user.addToSubscriptionGroup(id:)` |

| Parameter | Type |
|---|---|
| `subscription_group_id` (required) | `String` |

- [Braze Developer Guide: Subscription Groups](https://www.braze.com/docs/user_guide/message_building_by_channel/email/managing_user_subscriptions/#updating-email-subscription-states)

#### Remove from subscription group

| Remote Command | Braze Method |
|---|---|
| `removefromsubscriptiongroup` | `user.removeFromSubscriptionGroup(id:)` |

| Parameter | Type |
|---|---|
| `subscription_group_id` (required) | `String` |

- [Braze Developer Guide: Subscription Groups](https://www.braze.com/docs/user_guide/message_building_by_channel/email/managing_user_subscriptions/#updating-email-subscription-states)

#### Push Notifications

| Remote Command | Braze Method |
|---|---|
| `pushnotification` | `setPushNotificationSubscriptionType` |

| Parameter | Type | Example |
|---|---|---|
| `push_notification` | `String`| [`"optedin"`, `"subscribed"`, `"unsubscribed"`]|


- Braze Developer Guide: Analytics Push Notifications  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#setting-up-user-subscriptions)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#setting-up-user-subscriptions)

### Purchase Tracking

#### Log Purchase

| Remote Command | Braze Method |
|--- | ---|
| `logpurchase` | `logPurchase`|

| Parameter | Type |
|---|---|
| `product_id` (required)| `[String]` / `String[]` |
| `product_currency` (required) | `String` / `String` |
| `price` (required) | `[Double]` / `Double[]`|
| `product_qty`  | `[Int]` / `Int[]` |
| `purchase_properties` | `[AnyHashable: Any]` / `JSONObject` |


- Braze Developer Guide: Analytics Purchase Events  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/logging_purchases/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/logging_purchases/)

### Location Tracking

#### Set User's Last Known Location

| Remote Command | Braze Method |
|---|---|
| `setlastknownlocation` | `user.setLastKnownLocation` |

| Parameter | Type |
|---|---|
| `latitude` (required) | `Double` |
| `longitude` (required) | `Double` |
| `horizontalAccuracy` (required) | `Double` |
| `altitude`  | `Double` |
| `verticalAccuracy` | `Double` |


- [Braze Developer Guide: Analytics Location Tracking](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/location_tracking/#enabling-automatic-location-tracking)


### Data Privacy (Consent Options)

#### Enable SDK

| Remote Command | Braze Method (iOS) | Braze Method (Android) |
|---|---|---|
| `enablesdk` | `enabled` | `enableSdk` |

- Braze Developer Guide: Analytics Disabling  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/disabling_tracking/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/disabling_tracking/)

#### Disable SDK

| Remote Command | Braze Method (iOS) | Braze Method (Android) |
|---|---|---|
| `disablesdk` | `enabled` | `disableSdk` |

- Braze Developer Guide: Analytics Disabling  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/disabling_tracking/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/disabling_tracking/)

#### Wipe Data

| Remote Command | Braze Method |
|---|---|
|  `wipedata`| `wipeData` |


- Braze Developer Guide: Analytics Disabling  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/disabling_tracking/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/disabling_tracking/)

#### Set Ad Tracking Enabled

| Remote Command | Braze Method |
|---|---|
| `setadtrackingenabled` | `set(adTrackingEnabled:)` |

| Parameter | Type |
|---|---|
| `ad_tracking_enabled` (required)| `Bool` |

## Accessing the Braze instance (iOS)

The remote command offers a convenient way to map some of the functionality offered by Braze into your app, such as logging of events and purchases. 
However, some Braze features, such as content cards, feature flags, or notifications, have to be integrated into your app using the Braze instance.

To access the Braze instance directly, use the `onReady` method. The `onReady` method returns the Braze instance in the completion block once it's properly configured.

```swift
brazeRemoteCommand.onReady { braze in
    // use the Braze instance here
}
```

Once you have a reference to the Braze instance, use it as described in the Braze documentation.

### Automatic push integration

The latest Braze version supports a way to automate the processing of remote notifications. For more information, see [Braze Developer Guide: Automatic push integration](https://www.braze.com/docs/developer_guide/platform_integration_guides/swift/push_notifications/integration/#automatic-push-integration).

To use this feature the Braze instance must be initialized synchronously on the main thread in the `didFinishLaunchingWithOptions` method of the app delegate. This means you must configure the Braze instance directly instead of using our remote command configuration.

To configure the Braze instance directly, use this code:

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    let brazeConfig = Braze.Configuration(apiKey: "YOUR_API_KEY", endpoint: "YOUR_ENDPOINT")
    brazeConfig.push.automation = true
    // ...
    // add all your other configuration here
    // ...
    let brazeInstanceWrapper = BrazeInstance()
    brazeInstanceWrapper.initializeBraze(brazeConfig: brazeConfig)
    let brazeCommand = BrazeRemoteCommand(brazeInstance: brazeInstanceWrapper)
    let tealiumConfig = TealiumConfig(...)
    tealiumConfig.remoteCommands = [brazeCommand]
    // ... 
    // complete tealium initialization
    return true
}
```

### Manual push integration

To implement the manual push integration, keep the remote command configuration and enable the push integration directly by accessing the Braze instance.

For more information, see [Braze Developer Guide: Manual push integration](https://www.braze.com/docs/developer_guide/platform_integration_guides/swift/push_notifications/integration/#manual-push-integration).