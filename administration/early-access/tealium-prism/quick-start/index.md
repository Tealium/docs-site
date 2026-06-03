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
            url = URI(&#34;https://maven.tealiumiq.com/android/releases/&#34;)
        }
    }
}
```

In your project module&#39;s `build.gradle` file, add the following dependencies. You only need to specify the version number for the `platform()` entry:

```ruby
implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
implementation(&#34;com.tealium.prism:prism-core&#34;)
implementation(&#34;com.tealium.prism:prism-lifecycle&#34;)
implementation(&#34;com.tealium.prism:prism-moments-api&#34;)  
```



To install Tealium Prism Swift with Swift Package Manager:

1. In your Xcode project, select **File &gt; Swift Packages &gt; Add Package Dependency**.
1. Enter the repository URL: `https://github.com/tealium/tealium-prism-swift`.
1. Configure the version rules. We recommend configuring **Up to next major**. If the current Tealium Prism Swift library version does not appear in the list, reset your Swift package cache.
1. Select the modules to install and add the modules to each of your app targets in your Xcode project, under **Frameworks &gt; Libraries &amp; Embedded Content**.

To install with Cocoapods, add the following line to your podfile:

```ruby
pod &#39;tealium-prism&#39;
```



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

If you don&#39;t want to use remote settings, or want a local copy of those settings to provide different defaults, specify a local settings file:

```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
                           settingsFile: &#34;my_settings&#34;,
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/prod/settings.json&#34;)
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
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json&#34;,
)
let tealium = Tealium.create(config: config)
```

Each module can specify additional programmatic configuration. Doing so overrides local and remote configuration and cannot be changed remotely.
The following example specifies settings for the Collect module. Other settings not programmatically configured can be updated remotely.

```swift
Modules.collect { enforcedSettings in
    enforcedSettings.setEnabled(true)
        .setOrder(5)
        .setOverrideProfile(&#34;custom_profile&#34;)
        .setOverrideDomain(&#34;custom_domain&#34;)
}
```




## Track

To track events, pass an event name and optional type and data to the `track()` method. The name of the event appears in the data layer as `tealium_event`.



To track events, call [track()](/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html).

```kotlin
tealium.track(&#34;user_login&#34;, DataObject.create {
    put(&#34;customer_id&#34;, &#34;1234567890&#34;)
})
```


To track events, call [track()](/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html).

```swift
/// Basic Track with default event type and empty data layer.
tealium.track(&#34;homepage&#34;)

/// Track with full parameters
tealium.track(&#34;user_login&#34;, type: .event, dataLayer: [&#34;customer_id&#34;: &#34;1234567890&#34;])

/// Track with different view type
tealium.track(&#34;homepage&#34;, type: .view)
```



## Data Layer

To add data to the data layer:  



To get a data layer value use the [get()](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) method and subscribe if you need to handle the result or an error:
```kotlin
tealium.dataLayer.getString(&#34;customer_id&#34;).subscribe { result -&gt;
    val customerId = result.getOrNull()
    // do something with customerId
}
```

To set a data layer value use the [put()](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) method:   
```kotlin
tealium.dataLayer.put(&#34;my_string&#34;, &#34;my_string_value&#34;)
```

To set a data layer object use the `DataObject.Builder()`:
```kotlin
val globalContext = DataObject.Builder()
    .put(&#34;customer_id&#34;, &#34;12345&#34;)
    .put(&#34;is_logged_in&#34;, true)
    .put(&#34;consent_status&#34;, &#34;consented&#34;)
    .build()

dataLayer.put(globalContext, Expiry.FOREVER)
```

Use individual `put` operations only when atomicity is not required, because each call runs independently and in sequence. When setting multiple values and timing or consistency is important, use `transactionally` to apply all updates in a single atomic operation so they either all succeed or all fail.

```kotlin
tealium.dataLayer.transactionally { editor -&gt;
    editor.put(&#34;key&#34;, &#34;value&#34;.asDataItem(), Expiry.SESSION)
        .put(&#34;key2&#34;, &#34;value2&#34;.asDataItem(), Expiry.SESSION)
        .remove(&#34;key2&#34;)
        .commit()
}.onFailure {
    Log.d(&#34;DataLayer&#34;, &#34;Transactional update failed: ${it.message}&#34;)
}
```

To set an array value use the `DataList.Builder()`:
```kotlin
val productCategories = DataList.create {
  add(&#34;electronics&#34;)
  add(&#34;headphones&#34;)
}

dataLayer.put(
    key = &#34;product_category&#34;,
    value = productCategories,
    expiry = Expiry.SESSION
).subscribe({ }, { err -&gt; })
```

To set an expiration of the data use `Expiry`:
```kotlin
dataLayer.put(
    key = &#34;currency&#34;,
    value = DataItem(any = &#34;USD&#34;),
    expiry = Expiry.UNTIL_RESTART
)
dataLayer.put(
    key = &#34;order_total&#34;,
    value = 249.95,
    expiry = Expiry.afterTimeUnit(7, TimeUnit.DAYS)
)
```



To get a data layer value, call the [get()](/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method:  
```swift
tealium.dataLayer.get(key: &#34;customer_id&#34;,
                      as: String.self).subscribe { result in
    switch result {
    case .success(let value):
        print(&#34;Optional Value: \(String(describing: value))&#34;)
    case .failure(let error):
        print(&#34;Error: \(error)&#34;)
    }
}
```

To set a data layer value, use the [`put()`](/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method.

```swift
tealium.dataLayer.put(key: &#34;some_key&#34;, value: &#34;some value&#34;)
```

To set a data layer object use the `DataObject()`:

```swift
tealium.dataLayer.put(data: [
    &#34;customer_id&#34;: &#34;12345&#34;,
    &#34;is_logged_in&#34;: true,
    &#34;consent_status&#34;: &#34;consented&#34;,
    &#34;product_category&#34;: [&#34;electronics&#34;, &#34;headphones&#34;, &#34;/early-access/tealium-prism/quick-start&#34;]
])
```

To set an expiration of the data use [`Expiry`](/tealium-prism-swift/TealiumPrismCore/Enums/Expiry.html):
```swift
tealium.dataLayer.put(key: &#34;currency&#34;, 
                      value: &#34;USD&#34;, 
                      expiry: .untilRestart)

tealium.dataLayer.put(key: &#34;order_total&#34;, 
                      value: 249.95, 
                      expiry: .after(Date().advanced(by: 1000)))
```



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


To set the log level, call `setMinLogLevel()` in the settings of the [TealiumConfig builder](/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html):

```swift
var config = TealiumConfig(account: &#34;your_account&#34;,
                           profile: &#34;your_profile&#34;,
                           environment: &#34;dev&#34;,
                           modules: [],
                           settingsFile: nil,
                           settingsUrl: nil,
                           forcingSettings: { builder in
    builder.setMinLogLevel(.trace) // or .debug, .info, .warn, .error, .silent
})
```



### Trace

The [Mobile Trace Tool](/platforms/getting-started-mobile/trace/#mobile-trace-tool) provides a QR code you can scan with your device to view live events from a Tealium mobile SDK.



Learn more about using the [Trace Interface](/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-trace/).

```kotlin
trace.join(&#34;TRACE_ID&#34;)

// Leave the current trace session
trace.leave()

// Force end of visit for testing
trace.forceEndOfVisit()
```


Learn more about using the [Trace Protocol Reference](/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html).

```swift
// Join a trace session
tealium.trace.join(id: &#34;TRACE_ID&#34;)

// Leave the current trace session
tealium.trace.leave()

// Force end of visit for testing
tealium.trace.forceEndOfVisit()
```



### Live events

Use live events [to troubleshoot mobile installations](/platforms/getting-started-mobile/troubleshooting/).

Learn more about [Live events]().
