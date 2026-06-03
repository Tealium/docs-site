---
title: TealiumConfig
description: Reference guide for TealiumConfig class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/
---
## Class: `TealiumConfig`

The `TealiumConfig` class provides methods to set configuration options for the main `Tealium` class. The following document summarizes the commonly used methods and properties of the `TealiumConfig` class for Kotlin. Individual modules may also provide their own extensions for the TealiumConfig class if they are enabled - these are documented in the relevant module&#39;s own document.

| Method/Property                                                             | Description                                                                                  |
|:----------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------|
| [`adobeVisitorAuthState`](#adobevisitorauthstate)                           | Sets the current authentication state for the visitor.                                                                                                                           |
| [`adobeVisitorCustomVisitorId`](#adobevisitorcustomvisitorid)               | Sets the known visitor ID to the Adobe ECID, if it&#39;s known at initialization time. If the ECID changes in the future, call `linkECIDToKnownIdentifier` to update the visitor ID. |
| [`adobeVisitorDataProviderId`](#adobevisitordataproviderid)                 | Sets the data provider ID, provided by Adobe, which is required when linking an ECID to a known ID.                                                                              |
| [`adobeVisitorExistingEcid`](#adobevisitorexistingecid)                     | Sets the existing ECID from a previous installation to be used, such as the Adobe SDK, instead of requesting a new ECID.                                                         |
| [`adobeVisitorOrgId`](#adobevisitororgid)                                   | String containing the Adobe Org ID including the `@` portion.                                                                                                                    |
| [`adobeVisitorRetries`](#adobevisitorretries)                               | The number of allowed invalid visitor ID retries before a request fails, which results in tracking calls being sent anyway without an ECID.                                      |
| [`autoTrackingBlocklistFilename`](#autotrackingblocklistfilename)           | Sets the name of the local block list file.                                                  |
| [`autoTrackingBlocklistUrl`](#autotrackingblocklisturl)                     | Sets the URL of the remote block list file.                                                  |
| [`autoTrackingCollectorDelegate`](#autotrackingcollectordelegate)           | Sets the global delegate that executes for automatically tracked activities.                 |
| [`autoTrackingMode`](#autoTrackingBlocklistFilename)                        | Sets the tracking mode for the AutoTracking module.                                          |
| [`consentExpiry`](#consentexpiry)                                           | Sets the expiration of the user consent selections.                                                                                                                              |
| [`consentManagerEnabled`](#consentmanagerenabled)                           | Optional `Boolean` to enable/disable consent management functionality.                                                                                                           |
| [`consentManagerPolicy`](#consentmanagerpolicy)                             | Optional `ConsentPolicy` to determine which consent functionality to adhere to.                                                                                                  |
| [`consentManagerLoggingEnabled`](#consentmanagerloggingenabled)             | Optional `Boolean` to enable/disable logging of consent changes.                                                                                                                 |
| [`consentManagerLoggingUrl`](#consentmanagerloggingurl)                     | Optional `String` for the destination of any consent logging updates.                                                                                                            |
| [`consentManagerLoggingProfile`](#consentmanagerloggingprofile)             | Optional `String` to override the profile that Tealium Collect sends data to.                                                                                                            |
| [`deepLinkTrackingEnabled`](#deeplinktrackingenabled)                       | Enables or disables automatic tracking of deep links.                                                                                                                            |
| [`existingVisitorId`](#existingvisitorid)                                   | Set your own unique identifier, stored in   `tealium_visitor_id`.                                                                                                                            |
| [`hostedDataLayerMaxCacheTimeMinutes`](#hosteddatalayermaxcachetimeminutes) | Sets an expiration on the hosted data layer data.                                                                                                                                |
| [`hostedDataLayerEventMappings`](#hosteddatalayereventmappings)             | Sets the event mappings used by the hosted data layer module when looking up data layer IDs.                                                                                     |
| [`logLevel`](#loglevel)                                                     | Sets the log level property, which controls how much information is logged.                                                                                                      |
| [`remoteAPIEnabled`](#remoteapienabled)                                     | Enables or disables `remote_api` event. Required for the RemoteCommands module if the DispatchQueue module in use.                                     |
| [`sessionCountingEnabled`](#sessioncountingenabled)                         | Disables session counting for Tealium iQ accounts. Use this if you are self-hosting your Tealium JavaScript files                                        |
| [`TealiumConfig`](#tealiumconfig)                                           | Constructor method that creates an instance of `TealiumConfig`.                                                                                                                      |
| [`timedEventTriggers`](#timedeventtriggers)                                 | A list of `EventTrigger` objects for automatically tracking timed events.                                        |
| [`useRemoteLibrarySettings`](#useremotelibrarysettings)                     | Optional `Boolean` to enable or disable the [Mobile Publish Settings]() (default: disabled). Configure the Mobile Publish Settings in iQ Tag Management, or disable the feature. |

### `adobeVisitorAuthState`

Sets the current authentication state for the visitor.

Example:

```java
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_AUTHENTICATED
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_LOGGED_OUT
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_UNKNOWN
```

### `adobeVisitorCustomVisitorId`

Sets the known visitor ID to the Adobe ECID, if it&#39;s known at initialization time. If the ECID changes in the future, call [`linkECIDToKnownIdentifier`](/platforms/android-kotlin/api/tealium/#linkecidtoknownidentifier) to update the visitor ID.

```java
config.adobeVisitorCustomVisitorId = &#34;20381482060927465156359999806251989655&#34;
```

### `adobeVisitorDataProviderId`

Sets the data provider ID, provided by Adobe, which is required when linking an ECID to a known ID.

```java
config.adobeVisitorDataProviderId = &#34;01&#34;
```

### `adobeVisitorExistingEcid`

Sets the existing ECID from a previous installation to be used, such as the Adobe SDK, instead of requesting a new ECID.                                                         

Example:

```java
config.adobeVisitorExistingEcid = &#34;20381482060927465156359999806251989655&#34;
```

### `adobeVisitorOrgId`

String containing the Adobe Org ID including the `@` portion. If the Org ID is not provided, the module is not initialized and no visitor ID is retrieved. Tracking calls continue as normal without an Adobe ECID.

```java
config.adobeVisitorOrgId = STRING_VALUE
```

Example:

```java
config.adobeVisitorOrgId = &#34;1A2A111A111150AA0A110A12@AdobeOrg&#34;
```

### `adobeVisitorRetries`

The number of allowed invalid visitor ID retries before a request fails, which results in tracking calls being sent anyway without an ECID.

Example:

```java
config.adobeVisitorRetries = 5
```

### `autoTrackingBlocklistFilename`

For use with the [AutoTracking Module](/platforms/android-kotlin/module-list/autotracking/#block-list).

Sets the name of a JSON formatted block list file that contains a list of activities to omit from automatic tracking. The file should be available in the Android `assets` directory.

```kotlin
config.autoTrackingBlocklistFilename = &#34;autotracking-blocklist.json&#34;
```

### `autoTrackingBlocklistUrl`

For use with the [AutoTracking Module](/platforms/android-kotlin/module-list/autotracking/#block-list).

Sets a URL to a JSON formatted block list file that contains a list of activities to omit from automatic tracking.

```kotlin
config.autoTrackingBlocklistUrl = &#34;https://example.com/autotracking-blocklist.json&#34;
```

### `autoTrackingCollectorDelegate`

For use with the [AutoTracking Module](/platforms/android-kotlin/module-list/autotracking/#custom-data).

Sets a global delegate that executes for activities tracked by the [AutoTracking module](/platforms/android-kotlin/module-list/autotracking/). Edit this delegate to customize the data included with specific activities.

```kotlin
config.autoTrackingCollectorDelegate = myCollectorDelegate
```

### `autoTrackingMode`

Sets the level of tracking for the [AutoTracking module](/platforms/android-kotlin/module-list/autotracking/).

* `FULL`  
Track all activities except those annotated with `@Autotracked(track=false)`.
* `ANNOTATED`  
Track only the activities that are annotated with `@Autotracked`.
* `NONE`  
Disable all automatic tracking (for debug or dev builds of your app).

```kotlin
config.autoTrackingMode = AutoTrackingMode.FULL
```

### `Collectors`

Collectors are modules that gather supplemental information from the device and append it to the data layer before it&#39;s transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors. Default collectors are denoted by a `*` next to the collector name.

| Collector Name  | TealiumConfig Reference   |
|:----------------|:--------------------------|
| `AdobeVisitor`  | `Collectors.AdobeVisitor` |
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

These modules are enabled or disabled using the [`TealiumConfig`](/platforms/android-kotlin/api/tealium-config/) `collectors` property.

The following example adds to existing list of collectors you&#39;re using:  

```java
val config = TealiumConfig(collectors = mutableSetOf(Collectors.AdobeVisitor))
```

### `consentExpiry`

Sets the expiration time of the user consent selections. Set this property prior to Tealium initialization. The default expiration times for consent selections are:

- CCPA: 395 days
- GDPR: 365 days

The following sets the consent expiry to 90 days.

```java
config.consentExpiry = ConsentExpiry(90, TimeUnit.DAYS)
```

### `consentManagerEnabled`

Sets whether the ConsentManager module is enabled or not. It is also required to set a Policy through `consentManagerPolicy`.

```java
config.consentManagerEnabled = true  // enable
```

### `consentManagerPolicy`

Sets the `ConsentPolicy` that is adhered to within the app. This policy controls whether or not Dispatches are queued and dropped throughout the SDK in accordance with the relevant legal requirements.

```java
config.consentManagerPolicy = ConsentPolicy.GDPR
```

### `consentManagerLoggingEnabled`

Sets whether changes in consent preferences need to be sent to a remote server to be recorded.

```java
config.consentManagerLoggingEnabled = true
```

### `consentManagerLoggingProfile`

Overrides the profile that Tealium Collect sends data to.

```java
config.consentManagerLoggingProfile = &#34;us-mobile&#34;
```

### `consentManagerLoggingUrl`

Sets the URL used when logging consent preference changes.

```java
config.consentManagerLoggingUrl = url
```

### `deepLinkTrackingEnabled`

Enables or disables automatic tracking of standard deep links, such as links to the app from Facebook or other sources, as well as QR trace. Enabled by default.

```java
config.deepLinkTrackingEnabled = true
```

### `existingVisitorId`

Sets the data layer value for `tealium_visitor_id`. Use this when you have your own unique identifier.

```java
config.existingVisitorId = &#34;8243d23b56d5488571027547bc72d93&#34;
```

### `hostedDataLayerMaxCacheTimeMinutes`

Sets an expiration on the hosted data layer data. If this property isn&#39;t set, hosted data layer items persist for 7 days by default, and are re-downloaded from Tealium once this period has expired.

```java
hostedDataLayerMaxCacheTimeMinutes = 30
```

If your hosted data layer is frequently updated, setting a lower value may impact battery life due to increased network requests.

### `hostedDataLayerEventMappings`

Sets the hosted data layer keys (lookup variables) used by the hosted data layer module when retrieving data layer IDs. The key is the value in the `tealium_event` key of a dispatch.

```java
hostedDataLayerEventMappings = mapOf(&#34;pdp&#34; to &#34;product_id&#34;)
```

### `logLevel`

Sets the log level property to control how much information is logged. Setting this property overrides the default value that comes from the `environment` property in `TealiumConfig`.

Set log level to one of the following values:  

| Log Level | Log Activity Description                                                                       |
|:----------|:-----------------------------------------------------------------------------------------------|
| `DEV`     | Debug-level events used for debugging an application (recommended for development environment) .|
| `QA`      | Informational events that highlight the progress of the application.                        |
| `PROD`    | Error events such as critical errors and failures.                                             |
| `SILENT`  | No logging.                                                                                    |


```java
config.logLevel = LogLevel.DEV
```

View your development logs in the Android Studio using LogCat. View your production logs with the LogCat app by connecting your Android device.

### `remoteAPIEnabled`

Enables or disables `remote_api` event. Required for RemoteCommands module if DispatchQueue module in use. Default `false`.

```swift
config.remoteAPIEnabled = true
```

### `sessionCountingEnabled`
Disables session counting for Tealium iQ accounts. Use this if you are self-hosting your Tealium JavaScript files. Default `true`.                        

```swift
config.sessionCountingEnabled = false
```

### `TealiumConfig`

Constructor method that creates a `TealiumConfig` instance.

```java
val config = TealiumConfig(
      application,
      account,
      profile,
      environment);
```

The `TealiumConfig` instance is configured with the following parameters:

| Parameters    | Type          | Description              | Example            |
|:--------------|:--------------|:-------------------------|:-------------------|
| `application` | `Application` | The application instance | `applicationObj`   |
| `account`     | `String`      | Tealium account name     | `&#34;companyXYZ&#34;`     |
| `profile`     | `String`      | Tealium profile name     | `&#34;main&#34;`           |
| `environment` | `String`      | Tealium environment name | `Environment.PROD` |

The following is an example:

```java
// Assuming execution is within Application.onCreate()
val config = TealiumConfig(this, &#34;ACCOUNT_NAME&#34;, &#34;PROFILE_NAME&#34;, Environment.PROD)

// Add required Dispatchers
config.dispatchers.addAll(setOf(CollectDispatcher, TagManagementDispatcher))

// Add required Modules
config.modules.add(VisitorService)

// Automatic tracking mode
config.autoTrackingMode = AutoTrackingMode.FULL // (FULL, ANNOTATED, NONE)
```

### `timedEventTriggers`

A list of `EventTrigger` objects for automatically tracking timed events.

```kotlin
val config = TealiumConfig(…).apply {
  timedEventTriggers = mutableListOf(
     EventTrigger.forEventName(
       start_event,
       stop_event,
       timed_event_name)
  )  
}
```

The following are `EventTrigger` parameters:  

| Parameter          | Type      | Description                                                           |
|:-------------------|:----------|:----------------------------------------------------------------------|
| `start_event`      | `String`  | Name of the `TealiumEvent` to start the timed event                   |
| `stop_event`       | `String`  | Name of the `TealiumEvent` to stop the timed event                    |
| `timed_event_name` | `String?` | (Optional) Name of timed event (default: `&#34;start_event::stop_event&#34;`) |

### `useRemoteLibrarySettings`

Optional `Boolean` to enable or disable the [Mobile Publish Settings]() (default: disabled). Configure the Mobile Publish Settings in iQ Tag Management, or disable the feature.                     

```swift
config.useRemoteLibrarySettings = true
```