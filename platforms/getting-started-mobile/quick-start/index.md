---
title: Quick Start Guide for Mobile
url: https://docs.tealium.com/platforms/getting-started-mobile/quick-start/
---
## Install

Get started with installing Tealium for [Android](/platforms/android-java/install) or [iOS](/platforms/ios-swift/install).



To install Tealium for Android library with Maven:

1. Add the Tealium Maven URL to your project&#39;s top-level `build.gradle` file:

      ```ruby
      allprojects {
            repositories {
              mavenCentral()
              maven {
                url &#34;https://maven.tealiumiq.com/android/releases/&#34;
              }
            }
      }
      ```

2. In your project module&#39;s `build.gradle` file, add the following Maven dependency:

      ```ruby
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.X.X&#39;
      }
      ```
Check for the latest releases on [Github](https://github.com/tealium/tealium-kotlin/releases) and replace 1.X.X with the latest release number.



To install Tealium for iOS library with Swift Package Manager:

1. In your Xcode project, select **File &gt; Swift Packages &gt; Add Package Dependency**
2. Enter the repository URL: `https://github.com/tealium/tealium-swift`
3. Configure the version rules. Typically, **Up to next major** is recommended. If the current Tealium Swift library version does not appear in the list, then reset your Swift package cache.
4. Select the modules to install and add the modules to each of your app targets in your Xcode project, under **Frameworks &gt; Libraries &amp; Embedded Content**



## Initialize

Get started with initializing Tealium for [Android](/platforms/android-java/install/#initialize) or [iOS](/platforms/ios-swift/install/#initialize).




To initialize Tealium, configure a [`TealiumConfig`](/platforms/android-kotlin/api/tealium-config/) instance and pass it into a [`Tealium`](/platforms/android-kotlin/api/tealium/) instance. It&#39;s recommended to initialize the Tealium Kotlin library in the app&#39;s global application class within the `onCreate()` method.

Manage your [`Tealium`](/platforms/android-kotlin/api/tealium/#class-tealium) instance by using a tracking helper class, which provides a single point of entry for the Tealium Kotlin library and simplifies future upgrades. 

```kotlin
object TealiumHelper {

  lateinit var tealium: Tealium

  fun init(application: Application) {
    val tealiumConfig = TealiumConfig(
                      application,
                      &#34;ACCOUNT&#34;,
                      &#34;PROFILE&#34;,
                      Environment.DEV,
                      dataSourceId = &#34;DATASOURCE_ID&#34;,  //optional
                      modules = mutableSetOf(VisitorService),
                      dispatchers = mutableSetOf(TagManagement, Collect)
                    )
    tealium = Tealium.create(&#34;tealium_instance&#34;, tealiumConfig)
  }
}
```




To initialize Tealium, pass a [`TealiumConfig`](/platforms/ios-swift/api/tealium-config/) instance to the [`Tealium()`](/platforms/ios-swift/api/tealium/#tealium) constructor.

Manage your [`Tealium`](/platforms/ios-swift/api/tealium/#class-tealium) instance by using a tracking helper class, which provides a single point of entry for the Tealium iOS library and simplifies future upgrades. 

```swift
class TealiumHelper {
    static let shared = TealiumHelper()
    let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)
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
        tealium?.dataLayer.add(&#34;mykey&#34;, &#34;myvalue&#34;, expiry: .forever)

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

Mobile Publish Settings are enabled by default, and must be disabled if you don’t want to use them. Configure the Mobile Publish Settings in iQ Tag Management, or disable them using `config.shouldUseRemotePublishSettings = false`.




## Track

Get started with tracking views and events for [Android](/platforms/android-kotlin/track/) or [iOS](/platforms/ios-swift/track/).

### Track Views

To track screen views, pass an instance of `TealiumView(viewName:dataLayer:)` to the `track()` method.  `TealiumView` is comprised of a view name, which appears in the data layer as `tealium_event`, and an optional data dictionary.



To track views:  
```kotlin
val tealView = TealiumView(&#34;screen_view&#34;, mutableMapOf(&#34;screen_name&#34; to &#34;Home&#34;))
tealium.track(tealView);
```



To track views:  
```swift
let tealView = TealiumView(&#34;screen_view&#34;, dataLayer: [&#34;screen_name&#34;: &#34;Home&#34;])
tealium?.track(tealView)
```




### Track Events

To track non-view events, pass an instance of `TealiumEvent(eventName:dataLayer:)` to the `track()` method.  `TealiumEvent` is comprised of an event name, which appears in the data layer as `tealium_event`, and an optional data dictionary.



To track events:  
```kotlin
val tealEvent = TealiumEvent(&#34;user_login&#34;, mutableMapOf(&#34;customer_id&#34; to &#34;1234567890&#34;))
tealium.track(tealEvent);
```



To track events:  
```swift
let tealEvent = TealiumEvent(&#34;user_login&#34;, dataLayer: [&#34;customer_id&#34;: &#34;1234567890&#34;])
tealium?.track(tealEvent)
```

The [`track()`](/platforms/ios-swift/api/tealium/#track) method tracks an event by accepting a `TealiumDispatch` of type `TealiumEvent`, which is comprised of an event name and an optional data dictionary.




## Data Layer

Get started managing common data layer values and the data provided by each module for [Android](/platforms/android-kotlin/data-layer/) or [iOS](/platforms/ios-swift/data-layer/).

To add data to the data layer:  



To set a `String` value use the [putString()](/platforms/android-kotlin/api/data-layer/#putstring) method:   
```kotlin
tealium.dataLayer.putString(&#34;my_string&#34;, &#34;my_string_value&#34;)
```

Similarly for different data types, the method begins with `put`, such as [putInt()](/platforms/android-kotlin/api/data-layer/#putint) for integers and [putDoubleArray()](/platforms/android-kotlin/api/data-layer/#getdoublearray) for an array of floating-point numbers. Learn more about methods for different [data type](/platforms/android-kotlin/data-layer/#data-types).

To set a `String` value to expire after 1 day:  
```kotlin
tealium.dataLayer.putString(&#34;my_string&#34;, &#34;my_string_value&#34;, Expiry.afterTimeUnit(1, TimeUnit.DAYS))
```

Learn more about the [expiration types](/platforms/android-kotlin/data-layer/#data-expiration).


To set a value of any type, use the [`add()`](/platforms/ios-swift/api/tealium-data-layer/#add) method:  
```swift
tealium.dataLayer.add(key: &#34;my_value&#34;, value: 123456)
```

To set a value of any type to expire after 1 day:  
```swift
tealium?.dataLayer.add(key: &#34;my_value&#34;, value: 123456, expiry: .afterCustom((.days, 1)))
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



If you are using Tealium AudienceStream, `visitorId` is the anonymous ID associated with the visitor. Learn more about [anonymous IDs in AudienceStream]().

### User Identifier

When you identify known users, add a user identifier attribute to the persistent data storage.

Learn more about [user identifiers in AudienceStream]().



To add a user identifier, such as a customer ID:  
```kotlin
fun setKnownVisitorId(id: String) {
    tealium.dataLayer.putString(&#34;customer_id&#34;, id, Expiry.FOREVER)
}
```


To add a user identifier, such as a customer ID:  
```swift
func setKnownVisitorId(_ id: String) {
	tealium?.dataLayer.add(key: &#34;customer_id&#34;, value: id, expiry: .forever)
}
```



## Validate

Validate your data by inspecting log files, running a trace, and viewing live events.

### Logs

Get started with logging for [Android](/platforms/android-kotlin/install/#log-level) or [iOS](/platforms/ios-swift/install/#log-level).



To set the log level, set the [`logLevel`](/platforms/android-kotlin/api/tealium-config/#loglevel) property:

```kotlin
Logger.logLevel = LogLevel.DEV // or LogLevel.QA, LogLevel.PROD
```


To set the log level, set the [`logLevel`](/platforms/ios-swift/api/tealium-config/#loglevel) property:

```swift
config.logLevel = .debug // or .info, .error, .fault, .silent
```



### Trace

Get started with [trace](/platforms/getting-started-mobile/trace/) for [Android](/platforms/android-kotlin/track/#trace) or [iOS](/platforms/ios-swift/track/#trace).



To join a trace, call the [joinTrace()](/platforms/android-kotlin/api/tealium/#jointrace) method:

```kotlin
Tealium[&#34;INSTANCE_NAME&#34;]?.joinTrace(&#34;TRACE_ID&#34;)
```

To leave a trace, call the [leaveTrace()](/platforms/android-kotlin/api/tealium/#leavetrace) method:

```kotlin
Tealium[&#34;INSTANCE_NAME&#34;]?.leaveTrace()
```


To join a trace, call the [joinTrace()](/platforms/ios-swift/api/tealium/#jointrace) method:

```swift
tealium?.joinTrace(id: &#34;TRACE_ID&#34;)
```

To leave a trace, call the [leaveTrace()](/platforms/ios-swift/api/tealium/#leavetrace) method:

```swift
tealium?.leaveTrace()
```




The [Mobile Trace Tool](/platforms/getting-started-mobile/trace/#mobile-trace-tool) enhances the trace feature by providing a QR code that is scannable by your device, enabling you to quickly view events coming from the Tealium Mobile SDKs.

### Live Events

The Live Events feature in Tealium EventStream is available to all Tealium customers for the purpose of [toubleshooting mobile installations](/platforms/getting-started-mobile/troubleshooting/).

Learn more about using [Live Events]().
