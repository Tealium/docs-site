---
title: Remote Command: Airship
description: Tealium remote command integration for Airship on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/airship/
---

## Requirements

* [Airship credentials](https://docs.airship.com/guides/messaging/user-guide/admin/security/app-keys-secrets/)
* One of these mobile libraries:
  * [Tealium for Android](/platforms/android-java/)
  * [Tealium for iOS-Swift](/platforms/ios-swift/)
* Airship Remote Command tag in Tealium iQ Tag Management

## How It Works

The Airship integration uses three items:

1. The Airship native SDK
2. The Tealium Airship remote commands module that wraps the Airship methods
3. The Airship Remote Command tag that translates event tracking into native Airship calls

When you add the Airship remote command module to your app, the required Airship libraries are automatically installed without adding any vendor-specific code to your app. There is no need to install the Airship SDK separately.

## Install
### Dependency Manager




Swift Package Manager is the recommended and simplest way to install the TealiumAirship package. To install Airship remote commands for iOS using Swift Package Manager:

1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**

2. Enter the repository URL: `https://github.com/tealium/tealium-ios-airship-remote-command`

3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumAirship`  version does not appears in the list, then reset your Swift package cache.

4. Select the `TealiumAirship` module to install, and select the app target you want the module to be installed in.
5. If you are using any additional modules from the Tealium Swift library, follow [the Swift Package Manager instructions](/platforms/ios-swift/install/#swift-package-manager-recommended) to add them.

If your project has more than one app target and needs `TealiumAirship` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumAirship` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and  select the `TealiumAirship` module to add it to your app target.




1. Remove `pod &#34;tealium-swift&#34;` and `pod &#34;Airship&#34;` if they exist in your Podfile. The dependency for `tealium-swift` is already included in the `TealiumAirship` framework.

2. Add the following dependency to your Podfile:  
      ```ruby
      pod &#34;TealiumAirship&#34;
      ```
      The `TealiumAirship` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      &#34;tealium-swift/Core&#34;
      &#34;tealium-swift/RemoteCommands&#34;
      &#34;tealium-swift/TagManagement&#34;
      ```

3. Add any other required modules manually to your Podfile, such as the following:   
      ```ruby
      pod &#34;tealium-swift/Lifecycle&#34;
      pod &#34;tealium-swift/VisitorService&#34;
      ```
      Learn more about the [recommended modules for iOS](/platforms/ios-swift/modules/).

4. Import the modules `TealiumSwift` and `TealiumAirship` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Airship remote command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumAirship` framework.

2. Remove the following line if it exists in your Cartfile:  
      ```bash
      github &#34;urbanairship/ios-library&#34;
      ```

3.  Add the following dependency to your Cartfile:  
      ```bash
      github &#34;tealium/tealium-ios-airship-remote-command&#34;
      ```






1. Install [Tealium for Android](/platforms/android-java/install/) and add the Tealium Maven URL to your project’s top-level `build.gradle` file, if you haven&#39;t done so already.

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

2. Import the Tealium-Airship remote commands by adding the following dependencies in your app project&#39;s `build.gradle` file:  
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:airship:1.1.0&#39;
      }
      ```



### Manual Installation




The manual installation for Airship remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the Airship remote commands for your iOS project:

1. Install the [Airship SDK](https://github.com/urbanairship/ios-library), if you haven&#39;t already done so.

2. Clone the [Tealium iOS Airship remote command](https://github.com/tealium/tealium-ios-airship-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Add `Dispatchers.RemoteCommands` as a dispatcher.

4. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`.




The manual installation for Airship remote commands requires [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) to be installed. To install the Airship remote commands for your Android project:

1. Add `flatDir` to your project root `build.gradle` file:  
      ```groovy
      repositories {
          flatDir {
              dirs (&#39;/src/main/libs&#39;)
          }
      }
      ```

2. Add `tealium-airship.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:  
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-airship&#39;, ext:&#39;aar&#39;)
      }
      ```



## Initialize

Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s Android or Swift library.




The following example creates a Tealium instance and then registers the Airship remote command with Tealium&#39;s Swift library for iOS:

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
    let airship = AirshipRemoteCommand() 

    // Local JSON
    //let airship = AirshipRemoteCommand(type: .local(file: &#34;airship&#34;))

    // Remote JSON
    //let airship = AirshipRemoteCommand(type: .remote(url: &#34;https://some.domain.com/airship.json&#34;))
    remoteCommands.add(airship)
}
```




The following example creates a Tealium instance and then registers the Airship remote command for Android (Kotlin):

```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val airship = AirshipRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(airship);

    // Local JSON
    //remoteCommands?.add(airship, filename = &#34;airship.json&#34;);

    // Remote JSON
    //remoteCommands?.add(airship, remoteUrl = &#34;https://some.domain.com/airship.json&#34;); 
}
```




## Supported Methods

We map a command to each Airship method. To trigger an Airship method, pass the corresponding command in the specified format.

| Remote Command | Airship Method |
| :-- | :-- |
| `initialize` | `takeOff()` |
| `trackevent` | `UACustomEvent.track()` |
| `trackscreenview` | `trackScreen` |
| `enableanalytics` | `analytics()?.isEnabled` |
| `disableanalytics` | `analytics()?.isEnabled` |
| `setnameduser` | `UAirship.namedUser()?.identifier` |
| `setcustomidentifiers` | `analytics()?.associateDeviceIdentifiers` |
| `enableadvertisingidentifiers` | `analytics()?.associateDeviceIdentifiers` |
| `enableinappmessaging` | `UAInAppMessageManager.shared()?.isEnabled` |
| `disableinappmessaging` | `UAInAppMessageManager.shared()?.isEnabled` |
| `pauseinappmessaging` | `UAInAppMessageManager.shared()?.isPaused` |
| `unpauseinappmessaging` | `UAInAppMessageManager.shared()?.isPaused` |
| `setinappmessagingdisplayinterval` | `UAInAppMessageManager.shared()?.displayInterval` |
| `enableuserpushnotifications` | `UAirship.push()?.userPushNotificationsEnabled` |
| `disableuserpushnotifications` | `UAirship.push()?.userPushNotificationsEnabled` |
| `enablebackgroundpushnotifications` | `UAirship.push()?.backgroundPushNotificationsEnabled` |
| `disablebackgroundpushnotifications` | `UAirship.push()?.backgroundPushNotificationsEnabled` |
| `setpushnotificationoptions` | `UAirship.push()?.notificationOptions` |
| `setforegroundpresentationoptions` | `UAirship.push()?.defaultPresentationOptions` |
| `setbadgenumber` | `UAirship.push()?.badgeNumber` |
| `resetbadgenumber` | `UAirship.push()?.resetBadge()` |
| `enableautobadge` | `UAirship.push()?.isAutobadgeEnabled` |
| `disableautobadge` | `UAirship.push()?.isAutobadgeEnabled` |
| `enablequiettime` | `UAirship.push()?.isQuietTimeEnabled` |
| `disablequiettime` | `UAirship.push()?.isQuietTimeEnabled` |
| `setquiettimestart` | `UAirship.push()?.setQuietTimeStartHour` |
| `setchanneltags` | `UAirship.channel()?.tags` |
| `setnamedusertags` | `UAirship.namedUser()?.setTags()` |
| `addtag` | `UAirship.channel()?.addTag()` |
| `removetag` | `UAirship.channel()?.removeTag` |
| `addtaggroup` | `UAirship.channel()?.addTags, UAirship.namedUser()?.addTags` |
| `removetaggroup` | `UAirship.channel()?.removeTags, UAirship.namedUser()?.removeTags` |
| `setattributes` | `UAirship.channel()?.apply` |
| `displaymessagecenter` | `UAMessageCenter.shared().display()` |
| `setmessagecentertitle` | `UAMessageCenter.shared()?.defaultUI.title` |
| `setmessagecenterstyle` | `UAMessageCenter.shared().defaultUI.style` |
| `enablelocation` | `UALocation.shared().isLocationUpdatesEnabled` |
| `disablelocation` | `UALocation.shared().isLocationUpdatesEnabled` |
| `enablebackgroundlocation` | `UALocation.shared().isBackgroundLocationUpdatesAllowed` |
| `disablebackgroundlocation` | `UALocation.shared().isBackgroundLocationUpdatesAllowed` |

Since the Airship SDK is integrated with the Tealium SDK, you can trigger any native Airship functionality by calling the SDK directly, even if the functionality is not provided by the Tealium Airship Remote Command tag.

### SDK Setup

#### Initialize

The Airship SDK is initialized automatically upon launch. The Airship API keys are set in the tag configuration.

| Remote Command | Airship Method |
|---|---|
| `initialize`  | `takeOff()` |

**Possible UAConfig parameters**

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `productionAppKey` (required) | `String` | `MyProdKey` |
| `productionAppSecret` (required) | `String|MyProdSecret` |
| `developmentAppKey` (required) | `String` | `MyDevKey` |
| `developmentAppSecret` (required) | `String` | `MyDevSecret` |
| `site` (optional) | `String` | `eu/us` |
| `isDataCollectionOptInEnabled` (optional) | `Boolean` | `true` |
| `isInProduction` (optional) | `Boolean` | `true` |
| `developmentLogLevel` (optional) | `String` | `debug/error/info/none/trace/undefined/warn` |
| `productionLogLevel` (optional) | `String` | `debug/error/info/none/trace/undefined/warn` |
| `isAnalyticsEnabled` (optional) | `Boolean` | `true` |

Airship Developer Guide: Initial SDK Setup

- [iOS](https://docs.airship.com/platform/ios/getting-started/#takeoff)
- [Android](https://docs.airship.com/platform/android/getting-started/#takeoff)

#### trackEvent

Sends a custom event to Airship.

| Remote Command | Airship Method |
|---|---|
| `trackEvent`  | `UACustomEvent.track()` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `event_name` (required) | `String` | `Purchase` |
| `event` (optional) | `JSON object` | `{&#34;my_numeric_property&#34;: 1}` |
| `event_value` (optional) | `Number` | `1.5` |

Airship Developer Guide: Event Tracking

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-custom-events)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-custom-events)

#### trackScreenView

Tracks a screen view.

| Remote Command | Airship Method |
| :-- | :-- |
| `trackScreenView` | `UAirship.analytics()?.trackScreen` |


| Parameter | Type | Example |
| :-- | :-- | :-- |
| `screen_name` (required) | `String` | `Home Screen` |

Airship Developer Guide: Event Tracking

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-screen-tracking)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-screen-tracking)

#### enableAnalytics

Enables Airship Analytics after previously being disabled (default is enabled).

| Remote Command | Airship Method |
| :-- | :-- |
| `enableAnalytics` | `UAirship.analytics()?.isEnabled` |

Airship Developer Guide: Enable Analytics

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#disabling-analytics)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#disabling-analytics)

#### disableAnalytics

Disables Airship Analytics after previously being enabled (default is enabled).

| Remote Command | Airship Method |
| :-- | :-- |
| `disableAnalytics` | `UAirship.analytics()?.isEnabled` |

Airship Developer Guide: Disable Analytics

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#disabling-analytics)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#disabling-analytics)

#### setNamedUser

Sets a known user identifier for the current app user.

| Remote Command | Airship Method |
| :-- | :-- |
| `setNamedUser` | `UAirship.namedUser()?.identifier` |


| Parameter | Type | Example |
| :-- | :-- | :-- |
| `named_user_identifier` (required) | `String` | `email@tealium.com` |

Airship Developer Guide: Event Tracking

- [iOS](https://docs.airship.com/platform/ios/segmentation/#named-users-ios)
- [Android](https://docs.airship.com/platform/android/segmentation/#named-users-android)

#### setCustomIdentifiers

Sets any additional custom identifiers that you deem significant for the user.

| Remote Command | Airship Method |
| :-- | :-- |
| `setCustomIdentifiers` | `UAirship.analytics()?.associateDeviceIdentifiers` |


| Parameter | Type | Example |
| :-- | :-- | :-- |
| `custom` (required) | `JSON Object` (Strings Only) | `{&#34;my_custom_identifier&#34;:&#34;user@email.com&#34;}` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-custom-identifiers)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-custom-identifiers)

#### enableAdvertisingIdentifiers

Adds advertising identifiers to the dictionary of custom identifiers (IDFV, IDFA, Ad Tracking Enabled.

| Remote Command | Airship Method |
| :-- | :-- |
| `setCustomIdentifiers` | `UAirship.analytics()?.associateDeviceIdentifiers` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-custom-identifiers)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-custom-identifiers)

#### enableInAppMessaging

Enables the in-app messaging feature.

| Remote Command | Airship Method |
| :-- | :-- |
| `enableInAppMessaging` | `UAInAppMessageManager.shared()?.isEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#component-enablement)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#feature-enablement)

#### disableInAppMessaging

Disables the in-app messaging feature.

| Remote Command | Airship Method |
| :-- | :-- |
| `disableInAppMessaging` | `UAInAppMessageManager.shared()?.isEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#component-enablement)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#feature-enablement)

#### pauseInAppMessaging

Enables the in-app messaging feature.

| Remote Command | Airship Method |
| :-- | :-- |
| `pauseInAppMessaging` | `UAInAppMessageManager.shared()?.isPaused` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#pausing-message-display)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#pausing-message-display)

#### unPauseInAppMessaging

Enables the in-app messaging feature.

| Remote Command | Airship Method |
| :-- | :-- |
| `unPauseInAppMessaging` | `UAInAppMessageManager.shared()?.isPaused` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#pausing-message-display)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#pausing-message-display)

#### setInAppMessagingDisplayInterval

The amount of time Airship must wait before displaying a new in-app message, in *seconds*.

| Remote Command | Airship Method |
| :-- | :-- |
| `setInAppMessagingDisplayInterval` | `UAInAppMessageManager.shared()?.displayInterval` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `in_app_messaging_display_interval` (required) | `String` | `&#34;10&#34;` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#pausing-message-display)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#pausing-message-display)

#### enableUserPushNotifications

Enables user push notifications.

| Remote Command | Airship Method |
| :-- | :-- |
| `enableUserPushNotifications` | `UAirship.push()?.userPushNotificationsEnabled` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `push_notification_options` (optional) | `Array of Strings` | `[&#34;badge&#34;, &#34;sound&#34;, &#34;announcement&#34;]` |
Possible Push Messaging Options: `&#34;badge&#34;`, `&#34;sound&#34;`, `&#34;alert&#34;`, `&#34;carplay&#34;`, `&#34;announcement&#34;`, `&#34;critical&#34;`, `&#34;app_notification_settings&#34;`

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### disableUserPushNotifications

Disables user push notifications.

| Remote Command | Airship Method |
| :-- | :-- |
| `enableUserPushNotifications` | `UAirship.push()?.userPushNotificationsEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### enableBackgroundPushNotifications

Enables background push notifications.

| Remote Command | Airship Method |
| :-- | :-- |
| `enableUserPushNotifications` | `UAirship.push()?. backgroundPushNotificationsEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### disableBackgroundPushNotifications

Disables background push notifications.

| Remote Command | Airship Method |
| :-- | :-- |
| `disableBackgroundPushNotifications` | `UAirship.push()?.backgroundPushNotificationsEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### setPushNotificationOptions

Sets push notification options. iOS Only.

| Remote Command | Airship Method |
| :-- | :-- |
| `setPushNotificationOptions` | `UAirship.push()?.notificationOptions` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `push_notification_options` (required) | `Array of Strings` | `[&#34;badge&#34;, &#34;sound&#34;, &#34;announcement&#34;]` |

Possible Push Messaging Options: `&#34;badge&#34;`, `&#34;sound&#34;`, `&#34;alert&#34;`, `&#34;carplay&#34;`, `&#34;announcement&#34;`, `&#34;critical&#34;`, `&#34;app_notification_settings&#34;`

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#notification-options)

#### setForegroundPresentationOptions

Sets push notification presentation options. iOS Only.

| Remote Command | Airship Method |
| :-- | :-- |
| `setForegroundPresentationOptions` | `UAirship.push()?.defaultPresentationOptions` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `foreground_presentation_options` (required) | `Array of Strings` | `[&#34;badge&#34;, &#34;sound&#34;, &#34;alert&#34;]` |

Possible Foreground Presentation Options: `&#34;badge&#34;`, `&#34;sound&#34;`, `&#34;alert&#34;`

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#foreground-presentation-options)

#### setBadgeNumber

Sets badge number on your app&#39;s icon to a specified number. iOS Only.

| Remote Command | Airship Method |
| :-- | :-- |
| `setBadgeNumber` | `UAirship.push()?.badgeNumber` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `badge_number` (required) | `Number` | `3` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### resetBadgeNumber

Resets the badge number. iOS Only.

| Remote Command | Airship Method |
| :-- | :-- |
| `setBadgeNumber` | `UAirship.push()?.badgeNumber` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### enableAutoBadge

Enables the auto-badge feature. iOS Only.

| Remote Command | Airship Method |
| :-- | :-- |
| `enableAutoBadge` | `UAirship.push()?.isAutobadgeEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### disableAutoBadge

Disables the auto-badge feature. iOS Only.

| Remote Command | Airship Method |
| :-- | :-- |
| `disableAutoBadge` | `UAirship.push()?.isAutobadgeEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### enableQuietTime

Enables the quiet time feature. iOS Only.

| Remote Command | Airship Method |
| :-- | :-- |
| `enableAutoBadge` | `UAirship.push()?.isQuietTimeEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)

#### disableQuietTime

Disables the quiet time feature. iOS Only.

| Remote Command | Airship Method |
| :-- | :-- |
| `disableAutoBadge` | `UAirship.push()?.isQuietTimeEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)

#### setQuietTimeStart

Sets the time constraints for the Quiet Time feature. iOS only.

| Remote Command | Airship Method |
| :-- | :-- |
| `setQuietTimeStart` | `UAirship.push()?.isQuietTimeEnabled` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `quiet` (required) | `JSON Object` | `{&#39;start_hour&#39;: 3, &#39;start_minute&#39;: 30, &#39;end_hour&#39;: 4, &#39;end_minute&#39;: 30` |
Required within the quiet object:

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `start_hour` (required) | `Number` | `3` |
| `start_minute` (required) | `Number` | `30` |
| `end_hour` (required) | `Number` | `4` |
| `end_minute` (required) | `Number` | `30` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)

#### setChannelTags

Calls the updateRegistration function. Must be called after changing notification options. iOS Only.

| Remote Command | Airship Method |
| :-- | :-- |
| `updateRegistration` | `UAirship.push()?.updateRegistration` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)

#### setNamedUserTags

Sets tags for the named user, overwriting previously set tags.

| Remote Command | Airship Method |
| :-- | :-- |
| `setNamedUserTags` | `UAirship.channel()?.addTags` | `UAirship.namedUser()?.addTags` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `named_user_tags` (required) | `String Array` | `[&#34;silver-member&#34;, &#34;gold-member&#34;]` |
| `tag_group` (required) | `String` | `loyalty` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/segmentation/#ios-tag-groups)
- [Android](https://docs.airship.com/platform/android/segmentation/#android-tag-groups)

#### addTag

Adds a channel tag.

| Remote Command | Airship Method |
| :-- | :-- |
| `addTag` | `UAirship.channel()?.addTag` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `channel_tag` (required) | `String` | `&#34;a_tag&#34;` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/segmentation/#tags)
- [Android](https://docs.airship.com/platform/android/segmentation/#tags)

#### removeTag

Removes a channel tag.

| Remote Command | Airship Method |
| :-- | :-- |
| `removeTag` | `UAirship.channel()?.removeTag` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `channel_tag` (required) | `String` | `&#34;a_tag&#34;` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/segmentation/#tags)
- [Android](https://docs.airship.com/platform/android/segmentation/#tags)

#### addTagGroup

Adds a tag group for a named user or channel.

| Remote Command | Airship Method |
| :-- | :-- |
| `addTagGroup` | `UAirship.channel()?.addTags` | `UAirship.namedUser()?.addTags` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `named_user_tags` | `channel_tags` (required) | `String Array` | `[&#34;silver-member&#34;, &#34;gold-member&#34;]` |
| `tag_group` (required) | `String` | `loyalty` |
| `tag_type` (required) | `String` | `channel|named_user` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/segmentation/#ios-tag-groups)
- [Android](https://docs.airship.com/platform/android/segmentation/#android-tag-groups)

#### removeTagGroup

Removes a tag group for a named user or channel.

| Remote Command | Airship Method |
| :-- | :-- |
| `removeTagGroup` | `UAirship.channel()?.removeTags` | `UAirship.namedUser()?.removeTags` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `named_user_tags` | `channel_tags` (required) | `String Array` | `[&#34;silver-member&#34;, &#34;gold-member&#34;]` |
| `tag_group` (required) | `String` | `loyalty` |
| `tag_type` (required) | `String` | `channel` | `named_user` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/segmentation/#ios-tag-groups)
- [Android](https://docs.airship.com/platform/android/segmentation/#android-tag-groups)

#### setAttributes

Sets custom attributes.

| Remote Command | Airship Method |
| :-- | :-- |
| `setAttributes` | `UAirship.channel()?.apply` |


| Parameter | Type | Example |
| :-- | :-- | :-- |
| `attributes` (required) | `JSON object` | `{&#34;last\_product\_purchased&#34;: &#34;A1234567&#34;}` |

Attribute values must be either Strings or Numbers.

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/segmentation/#attributes)
- [Android](https://docs.airship.com/platform/android/segmentation/#attributes)

#### displayMessageCenter

Displays the message center.

| Remote Command | Airship Method |
| :-- | :-- |
| `displayMessageCenter` | `UAMessageCenter.shared().display` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/message-center/#displaying-the-message-center)
- [Android](https://docs.airship.com/platform/android/message-center/#android-rich-push-inbox-intents)

#### setMessageCenterTitle

Sets the message center title. iOS only.

| Remote Command | Airship Method |
| :-- | :-- |
| `setMessageCenterTitle` | `UAMessageCenter.shared().defaultUI.title` |


| Parameter | Type | Example |
| :-- | :-- | :-- |
| `message_center_title` (required) | `String` | `&#34;Custom Message Center&#34;` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/message-center/#title)

#### setMessageCenterStyle

Sets the message center style. iOS only.

| Remote Command | Airship Method |
| :-- | :-- |
| `setMessageCenterStyle` | `UAMessageCenter.shared().defaultUI.style` |

| Parameter | Type | Example |
| :-- | :-- | :-- |
| `message_center_style` (required) | `JSON object` | Example below |

```
{&#34;titleFont&#34;: {&#34;size&#34;: Double, &#34;name&#34;:&#34;fontname&#34;},
 &#34;cellTitleFont&#34;: {&#34;size&#34;: Double, &#34;name&#34;:&#34;fontname&#34;},
 &#34;cellDateFont&#34;: {&#34;size&#34;: Double, &#34;name&#34;:&#34;fontname&#34;},
 &#34;navigationBarColor&#34;: {&#34;red&#34;: Double, &#34;green&#34;: Double, &#34;blue&#34;: Double, &#34;alpha&#34;: Double}
 &#34;titleColor&#34;: {&#34;red&#34;: Double, &#34;green&#34;: Double, &#34;blue&#34;: Double, &#34;alpha&#34;: Double}
 &#34;tintColor&#34;: {&#34;red&#34;: Double, &#34;green&#34;: Double, &#34;blue&#34;: Double, &#34;alpha&#34;: Double}
 }
```

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/message-center/#styling-ios-mc)

#### enableLocation

Enables Location.

| Remote Command | Airship Method |
| :-- | :-- |
| `enableLocation` | `UALocation.shared().isLocationUpdatesEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/location/#enabling-location)
- [Android](https://docs.airship.com/platform/android/location-targeting/#continuous-location-updates)

#### disableLocation

Disables location.

| Remote Command | Airship Method |
| :-- | :-- |
| `disableLocation` | `UALocation.shared().isLocationUpdatesEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/location/#allow-background-location)
- [Android](https://docs.airship.com/platform/android/location-targeting/#using-airship-location)

#### enableBackgroundLocation

Enables background location.

| Remote Command | Airship Method |
| :-- | :-- |
| `enableBackgroundLocation` | `UALocation.shared().isBackgroundLocationUpdatesAllowed` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/location/#allow-background-location)
- [Android](https://docs.airship.com/platform/android/location-targeting/#continuous-location-updates)

#### disableBackgroundLocation

Disables background location.

| Remote Command | Airship Method |
| :-- | :-- |
| `disableBackgroundLocation` | `UALocation.shared().isBackgroundLocationUpdatesAllowed` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/location/#allow-background-location)
- [Android](https://docs.airship.com/platform/android/location-targeting/#continuous-location-updates)
