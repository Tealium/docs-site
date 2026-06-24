---
title: Quick start
description: Set up Tealium Prism for iOS and Android by installing the SDK, initializing a configuration, and sending your first events with data layer values.
url: https://docs.tealium.com/platforms/prism-mobile/quick-start/
---
This guide walks you through installing the Prism SDK, initializing a Tealium instance, sending your first tracking call, and validating the results.

## Install



To install the Tealium Prism Kotlin library with Maven:

In your Android project, add the following Maven repository:

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

In your project module&#39;s `build.gradle` file, add the following dependencies. You only need to specify the version number for the `platform()` entry:

```kotlin
implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
implementation(&#34;com.tealium.prism:prism-core&#34;)
implementation(&#34;com.tealium.prism:prism-lifecycle&#34;)
implementation(&#34;com.tealium.prism:prism-moments-api&#34;)
```

The following Prism Kotlin modules are available as individual dependencies:

* `prism-core` (required)
* `prism-lifecycle`
* `prism-moments-api`
* `prism-appdata`
* `prism-collect`
* `prism-connectivity-data`
* `prism-deeplink`
* `prism-device-data`
* `prism-time-data`
* `prism-trace`



To install Tealium Prism Swift with Swift Package Manager:

1. In your Xcode project, select **File &gt; Swift Packages &gt; Add Package Dependency**.
1. Enter the repository URL: `https://github.com/tealium/tealium-prism-swift`.
1. Configure the version rules. We recommend configuring **Up to next major**. If the current Tealium Prism Swift library version does not appear in the list, reset your Swift package cache.
1. Select the modules to install and add the modules to each of your app targets in your Xcode project, under **Frameworks &gt; Libraries &amp; Embedded Content**.

To install with CocoaPods, add the following line to your Podfile:

```ruby
pod &#39;tealium-prism&#39;
```

The following Prism Swift modules are available as individual dependencies:

* `TealiumPrismCore` (required)
* `TealiumPrismLifecycle`
* `TealiumPrismMomentsAPI`
* `TealiumPrismAppData`
* `TealiumPrismCollect`
* `TealiumPrismConnectivityData`
* `TealiumPrismDeepLink`
* `TealiumPrismDeviceData`
* `TealiumPrismDataLayer`
* `TealiumPrismTimeData`
* `TealiumPrismTrace`



For detailed installation instructions including CocoaPods, Carthage, and manual installation, see [Install]().

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



To initialize Tealium, pass a [`TealiumConfig`](/tealium-prism-swift/TealiumPrismCore/Structs/TealiumConfig.html) instance to the [`Tealium.create()`](/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html) static method.

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json&#34;)
let tealium = Tealium.create(config: config)
```

To configure the SDK programmatically and enable specific modules, add the modules to the configuration:

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



For more details on configuration options, see [Install]().

## Track

To track events, pass an event name and optional type and data to the `track()` method. The name of the event appears in the data layer as `tealium_event`.



To track events, call [`track()`](/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html).

```kotlin
tealium.track(&#34;user_login&#34;, DataObject.create {
    put(&#34;customer_id&#34;, &#34;1234567890&#34;)
})
```


To track events, call [`track()`](/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html).

```swift
// Basic track with default event type and empty data layer
tealium.track(&#34;homepage&#34;)

// Track with full parameters
tealium.track(&#34;user_login&#34;, type: .event, dataLayer: [&#34;customer_id&#34;: &#34;1234567890&#34;])

// Track with view type
tealium.track(&#34;homepage&#34;, type: .view)
```



For more details on tracking, see [Track]().

## Data layer

To add data to the data layer:



To set a data layer value, use the [`put()`](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) method:

```kotlin
tealium.dataLayer.put(&#34;my_string&#34;, &#34;my_string_value&#34;)
```

To get a data layer value, use the [`get()`](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) method and subscribe to handle the result:

```kotlin
tealium.dataLayer.getString(&#34;customer_id&#34;).subscribe { result -&gt;
    val customerId = result.getOrNull()
    // do something with customerId
}
```


To set a data layer value, use the [`put()`](/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method:

```swift
tealium.dataLayer.put(key: &#34;some_key&#34;, value: &#34;some value&#34;)
```

To get a data layer value, call the [`get()`](/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method:

```swift
tealium.dataLayer.get(key: &#34;customer_id&#34;,
                      as: String.self).subscribe { result in
    switch result {
    case .success(let value):
        print(&#34;Value: \(String(describing: value))&#34;)
    case .failure(let error):
        print(&#34;Error: \(error)&#34;)
    }
}
```



For more details on the data layer, see [Data layer]().

## Validate

Validate your data by inspecting log files, running a trace, and viewing live events.

### Logs



To set the log level, call `setLogLevel()` in the settings of the `TealiumConfig` builder:

```kotlin
val config = TealiumConfig.Builder(...)
  .configureSettings { settings -&gt;
    settings.setLogLevel(LogLevel.WARN)
  }
```

For more information, see [LogLevel](/tealium-prism-kotlin/core/com.tealium.prism.core.api.logger/-log-level/index.html).


To set the log level, call `setMinLogLevel()` in the settings of the [`TealiumConfig` builder](/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html):

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



### Trace

The [Mobile Trace Tool]() provides a QR code you can scan with your device to view live events from a Tealium mobile SDK.



Learn more about using the [Trace interface](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-trace/).

```kotlin
trace.join(&#34;TRACE_ID&#34;)

// Leave the current trace session
trace.leave()

// Force end of visit for testing
trace.forceEndOfVisit()
```


Learn more about using the [Trace protocol reference](/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html).

```swift
// Join a trace session
tealium.trace.join(id: &#34;TRACE_ID&#34;)

// Leave the current trace session
tealium.trace.leave()

// Force end of visit for testing
tealium.trace.forceEndOfVisit()
```



### Live events

Use live events [to troubleshoot mobile installations]().

Learn more about [Live events]().
