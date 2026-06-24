---
title: Modules
description: A list of the available modules for the Tealium Prism SDK for Kotlin and Swift.
url: https://docs.tealium.com/platforms/prism-mobile/modules/
---
The Tealium Prism library uses a modular architecture. Install only the modules you need to maintain a smaller resource footprint. All modules depend on the Core module.

## Available modules



| Module | Dependency | Description |
| :--- | :--- | :--- |
| Core | `prism-core` | Required. Provides the Tealium instance, configuration, tracking, and data layer. |
| [Lifecycle](/platforms/prism-mobile/module-list/lifecycle/) | `prism-lifecycle` | Tracks app lifecycle events such as launch, wake, and sleep. |
| [Moments API](/platforms/prism-mobile/module-list/moments-api/) | `prism-moments-api` | Provides access to real-time visitor profiles from Tealium AudienceStream. |
| [AppData](/platforms/prism-mobile/module-list/appdata/) | `prism-appdata` | Collects app-level data such as app name, version, and build number. |
| [Collect](/platforms/prism-mobile/module-list/collect/) | `prism-collect` | Dispatches events to the Tealium Collect endpoint. |
| [ConnectivityData](/platforms/prism-mobile/module-list/connectivitydata/) | `prism-connectivity-data` | Collects device connectivity information such as network type. |
| [DeepLink](/platforms/prism-mobile/module-list/deep-link/) | `prism-deeplink` | Handles deep link URLs and passes deep link data to the data layer. |
| [DeviceData](/platforms/prism-mobile/module-list/devicedata/) | `prism-device-data` | Collects device information such as model, OS version, and screen resolution. |
| [TimeData](/platforms/prism-mobile/module-list/timedata/) | `prism-time-data` | Adds timestamp data to tracking calls. |
| Trace | `prism-trace` | Enables trace sessions for debugging and validation. |


| Module | Package | Description |
| :--- | :--- | :--- |
| Core | `TealiumPrismCore` | Required. Provides the Tealium instance, configuration, tracking, and data layer. |
| [Lifecycle](/platforms/prism-mobile/module-list/lifecycle/) | `TealiumPrismLifecycle` | Tracks app lifecycle events such as launch, wake, and sleep. |
| [Moments API](/platforms/prism-mobile/module-list/moments-api/) | `TealiumPrismMomentsAPI` | Provides access to real-time visitor profiles from Tealium AudienceStream. |
| [AppData](/platforms/prism-mobile/module-list/appdata/) | `TealiumPrismAppData` | Collects app-level data such as app name, version, and build number. |
| [Collect](/platforms/prism-mobile/module-list/collect/) | `TealiumPrismCollect` | Dispatches events to the Tealium Collect endpoint. |
| [ConnectivityData](/platforms/prism-mobile/module-list/connectivitydata/) | `TealiumPrismConnectivityData` | Collects device connectivity information such as network type. |
| [DeepLink](/platforms/prism-mobile/module-list/deep-link/) | `TealiumPrismDeepLink` | Handles deep link URLs and passes deep link data to the data layer. |
| [DeviceData](/platforms/prism-mobile/module-list/devicedata/) | `TealiumPrismDeviceData` | Collects device information such as model, OS version, and screen resolution. |
| DataLayer | `TealiumPrismDataLayer` | Extended data layer operations and persistence. |
| [TimeData](/platforms/prism-mobile/module-list/timedata/) | `TealiumPrismTimeData` | Adds timestamp data to tracking calls. |
| Trace | `TealiumPrismTrace` | Enables trace sessions for debugging and validation. |



## Install modules



Add the Prism BOM and the modules you need to your `build.gradle` file:

```kotlin
implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
implementation(&#34;com.tealium.prism:prism-core&#34;)
implementation(&#34;com.tealium.prism:prism-lifecycle&#34;)
implementation(&#34;com.tealium.prism:prism-collect&#34;)
```


Select the modules you need when adding the Swift package dependency, or specify them in your Podfile for CocoaPods.



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



```kotlin
val config = TealiumConfig.Builder(
    accountName = &#34;my_account&#34;,
    profileName = &#34;my_profile&#34;,
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

let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
                           modules: [
                            Modules.appData(),
                            Modules.collect(),
                            Modules.lifecycle(),
                           ],
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json&#34;)
```


