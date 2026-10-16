---
title: Modules
description: A list of the available modules for the Tealium Prism SDK for Kotlin, Swift, and React Native.
url: https://docs.tealium.com/platforms/prism-mobile/modules/
---
The Tealium Prism library uses a modular architecture. Install only the modules you need to maintain a smaller resource footprint. All modules depend on the Core module.

## Available modules



| Module | Package | Description |
| :--- | :--- | :--- |
| Core | `prism-core` | Required. Provides the Tealium instance, configuration, tracking, and data layer. |
| [Lifecycle](https://docs.tealium.com/platforms/prism-mobile/module-list/lifecycle/) | `prism-lifecycle` | Tracks app lifecycle events such as launch, wake, and sleep. |
| [Moments API](https://docs.tealium.com/platforms/prism-mobile/module-list/moments-api/) | `prism-moments-api` | Provides access to real-time visitor profiles from Tealium AudienceStream. |
| [Moments iQ](https://docs.tealium.com/platforms/prism-mobile/module-list/moments-iq/) | — | Configures in-app survey and experience widgets from the Tealium iQ mobile profile. |
| [AppData](https://docs.tealium.com/platforms/prism-mobile/module-list/appdata/) | `prism-appdata` | Collects app-level data such as app name, version, and build number. |
| [Collect](https://docs.tealium.com/platforms/prism-mobile/module-list/collect/) | `prism-collect` | Dispatches events to the Tealium Collect endpoint. |
| [ConnectivityData](https://docs.tealium.com/platforms/prism-mobile/module-list/connectivitydata/) | `prism-connectivity-data` | Collects device connectivity information such as network type. |
| [DeepLink](https://docs.tealium.com/platforms/prism-mobile/module-list/deep-link/) | `prism-deeplink` | Handles deep link URLs and passes deep link data to the data layer. |
| [DeviceData](https://docs.tealium.com/platforms/prism-mobile/module-list/devicedata/) | `prism-device-data` | Collects device information such as model, OS version, and screen resolution. |
| [TimeData](https://docs.tealium.com/platforms/prism-mobile/module-list/timedata/) | `prism-time-data` | Adds timestamp data to tracking calls. |
| Trace | `prism-trace` | Enables trace sessions for debugging and validation. |


| Module | Package | Description |
| :--- | :--- | :--- |
| Core | `TealiumPrismCore` | Required. Provides the Tealium instance, configuration, tracking, and data layer. |
| [Lifecycle](https://docs.tealium.com/platforms/prism-mobile/module-list/lifecycle/) | `TealiumPrismLifecycle` | Tracks app lifecycle events such as launch, wake, and sleep. |
| [Moments API](https://docs.tealium.com/platforms/prism-mobile/module-list/moments-api/) | `TealiumPrismMomentsAPI` | Provides access to real-time visitor profiles from Tealium AudienceStream. |
| [Moments iQ](https://docs.tealium.com/platforms/prism-mobile/module-list/moments-iq/) | — | Configures in-app survey and experience widgets from the Tealium iQ mobile profile. |
| [AppData](https://docs.tealium.com/platforms/prism-mobile/module-list/appdata/) | `TealiumPrismAppData` | Collects app-level data such as app name, version, and build number. |
| [Collect](https://docs.tealium.com/platforms/prism-mobile/module-list/collect/) | `TealiumPrismCollect` | Dispatches events to the Tealium Collect endpoint. |
| [ConnectivityData](https://docs.tealium.com/platforms/prism-mobile/module-list/connectivitydata/) | `TealiumPrismConnectivityData` | Collects device connectivity information such as network type. |
| [DeepLink](https://docs.tealium.com/platforms/prism-mobile/module-list/deep-link/) | `TealiumPrismDeepLink` | Handles deep link URLs and passes deep link data to the data layer. |
| [DeviceData](https://docs.tealium.com/platforms/prism-mobile/module-list/devicedata/) | `TealiumPrismDeviceData` | Collects device information such as model, OS version, and screen resolution. |
| DataLayer | `TealiumPrismDataLayer` | Extended data layer operations and persistence. |
| [TimeData](https://docs.tealium.com/platforms/prism-mobile/module-list/timedata/) | `TealiumPrismTimeData` | Adds timestamp data to tracking calls. |
| Trace | `TealiumPrismTrace` | Enables trace sessions for debugging and validation. |


React Native modules are npm packages. Install only the packages your app needs.

| Module | Package | Description |
| :--- | :--- | :--- |
| Core | `@tealium/prism-react-native` | Required. Wraps the native iOS and Android Prism SDKs. Provides the Tealium instance, tracking, and data layer. |
| Lifecycle | `@tealium/prism-react-native-lifecycle` | Tracks app lifecycle events such as launch, wake, and sleep. |

Module enablement is controlled by your Tealium settings JSON, not by individual packages.



## Install modules



Add the Prism BOM and the modules you need to your `build.gradle` file:

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-core")
implementation("com.tealium.prism:prism-lifecycle")
implementation("com.tealium.prism:prism-collect")
```


Select the modules you need when adding the Swift package dependency, or specify them in your Podfile for CocoaPods.


Install the core package with npm:

```bash
npm install @tealium/prism-react-native
```

To add the Lifecycle module:

```bash
npm install @tealium/prism-react-native-lifecycle
```

Install the native iOS dependencies:

```bash
cd ios && pod install
```



## Configure modules in the UI

SDK modules are available in your Tealium mobile profile as a marketplace, similar to tags. You can add, configure, and manage modules from the UI without changing your app code.

To add a module in the UI:

1. Go to your Tealium mobile profile.
1. Go to **Modules**.
1. Select **Add Module** and choose a module from the marketplace.
1. Configure the module settings.
1. Save and publish your changes.

The SDK picks up the updated module configuration on the next remote settings refresh or app startup.

## Advanced: programmatic module activation

To activate modules programmatically, specify them in your `TealiumConfig` during SDK initialization:


<blockquote>
React Native does not support programmatic module activation. Enable and configure modules in your Tealium mobile profile or settings JSON.
</blockquote>




```kotlin
val config = TealiumConfig.Builder(
    accountName = "my_account",
    profileName = "my_profile",
    environment = Environment.PROD,
    modules = listOf(
        Modules.appData(),
        Modules.collect(),
        Modules.lifecycle(),
    )
).build()
```


```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
import TealiumPrismLifecycle
import TealiumPrismCollect
#endif

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                            Modules.appData(),
                            Modules.collect(),
                            Modules.lifecycle(),
                           ],
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json")
```


