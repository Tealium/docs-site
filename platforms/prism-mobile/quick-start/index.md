---
title: Quick start
description: Set up Tealium Prism for iOS, Android, and React Native by installing the SDK, initializing a configuration, and sending your first events with data layer values.
url: https://docs.tealium.com/platforms/prism-mobile/quick-start/
---
This guide walks you through creating a mobile profile, installing the Prism SDK, initializing a Tealium instance, sending your first tracking call, and validating the results.

## Create a mobile profile

Before you install the SDK, create a mobile profile in Tag Management. For instructions, see [Create a mobile profile](https://docs.tealium.com/create-mobile-profile/).

## Install



To install the Tealium Prism Kotlin library with Maven:

In your Android project, add the following Maven repository:

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

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-core")
implementation("com.tealium.prism:prism-lifecycle")
implementation("com.tealium.prism:prism-moments-api")
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

1. In your Xcode project, select **File > Swift Packages > Add Package Dependency**.
1. Enter the repository URL: `https://github.com/tealium/tealium-prism-swift`.
1. Configure the version rules. We recommend configuring **Up to next major**. If the current Tealium Prism Swift library version does not appear in the list, reset your Swift package cache.
1. Select the modules to install and add the modules to each of your app targets in your Xcode project, under **Frameworks > Libraries & Embedded Content**.

To install with CocoaPods, add the following line to your Podfile:

```ruby
pod 'tealium-prism'
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


Tealium Prism React Native requires React Native 0.85 with the New Architecture (TurboModules).

To install the Tealium Prism React Native library with npm:

```bash
npm install @tealium/prism-react-native @tealium/prism-react-native-lifecycle
```

To install with Yarn instead:

```bash
yarn add @tealium/prism-react-native @tealium/prism-react-native-lifecycle
```

To install the native iOS dependencies:

```bash
cd ios && pod install
```

Android requires no additional steps.



For detailed installation instructions including CocoaPods, Carthage, and manual installation, see [Install](https://docs.tealium.com/install/).

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

To configure the SDK programmatically and enable specific modules, add the modules to the configuration:

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



To initialize Tealium, call [`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create) with your account, profile, and [environment](https://docs.tealium.com/tealium-prism-react-native/variables/Environment.html). We recommend creating one instance when the app starts and sharing it across your app.

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

On iOS, add the settings file to your app target. On Android, put the settings file in `android/app/src/main/assets/`.

The installed packages and your Tealium settings decide which modules run.



For more details on configuration options, see [Install](https://docs.tealium.com/install/).

## Track

To track events, pass an event name and optional type and data to the `track()` method. The name of the event appears in the data layer as `tealium_event`.



To track events, call [`track()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api/-tealium/track.html).

```kotlin
tealium.track("user_login", DataObject.create {
    put("customer_id", "1234567890")
})
```


To track events, call [`track()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/Tealium.html).

```swift
// Basic track with default event type and empty data layer
tealium.track("homepage")

// Track with full parameters
tealium.track("user_login", type: .event, dataLayer: ["customer_id": "1234567890"])

// Track with view type
tealium.track("homepage", type: .view)
```


To track events, call [`track()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#track). `track()` returns a Promise that rejects if the SDK cannot serialize the data.

```javascript
// Track an event with the default type.
await tealium.track("homepage");

// Track an event with data.
await tealium.track("user_login", "event", { customer_id: "1234567890" });

// Track a view.
await tealium.track("homepage", "view");
```



For more details on tracking, see [Track](https://docs.tealium.com/track/).

## Data layer


To add data to the data layer:



To set a data layer value, use the [`put()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/put.html) method:

```kotlin
tealium.dataLayer.put("my_string", "my_string_value")
```

To get a data layer value, use the [`get()`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-data-layer/get.html) method and subscribe to handle the result:

```kotlin
tealium.dataLayer.getString("customer_id").subscribe { result ->
    val customerId = result.getOrNull()
    // do something with customerId
}
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


To get a data layer value, call the [`get()`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html) method:
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

To set multiple data layer values at once, pass a dictionary to [`put(data:)`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DataLayer.html):

```swift
tealium.dataLayer.put(data: [
    "customer_id": "12345",
    "is_logged_in": true,
    "consent_status": "consented",
    "product_category": ["electronics", "headphones"]
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



To get a data layer value, call [`get()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#get) on [`tealium.dataLayer`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#datalayer):

```javascript
const customerId = await tealium.dataLayer.get("customer_id");
```

To set a data layer value, call [`put()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#put):

```javascript
await tealium.dataLayer.put("my_string", "my_string_value");
```

To set several values in one call, pass a plain object to [`putAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#putall):

```javascript
await tealium.dataLayer.putAll({
  customer_id: "12345",
  is_logged_in: true,
  consent_status: "consented",
  product_category: ["electronics", "headphones"],
});
```

To set an expiration of the data, pass an [expiry](https://docs.tealium.com/tealium-prism-react-native/types/Expiry.html) as the last argument:

```javascript
await tealium.dataLayer.put("currency", "USD", "untilRestart"); // or "session", "forever"

const sevenDays = 7 * 24 * 60 * 60 * 1000;
await tealium.dataLayer.put("order_total", 249.95, new Date(Date.now() + sevenDays));
```

To get every data layer value, call [`getAll()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#getall):

```javascript
const data = await tealium.dataLayer.getAll();
```

To remove data layer values, call [`remove()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#remove) with a key or an array of keys:

```javascript
await tealium.dataLayer.remove("customer_id");
await tealium.dataLayer.remove(["is_logged_in", "consent_status"]);
```

To remove every data layer value, call [`clear()`](https://docs.tealium.com/tealium-prism-react-native/interfaces/DataLayer.html#clear):

```javascript
await tealium.dataLayer.clear();
```



For more details on the data layer, see [Data layer](https://docs.tealium.com/data-layer/).

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


To set the log level, call `setMinLogLevel()` in the settings of the [`TealiumConfig` builder](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CoreSettingsBuilder.html):

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


To set the log level, pass a [`LogLevel`](https://docs.tealium.com/tealium-prism-react-native/types/LogLevel.html) as the sixth argument of [`Tealium.create()`](https://docs.tealium.com/tealium-prism-react-native/classes/Tealium.html#create). Pass `undefined` for the settings arguments that you do not use:

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



### Trace

The [Mobile Trace Tool](https://docs.tealium.com/platforms/getting-started-mobile/debug-with-trace/) provides a QR code you can scan with your device to view live events from a Tealium mobile SDK.



Learn more about using the [Trace interface](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.modules/-trace/).

```kotlin
trace.join("TRACE_ID")

// Leave the current trace session
trace.leave()

// Force end of visit for testing
trace.forceEndOfVisit()
```


Learn more about using the [Trace protocol reference](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html).

```swift
// Join a trace session
tealium.trace.join(id: "TRACE_ID")

// Leave the current trace session
tealium.trace.leave()

// Force end of visit for testing
tealium.trace.forceEndOfVisit()
```


Learn more about using the [Trace interface](https://docs.tealium.com/tealium-prism-react-native/interfaces/Trace.html).

```javascript
// Join a trace session.
await tealium.trace.join("TRACE_ID");

// Force end of visit for testing.
await tealium.trace.forceEndOfVisit();

// Leave the current trace session.
await tealium.trace.leave();
```

To use these calls, enable the Trace module in your Tealium settings. Otherwise, the Promise rejects.



### Live events

Use live events [to troubleshoot mobile installations](https://docs.tealium.com/platforms/getting-started-mobile/troubleshooting/).

Learn more about [Live events](https://docs.tealium.com/about-live-events/).
