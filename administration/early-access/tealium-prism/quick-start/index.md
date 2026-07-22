---
title: Quick start guide for Tealium Prism
description: Set up Tealium Prism for iOS and Android by installing the SDK, initializing a configuration, and sending your first events with data layer values.
url: https://docs.tealium.com/administration/early-access/tealium-prism/quick-start/
---
## Install



To install the Tealium Prism Kotlin library with Maven:

In your Android project, add the following maven repository:

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

In your project module's `build.gradle` file, add the following dependencies. You only need to specify the version number for the `platform()` entry:

```ruby
implementation(platform("com.tealium.prism:prism-bom:0.4.0"))
implementation("com.tealium.prism:prism-core")
implementation("com.tealium.prism:prism-lifecycle")
implementation("com.tealium.prism:prism-moments-api")  
```



To install Tealium Prism Swift with Swift Package Manager:

1. In your Xcode project, select **File > Swift Packages > Add Package Dependency**.
1. Enter the repository URL: `https://github.com/tealium/tealium-prism-swift`.
1. Configure the version rules. We recommend configuring **Up to next major**. If the current Tealium Prism Swift library version does not appear in the list, reset your Swift package cache.
1. Select the modules to install and add the modules to each of your app targets in your Xcode project, under **Frameworks > Libraries & Embedded Content**.

To install with Cocoapods, add the following line to your podfile:

```ruby
pod 'tealium-prism'
```



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



To initialize Tealium, pass a [`TealiumConfig`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html) instance to the [`Tealium.create()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) static method.

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json")
let tealium = Tealium.create(config: config)
```

If you don't want to use remote settings, or want a local copy of those settings to provide different defaults, specify a local settings file:

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           settingsFile: "my_settings",
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json")
let tealium = Tealium.create(config: config)
```

To configure the entire SDK programmatically, enable specific modules by default, or modify module settings, add the modules to the configuration:

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
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json",
)
let tealium = Tealium.create(config: config)
```

Each module can specify additional programmatic configuration. Doing so overrides local and remote configuration and cannot be changed remotely.
The following example specifies settings for the Collect module. Other settings not programmatically configured can be updated remotely.

```swift
Modules.collect { enforcedSettings in
    enforcedSettings.setEnabled(true)
        .setOrder(5)
        .setOverrideProfile("custom_profile")
        .setOverrideDomain("custom_domain")
}
```




## Track

To track events, pass an event name and optional type and data to the `track()` method. The name of the event appears in the data layer as `tealium_event`.



To track events, call [track()](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html).

```kotlin
tealium.track("user_login", DataObject.create {
    put("customer_id", "1234567890")
})
```


To track events, call [track()](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html).

```swift
/// Basic Track with default event type and empty data layer.
tealium.track("homepage")

/// Track with full parameters
tealium.track("user_login", type: .event, dataLayer: ["customer_id": "1234567890"])

/// Track with different view type
tealium.track("homepage", type: .view)
```



## Data Layer

To add data to the data layer:  



To get a data layer value use the [get()](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) method and subscribe if you need to handle the result or an error:
```kotlin
tealium.dataLayer.getString("customer_id").subscribe { result ->
    val customerId = result.getOrNull()
    // do something with customerId
}
```

To set a data layer value use the [put()](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) method:   
```kotlin
tealium.dataLayer.put("my_string", "my_string_value")
```

To set a data layer object use the `DataObject.Builder()`:
```kotlin
val globalContext = DataObject.Builder()
    .put("customer_id", "12345")
    .put("is_logged_in", true)
    .put("consent_status", "consented")
    .build()

dataLayer.put(globalContext, Expiry.FOREVER)
```

Use individual `put` operations only when atomicity is not required, because each call runs independently and in sequence. When setting multiple values and timing or consistency is important, use `transactionally` to apply all updates in a single atomic operation so they either all succeed or all fail.

```kotlin
tealium.dataLayer.transactionally { editor ->
    editor.put("key", "value".asDataItem(), Expiry.SESSION)
        .put("key2", "value2".asDataItem(), Expiry.SESSION)
        .remove("key2")
        .commit()
}.onFailure {
    Log.d("DataLayer", "Transactional update failed: ${it.message}")
}
```

To set an array value use the `DataList.Builder()`:
```kotlin
val productCategories = DataList.create {
  add("electronics")
  add("headphones")
}

dataLayer.put(
    key = "product_category",
    value = productCategories,
    expiry = Expiry.SESSION
).subscribe({ }, { err -> })
```

To set an expiration of the data use `Expiry`:
```kotlin
dataLayer.put(
    key = "currency",
    value = DataItem(any = "USD"),
    expiry = Expiry.UNTIL_RESTART
)
dataLayer.put(
    key = "order_total",
    value = 249.95,
    expiry = Expiry.afterTimeUnit(7, TimeUnit.DAYS)
)
```



To get a data layer value, call the [get()](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method:  
```swift
tealium.dataLayer.get(key: "customer_id",
                      as: String.self).subscribe { result in
    switch result {
    case .success(let value):
        print("Optional Value: \(String(describing: value))")
    case .failure(let error):
        print("Error: \(error)")
    }
}
```

To set a data layer value, use the [`put()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method.

```swift
tealium.dataLayer.put(key: "some_key", value: "some value")
```

To set a data layer object use the `DataObject()`:

```swift
tealium.dataLayer.put(data: [
    "customer_id": "12345",
    "is_logged_in": true,
    "consent_status": "consented",
    "product_category": ["electronics", "headphones", "/early-access/tealium-prism/quick-start"]
])
```

To set an expiration of the data use [`Expiry`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Enums/Expiry.html):
```swift
tealium.dataLayer.put(key: "currency", 
                      value: "USD", 
                      expiry: .untilRestart)

tealium.dataLayer.put(key: "order_total", 
                      value: 249.95, 
                      expiry: .after(Date().advanced(by: 1000)))
```



## Validate

Validate your data by inspecting log files, running a trace, and viewing live events.

### Logs



To set the log level, call `setLogLevel()` in the settings of the `TealiumConfig` builder:

```kotlin
val config = TealiumConfig.Builder(...)
  .configureSettings { settings ->
    settings.setLogLevel(LogLevel.WARN)
  }
```

For more information, see [LogLevel](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html).


To set the log level, call `setMinLogLevel()` in the settings of the [TealiumConfig builder](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html):

```swift
var config = TealiumConfig(account: "your_account",
                           profile: "your_profile",
                           environment: "dev",
                           modules: [],
                           settingsFile: nil,
                           settingsUrl: nil,
                           forcingSettings: { builder in
    builder.setMinLogLevel(.trace) // or .debug, .info, .warn, .error, .silent
})
```



### Trace

The [Mobile Trace Tool](https://docs.tealium.com/platforms/getting-started-mobile/trace/#mobile-trace-tool) provides a QR code you can scan with your device to view live events from a Tealium mobile SDK.



Learn more about using the [Trace Interface](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-trace/).

```kotlin
trace.join("TRACE_ID")

// Leave the current trace session
trace.leave()

// Force end of visit for testing
trace.forceEndOfVisit()
```


Learn more about using the [Trace Protocol Reference](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html).

```swift
// Join a trace session
tealium.trace.join(id: "TRACE_ID")

// Leave the current trace session
tealium.trace.leave()

// Force end of visit for testing
tealium.trace.forceEndOfVisit()
```



### Live events

Use live events [to troubleshoot mobile installations](https://docs.tealium.com/platforms/getting-started-mobile/troubleshooting/).

Learn more about [Live events](https://docs.tealium.com/about-live-events/).
