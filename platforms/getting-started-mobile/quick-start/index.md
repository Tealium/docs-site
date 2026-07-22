---
title: Quick Start Guide for Mobile
url: https://docs.tealium.com/platforms/getting-started-mobile/quick-start/
---
## Install

Get started with installing Tealium for [Android](https://docs.tealium.com/platforms/android-java/install) or [iOS](https://docs.tealium.com/platforms/ios-swift/install).



To install Tealium for Android library with Maven:

1. Add the Tealium Maven URL to your project's top-level `build.gradle` file:

      ```ruby
      allprojects {
            repositories {
              mavenCentral()
              maven {
                url "https://maven.tealiumiq.com/android/releases/"
              }
            }
      }
      ```

2. In your project module's `build.gradle` file, add the following Maven dependency:

      ```ruby
      dependencies {
            implementation 'com.tealium:kotlin-core:1.X.X'
      }
      ```

<blockquote>
Check for the latest releases on [Github](https://github.com/tealium/tealium-kotlin/releases) and replace 1.X.X with the latest release number.
</blockquote>




To install Tealium for iOS library with Swift Package Manager:

1. In your Xcode project, select **File > Swift Packages > Add Package Dependency**
2. Enter the repository URL: `https://github.com/tealium/tealium-swift`
3. Configure the version rules. Typically, **Up to next major** is recommended. If the current Tealium Swift library version does not appear in the list, then reset your Swift package cache.
4. Select the modules to install and add the modules to each of your app targets in your Xcode project, under **Frameworks > Libraries & Embedded Content**



## Initialize

Get started with initializing Tealium for [Android](https://docs.tealium.com/platforms/android-java/install/#initialize) or [iOS](https://docs.tealium.com/platforms/ios-swift/install/#initialize).




To initialize Tealium, configure a [`TealiumConfig`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/) instance and pass it into a [`Tealium`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/) instance. It's recommended to initialize the Tealium Kotlin library in the app's global application class within the `onCreate()` method.


<blockquote>
Manage your [`Tealium`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#class-tealium) instance by using a tracking helper class, which provides a single point of entry for the Tealium Kotlin library and simplifies future upgrades.
</blockquote>


```kotlin
object TealiumHelper {

  lateinit var tealium: Tealium

  fun init(application: Application) {
    val tealiumConfig = TealiumConfig(
                      application,
                      "ACCOUNT",
                      "PROFILE",
                      Environment.DEV,
                      dataSourceId = "DATASOURCE_ID",  //optional
                      modules = mutableSetOf(VisitorService),
                      dispatchers = mutableSetOf(TagManagement, Collect)
                    )
    tealium = Tealium.create("tealium_instance", tealiumConfig)
  }
}
```




To initialize Tealium, pass a [`TealiumConfig`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/) instance to the [`Tealium()`](https://docs.tealium.com/platforms/ios-swift/api/tealium/#tealium) constructor.


<blockquote>
Manage your [`Tealium`](https://docs.tealium.com/platforms/ios-swift/api/tealium/#class-tealium) instance by using a tracking helper class, which provides a single point of entry for the Tealium iOS library and simplifies future upgrades.
</blockquote>


```swift
class TealiumHelper {
    static let shared = TealiumHelper()
    let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")
    var tealium: Tealium?

    private init() {

        // add necessary config options
        config.batchingEnabled = true
        config.logLevel = .debug

        // add the Collectors you want - no need to include if want all compiled collectors
        config.collectors = [Collectors.Lifecycle,
                             Collectors.Location,
                             Collectors.VisitorService]

        // add the Dispatchers you want - no need to include if want compiled dispatchers
        config.dispatchers = [Dispatchers.TagManagement,
                              Dispatchers.RemoteCommands]

        tealium = Tealium(config: config)

        // optional post init processing
        tealium?.dataLayer.add("mykey", "myvalue", expiry: .forever)

    }

    public func start() {
        _ = TealiumHelper.shared
    }

    class func trackView(title: String, data: [String: Any]?) {    
      let tealView = TealiumView(title, dataLayer: data)
      TealiumHelper.shared.tealium?.track(tealView)
    }

    class func trackEvent(title: String, data: [String: Any]?) {
      let tealEvent = TealiumEvent(title, dataLayer: data)
      TealiumHelper.shared.tealium?.track(tealEvent)
    }
}
```


<blockquote>
Mobile Publish Settings are enabled by default, and must be disabled if you don’t want to use them. Configure the Mobile Publish Settings in iQ Tag Management, or disable them using `config.shouldUseRemotePublishSettings = false`.
</blockquote>





## Track

Get started with tracking views and events for [Android](https://docs.tealium.com/platforms/android-kotlin/track/) or [iOS](https://docs.tealium.com/platforms/ios-swift/track/).

### Track Views

To track screen views, pass an instance of `TealiumView(viewName:dataLayer:)` to the `track()` method.  `TealiumView` is comprised of a view name, which appears in the data layer as `tealium_event`, and an optional data dictionary.



To track views:  
```kotlin
val tealView = TealiumView("screen_view", mutableMapOf("screen_name" to "Home"))
tealium.track(tealView);
```



To track views:  
```swift
let tealView = TealiumView("screen_view", dataLayer: ["screen_name": "Home"])
tealium?.track(tealView)
```




### Track Events

To track non-view events, pass an instance of `TealiumEvent(eventName:dataLayer:)` to the `track()` method.  `TealiumEvent` is comprised of an event name, which appears in the data layer as `tealium_event`, and an optional data dictionary.



To track events:  
```kotlin
val tealEvent = TealiumEvent("user_login", mutableMapOf("customer_id" to "1234567890"))
tealium.track(tealEvent);
```



To track events:  
```swift
let tealEvent = TealiumEvent("user_login", dataLayer: ["customer_id": "1234567890"])
tealium?.track(tealEvent)
```

The [`track()`](https://docs.tealium.com/platforms/ios-swift/api/tealium/#track) method tracks an event by accepting a `TealiumDispatch` of type `TealiumEvent`, which is comprised of an event name and an optional data dictionary.




## Data Layer

Get started managing common data layer values and the data provided by each module for [Android](https://docs.tealium.com/platforms/android-kotlin/data-layer/) or [iOS](https://docs.tealium.com/platforms/ios-swift/data-layer/).

To add data to the data layer:  



To set a `String` value use the [putString()](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#putstring) method:   
```kotlin
tealium.dataLayer.putString("my_string", "my_string_value")
```

Similarly for different data types, the method begins with `put`, such as [putInt()](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#putint) for integers and [putDoubleArray()](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#getdoublearray) for an array of floating-point numbers. Learn more about methods for different [data type](https://docs.tealium.com/platforms/android-kotlin/data-layer/#data-types).

To set a `String` value to expire after 1 day:  
```kotlin
tealium.dataLayer.putString("my_string", "my_string_value", Expiry.afterTimeUnit(1, TimeUnit.DAYS))
```

Learn more about the [expiration types](https://docs.tealium.com/platforms/android-kotlin/data-layer/#data-expiration).


To set a value of any type, use the [`add()`](https://docs.tealium.com/platforms/ios-swift/api/tealium-data-layer/#add) method:  
```swift
tealium.dataLayer.add(key: "my_value", value: 123456)
```

To set a value of any type to expire after 1 day:  
```swift
tealium?.dataLayer.add(key: "my_value", value: 123456, expiry: .afterCustom((.days, 1)))
```





## Identity Resolution

Learn how to use the Tealium anonymous ID and set your own user identifiers.

### Anonymous ID

The Tealium library generates a unique persistent anonymous ID the first time the app is launched. The value is stored in `visitorId`. This value is included in each tracked event as the attribute `tealium_visitor_id`.



To get the visitor ID:  
```kotlin
class TealiumHelper {
	lateinit var tealium: Tealium

    fun getVisitorId(): String {
        return tealium.visitorId
    }
}
```


To get the visitor ID:  
```swift
class TealiumHelper {
	var tealium: Tealium?

    var visitorId: String? {
		tealium?.visitorId
	}
}
```



If you are using Tealium AudienceStream, `visitorId` is the anonymous ID associated with the visitor. Learn more about [anonymous IDs in AudienceStream](https://docs.tealium.com/anonymous-user-visitor-id-attributes/).

### User Identifier

When you identify known users, add a user identifier attribute to the persistent data storage.

Learn more about [user identifiers in AudienceStream](https://docs.tealium.com/anonymous-user-visitor-id-attributes/).



To add a user identifier, such as a customer ID:  
```kotlin
fun setKnownVisitorId(id: String) {
    tealium.dataLayer.putString("customer_id", id, Expiry.FOREVER)
}
```


To add a user identifier, such as a customer ID:  
```swift
func setKnownVisitorId(_ id: String) {
	tealium?.dataLayer.add(key: "customer_id", value: id, expiry: .forever)
}
```



## Validate

Validate your data by inspecting log files, running a trace, and viewing live events.

### Logs

Get started with logging for [Android](https://docs.tealium.com/platforms/android-kotlin/install/#log-level) or [iOS](https://docs.tealium.com/platforms/ios-swift/install/#log-level).



To set the log level, set the [`logLevel`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#loglevel) property:

```kotlin
Logger.logLevel = LogLevel.DEV // or LogLevel.QA, LogLevel.PROD
```


To set the log level, set the [`logLevel`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#loglevel) property:

```swift
config.logLevel = .debug // or .info, .error, .fault, .silent
```



### Trace

Get started with [trace](https://docs.tealium.com/platforms/getting-started-mobile/trace/) for [Android](https://docs.tealium.com/platforms/android-kotlin/track/#trace) or [iOS](https://docs.tealium.com/platforms/ios-swift/track/#trace).



To join a trace, call the [joinTrace()](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#jointrace) method:

```kotlin
Tealium["INSTANCE_NAME"]?.joinTrace("TRACE_ID")
```

To leave a trace, call the [leaveTrace()](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#leavetrace) method:

```kotlin
Tealium["INSTANCE_NAME"]?.leaveTrace()
```


To join a trace, call the [joinTrace()](https://docs.tealium.com/platforms/ios-swift/api/tealium/#jointrace) method:

```swift
tealium?.joinTrace(id: "TRACE_ID")
```

To leave a trace, call the [leaveTrace()](https://docs.tealium.com/platforms/ios-swift/api/tealium/#leavetrace) method:

```swift
tealium?.leaveTrace()
```




The [Mobile Trace Tool](https://docs.tealium.com/platforms/getting-started-mobile/trace/#mobile-trace-tool) enhances the trace feature by providing a QR code that is scannable by your device, enabling you to quickly view events coming from the Tealium Mobile SDKs.

### Live Events

The Live Events feature in Tealium EventStream is available to all Tealium customers for the purpose of [toubleshooting mobile installations](https://docs.tealium.com/platforms/getting-started-mobile/troubleshooting/).

Learn more about using [Live Events](https://docs.tealium.com/about-live-events/).
