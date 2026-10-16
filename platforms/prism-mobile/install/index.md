---
title: Install
description: Install and initialize the Tealium Prism SDK for Android (Kotlin), iOS (Swift), and React Native.
url: https://docs.tealium.com/platforms/prism-mobile/install/
---
The Tealium Prism SDK is distributed as a set of modules. Install only the modules your app needs, then initialize the SDK with your Tealium account credentials.

## Requirements



* [Android Studio](https://developer.android.com/studio)
* Android SDK (Lollipop/5.0+ / API Level 21+)
* [Tealium iQ Mobile Profile](https://docs.tealium.com/create-mobile-profile/)
* [Tealium account](https://docs.tealium.com/introduction-to-customer-data-hub/)


* Xcode 14.0+
* iOS 12.0+, macOS 10.14+, tvOS 12.0+, watchOS 4.0+
* [Tealium iQ Mobile Profile](https://docs.tealium.com/create-mobile-profile/)
* [Tealium account](https://docs.tealium.com/introduction-to-customer-data-hub/)


* React Native 0.85 with the New Architecture (TurboModules)
* Android API level 24 or later
* iOS 15.1 or later
* [Tealium iQ Mobile Profile](https://docs.tealium.com/create-mobile-profile/)
* [Tealium account](https://docs.tealium.com/introduction-to-customer-data-hub/)



## Install

The Tealium Prism library is divided into modules. Install only the modules you need to maintain a smaller resource footprint. For a list of available modules, see [Modules](https://docs.tealium.com/modules/).



### Maven

To install the Tealium Prism Kotlin library with Maven:

1. Add the Tealium Maven URL to your project's top-level `build.gradle` file:

    ```kotlin
    dependencyResolutionManagement {
        repositories {
            // .. other repos
            maven {
                url = URI("https://maven.tealiumiq.com/android/releases/")
            }
        }
    }
    ```

1. In your project module's `build.gradle` file, add the following dependencies. You only need to specify the version number for the `platform()` entry:

    ```kotlin
    implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
    implementation("com.tealium.prism:prism-core")
    implementation("com.tealium.prism:prism-lifecycle")
    implementation("com.tealium.prism:prism-moments-api")
    ```



### Swift package manager (recommended)

To install Tealium Prism Swift with Swift Package Manager:

1. In your Xcode project, select **File > Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-prism-swift`.
1. Configure the version rules. We recommend using **Up to next major**. If the current Tealium Prism library version does not appear in the list, reset your Swift package cache.
1. Select the modules to install and select the app target you want the modules to be installed in.

### CocoaPods

To install with CocoaPods, add the following line to your Podfile:

```ruby
pod 'tealium-prism'
```

### Carthage

To install with Carthage:

1. Add the following to your Cartfile:
    ```bash
    github "tealium/tealium-prism-swift"
    ```
1. To produce frameworks for iOS, macOS, tvOS, and watchOS, run the following command:
    ```sh
    carthage update --use-xcframeworks
    ```
1. Drag the frameworks you require into your Xcode project in the section **General > Embedded Binaries**.


Install the core package with npm:

```bash
npm install @tealium/prism-react-native
```

To install the Lifecycle module:

```bash
npm install @tealium/prism-react-native-lifecycle
```

Install the native iOS dependencies:

```bash
cd ios && pod install
```

Android requires no additional steps.



## Initialize




To initialize Tealium, pass a [`TealiumConfig`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium-config/) instance to the [`Tealium.create()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-instance-manager/) method. We recommend initializing the Tealium Kotlin library in the app's global application class within the `onCreate()` method.

```kotlin
import com.tealium.prism.core.api.Tealium
import com.tealium.prism.core.api.TealiumConfig

val config = TealiumConfig.Builder(
   accountName = "my_account",
   profileName = "my_profile",
   environment = Environment.PROD,
   modules = listOf(
        Modules.appData(),
        Modules.collect(),
        Modules.connectivityData(),
        Modules.deepLink(),
        Modules.deviceData(),
        Modules.lifecycle(),
        Modules.timeData(),
        Modules.trace(),
       )
).build()
val tealium = Tealium.create(config)
```

Replace the following placeholders in the code:

* `my_account`: your Tealium account name in lowercase.
* `my_profile`: your Tealium profile name in lowercase.
* `Environment.PROD`: the environment where you want to initialize Tealium (`DEV`, `QA`, or `PROD`).



To initialize Tealium, pass a [`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html) instance to the [`Tealium.create()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) static method.


<blockquote>
We recommend managing your `Tealium` instance with a tracking helper class, which provides a single point of entry for the Tealium iOS library and simplifies future upgrades.
</blockquote>


```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
import TealiumPrismLifecycle
import TealiumPrismMomentsAPI
#endif

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                            Modules.appData(),
                            Modules.collect(),
                            Modules.connectivityData(),
                            Modules.deepLink(),
                            Modules.deviceData(),
                            Modules.lifecycle(),
                            Modules.momentsAPI(),
                            Modules.timeData(),
                            Modules.trace(),
                           ],
                           settingsFile: "my_settings",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json")
let tealium = Tealium.create(config: config)
```

Replace the following placeholders in the code:

* `my_account`: your Tealium account name in lowercase.
* `my_profile`: your Tealium profile name in lowercase.
* `prod`: the environment where you want to initialize Tealium (`dev`, `qa`, or `prod`).


To initialize Tealium, call [`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create) with your account, profile, and environment. We recommend creating one instance when the app starts and sharing it across your app.

```javascript
import { Tealium, Environment } from "@tealium/prism-react-native";

const tealium = Tealium.create(
  "my_account",
  "my_profile",
  Environment.prod,
  "my_settings.json",
  "https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json"
);
```

Replace the following placeholders in the code:

* `my_account`: your Tealium account name in lowercase.
* `my_profile`: your Tealium profile name in lowercase.
* `Environment.prod`: the environment where you want to initialize Tealium (`Environment.dev`, `Environment.qa`, or `Environment.prod`).



## Configuration

Prism merges settings from three sources in the following priority order:

| Method | Priority | Use when |
| :--- | :--- | :--- |
| Programmatic | 1 (highest) | Runtime-calculated values or settings that must be locked in code. |
| Remote settings | 2 | Standard operational configuration — modules, barriers, transformations, rules. |
| Local JSON | 3 | Fallback defaults bundled with the app. |

This priority order ensures that critical or security-sensitive settings cannot be accidentally overridden by lower-priority sources.

### Remote and local settings



Configure remote and local settings using the `TealiumConfig.Builder`:

```kotlin
val config = TealiumConfig.Builder(
   accountName = "my_account",
   profileName = "my_profile",
   environment = Environment.PROD,
   modules = listOf(Modules.collect())
).build()
```


<blockquote>
Remote settings are fetched automatically based on your account, profile, and environment. The Kotlin SDK resolves the settings URL from these values.
</blockquote>



Use the `settingsUrl` parameter to specify a remote settings URL, and the `settingsFile` parameter for a local fallback:

```swift
let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           settingsFile: "my_settings",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json")
let tealium = Tealium.create(config: config)
```

If you don't want to use remote settings, or want a local copy of those settings to provide different defaults, specify a local settings file with `settingsFile` and omit `settingsUrl`.


Pass `settingsFile` and `settingsUrl` as the fourth and fifth arguments of `Tealium.create()`. Settings precedence: local file < remote URL < programmatic.

```javascript
const tealium = Tealium.create(
  "my_account",
  "my_profile",
  Environment.prod,
  "my_settings.json",    // local settings file (optional)
  "https://tags.tiqcdn.com/dle/my_account/my_profile/mobile_settings_prod.json" // remote URL (optional)
);
```

To use only a local settings file, omit the `settingsUrl` argument or pass `undefined`.



### Log level



To set the log level, call `setLogLevel()` in the settings of the `TealiumConfig` builder:

```kotlin
val config = TealiumConfig.Builder(...)
  .configureSettings { settings ->
    settings.setLogLevel(LogLevel.WARN)
  }
```

For more information, see [LogLevel](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html).


To set the log level, call `setMinLogLevel()` in the forced settings builder of the [`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html):

```swift
var config = TealiumConfig(account: "your_account",
                           profile: "your_profile",
                           environment: "dev",
                           modules: [],
                           settingsFile: nil,
                           settingsUrl: nil,
                           forcingSettings: { builder in
    builder.setMinLogLevel(.trace)
})
```

Available log levels: `.trace`, `.debug`, `.info`, `.warn`, `.error`, `.silent`.


To set the log level, pass a [`LogLevel`](https://docs.tealium.com/tealium-prism-react-native/types/LogLevel.html) as the sixth argument of [`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create). Pass `undefined` for unused settings arguments:

```javascript
const tealium = Tealium.create(
  "my_account",
  "my_profile",
  Environment.dev,
  undefined,
  undefined,
  "debug" // or "trace", "info", "warn", "error", "silent"
);
```



### Module-specific enforced settings


<blockquote>
React Native does not support programmatic per-module settings. Configure modules in your Tealium mobile profile or settings JSON.
</blockquote>




Configure module-specific settings in the `TealiumConfig.Builder`:

```kotlin
val config = TealiumConfig.Builder(
   accountName = "my_account",
   profileName = "my_profile",
   environment = Environment.PROD,
   modules = listOf(
        Modules.collect(),
        Modules.lifecycle(),
       )
).configureSettings { settings ->
    settings.setLogLevel(LogLevel.DEBUG)
}.build()
```


Each module can specify additional programmatic configuration using the `Modules.collect { }` closure pattern. Doing so overrides local and remote configuration and cannot be changed remotely.

The following example specifies settings for the Collect module. Other settings not programmatically configured can be updated remotely.

```swift
Modules.collect { enforcedSettings in
    enforcedSettings.setEnabled(true)
        .setOrder(5)
        .setOverrideProfile("custom_profile")
        .setOverrideDomain("custom_domain")
}
```


