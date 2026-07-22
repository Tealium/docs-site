---
title: TealiumConfig
description: A class to set configuration options for the main Tealium class. Individual modules provide their own extensions for the TealiumConfig class if they are enabled.
url: https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/
---
## Class: `TealiumConfig`

The following summarizes the commonly used methods and properties of the iOS (Swift) `TealiumConfig` class.

| Method/Property | Description |
| ----- | ------ |
| `addDelegate()` | Adds a new delegate conforming to the TealiumDelegate protocol |
| `addRemoteCommand()` | Adds remote commands for later execution |
| `batchingBypassKeys` |Sets a list of event names for which batching is bypassed (sent as individual events) |
| `batchingEnabled` | Enables or disables (default) event batching |
| `batchSize` | Sets the amount of events to combine into a single batch request (max: 10) |
| `collectOverrideProfile` | Overrides the Tealium Collect profile to send data to a different Tealium profile |
| `collectOverrideURL` | Overrides the Tealium Collect URL to send data to a different endpoint |
| `connectivityRefreshEnabled` | If enabled (default), the connectivity module checks for a connection at a specified interval |
| `connectivityRefreshInterval` | Sets the default connectivity refresh interval in seconds |
| `consentLoggingEnabled` | Enables or disables the consent logging feature |
| `delegates` | Returns an array of the enabled delegates |
| `dispatchAfter` | Sets the number of events after which the queue is flushed |
| `dispatchExpiration` | Sets the batch expiration in days. If the device is offline for an extended period, older events are deleted |
| `dispatchQueueLimit` | Sets the maximum number of queued events. If this number is reached, and the queue has not been flushed, the oldest events are deleted. |
| `enableRemoteHTTPCommand()` | Enables the built-in remote HTTP command |
| `existingVisitorId` | Sets the existing visitor ID, used as the first party ID in the app extension |
| `geofenceFileName` | Sets the name of a local geofences JSON file asset. _Do not include the file extension._ |
| `geofenceUrl` | Sets the URL of a hosted JSON file |
| `initialUserConsentCategories` | Sets the user's initial consent categories when the library starts up for the first time |
| `initialUserConsentStatus` | Sets the initial user consent status |
| `logLevel` | Sets a new log level |
| `memoryReportingEnabled` | Enables or disables memory reporting in the DeviceData module |
| `modulesList`| The list of modules to be enabled or disabled |
| `overrideConsentPolicy` | Overrides the default consent `policy` parameter |
| `remoteAPIEnabled` |Enables (`true`) or disables (`false`) `remote_api` event. Required for RemoteCommands module if DispatchQueue module in use. |
| `remoteCommand` | Returns an array of all registered remote commands |
| `remoteHTTPCommandDisabled` | Disables the built-in remote HTTP command if `true`|
| `rootView` | Sets the current `UIView` for `WKWebView` to be attached to|
| `searchAdsEnabled` | Enables or disables the Apple Search Ads API in the Attribution module |
| `shouldAddCookieObserver` | Determines if Tealium should add a `WKWebView` Cookie Observer |
| `shouldUseRemotePublishSettings` | Sets the Mobile Publish Settings (default: enabled)|
| `tagManagementOverrideURL` | Overrides the default URL used by the Tag Management module |
| `TealiumConfig()`  | Constructor for a `TealiumConfig` object |
| `updateDistance`  | Sets the distance interval (meters) in which the location updates are received |
| `useHighAccuracy` | Sets the location precision to low accuracy (default) or high accuracy |



### `addDelegate()`
Adds a new delegate conforming to the TealiumDelegate protocol.

```swift
addDelegate(delegate)
```

| Parameter   | Type    | Description                                       |
|-------------|---------|---------------------------------------------------|
| `delegate`  | `TealiumDelegate`  | A class conforming to the TealiumDelegate protocol  |

The following example assumes the current module has implemented the `TealiumDelegate` protocol:

```swift
config.addDelegate(self)
```

### `addRemoteCommand()`

Adds remote commands for later execution.

```swift
addRemoteCommand(command)
```

| Parameter   | Type    | Description                                       |
|-------------|---------|---------------------------------------------------|
| `command`   | `TealiumRemoteCommand`  | Instance of a TealiumRemoteCommand to be added |

The following example, placed prior to Tealium initialization, shows how add remote commands:

```swift
#if os(iOS)
let remoteCommand = TealiumRemoteCommand(commandId: "test",
        description: "test") { response in
			print("Remote Command 'test' executed")
}
config.addRemoteCommand(remoteCommand)
#endif
```

### `batchingBypassKeys`

Sets a list of event names for which batching is bypassed (sent as individual events).

```swift
config.batchingBypassKeys = ["home_screen"]
```

### `batchingEnabled`

Enables (`true`) or disables (`false`) event batching. Disabled by default.

```swift
config.batchingEnabled = true
```

### `batchSize`

Sets the amount of events to combine into a single batch request. Maximum is 10.

```swift
config.batchSize = 8
```

### `collectOverrideProfile`

Overrides the Tealium Collect profile to send data to a different Tealium profile.

```swift
config.collectOverrideProfile = "main"
```

### `collectOverrideURL`

Overrides the Tealium Collect URL to send data to a different endpoint.

```swift
config.collectOverrideURL = url
```

| Property value  | Type | Description |
| --- | --- | --- |
| `url` | `String` | The URL to override |

The default URL is:  
```bash
https://collect.tealiumiq.com/event/
```
The default URL with event batching is:  
```bash
https://collect.tealiumiq.com/bulk-event/
```

The method is typically used to set a custom hostname, or to set a specific region hostname. The following example sets the Tealium Collect base URL to stay within the EU Central region:

```swift
let url = "https://collect-eu-central-1.tealiumiq.com/event/"
config.collectOverrideURL = url
```

### `connectivityRefreshEnabled`

If enabled (default), the connectivity module checks for a connection at a specified interval (controlled by `setConnectivityRefreshInterval`). Queued dispatches are then sent as soon as a connection is resumed.

```swift
config.connectivityRefreshEnabled = true
```

### `connectivityRefreshInterval`

Sets the default connectivity refresh interval in seconds. Default is 30 seconds if not set on the TealiumConfig instance.

```swift
config.connectivityRefreshInterval = 30
```


### `consentLoggingEnabled`

Enables the [Consent Logging](https://docs.tealium.com/consent-change-event-specifications/) feature, which sends all consent status changes to Tealium Customer Data Hub for auditing purposes.

```swift
config.consentLoggingEnabled = true
```


### `delegates`

Returns an array of the enabled delegates.

The following example shows how to get an array of enabled delegates:

```swift
let delegates = config.delegates
```

### `dispatchAfter`

Number of events after which to automatically flush the queue.

```swift
config.dispatchAfter = 20
```

### `dispatchExpiration`

Sets the dispatch expiration in days. If the device is offline for an extended period. Older events are deleted.

```swift
config.dispatchExpiration = 5
```

### `dispatchQueueLimit`

Sets the maximum number of events to store in the event queue. If this number is reached, and the queue has not been flushed, the oldest events are deleted.

```swift
config.dispatchQueueLimit = 50
```



### `enableRemoteHTTPCommand()`
Enables the built-in remote HTTP command (see [Swift Module: RemoteCommands](https://docs.tealium.com/platforms/ios-swift-v1/module-list/remote-commands/)).


```swift
enableRemoteHTTPCommand()
```

### `existingVisitorId`

Sets the existing visitor ID, used as the first party ID in the app extension |

```swift
config.existingVisitorId = id
```

### `geofenceFileName`

Sets the name of a local geofences file asset. Do not include the file extension.

```swift
config.geofenceFileName = <String>
```

| Type | Description | Example |
| --- | --- | --- |
| `String` | The JSON file name | `"geofences"` |

### `geofenceUrl`

Sets the URL of a hosted geofences file.

```swift
config.geofenceUrl = <String (url)>
```

| Type | Description | Example |
 --- | --- | --- |
| `String` | The URL of a geofences file  | `"https://example.com/.../geofences.json"` |

### `initialUserConsentCategories`

Sets the user's initial consent categories when the library starts up for the first time. If there are saved preferences, these override any preferences passed in the config object. Sets the consent status to `.consented`.

```swift
config.initialUserConsentCategories = [.cdp, .analytics]
```

### `initialUserConsentStatus`

Sets the initial user consent status. This happens for the user when the library starts up for the first time. If there are saved preferences, these override any preferences passed in the config object.

Sets the list of consented categories to include ALL available consent categories, if the status is `.consented`. Does not allow categories to be set selectively.

Use this method to ignore all tracked events prior to consent, overriding the default behavior of queueing events prior to consent being granted. Add the following line to the config object:

```swift
config.initialUserConsentStatus = .notConsented
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `status` | `TealiumConsentStatus` | A value from TealiumConsentStatus enum | [`.unknown`, `.consented`, `.notConsented`] |


The following define the different types of Tealium consent statuses from the `TealiumConsentStatus` enum.

**.unknown**  
The `unknown` status is the default setting for the consent manager. In this state, the consent manager queues events locally until an affirmative `consented`/`notConsented` status is provided.

**.consented**  
The `consented` status is set when the user has consented to tracking. In this state, the consent manager allow all tracking calls to continue as normal.

**.notConsented**  
The `notConsented` status is set when the user has declined tracking. In this state, the consent manager drops all tracking calls and halt further processing by the SDK.



### `logLevel`

Sets a new log level (see [Swift Module: Logger](https://docs.tealium.com/platforms/ios-swift-v1/module-list/logger/)).

The following example shows how to set the log level to `errors`:

```swift
let newLogLevel = TealiumLogLevel.errors
config.logLevel = newLogLevel
```


### `memoryReportingEnabled`

Enables or disables memory reporting in the DeviceData module (default: disabled).

```swift
config.memoryReportingEnabled = true
```

### `modulesList`

Set a net modules list (see [Modules List](https://docs.tealium.com/platforms/ios-swift-v1/modules/)).

The following example shows how to blacklist the autotracking module:

```swift
let modulesList = TealiumModulesList(isWhitelist: false, moduleNames: ["autotracking"])
config.modulesList = list
```

The TealiumModulesList `struct` has the following parameters:

| Parameter  | Type    | Description                                       | Example |
|------------|---------|---------------------------------------------------| ------- |
| `isWhiteList`     | `Bool`  | Determines if modules list is a blacklist (`false`) or a whitelist (`true`) | `moduleNames: ["autotracking"] `|
| `modulesList`     | `[String]`  | Array of module names to enable or disable | [`"true"`, `"false"`] |


### `overrideConsentPolicy`

Overrides the default consent `policy` parameter (default: `"gdpr"`).

```swift
let policy = "ccpa"
config.overrideConsentPolicy = policy
```

### `remoteAPIEnabled`

Enables (`true`) or disables (`false`) `remote_api` event. Required for RemoteCommands module if DispatchQueue module in use. Default `false`.

```swift
config.remoteAPIEnabled = true
```

### `remoteCommands`

Returns an array of all registered remote commands.

The following example shows how to get an array of all registered remote commands:

```swift
let remoteCommands = config.remoteCommands
```

### `remoteHTTPCommandDisabled`
Disables the built-in remote HTTP command (see [Swift Module: RemoteCommands](https://docs.tealium.com/platforms/ios-swift-v1/module-list/remote-commands/)).

```swift
config.remoteHTTPCommandDisabled = true
```

### `rootView`

Sets the current `UIView` for `WKWebView` to be attached to. Only required if you have a complex view hierarchy, such as with a push notification, where auto-detection may fail.

```swift
let view = self.view
config.rootView = view
```


### `searchAdsEnabled`
Enables or disables memory reporting in the DeviceData module (default: disabled).                         |

```swift
config.searchAdsEnabled = true
```

### `shouldAddCookieObserver`

If set to `true` (default), this method determines if a cookie observer should be added to successfully migrate all cookies. If set to `false`, if multiple cookie observers are present then only one of them is called, which may cause some cookies to not migrate.


```swift
config.shouldAddCookieObserver = false
```


<blockquote>
The [`shouldAddCookieObserver`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#shouldaddcookieobserver) property lets you use your own cookie observer during cookie synchronization, which requires a cookie observer to retrieve cookies on the main thread after setting them. This issue is caused by bugs in `WKWebView`, which prevents your own observer from being called.
</blockquote>
  

### `shouldUseRemotePublishSettings`

Sets the [Mobile Publish Settings](https://docs.tealium.com/creating-a-mobile-profile/) (version 1.9.0+) to enabled (default) or disabled.

```Swift
config.shouldUseRemotePublishSettings = false
```


<blockquote>
In version 1.9.0+, Mobile Publish Settings are enabled by default, and must be disabled if you don’t want to use them. Configure the Mobile Publish Settings in iQ Tag Management, or disable it using `config.shouldUseRemotePublishSettings = false` in the Swift installation. Failure to do causes initialization failures and prevent tracking.
</blockquote>


### `tagManagementOverrideURL`

Overrides the default URL used by the Tag Management module. This is needed if you are self-hosting your Tealium JavaScript files.

The following example shows how to override the default URL used by the Tag Management module.

```swift
let url = "https://tags.mycdn.com/utag/myaccount/myprofile/myenv/mobile.html"
config.tagManagementOverrideURL =  url
```

### `TealiumConfig()`

Constructor for a `TealiumConfig` object. This object is required to initialize the library for your specific account.

```swift
TealiumConfig(account:String, profile:String, environment:String, optionalData:Dictionary, dataSource:String)
```

| Parameter     | Type      | Description                                      | Example |
|---------------|-----------|--------------------------------------------------| ------- |
| `account`     | `String`  | Tealium account name                             | `"companyXYZ"` |
| `profile`     | `String`  | Tealium profile name         | `"main"`|
| `environment` | `String`  | Tealium environment name                        | [`"dev"`, `"qa"`, `"prod"`] |
| `datasource` | `String`  | (Optional) Tealium data source key from CDH    | `"abc123"` |


### `updateDistance`

Sets the distance interval (meters) in which location updates are received.


<blockquote>
Only use this method if `useHighAccuracy` is set to `true`.
</blockquote>



```swift
config.updateDistance = <Double>
```

| Type | Description | Example |
| --- | --- | --- |
| `Double` | The distance interval (meters) in which location updates are received | `150.0` |

Usage example:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```

### `useHighAccuracy`

Sets the location precision to low accuracy (default) or high accuracy.

The property is disabled (`false`) by default, which sets the location precision to low accuracy. If the location enabled device moves 500 meters or more, then this is considered a significant location changes causing a location update. Location updates typically take longer than five minutes with this setting.

Learn more about [Apple's significant-change location service](https://developer.apple.com/documentation/corelocation/getting_the_user_s_location/using_the_significant-change_location_service).

If enabled (`true`), the property sets the location of data precision to the highest possible accuracy. The initial event is delivered as quickly as possible and then continues to determine the location and delivers additional events, as necessary, when that data is available.

Learn more about [Apple's accuracy of location data](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423836-desiredaccuracy?language=swift).


Using high accuracy results in greater battery consumption for your device than low accuracy, due to more frequent location updates.   

```swift
config.useHighAccuracy = <Bool>
```

| Type | Description | Example |
| --- | --- | --- |
| `Boolean` | Sets the location data accuracy | `true` |


Usage example:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```
