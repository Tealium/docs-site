---
title: TealiumConfig
description: A class to set configuration options for the main Tealium class. Individual modules provide their own extensions for the TealiumConfig class if they are enabled.
url: https://docs.tealium.com/platforms/ios-swift/api/tealium-config/
---
## Class: `TealiumConfig`

The following summarizes the commonly used methods and properties of the iOS (Swift) `TealiumConfig` class.

| Method/Property | Description |
| ----- | ------ |
| [`addRemoteCommand()`](#addremotecommand) | Adds remote commands for later execution |
| [`adobeVisitorAuthState`](#adobevisitorauthstate) | Sets the current authentication state for the visitor.                                                                                                                                                                   |
| [`adobeVisitorCustomVisitorId`](#adobevisitorcustomvisitorid) | Sets the known visitor ID to the Adobe ECID, if it's known at initialization time. If the ECID changes in the future, call `linkECIDToKnownIdentifier` to update the visitor ID.                                         |
| [`adobeVisitorDataProviderId`](#adobevisitordataproviderid) | Sets the data provider ID, provided by Adobe, which is required when linking an ECID to a known ID.                                                                                                                      |
| [`adobeVisitorExistingEcid`](#adobevisitorexistingecid) | Sets the existing ECID from a previous installation to be used, such as the Adobe SDK, instead of requesting a new ECID.                                                                                                 |
| [`adobeVisitorOrgId`](#adobevisitororgid) | String containing the Adobe Org ID including the `@` portion.                                                                                                                                                            |
| [`adobeVisitorRetries`](#adobevisitorretries) | The number of allowed invalid visitor ID retries before a request fails, which results in tracking calls being sent anyway without an ECID.                                                                              |
| [`appDelegateProxyEnabled`](#appDelegateProxyEnabled) | Enables (default) or disables the Tealium AppDelegate proxy |
| [`autoTrackingBlocklistFilename`](#autotrackingblocklistfilename) | Sets the name of the local block list file.                                                  |
| [`autoTrackingBlocklistURL`](#autotrackingblocklisturl) | Sets the URL of the remote block list file.                                                  |
| [`autoTrackingCollectorDelegate`](#autotrackingcollectordelegate) | Sets the global delegate that executes for automatically tracked views.                 |
| [`batchingBypassKeys`](#batchingbypasskeys) |Sets a list of event names for which batching is bypassed (sent as individual events) |
| [`batchingEnabled`](#batchingenabled) | Enables or disables (default) event batching |
| [`batchSize`](#batchsize) | Sets the amount of events to combine into a single batch request (max: 10) |
| [`batteryReportingEnabled`](#batteryreportingenabled) | Enables or disables battery reporting in the DeviceData module |
| [`connectivityRefreshEnabled`](#connectivityrefreshenabled) | If enabled (default), the connectivity module checks for a connection at a specified interval |
| [`connectivityRefreshInterval`](#connectivityrefreshinterval) | Sets the default connectivity refresh interval in seconds |
| [`consentExpiry`](#consentexpiry) | Sets the expiration time of the user consent selections |
| [`consentLoggingEnabled`](#consentloggingenabled) | Enables or disables the consent logging feature |
| [`consentPolicy`](#consentpolicy) | Sets the [consent policy](https://docs.tealium.com/platforms/ios-swift/consent-management/#set-policy) (defaults to GDPR) |
| [`deepLinkTrackingEnabled`](#deeplinktrackingenabled) | Enables or disables automatic tracking of deep links |
| [`desiredAccuracy`](#desiredaccuracy) | The accuracy of the location data that your app wants to receive |
| [`diskStorageDirectory`](#diskstoragedirectory) | Sets the directory to be used for disk storage. Default `.caches`. |
| [`dispatchAfter`](#dispatchafter) | Sets the number of events after which the queue is flushed |
| [`dispatchExpiration`](#dispatchexpiration) | Sets the batch expiration in days. If the device is offline for an extended period, older events are deleted |
| [`dispatchQueueLimit`](#dispatchqueuelimit) | Sets the maximum number of queued events. If this number is reached, and the queue has not been flushed, the oldest events are deleted. |
| [`dispatchListeners`](#dispatchlisteners) | Provides the option to add custom `DispatchListener`s to listen for tracking calls just prior to dispatch |
| [`dispatchValidators`](#dispatchvalidators) | Provides the option to add custom `DispatchValidator`s to control whether to dispatch, queue, or drop events events |
| [`enableBackgroundLocation`](#enablebackgroundlocation) | Enables location updates to take place while the app is running in the background |
| [`existingVisitorId`](#existingvisitorid) | Sets the existing visitor ID, used as the first party ID in the app extension |
| [`geofenceFileName`](#geofencefilename)  | Sets the name of a local geofences JSON file asset. _Do not include the file extension._ |
| [`geofenceTrackingEnabled`](#geofencetrackingenabled) | Disables or enables geofence tracking |
| [`geofenceUrl`](#geofenceurl)  | Sets the URL of a hosted JSON file |
| [`hostedDataLayerExpiry`](#hosteddatalayerexpiry) | Sets an expiration on the hosted data layer data |
| [`hostedDataLayerKeys`](#hosteddatalayerkeys) | Sets the event mappings used by the hosted data layer module when looking up data layer IDs |
| [`isCollectEnabled`](#iscollectenabled)  | Provides an option to disable the Collect dispatcher |
| [`lifecycleAutoTrackingEnabled`](#lifecycleautotrackingenabled) | Enables or disables lifecycle auto tracking. Default is `true`. If set to `false` and you want lifecycle launch/sleep/wake events, they need to be manually called using the public methods in the `LifecycleModule` |
| [`logger`](#logger)  | Sets a custom logger conforming to the `TealiumLoggerProtocol` that replaces the current `TealiumLogger` |
| [`logLevel`](#loglevel) | Sets the log level property, which controls how much information is logged |
| [`logType`](#logtype) | Sets a new log type |
| [`memoryReportingEnabled`](#memoryreportingenabled) | Enables or disables memory reporting in the DeviceData module |
| [`minimumFreeDiskSpace`](#minimumfreediskspace) | Sets the minimum free disk space in Megabytes  for Disk Storage to be enabled |
| [`minutesBetweenRefresh`](#minutesbetweenrefresh) | Determines how often to fetch the publish settings |
| [`onConsentExpiration`](#onconsentexpiration) | Callback to execute once consent selections expire |
| [`overrideCollectProfile`](#overrideCollectProfile) | Overrides the Tealium Collect profile to send data to a different Tealium profile |
| [`overrideCollectURL`](#overrideCollectURL) | Overrides the Tealium Collect URL to send data to a different endpoint |
| [`overrideCollectBatchURL`](#overrideCollectBatchURL) | Overrides the Tealium Collect Batch URL to send data to a different endpoint |
| [`overrideCollectDomain`](#overrideCollectDomain) | Overrides the Tealium Collect domain name to send data to a different endpoint |
| [`overrideConsentCategoriesKey`](#overrideconsentcategorieskey) | Overrides the name of the consent categories event attribute. Use this to support custom enforcement of server-side consent. (default: `consent_categories`)|
| [`publishSettingsProfile`](#publishsettingsprofile) | Overrides the publish settings profile |
| [`publishSettingsURL`](#publishsettingsurl) | Overrides the publish settings URL |
| [`remoteAPIEnabled`](#remoteapienabled) | Enables or disables `remote_api` event. Required for RemoteCommands module if DispatchQueue module in use. |
| [`remoteCommands`](#remotecommands) | Returns an array of all registered remote commands |
| [`remoteHTTPCommandDisabled`](#remotehttpcommanddisabled) | Disables the built-in remote HTTP command if `true`|
| [`rootView`](#rootview) | Sets the current `UIView` for `WKWebView` to be attached to|
| [`screenReportingEnabled`](#screenreportingenabled) | Enables or disables screen reporting in the DeviceData module |
| [`searchAdsEnabled`](#searchadsenabled) | Enables or disables the Apple Search Ads API in the Attribution module |
| [`sendCrashDataOnCrashDetected`](#sendcrashdataoncrashdetected) | Sends a crash event when a crash is detected and only adds crash data to that event |
| [`sendDeepLinkEvent`](#senddeeplinkevent) | Sends a `deep_link` event with related data every time a deep link is received |
| [`sessionCountingEnabled`](#sessioncountingenabled) | Disables session counting for Tealium iQ accounts. Use this if you are self-hosting your Tealium JavaScript files |
| [`shouldAddCookieObserver`](#shouldaddcookieobserver) | Determines whether to add a `WKWebView` cookie observer |
| [`shouldUseRemotePublishSettings`](#shoulduseremotepublishsettings) | Sets the Mobile Publish Settings (default: enabled)|
| [`skAdAttributionEnabled`](#skadattributionenabled) | Enables the use [SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork) framework |
| [`skAdConversionKeys`](#skadconversionkeys) | Defines the event and value for which to call the [`SKAdNetwork.updateConversionValue()`](https://developer.apple.com/documentation/storekit/skadnetwork/3566697-updateconversionvalue) method |
| [`tagManagementOverrideURL`](#tagmanagementoverrideurl) | Overrides the default URL used by the Tag Management module |
| [`TealiumConfig()`](#tealiumconfig) | Constructor for a `TealiumConfig` object |
| [`timedEventTriggers`](#timedeventtriggers) | A list of `TimedEventTrigger` objects for automatically tracking timed events |
| [`updateDistance`](#updatedistance)  | Sets the distance interval (meters) in which the location updates are received |
| [`useHighAccuracy`](#usehighaccuracy) | Sets the location precision to low accuracy (default) or high accuracy |
| [`visitorIdentityKey`](#visitoridentitykey) | A config key that specifies the data layer key that represents the customer identifier. It can be used to enable [visitor switching](https://docs.tealium.com/platforms/getting-started-mobile/identity-resolution/#visitor-switching). |
| [`webviewProcessPool`](#webviewprocesspool) | Prevents cookie synchronization issues if your app contains other webviews besides the Tealium Tag Management webview |
| [`webviewConfig`](#webviewconfig) | Permits a custom `WKWebviewConfiguration` object to be passed, which is used by the Tealium Tag Management webview |

### `addRemoteCommand()`

Adds remote commands for later execution.

```swift
addRemoteCommand(command)
```

| Parameter | Type            | Description                                      |
|:----------|:----------------|:-------------------------------------------------|
| `command` | `RemoteCommand` | Instance of a `TealiumRemoteCommand` to be added |

The following example, placed prior to Tealium initialization, shows how add remote commands:

```swift
#if os(iOS)
let remoteCommand = RemoteCommand(commandId: "test",
        description: "test") { response in
			print("Remote Command 'test' executed")
}
config.addRemoteCommand(remoteCommand)
#endif
```

### `adobeVisitorAuthState`

Sets the current authentication state for the visitor.

Example:

```swift
config.adobeVisitorAuthState = .authenticated
config.adobeVisitorAuthState = .loggedOut
config.adobeVisitorAuthState = .unknown
```

### `adobeVisitorCustomVisitorId`

Sets the known visitor ID to the Adobe ECID, if it's known at initialization time. If the ECID changes in the future, call [`linkECIDToKnownIdentifier`](https://docs.tealium.com/platforms/ios-swift/api/tealium/#linkecidtoknownidentifier) to update the visitor ID.

```swift
config.adobeVisitorCustomVisitorId = "20381482060927465156359999806251989655"
```

### `adobeVisitorDataProviderId`

Sets the data provider ID, provided by Adobe, which is required when linking an ECID to a known ID.

```swift
config.adobeVisitorDataProviderId = "01"
```

### `adobeVisitorExistingEcid`

Sets the existing ECID from a previous installation to be used, such as the Adobe SDK, instead of requesting a new ECID.                                                         

Example:

```swift
config.adobeVisitorExistingEcid = "20381482060927465156359999806251989655"
```

### `adobeVisitorOrgId`

String containing the Adobe Org ID including the `@` portion. If the Org ID is not provided, the module is not initialized and no visitor ID is retrieved. Tracking calls continue as normal without an Adobe ECID.

```swift
config.adobeVisitorOrgId = STRING_VALUE
```

Example:

```swift
config.adobeVisitorOrgId = "1A2A111A111150AA0A110A12@AdobeOrg"
```

### `adobeVisitorRetries`

The number of allowed invalid visitor ID retries before a request fails, which results in tracking calls being sent anyway without an ECID.

Example:

```swift
config.adobeVisitorRetries = 5
```

### `appDelegateProxyEnabled`

Enables the AppDelegate proxy to automatically deep link tracking and initiate a Tealium trace session from a deep link. The property is enabled and set `true` by default. To disable, set property to `false`.

```swift
config.appDelegateProxyEnabled = false
```

### `autoTrackingBlocklistFilename`

For use with the [AutoTracking Module](https://docs.tealium.com/platforms/ios-swift/module-list/autotracking/#block-list).

Sets the name of the block list file that contains a list of views to omit from automatic tracking. The file should be available in the Android `assets` directory.

```swift
config.autoTrackingBlocklistFilename = "autotracking-blocklist.json"
```

### `autoTrackingBlocklistURL`

For use with the [AutoTracking Module](https://docs.tealium.com/platforms/ios-swift/module-list/autotracking/#block-list).

Sets a URL to a JSON formatted block list file that contains a list of views to omit from automatic tracking.

```swift
config.autoTrackingBlocklistUrl = "https://example.com/autotracking-blocklist.json"
```

### `autoTrackingCollectorDelegate`

For use with the [AutoTracking Module](https://docs.tealium.com/platforms/ios-swift/module-list/autotracking/).

The global delegate set on the `TealiumConfig` object that executes for views tracked by the [AutoTracking module](https://docs.tealium.com/platforms/ios-swift/module-list/autotracking/). Edit this delegate to customize the data included with specific views.

```swift
config.autoTrackingCollectorDelegate = myCollectorDelegate
```

### `batchingBypassKeys`

Sets a list of event names for which batching is bypassed (sent as individual events).

```swift
config.batchingBypassKeys = ["home_screen"]
```

### `batchingEnabled`

Enables or disables event batching. Disabled by default.

```swift
config.batchingEnabled = true
```

### `batchSize`

Sets the amount of events to combine into a single batch request. Maximum is 10.

```swift
config.batchSize = 8
```

### `Collectors`

Collectors are modules that gather supplemental information from the device and append it to the data layer before it's transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors. Default collectors are denoted by a `*` next to the collector name.

| Collector Name  | TealiumConfig Reference   |
|:----------------|:--------------------------|
| `AdobeVisitor`  | `Collectors.AdobeVisitor` |
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

These modules are enabled or disabled using the [`TealiumConfig`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/) `collectors` property.

The following example adds to existing list of collectors you're using:  

```swift
config.collectors = [Collectors.AdobeVisitor]
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

### `consentExpiry`

Sets the expiration time of the user consent selections. Set this property when initializing Tealium. The default expiration times for consent selections are:

- CCPA: 395 days
- GDPR: 365 days  

The following sets the consent expiry to 90 days.

```swift
config.consentExpiry = (90, .days)
```

### `consentLoggingEnabled`

Enables the [Consent Logging](https://docs.tealium.com/consent-change-event-specifications/) feature, which sends all consent status changes to Tealium Customer Data Hub for auditing purposes.

```swift
config.consentLoggingEnabled = true
```

### `consentPolicy`

Sets the [consent policy](https://docs.tealium.com/platforms/ios-swift/consent-management/#set-policy). Consent manager is only enabled if this property is set.


```swift
config.consentPolicy = .ccpa
```

### `deepLinkTrackingEnabled`

Enables or disables automatic tracking of standard deep links, such as links to the app from Facebook or other sources, as well as QR trace. Enabled by default.

```swift
config.deepLinkTrackingEnabled = true
```

### `desiredAccuracy`

The accuracy of the location data that your app wants to receive.

```swift
config.desiredAccuracy = .best
```

The available `desiredAccuracy` options are:

| `desiredAccuracy` option | Description                                                                                                  |
|:-------------------------|:-------------------------------------------------------------------------------------------------------------|
| `.bestForNavigation`     | Level of accuracy intended for use in navigation apps that require precise position information at all times |
| `.best`                  | Very high accuracy but don’t need the same level of accuracy required for navigation apps                    |
| `.nearestTenMeters`      | Accuracy to the nearest 10 meters                                                                            |
| `.nearestHundredMeters`  | Accuracy to the nearest 100 meters                                                                           |
| `.reduced`               | Accuracy within 1-20 kilometers                                                                              |
| `.withinOneKilometer`    | Accuracy to the nearest 1 kilometer                                                                          |
| `.withinThreeKilometers` | Accuracy to the nearest 3 kilometers                                                                         |

Learn more about Apple's [desired accuracy constants](https://developer.apple.com/documentation/corelocation/cllocationaccuracy).

### `diskStorageDirectory`

Sets the directory to be used for disk storage. Default `.caches`.

```swift
config.diskStorageDirectory = .documents
```

### `dispatchListeners`

Provides the option to add custom `DispatchListener`s to listen for tracking calls just prior to dispatch.

```swift
config.dispatchListeners = [self]
```

### `dispatchValidators`

Provides the option to add custom `DispatchValidator`s to control whether to dispatch, queue or drop events.

```swift
config.dispatchValidators = [self]
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

### `enableBackgroundLocation`

Enables location updates to take place while the app is running in the background.

```swift
config.enableBackgroundLocation = true
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

| Type     | Description        | Example          |
|:---------|:-------------------|:-----------------|
| `String` | The JSON file name | `geofences` |

### `geofenceTrackingEnabled`

Disables or enables geofence tracking.

```swift
config.geofenceTrackingEnabled = false
```

| Type     | Description        | Example          |
|:---------|:-------------------|:-----------------|
| `Bool` | Boolean indicating whether geofencing should be enabled | `false` |

### `geofenceUrl`

Sets the URL of a hosted geofences file.

```swift
config.geofenceUrl = <String (url)>
```

| Type     | Description                 | Example                                  |
|:---------|:----------------------------|:-----------------------------------------|
| `String` | The URL of a geofences file | `https://example.com/.../geofences.json` |

### `hostedDataLayerExpiry`

Sets an expiration on the hosted data layer data. If this property isn't set, hosted data layer items persist for 7 days by default, and are re-downloaded once this period has expired.

```swift
config.hostedDataLayerExpiry = (1, unit: .minutes)
```


<blockquote>
Setting a shorter expiration time reduces mobile device battery life due to increased network requests.
</blockquote>


### `hostedDataLayerKeys`

Sets the hosted data layer keys (lookup variables) used by the hosted data layer module when retrieving data layer IDs.

```swift
config.hostedDataLayerKeys = ["product_view" : "product_id"]
```

### `isCollectEnabled`

Provides option to disable the collect dispatcher. Mainly intended for use by remote publish settings.

```swift
config.isCollectEnabled = false
```

### `lifecycleAutoTrackingEnabled`

Enables or disables lifecycle auto tracking. Default is `true`. If set to `false` and you want lifecycle launch/sleep/wake events, they need to be manually called using the public methods in the `LifecycleModule`.

```swift
config.lifecycleTrackingEnabled = false
```

### `logger`

Sets a custom logger conforming to the `TealiumLoggerProtocol` that replaces the current `TealiumLogger`.

The following example shows how to set your custom logger on the config object:

```swift
class CustomLogger: TealiumLoggerProtocol {
	// ... conforming to the TealiumLoggerProtocol
	// plus your own custom methods
}

class TealiumHelper {
	let config = TealiumConfig(...)
	var tealium: Tealium?
	let customLogger = CustomLogger()

	// ...

	private init() {
		config.logger = customLogger
		// ...
		tealium = Tealium(config: config)
	}
}
```

### `logLevel`

Sets the log level property, which controls how much information is logged, to one of the following values:

| Log Level | Log Activity Description                                                                       |
|:----------|:-----------------------------------------------------------------------------------------------|
| `.debug`  | Debug-level events used for debugging an application (recommended for development environment) |
| `.info`   | Informational events that highlight the progress of the application                            |
| `.error`  | Error events such as critical errors and failures                                              |
| `.fault`  | Fault or severe events such as system-level or multi-process errors                            |
| `.silent` | No logging                                                                                     |

```swift
config.logLevel = .debug
```


<blockquote>
View your development logs in the Xcode console or the Mac Console app. View your production logs with the Console app by connecting your iOS device.
</blockquote>


### `logType`

Sets a new logger type. The default is `.os` or [`OSLog`](https://developer.apple.com/documentation/os/oslog)

The following example shows how to set the log level to `print`:

```swift
config.logType = .print
```

### `memoryReportingEnabled`

Enables or disables memory reporting in the DeviceData module (default: disabled).

```swift
config.memoryReportingEnabled = true
```

### `batteryReportingEnabled`

Enables or disables battery reporting in the DeviceData module (default: enabled).

```swift
config.batteryReportingEnabled = true
```


### `screenReportingEnabled`

Enables or disables screen reporting in the DeviceData module (default: enabled).

```swift
config.screenReportingEnabled = true
```

### `minimumFreeDiskSpace`

Sets the minimum free disk space in Megabytes for Disk Storage to be enabled

```swift
config.minimumFreeDiskSpace = 25
```

### `minutesBetweenRefresh`

Determines how often to fetch the publish settings.

```swift
config.minutesBetweenRefresh = 15
```

### `onConsentExpiration`

Callback to execute once consent selections expire.

```swift
config.onConsentExpiration = {
	// display consent modal
}
```

### `overrideCollectProfile`

Overrides the Tealium Collect profile to send data to a different Tealium profile.

```swift
config.overrideCollectProfile = "main"
```

### `overrideCollectURL`

Overrides the Tealium Collect URL to send data to a different endpoint. If using the event batching feature, also override the [overrideCollectBatchURL](#overrideCollectBatchURL) property.

```swift
config.overrideCollectURL = url
```

| Property value | Type     | Description         |
|:---------------|:---------|:--------------------|
| `url`          | `String` | The URL to override |

The default URL is:  
```bash
https://collect.tealiumiq.com/event/
```

The property is used to set a custom hostname or to set a specific region hostname. The following example sets the Tealium Collect base URL to stay within the EU Central region:

```swift
let url = "https://collect-eu-central-1.tealiumiq.com/event/"
config.overrideCollectURL = url
```

### `overrideCollectBatchURL`

Overrides the Tealium Collect batch URL to send data to a different endpoint.

```swift
config.overrideCollectBatchURL = url
```

| Property value | Type     | Description         |
|:---------------|:---------|:--------------------|
| `url`          | `String` | The URL to override |

The default URL with event batching is:  
```bash
https://collect.tealiumiq.com/bulk-event/
```

The method is typically used to set a custom hostname, or to set a specific region hostname. The following example sets the Tealium Collect base URL to stay within the EU Central region:

```swift
let url = "https://collect-eu-central-1.tealiumiq.com/bulk-event/"
config.overrideCollectBatchURL = url
```

### `overrideCollectDomain`

Overrides the default Collect domain. Set the value to a hostname with the protocol excluded, such as `my-company.com`. Use this property for both batch and single event dispatches. If `overrideCollectURL` or `overrideCollectBatchURL` is populated, this property takes precedence.

```swift
config.overrideCollectDomain = "my-company.com"
```

### `overrideConsentCategoriesKey`

Overrides the name of the consent categories attribute sent in consent events. Use this to support custom enforcement of server-side consent. The default value is `consent_categories`.

```swift
config.overrideConsentCategoriesKey = "consent_categories_granted"
```

Default consent event:
```
{
    "tealium_event"      : "grant_partial_consent",
    "policy"             : "gdpr",
    "consent_categories" : ["Affiliates", "Social"]
}
```

Consent event with override:
```
{
    "tealium_event"              : "grant_partial_consent",
    "policy"                     : "gdpr",
    "consent_categories_granted" : ["Affiliates", "Social"]
}
```

Learn more about [disabling automatic enforcement of server-side consent](https://docs.tealium.com/server-side-consent-management/).


### `publishSettingsProfile`

Overrides the publish settings profile.

```swift
config.publishSettingsProfile = "main"
```

### `publishSettingsURL`

Overrides the publish settings URL.

```swift
config.publishSettingsURL = "https://www.example.com/custom/publish/settings.html"
```

### `remoteAPIEnabled`

Enables or disables `remote_api` event. Required for RemoteCommands module if DispatchQueue module in use. Default `false`.

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
Disables the built-in remote HTTP command (see [Swift Module: RemoteCommands](https://docs.tealium.com/platforms/ios-swift/module-list/remote-commands/)).

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
Enables or disables the Apple Search Ads API in the Attribution module (default: disabled).

```swift
config.searchAdsEnabled = true
```

### `sendCrashDataOnCrashDetected`
Sends a crash event when a crash is detected and only adds crash data to that event (default: false).

```swift
config.sendCrashDataOnCrashDetected = true
```

### `sendDeepLinkEvent`
Sends a `deep_link` event with related data every time a deep link is received (default: false).

```swift
config.sendDeepLinkEvent = true
```

### `sessionCountingEnabled`
Disables session counting for Tealium iQ accounts. Use this if you are self-hosting your Tealium JavaScript files (default: true).

```swift
config.sessionCountingEnabled = false
```

### `shouldAddCookieObserver`

If set to `true` (default), this method determines whether to add a `WKWebView` cookie observer to successfully migrate all cookies. If set to `false`, if multiple cookie observers are present then only one of them is called, which may cause some cookies to not migrate.


```swift
config.shouldAddCookieObserver = false
```


<blockquote>
The [`shouldAddCookieObserver`](#shouldaddcookieobserver) property permits using your own cookie observer during cookie synchronization, which requires a cookie observer to retrieve cookies on the main thread after setting them. This issue is caused by bugs in `WKWebView`, which prevents your own observer from being called.
</blockquote>
  

### `shouldUseRemotePublishSettings`

Sets the [Mobile Publish Settings](https://docs.tealium.com/creating-a-mobile-profile/) (version 1.9.0+) to enabled (default) or disabled.

```swift
config.shouldUseRemotePublishSettings = false
```


<blockquote>
Mobile Publish Settings are enabled by default, and must be disabled if you don’t want to use them. Configure the Mobile Publish Settings in iQ Tag Management, or disable the feature using `config.shouldUseRemotePublishSettings = false` in the Swift installation. Failure to do causes initialization failures and prevents tracking.
</blockquote>


### `skAdAttributionEnabled`
Enables or disables the Apple SKAdNetwork API in the Attribution module (default: disabled).                         

```swift
config.skAdAttributionEnabled = true
```

### `skAdConversionKeys`
Dictionary defining the event for which to call the `SKAdNetwork.updateConversionValue()` method and the key to use as the conversion value.                         

```swift
config.skAdConversionKeys = ["purchase": "number_of_coins"]
```

In this case, the below event will equate to: `SKAdNetwork.updateConversionValue(40)`

```swift
tealium?.track("purchase", dataLayer: ["number_of_coins": 40])
```

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
TealiumConfig(account:String, profile:String, environment:String, dataSource:String)
```

| Parameter     | Type     | Description                                 | Example               |
|:--------------|:---------|:--------------------------------------------|:----------------------|
| `account`     | `String` | Tealium account name                        | `companyXYZ`          |
| `profile`     | `String` | Tealium profile name                        | `main`                |
| `environment` | `String` | Tealium environment name                    | [`dev`, `qa`, `prod`] |
| `datasource`  | `String` | (Optional) Tealium data source key from CDH | `abc123`              |


### `timedEventTriggers`

A list of `TimedEventTrigger` objects for automatically tracking timed events.

```swift
config.timedEventTriggers = [TimedEventTrigger(start: "START_EVENT",
                                               stop: "STOP_EVENT",
                                               name: "TIMED_EVENT_NAME")]
```
The following are `TimedEventTrigger` parameters:  

| Parameter | Type      | Description                                                           |
|:----------|:----------|:----------------------------------------------------------------------|
| `start`   | `String`  | Name of the `TealiumEvent` to start the timed event                   |
| `stop`    | `String`  | Name of the `TealiumEvent`  to stop the timed event                   |
| `name`    | `String?` | (Optional) Name of timed event (default: `"START_EVENT::STOP_EVENT"`) |


### `updateDistance`

Sets the distance interval (meters) in which location updates are received.


<blockquote>
Only use this method if `useHighAccuracy` is set to `true`.
</blockquote>



```swift
config.updateDistance = <Double>
```

| Type     | Description                                                           | Example |
|:---------|:----------------------------------------------------------------------|:--------|
| `Double` | The distance interval (meters) in which location updates are received | `150.0` |

Usage example:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE")
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```

### `useHighAccuracy`

Sets the location precision to low accuracy (default) or high accuracy.

The property is disabled by default, which sets the location precision to low accuracy. If the location enabled device moves 500 meters or more, then this is considered a significant location changes causing a location update. Location updates typically take longer than five minutes with this setting.

Learn more about [Apple's significant-change location service](https://developer.apple.com/documentation/corelocation/getting_the_user_s_location/using_the_significant-change_location_service).

If enabled, the property sets the location of data precision to the highest possible accuracy. The initial event is delivered as quickly as possible and then continues to determine the location and delivers additional events, as necessary, when that data is available.

Learn more about [Apple's accuracy of location data](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423836-desiredaccuracy?language=swift).

Using high accuracy results in greater battery consumption for your device than low accuracy, due to more frequent location updates.   

```swift
config.useHighAccuracy = <Bool>
```

| Type      | Description                     | Example |
|:----------|:--------------------------------|:--------|
| `Boolean` | Sets the location data accuracy | `true`  |


Usage example:

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE")
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```

### `visitorIdentityKey`

Used to enable visitor switching on the specified `visitorIdentityKey` in the data layer.

Example:   

```swift
  func start() {
      let customerIdentifierKey = "customer_id"
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE")
      config.visitorIdentityKey = customerIdentifierKey
      // use the same customerIdentifierKey for storing a specific customer identifier in the data layer
  }
```

### `webviewProcessPool`

Prevent cookie synchronization issues if your app contains other webviews besides the Tealium Tag Management webview. If you use a webview in your app, create and retain a singleton `WKProcessPool` instance and set it prior to instantiating Tealium.

Example:   

```swift
let processPool = MyApp.wkProcessPool
config.webviewProcessPool = processPool
```

### `webviewConfig`

Permits a custom `WKWebviewConfiguration` object to be passed, which is used by the Tealium Tag Management webview. If using this option instead of `webviewProcessPool` option, set the singleton `WKProcessPool` through the customizable `WKWebviewConfiguration` `processPool` property.


<blockquote>
It is recommended to use this option as it may be required if future API changes are made to `WKWebView`.
</blockquote>


Example:   

```swift
let processPool = MyApp.wkProcessPool
let configuration = WKWebViewConfiguration()
configuration.processPool = processPool
config.webviewConfig = configuration
```
