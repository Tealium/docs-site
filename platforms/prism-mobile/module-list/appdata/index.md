---
title: AppData module
description: Adds information about the app bundle to the data layer.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/appdata/
---
## About the AppData module

The AppData module is a collector that automatically enriches tracking data with essential application metadata. It gathers application-specific information from the app bundle and makes it available to all tracking events.

## Install



Add the `prism-appdata` dependency to your `build.gradle` file:

```kotlin
implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
implementation(&#34;com.tealium.prism:prism-appdata&#34;)
```


The AppData module is included in `TealiumPrismCore`. Add it as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod &#39;tealium-prism/Core&#39;
```

To install the full Prism library instead:

```ruby
pod &#39;tealium-prism&#39;
```



## Initialize

The AppData module initializes automatically when it is configured. No code changes are required for most integrations. Configure the module in the Tealium platform UI, or bundle a local JSON configuration file with your app.

### Advanced: programmatic initialization

To force the module to initialize with default values, even when no platform or local JSON configuration is present, add it to the `modules` list in your `TealiumConfig`. Adding the module to `TealiumConfig` is useful for testing or when you need to set values dynamically at runtime.



```kotlin
val config = TealiumConfig.Builder(
    accountName = &#34;my_account&#34;,
    profileName = &#34;my_profile&#34;,
    environment = Environment.PROD,
    modules = listOf(
        Modules.appData(),
        // other modules...
    )
).build()
```


```swift
let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
                           modules: [
                               Modules.appData(),
                               // other modules...
                           ])
```



## Data layer

The following variables are added to each tracking call while the module is enabled:

| Variable | Description | Example |
| :--- | :--- | :--- |
| `app_build` | Build number of the app | `&#34;42&#34;` |
| `app_memory_usage` | Current app memory usage | `&#34;775 MB&#34;` |
| `app_name` | Application display name (iOS: `CFBundleName`; Android: `android:label`) | `&#34;Digital Velocity&#34;` |
| `app_rdns` | Reverse DNS application ID (iOS: `CFBundleIdentifier`; Android: manifest `package`) | `&#34;com.tealium.digitalvelocity&#34;` |
| `app_uuid` | Random identifier that persists for the lifetime of the app installation. Resets if the app is uninstalled. | `&#34;4AB81234-C2A8-46DE-9AED-7ACE555521E0&#34;` |
| `app_version` | User-facing version of the app | `&#34;1.0.0&#34;` |

