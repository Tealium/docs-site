---
title: Install
description: Install and initialize the Tealium Prism SDK for Android (Kotlin) and iOS (Swift).
url: https://docs.tealium.com/platforms/prism-mobile/install/
---
## Requirements



* [Android Studio](https://developer.android.com/studio)
* Android SDK (Lollipop/5.0&#43; / API Level 21&#43;)
* [Tealium iQ Mobile Profile]()
* [Tealium account]()


* Xcode 14.0&#43;
* iOS 12.0&#43;, macOS 10.14&#43;, tvOS 12.0&#43;, watchOS 4.0&#43;
* [Tealium iQ Mobile Profile]()
* [Tealium account]()



## Install

The Tealium Prism library is divided into modules. Install only the modules you need to maintain a smaller resource footprint. For a list of available modules, see [Modules]().



### Maven

To install the Tealium Prism Kotlin library with Maven:

1. Add the Tealium Maven URL to your project&#39;s top-level `build.gradle` file:

    ```kotlin
    dependencyResolutionManagement {
        repositories {
            // .. other repos
            maven {
                url = URI(&#34;https://maven.tealiumiq.com/android/releases/&#34;)
            }
        }
    }
    ```

1. In your project module&#39;s `build.gradle` file, add the following dependencies. You only need to specify the version number for the `platform()` entry:

    ```kotlin
    implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
    implementation(&#34;com.tealium.prism:prism-core&#34;)
    implementation(&#34;com.tealium.prism:prism-lifecycle&#34;)
    implementation(&#34;com.tealium.prism:prism-moments-api&#34;)
    ```



### Swift package manager (recommended)

To install Tealium Prism Swift with Swift Package Manager:

1. In your Xcode project, select **File &gt; Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-prism-swift`.
1. Configure the version rules. We recommend using **Up to next major**. If the current Tealium Prism library version does not appear in the list, reset your Swift package cache.
1. Select the modules to install and select the app target you want the modules to be installed in.

### CocoaPods

To install with CocoaPods, add the following line to your Podfile:

```ruby
pod &#39;tealium-prism&#39;
```

### Carthage

To install with Carthage:

1. Add the following to your Cartfile:
    ```bash
    github &#34;tealium/tealium-prism-swift&#34;
    ```
1. To produce frameworks for iOS, macOS, tvOS, and watchOS, run the following command:
    ```sh
    carthage update --use-xcframeworks
    ```
1. Drag the frameworks you require into your Xcode project in the section **General &gt; Embedded Binaries**.



## Initialize




To initialize Tealium, pass a [`TealiumConfig`](/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium-config/) instance to the [`Tealium.create()`](/tealium-prism-kotlin/core/com.tealium.prism.core.api/-instance-manager/) method. We recommend initializing the Tealium Kotlin library in the app&#39;s global application class within the `onCreate()` method.

```kotlin
import com.tealium.prism.core.api.Tealium
import com.tealium.prism.core.api.TealiumConfig

val config = TealiumConfig.Builder(
   accountName = &#34;my_account&#34;,
   profileName = &#34;my_profile&#34;,
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



To initialize Tealium, pass a [`TealiumConfig`](/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html) instance to the [`Tealium.create()`](/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) static method.

We recommend managing your `Tealium` instance with a tracking helper class, which provides a single point of entry for the Tealium iOS library and simplifies future upgrades.

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
import TealiumPrismLifecycle
import TealiumPrismMomentsAPI
#endif

let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
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
                           settingsFile: &#34;my_settings&#34;,
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json&#34;)
let tealium = Tealium.create(config: config)
```

Replace the following placeholders in the code:

* `my_account`: your Tealium account name in lowercase.
* `my_profile`: your Tealium profile name in lowercase.
* `prod`: the environment where you want to initialize Tealium (`dev`, `qa`, or `prod`).



## Configuration

Prism uses a three-tier configuration priority system. Settings are merged in the following priority order:

| Tier | Priority | Description |
| :--- | :--- | :--- |
| Programmatic | 1 (Highest) | Security-critical IDs and environment locks. Cannot be overridden. |
| Remote JSON | 2 | Real-time updates for operational settings such as batch sizes or sampling. |
| Local JSON | 3 (Lowest) | Default fallback settings bundled with the app. |

This priority order ensures that critical or security-sensitive settings cannot be accidentally overridden by lower-priority sources.

### Remote and local settings



Configure remote and local settings using the `TealiumConfig.Builder`:

```kotlin
val config = TealiumConfig.Builder(
   accountName = &#34;my_account&#34;,
   profileName = &#34;my_profile&#34;,
   environment = Environment.PROD,
   modules = listOf(Modules.collect())
).build()
```

Remote settings are fetched automatically based on your account, profile, and environment. The Kotlin SDK resolves the settings URL from these values.


Use the `settingsUrl` parameter to specify a remote settings URL, and the `settingsFile` parameter for a local fallback:

```swift
let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
                           settingsFile: &#34;my_settings&#34;,
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json&#34;)
let tealium = Tealium.create(config: config)
```

If you don&#39;t want to use remote settings, or want a local copy of those settings to provide different defaults, specify a local settings file with `settingsFile` and omit `settingsUrl`.



### Log level



To set the log level, call `setLogLevel()` in the settings of the `TealiumConfig` builder:

```kotlin
val config = TealiumConfig.Builder(...)
  .configureSettings { settings -&gt;
    settings.setLogLevel(LogLevel.WARN)
  }
```

For more information, see [LogLevel](/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html).


To set the log level, call `setMinLogLevel()` in the forced settings builder of the [`TealiumConfig`](/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html):

```swift
var config = TealiumConfig(account: &#34;your_account&#34;,
                           profile: &#34;your_profile&#34;,
                           environment: &#34;dev&#34;,
                           modules: [],
                           settingsFile: nil,
                           settingsUrl: nil,
                           forcingSettings: { builder in
    builder.setMinLogLevel(.trace)
})
```

Available log levels: `.trace`, `.debug`, `.info`, `.warn`, `.error`, `.silent`.



### Module-specific enforced settings



Configure module-specific settings in the `TealiumConfig.Builder`:

```kotlin
val config = TealiumConfig.Builder(
   accountName = &#34;my_account&#34;,
   profileName = &#34;my_profile&#34;,
   environment = Environment.PROD,
   modules = listOf(
        Modules.collect(),
        Modules.lifecycle(),
       )
).configureSettings { settings -&gt;
    settings.setLogLevel(LogLevel.DEBUG)
}.build()
```


Each module can specify additional programmatic configuration using the `Modules.collect { }` closure pattern. Doing so overrides local and remote configuration and cannot be changed remotely.

The following example specifies settings for the Collect module. Other settings not programmatically configured can be updated remotely.

```swift
Modules.collect { enforcedSettings in
    enforcedSettings.setEnabled(true)
        .setOrder(5)
        .setOverrideProfile(&#34;custom_profile&#34;)
        .setOverrideDomain(&#34;custom_domain&#34;)
}
```


