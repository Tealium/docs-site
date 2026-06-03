---
title: Remote Command: FullStory
description: Tealium remote command integration for FullStory on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/fullstory/
---
## Requirements

* One of the following mobile libraries:
    * [Tealium for Android-Kotlin](/platforms/android-kotlin/) (1.0.0&#43;)
    * [Tealium for Android-Java](/platforms/android-java/) (5.9.0&#43; for FullStory 1.0.0&#43; or &lt;5.9.0 for previous versions)
    * [Tealium for iOS-Swift](/platforms/ios-swift/) (2.18.0&#43;)
* One of the following remote command integrations:
    * [FullStory Remote Command JSON File](/platforms/remote-commands/integrations/fullstory/#json-template) (Requires Android-Kotlin 1.0.0&#43; or iOS-Swift 2.18.0&#43;)
    * [FullStory Remote Command tag]() in Tealium iQ Tag Management

## How it works

The FullStory integration uses three components:

1. The FullStory native SDK.
1. The remote commands module that wraps the FullStory methods.
1. Either the JSON configuration file or Remote Command tag that translates event tracking into native FullStory calls.

Adding the FullStory remote command module to your app automatically installs and builds the required FullStory libraries. If you are using a dependency manager installation, you do not need to install the FullStory SDK separately.

If you are using CocoaPods or Carthage as your dependency manager, you will have to manually download the FullStory command line tool so you can add it as a [build script](#ios-build-script)

There are two remote command options:

* Use a JSON configuration file (Recommended), hosted either remotely or locally within the app.
* Use iQ Tag Management to configure the mappings and add the Remote Command tag for the vendor integration.

For more information, see [vendor integrations](/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency manager

We recommend installing modules with one of the following dependency managers:




1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**.
1. Enter the following repository URL: `https://github.com/tealium/tealium-ios-fullstory-remote-command` .
1. Configure the version rules. We recommend the `Up to next major` setting. If the current `TealiumFullstory` version does not appear in the list, then reset your Swift package cache.
1. Select the `TealiumFullstory` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs the `TealiumFullstory` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumFullstory` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
1. In your Xcode project, select the app target under the **TARGETS** section.
1. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and select the `TealiumFullstory` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.



To install FullStory remote commands for iOS using CocoaPods:

1. Remove `tealium-swift` if it already exists your Podfile. The dependency for `tealium-swift` is already included in the `TealiumFullstory` framework.
2. Add the following dependency to your Podfile:  
    ```ruby
    pod &#34;TealiumFullstory&#34;
    ```
    The `TealiumFullstory` pod includes the following `TealiumSwift` dependencies:  
    ```bash
    &#39;tealium-swift/Core&#39;
    &#39;tealium-swift/RemoteCommands&#39;
    &#39;tealium-swift/TagManagement&#39;
    ```
3. Import the modules `TealiumSwift` and `TealiumFullstory` into your `TealiumHelper` file, and any other files that access the `Tealium` class, or the FullStory Remote Command.





To install FullStory remote commands for iOS using Carthage:

1. Remove `tealium-swift` from your Cartfile. The dependency for 
`tealium-swift` is already included in the `TealiumFullstory` framework.
1. Add the following dependency to your Cartfile:
    ```bash
    github &#34;tealium/tealium-ios-fullstory-remote-command&#34;
    ```




To install FullStory remote commands for Android using Maven:

1. Install [Tealium for Android 
(Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) and add the Tealium Maven URL to your project’s top-level `build.gradle` file, if you haven&#39;t done so already.
    ```groovy
    allprojects {
        repositories {
            mavenCentral()
            maven {
                url &#34;https://maven.tealiumiq.com/android/releases/&#34;
            }
            maven {
                url &#34;https://maven.fullstory.com&#34;
            }
        }
    }
    ```
2. Import both the FullStory SDK and Tealium-FullStory remote commands by 
adding the following dependencies in your app project&#39;s `build.gradle` 
file:
    ```groovy
    dependencies {
        implementation &#39;com.tealium.remotecommands:fullstory:1.1.0&#39;
    }
    ```
3. Add the FullStory gradle plugin to your App/Module `build.gradle`. Replace `&lt;PLUGIN PROPERTIES&gt;` with [available 
properties](https://help.fullstory.com/hc/en-us/articles/360040596093-Getting-Started-with-Android-Data-Capture#01F5E7XFMG19SNYS77NYETKDMQ):
    ```groovy
    fullstory {
        &lt;PLUGIN PROPERTIES&gt;
    }
    ```



### Manual installation (iOS)

The manual installation for FullStory remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the FullStory remote commands for your iOS project:

1. Install the [FullStory 
SDK](https://help.fullstory.com/hc/en-us/articles/360042772333-Getting-Started-with-iOS-Data-Capture), if you haven&#39;t already done so.
1. Clone the [Tealium iOS FullStory remote command](https://github.com/tealium/tealium-ios-fullstory-remote-command) repo and drag the files in the `Sources` folder into your project.
1. Add `Dispatchers.RemoteCommands` as a dispatcher.
1. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`.

## Initialize

For all Tealium libraries, register the FullStory remote commands when you 
initialize.

### Android (Kotlin)

Initialize remote commands with a JSON configuration file or the Remote 
Command tag for Tealium&#39;s Android (Kotlin) library.




The following code is designed for use with the JSON Remote Commands 
feature, using the local file option:
```kotlin
val config = TealiumConfig(application,
    &#34;ACCOUNT&#34;,
    &#34;PROFILE&#34;,
    Environment.DEV,
    dispatchers = mutableSetOf(Dispatchers.RemoteCommands));

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Initialize FullStory Remote Command
    val fullstoryCommand = FullStoryRemoteCommand()
    // register the command
    remoteCommands?.add(fullstoryCommand, filename = &#34;tealium-fullstory.json&#34;)
}
```


The following code is designed for use with the Remote Command tag feature:
```kotlin
val config = TealiumConfig(application,
    &#34;ACCOUNT&#34;,
    &#34;PROFILE&#34;,
    Environment.DEV,
    dispatchers = mutableSetOf(Dispatchers.RemoteCommands));

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Initialize FullStory Remote Command
    val fullstoryCommand = FullStoryRemoteCommand()
    // register the command
    remoteCommands?.add(fullstoryCommand)
}
```



### Android (Java)




The JSON Remote Command file feature for Android is only available in the Kotlin SDK.



The following code is designed for use with the Remote Command tag feature:
```java
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

FullStoryRemoteCommand fullstory = new FullStoryRemoteCommand();

// register the command
teal.addRemoteCommand(fullstory);
```



### iOS (Swift)

Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s iOS (Swift) library.




The following code is designed for use with the JSON Remote Commands feature, using the local file option:
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
    profile: &#34;PROFILE&#34;,
    environment: &#34;ENVIRONMENT&#34;,
    dataSource: &#34;DATASOURCE&#34;,
    options: nil)
config.dispatchers = [Dispatchers.TagManagement, 
Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
    let fullstory = FullstoryRemoteCommand(type: .local(file: &#34;fullstory&#34;))
    remoteCommands.add(fullstory)
}
```



The following code is designed for use with the Remote Command tag feature:
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
    profile: &#34;PROFILE&#34;,
    environment: &#34;ENVIRONMENT&#34;,
    dataSource: &#34;DATASOURCE&#34;,
    options: nil)
config.dispatchers = [Dispatchers.TagManagement, 
Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
    let fullstory = FullstoryRemoteCommand()
    remoteCommands.add(fullstory)
}

```




## JSON template

If you are configuring remote commands using a [JSON configuration file](/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
  &#34;config&#34;: {},
  &#34;mappings&#34;: {
    &#34;tealium_event&#34;: &#34;event_name&#34;,
    &#34;uid&#34;: &#34;uid_str&#34;,
    &#34;email&#34;: &#34;user_variables.email_str&#34;,
    &#34;phone&#34;: &#34;user_variables.phone_str&#34;,
    &#34;cart_id&#34;: &#34;event.cart_id_str&#34;,
    &#34;product_id&#34;: &#34;event.product_id_str&#34;,
    &#34;price&#34;: &#34;event.price_real&#34;,
    &#34;name&#34;: &#34;event.name_str&#34;,
    &#34;category&#34;: &#34;event.categoryProperties&#34;
  },
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;logevent&#34;,
    &#34;identify_user&#34;: &#34;identify&#34;,
    &#34;tealiumSampleEvent&#34;: &#34;logevent&#34;,
    &#34;tealiumSampleEventWithData&#34;: &#34;logevent&#34;
  }
}
```

## Supported methods

We map a command to each FullStory method. To trigger a FullStory method, pass the corresponding command in the specified format.

| Remote Command | FullStory Method |
| -----------------| -------------------- |
| `logevent` | `FS.event()` |
| `identify` | `FS.identify()` |
| `setuservariables` | `FS.setUserVars()` |
| `shutdown` | `FS.shutdown()` |
| `restart` | `FS.restart()` |
| `consent` | `FS.consent()` |
| `anonymize` | `FS.anonymize()` |
| `resetidletimer` | `FS.resetIdleTimer()` |
| `log` | `FS.log()` |

Since the FullStory SDK is installed alongside the Tealium SDK, you can trigger any native FullStory functionality by calling the SDK directly, even if the functionality is not provided by the Tealium FullStory Remote Command tag.

### SDK setup

#### Initialize

The FullStory SDK is initialized automatically upon launch.

FullStory Developer Guide: Initial SDK Setup

* [Mobile getting started](https://developer.fullstory.com/mobile/getting-started/) 

### Log event

| Remote Command | FullStory Method |
| ---------------- | ---------------- |
| `logevent` | `FS.event()` |

| Parameter | Type |
| --------- | ---- |
| `event_name` (required) | String |
| `event` | Map |

FullStory Developer Guide: Log Event

* [Android](https://developer.fullstory.com/mobile/android/capture-events/analytics-events/)
* [iOS](https://developer.fullstory.com/mobile/ios/capture-events/analytics-events/)

### Identify

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `identify` | `FS.identify()` |

| Parameter | Type |
| --------- | ---- |
| `uid` (required) | String |
| `user_variables` | Map |

FullStory Developer Guide: Identify

* [Android](https://developer.fullstory.com/mobile/android/identification/identify-users/)
* [iOS](https://developer.fullstory.com/mobile/ios/identification/identify-users/)

### Set user variables

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `setuservariables` | `FS.setUserVars()` |

| Parameter | Type |
| --------- | ---- |
| `user_variables` (required) | Map |

 The `user_variables` parameter takes an object of key-value pairs, where keys are `strings` and the values are suffixed with the data type (for example: `_str`, `_int`, `_bool`). For more information, see [Setting custom API properties](https://developer.fullstory.com/mobile/user-identification/set-user-properties/)

FullStory Developer Guide: Set User Variables

* [Android](https://developer.fullstory.com/mobile/android/identification/set-user-properties/)
* [iOS](https://developer.fullstory.com/mobile/ios/identification/set-user-properties/)

### Shutdown

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `shutdown` | `FS.shutdown()` |

Stops the FullStory recording. Use `restart` to resume recording after a shutdown.

FullStory Developer Guide: Shutdown

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/capture-data/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/capture-data/)

### Restart

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `restart` | `FS.restart()` |

Resumes FullStory recording after `shutdown` stops it.

FullStory Developer Guide: Restart

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/capture-data/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/capture-data/)

### Consent

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `consent` | `FS.consent()` |

| Parameter | Type |
| --------- | ---- |
| `consent_granted` (required) | Boolean |

Grants or revokes user consent for FullStory session recording.

FullStory Developer Guide: Consent

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/user-consent/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/user-consent/)

### Anonymize

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `anonymize` | `FS.anonymize()` |

Anonymizes the current user session, removing any previously set user identification.

FullStory Developer Guide: Anonymize

* [Android](https://developer.fullstory.com/mobile/android/identification/anonymize-users/)
* [iOS](https://developer.fullstory.com/mobile/ios/identification/anonymize-users/)

### Reset idle timer

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `resetidletimer` | `FS.resetIdleTimer()` |

Resets the FullStory idle timeout timer, extending the current session.

FullStory Developer Guide: Reset Idle Timer

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/reset-idle-timer/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/reset-idle-timer/)

### Log

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `log` | `FS.log()` |

| Parameter | Type |
| --------- | ---- |
| `log_level` (required) | String |
| `log_message` (required) | String |

Logs a message at the specified level. Accepted `log_level` values differ by platform:

| Platform | Accepted values |
| -------- | --------------- |
| Android | `log`, `error`, `warn`/`warning`, `info`, `debug` |
| iOS | `assert`, `error`, `warning`, `info`, `debug` |

FullStory Developer Guide: Log

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/logging/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/logging/)