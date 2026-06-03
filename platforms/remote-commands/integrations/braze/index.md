---
title: Remote Command: Braze
description: Tealium remote command integration for Braze on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/braze/
---
## Requirements

* Braze API key
* One of the following mobile libraries:
  * [Tealium for Android-Kotlin](/platforms/android-kotlin/) (1.0.0&#43;)
  * [Tealium for Android-Java](/platforms/android-java/) (5.9.0&#43; for Braze 1.0.0&#43; or &lt;5.9.0 for previous versions)
  * [Tealium for iOS-Swift](/platforms/ios-swift/) (2.8.0&#43;)
* One of the following remote command integrations:
  * [Braze Remote Command JSON File](/platforms/remote-commands/integrations/braze/#json-template) (Requires Android-Kotlin 1.0.0&#43; or iOS-Swift 2.1.0&#43;)
  * Braze Remote Command tag in Tealium iQ Tag Management

## How It Works

The Braze integration uses the following items:

1. The Braze native SDK.
2. The remote commands module that wraps the Braze methods.
3. Either the JSON configuration file or the Remote Command tag that translates event tracking into native Braze calls.

Adding the Braze remote command module to your app automatically installs and builds the required Braze libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Braze SDK separately.

There are two remote command options: a JSON configuration file or using iQ Tag Management to configure the mappings. Using a JSON configuration file is recommended for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](/platforms/remote-commands/how-it-works/#vendor-integrations).


## Install

### Dependency Manager




1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-braze-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumBraze` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumBraze` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs the `TealiumBraze` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumBraze` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and select the `TealiumBraze` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod &#34;BrazeKit&#34;` if they exist in your Podfile. The dependency for `tealium-swift` is already included in the `TealiumBraze` framework.

2. Add the following dependency to your Podfile:  
      ```ruby
      pod &#34;TealiumBraze&#34;
      ```  
      The `TealiumBraze` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      ```

3. Import the `TealiumSwift` and `TealiumBraze` modules in your `TealiumHelper` file, and any other files that access the `Tealium` class or the Braze remote command.





1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumBraze` framework.

2.  Add the following dependency to your Cartfile:  
      ```bash
      github &#34;tealium/tealium-ios-braze-remote-command&#34;
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

2. Import both the Braze SDK and Tealium-Braze remote commands by adding the following dependencies in your app project&#39;s `build.gradle` file:  
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:braze:3.0.0&#39;
            implementation &#39;com.braze:android-sdk-ui:29.0.1&#39;
      }
      ```



1. Navigate to the root of your React Native project.

2. Download and install the `tealium-react-braze` package with the following command:  
    ```bash
    yarn add tealium-react-braze
    ```
3. React Native Autolinking is enabled in version 1.0.7 of the NPM package and is no longer needed to run `react-native link` if using version 0.60&#43; of React Native.



### Manual Installation




The manual installation for Braze remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the Braze remote commands for your iOS project:

1. Install the [Braze SDK](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/initial_sdk_setup/initial_sdk_setup/), if you haven&#39;t already done so.

2. Clone the [Tealium iOS Braze remote command](https://github.com/tealium/tealium-ios-braze-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`




The manual installation for Braze remote commands requires [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) to be installed.

To install the Braze remote commands for your Android project:

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

2. Add `tealium-braze.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:

      ```groovy
      dependencies {
            implementation(name:&#39;tealium-braze&#39;, ext:&#39;aar&#39;)
      }
      ```




## Initialize



Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium’s iOS (Swift) library:  
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
    let braze = BrazeRemoteCommand(brazeLocation: BrazeLocationProvider()) 

    // Local JSON
    //let braze = BrazeRemoteCommand(type: .local(file: &#34;braze&#34;), brazeLocation: BrazeLocationProvider()) 

    // Remote JSON
    //let braze = BrazeRemoteCommand(type: .remote(url: &#34;https://some.domain.com/braze.json&#34;), brazeLocation: BrazeLocationProvider()) 

    remoteCommands.add(braze)
}
```


Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s Kotlin library:
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
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
    braze.registerConfigOverride { builder -&gt;
        // builder.setIsLocationCollectionEnabled(true);
        // builder.setGeofencesEnabled(true);
        // builder.setPushDeepLinkBackStackActivityEnabled(true);
        // builder.setPushDeepLinkBackStackActivityClass(UserActivity.class);
    }

    // register the command

    // Webview Tag
    remoteCommands?.add(braze); 

    // Local JSON
    //remoteCommands?.add(braze, filename = &#34;braze.json&#34;); 

    // Remote JSON
    //remoteCommands?.add(braze, remoteUrl = &#34;https://some.domain.com/braze.json&#34;); 
}
```


Initialize remote commands with the Remote Command tag for Tealium&#39;s Android (Java) library:  
```java
import com.tealium.remotecommands.BrazeRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

BrazeRemoteCommand braze;
// Initialize with default configuration options.
braze = new BrazeRemoteCommand(config);

// Or alternatively initialize with some additional config options:
Set&lt;Class&gt; sessionHandlingBlacklist = new HashSet&lt;&gt;();
Set&lt;Class&gt; inAppMessageBlacklist = new HashSet&lt;&gt;();
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
import BrazeRemoteCommand from &#39;tealium-react-braze&#39;;
BrazeRemoteCommand.initialize();

// Webview Tag
let braze = { id: BrazeRemoteCommand.name } 

// Local JSON
//let braze = { id: BrazeRemoteCommand.name, path: &#34;braze.json&#34; } 

// Remote JSON
//let braze = { id: BrazeRemoteCommand.name, url: &#34;https://some.domain.com/braze.json&#34; } 

let config = TealiumConfig {
    // ...
    remoteCommands: [braze]
}
```





## JSON Template

If you are configuring remote commands using a [JSON configuration file](/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
    &#34;config&#34;: {
        &#34;api_key&#34;: &#34;YOUR_API_KEY&#34;,
        &#34;custom_endpoint&#34;: &#34;sdk.iad-01.braze.com&#34;,
        &#34;session_timeout&#34;: 30,
        &#34;trigger_interval_seconds&#34;: 100,
        &#34;enable_geofences&#34;: true,
        &#34;enable_automatic_geofences&#34;: true,
        &#34;enable_automatic_location&#34;: true,
        &#34;push_story_identifier&#34;: &#34;YOUR_IDENTIFIER&#34;,
        &#34;use_uuid_as_device_id&#34;: true,
        &#34;forward_universal_links&#34;: true
    },
    &#34;mappings&#34;: {
        &#34;customer_id&#34;: &#34;user_id&#34;,
        &#34;customer_first_name&#34;: &#34;first_name&#34;,
        &#34;customer_last_name&#34;: &#34;last_name&#34;,
        &#34;customer_gender&#34;: &#34;gender&#34;,
        &#34;customer_language&#34;: &#34;language&#34;,
        &#34;customer_email&#34;: &#34;email&#34;,
        &#34;customer_home_city&#34;: &#34;home_city&#34;,
        &#34;customer_dob&#34;: &#34;date_of_birth&#34;,
        &#34;customer_alias&#34;: &#34;user_alias&#34;,
        &#34;customer_alias_label&#34;: &#34;alias_label&#34;,
        &#34;pet&#34;: &#34;set_custom_attribute.pet&#34;,
        &#34;pet_count&#34;: &#34;set_custom_attribute.pet_count&#34;,
        &#34;pet_count_unset&#34;: &#34;unset_custom_attribute.pet_count_unset&#34;,
        &#34;pet_count_increment&#34;: &#34;increment_custom_attribute.pet_count_increment&#34;,
        &#34;pet_names&#34;: &#34;set_custom_array_attribute.pet_names&#34;,
        &#34;pet_names_append&#34;: &#34;append_custom_array_attribute.pet_names_append&#34;,
        &#34;pet_names_remove&#34;: &#34;remove_custom_array_attribute.pet_names_remove&#34;,
        &#34;screen_name&#34;: &#34;screen_name&#34;,
        &#34;email_notification&#34;: &#34;email_notification&#34;,
        &#34;push_notification&#34;: &#34;push_notification&#34;,
        &#34;event_name&#34;: &#34;event_name&#34;,
        &#34;current_level&#34;: &#34;event.current_level&#34;,
        &#34;start_date&#34;: &#34;event.start_date&#34;,
        &#34;high_score&#34;: &#34;event.high_score&#34;,
        &#34;product_id&#34;: &#34;product_id&#34;,
        &#34;product_quantity&#34;: &#34;product_qty&#34;,
        &#34;product_unit_price&#34;: &#34;product_unit_price&#34;,
        &#34;currency_code&#34;: &#34;product_currency&#34;,
        &#34;rewards_member&#34;: &#34;purchase.rewards_member&#34;,
        &#34;rewards_points_earned&#34;: &#34;purchase.rewards_points_earned&#34;,
        &#34;date_joined_program&#34;: &#34;purchase.date_joined_program&#34;,
        &#34;latitude&#34;: &#34;location_latitude&#34;,
        &#34;longitude&#34;: &#34;location_longitude&#34;,
        &#34;horizontal_accuracy&#34;: &#34;location_horizontal_accuracy&#34;,
        &#34;vertical_accuracy&#34;: &#34;location_vertical_accuracy&#34;
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;initialize&#34;,
        &#34;setengagement&#34;: &#34;emailnotification,pushnotification&#34;,
        &#34;log_custom_event&#34;: &#34;logcustomevent&#34;,
        &#34;set_location&#34;: &#34;setlastknownlocation&#34;,
        &#34;custom_attribute&#34;: &#34;setcustomattribute&#34;,
        &#34;unset_custom_attribute&#34;: &#34;unsetcustomattribute&#34;,
        &#34;custom_array_attribute&#34;: &#34;appendcustomarrayattribute&#34;,
        &#34;append_custom_array_attribute&#34;: &#34;appendcustomarrayattribute&#34;,
        &#34;remove_custom_array_attribute&#34;: &#34;removecustomarrayattribute&#34;,
        &#34;increment_custom_attribute&#34;: &#34;incrementcustomattribute&#34;,
        &#34;log_purchase&#34;: &#34;logpurchase&#34;,
        &#34;user_attribute&#34;: &#34;userattribute,useridentifier,useralias&#34;,
        &#34;user_login&#34;: &#34;useridentifier,useralias&#34;,
        &#34;user_alias&#34;: &#34;useralias&#34;,
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


Since the Braze SDK is installed alongside the Tealium SDK, trigger any native Braze functionality given the corresponding tag configuration.

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
| `email_notification` | `String`| [`&#34;optedin&#34;`, `&#34;subscribed&#34;`, `&#34;unsubscribed&#34;`]|

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
| `push_notification` | `String`| [`&#34;optedin&#34;`, `&#34;subscribed&#34;`, `&#34;unsubscribed&#34;`]|


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

#### Set User&#39;s Last Known Location

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

To access the Braze instance directly, use the `onReady` method. The `onReady` method returns the Braze instance in the completion block once it&#39;s properly configured.

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
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -&gt; Bool {
    let brazeConfig = Braze.Configuration(apiKey: &#34;YOUR_API_KEY&#34;, endpoint: &#34;YOUR_ENDPOINT&#34;)
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