---
title: Remote Command: Contentsquare
description: Tealium remote command integration for Contentsquare on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/contentsquare/
---
## Requirements

* One of these mobile libraries:
  * [Tealium for Android-Kotlin](https://docs.tealium.com/platforms/android-kotlin/) (1.0.0+)
  * [Tealium for Android-Java](https://docs.tealium.com/platforms/android-java/) (5.9.0+ for Contentsquare 1.0.0+ or <5.9.0 for previous versions)
  * [Tealium for iOS-Swift](https://docs.tealium.com/platforms/ios-swift/)
* One of these remote command integrations:
  * [Contentsquare Remote Command JSON File](https://docs.tealium.com/platforms/remote-commands/integrations/contentsquare/#json-template) (Requires Android-Kotlin 1.0.0+ or iOS-Swift 2.12.0+)
  * Contentsquare Remote Command tag in Tealium iQ Tag Management

## How It Works

The Contentsquare integration uses three items:

1. The Contentsquare native SDK
2. The remote commands module that wraps the Contentsquare methods
3. Either the JSON configuration file or Remote Command tag that translates event tracking into native Contentsquare calls

Adding the Contentsquare remote command module to your app automatically installs and builds the required Contentsquare libraries. If you are using a dependency manager installation, there is no need to install the Contentsquare SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File > Add Packages... > Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-contentsquare-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumContentSquare` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumContentSquare` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumContentSquare` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumContentSquare` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General > Frameworks, Libraries & Embedded Content** and  select the `TealiumContentSquare` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod "CS_iOS_SDK"` if they already exist in your Podfile. The dependency for `tealium-swift` is already included in the `TealiumContentsquare` framework.

2. Add the following dependency to your Podfile:
      ```ruby
      pod "TealiumContentsquare"
      ```
      The `TealiumContentsquare` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      ```

3. Import the modules `TealiumSwift` and `TealiumContentsquare` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Contentsquare Remote Command.





1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumContentsquare` framework.

2. Remove the following line if it exists in your Cartfile:  
      ```bash
      github "ContentSquare/CS_iOS_SDK"
      ```

3.  Add the following dependency to your Cartfile:  
      ```bash
      github "tealium/tealium-ios-contentsquare-remote-command"
      ```


<blockquote>
Tealium for Swift SDK (version 1.6.5+) requires the `TealiumDelegate` module to be included with your installation.
</blockquote>






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

2. Import both the Contentquare SDK and Tealium-Contentsquare remote commands by adding the following dependencies in your app project's `build.gradle` file:  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:contentsquare:2.3.0'
      }
      ```


### Manual Installation




The manual installation for Contentsquare remote commands requires the [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/) library to be installed. To install the Contentsquare remote commands for your iOS project:

1. Install the [Contentsquare SDK](https://docs.contentsquare.com/ios/#how-to-include-it), if you haven't already done so.

2. Clone the [Tealium iOS Contentsquare remote command](https://github.com/tealium/tealium-ios-contentsquare-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Set the [`remoteAPIEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true.`




The manual installation for Contentsquare remote commands requires [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) to be installed.

To install the Contentsquare remote commands for your Android project:

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

2. Add `tealium-contentsquare.aar` to `<PROJECT_ROOT>/<MODULE>/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:

      ```groovy
      dependencies {
            implementation(name:'tealium-contentsquare', ext:'aar')
      }
      ```




## Initialize

For all Tealium libraries, register the Contentsquare remote commands when you initialize.





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
    let contentsquare = ContentsquareRemoteCommand()   

    // Local JSON
    //let contentsquare = ContentsquareRemoteCommand(type: .local(file: "contentsquare")) 

    // Remote JSON
    //let contentsquare = ContentsquareRemoteCommand(type: .remote(url: "https://some.domain.com/contentsquare.json")) 

    remoteCommands.add(contentsquare)
}
```


Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's Android (Kotlin) library:
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Initialize with `Application` to take advantage of consent management and other
    // advanced features
    val contentsquare = ContentsquareRemoteCommand(this);

    // Or for simple tracking, you can initialize without `Application`
    val contentsquare = ContentsquareRemoteCommand();
    // register the command

    // Webview Tag
    remoteCommands?.add(contentsquare); 

    // Local JSON
    //remoteCommands?.add(contentsquare, filename = "contentsquare.json"); 

    // Remote JSON
    //remoteCommands?.add(contentsquare, remoteUrl = "https://some.domain.com/contentsquare.json"); 
```



Initialize remote commands with the Remote Command tag for Tealium's Android (Java) library:  
```java
import com.tealium.remotecommands.contentsquare.ContentsquareRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// Initialize with `Application` to take advantage of consent management and other
// advanced features
ContentsquareRemoteCommand contentsquare = new ContentsquareRemoteCommand(this);

// Or for simple tracking, you can initialize without `Application`
ContentsquareRemoteCommand contentsquare = new ContentsquareRemoteCommand();

// register the command
teal.addRemoteCommand(contentsquare);
```



## JSON Template

If you are configuring remote commands using a [JSON configuration file](https://docs.tealium.com/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
  "config": {},
  "mappings": {
    "screen": "screen_name",
    "dynamic_var": "dynamic_var",
    "user_id": "user_identifier",
    "custom_vars": "custom_vars",
    "price": "purchase.price",
    "currency": "purchase.currency",
    "transaction_id": "purchase.transaction_id"
  },
  "commands": {
    "screen_title": "sendscreenview",
    "dynamic_var": "senddynamicvar",
    "user_identifier": "senduseridentifier",
    "transaction": "sendtransaction",
    "stop_tracking": "stoptracking",
    "resume_tracking": "resumetracking",
    "forget_me": "forgetme",
    "opt_in": "optin",
    "opt_out": "optout"
  }
}
```

## Supported Methods

We map a command to each Contentsquare method. To trigger a Contentsquare method, pass the corresponding command in the specified format.

| Remote Command      | Contentsquare Method  |
| ------------------- | --------------------- |
| `sendscreenview`    | `send()`              |
| `sendtransaction`   | `send()`              |
| `senddynamicvar`    | `send()`              |
| `senduseridentifier`| `sendUserIdentifier()`|
| `stoptracking`      | `stopTracking()`      |
| `resumetracking`    | `resumeTracking()`    |
| `forgetme`          | `forgetMe()`          |
| `optin`             | `optIn()`             |
| `optout`            | `optOut()`            |


<blockquote>
Since the Contentsquare SDK is installed alongside the Tealium SDK, trigger any native Contentsquare functionality given the corresponding tag configuration.
</blockquote>


### SDK Setup

#### Initialize

The Contentsquare SDK is initialized automatically upon launch.

Contentsquare Developer Guide: Initial SDK Setup

- [Android](https://docs.contentsquare.com/android/#add-contentsquare-to-your-app)
- [iOS](https://docs.contentsquare.com/ios/#get-started)

### Track Screens

| Remote Command   | Contentsquare Method |
| ---------------- | -------------------- |
| `sendscreenview` | `send`               |

| Parameter                | Type     |
| ------------------------ | -------- |
| `screen_name` (required) | `String` |
| `custom_vars` (optional) | `Array`  |

**Custom Variables Format:**
Each custom variable object should contain:
- `index` (required): `Int` - The custom variable index
- `name` (required): `String` - The custom variable name  
- `value` (required): `String` - The custom variable value

Contentsquare Developer Guide: Analytics User IDs  

- [Android](https://docs.contentsquare.com/android/#track-screens)
- [iOS](https://docs.contentsquare.com/ios/#track-screens)

### Track Transactions

| Remote Command    | Contentsquare Method |
| ----------------- | -------------------- |
| `sendtransaction` | `send`               |

| Parameter                   | Type              |
| --------------------------- | ----------------- |
| `price` (required)          | `Double or Float` |
| `currency` (required)       | `String`          |
| `transaction_id` (optional) | `String`          |

Contentsquare Developer Guide: Track Transactions  

- [Android](https://docs.contentsquare.com/android/#track-transactions)
- [iOS](https://docs.contentsquare.com/ios/#track-transactions)

### Track Dynamic Variables

| Remote Command    | Contentsquare Method |
| ----------------- | -------------------- |
| `senddynamicvar`  | `send`               |

| Parameter                   | Type              |
| --------------------------- | ----------------- |
| `dynamic_var` (required)    | `Object`          |


<blockquote>
The `dynamic_var` parameter takes a JSON object of key-value pairs, where keys are `strings` and the values are either `UInt32` or `strings`. Examples: `{"my_dynamic_string_var_name": "some string value"}`, `{"my_dynamic_int_var_name": 123}`, `{"my_dynamic_string_var_name": "some string value," "my_dynamic_int_var_name": 123}`.
</blockquote>


Contentsquare Developer Guide: Track Dynamic Variables

- [Android](https://docs.contentsquare.com/android/#track-dynamic-variables)
- [iOS](https://docs.contentsquare.com/ios/#track-dynamic-variables)

### Track User Identifier

| Remote Command       | Contentsquare Method |
| -------------------- | -------------------- |
| `senduseridentifier` | `sendUserIdentifier` |

| Parameter                        | Type     |
| -------------------------------- | -------- |
| `user_identifier` (required)     | `String` |

Contentsquare Developer Guide: Track User Identifier

- [Android](https://docs.contentsquare.com/en/android/session-replay/)
- [iOS](https://docs.contentsquare.com/en/ios/session-replay/)

### Consent Options

#### Stop / Resume Tracking

| Remote Command   | Contentsquare Method |
| ---------------- | -------------------- |
| `stoptracking`   | `stopTracking`       |
| `resumetracking` | `resumeTracking`     |

Contentsquare Developer Guide: Stop / Resume Tracking

- [Android](https://docs.contentsquare.com/android/#stop-resume-tracking)
- [iOS](https://docs.contentsquare.com/ios/#stop-resume-tracking)

#### Opt In

| Remote Command | Contentsquare Method |
| -------------- | -------------------- |
| `optin`        | `optIn`              |

Contentsquare Developer Guide: Opt In

- [Android](https://docs.contentsquare.com/android/#opt-in)
- [iOS](https://docs.contentsquare.com/ios/#opt-in)

#### Opt Out

| Remote Command | Contentsquare Method |
| -------------- | -------------------- |
| `optout`       | `optOut`             |

Contentsquare Developer Guide: Opt Out

- [Android](https://docs.contentsquare.com/android/#opt-out)
- [iOS](https://docs.contentsquare.com/ios/#opt-out)

#### Forget Me

| Remote Command | Contentsquare Method |
| -------------- | -------------------- |
| `forgetme`     | `forgetMe`           |

Contentsquare Developer Guide: Forget Me

- [Android](https://docs.contentsquare.com/android/#forget-me)
- [iOS](https://docs.contentsquare.com/ios/#forget-me)