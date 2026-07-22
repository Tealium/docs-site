---
title: TealiumConfig
description: A class to set configuration options for the main Tealium class. Individual modules provide their own extensions for the `TealiumConfig` class if they are enabled.
url: https://docs.tealium.com/platforms/flutter/api/tealium-config/
---
## `TealiumConfig`

The following summarizes the properties of the `TealiumConfig` class.

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `String` | (Required) Tealium account name | `companyXYZ`|
| `batchingEnabled` | `bool` | Enables or disables event batching (default: disabled) | `false` |
| `collectors` | `List<Collectors>` | (Required) Sets the list of [`Collectors`](#collectors) to initialize the Tealium library with | `[Collectors.AppData]` |
| `consentExpiry`| [`ConsentExpiry`](#consentexpiry) | Sets the expiration of the user's consent preferences (default is dependent upon policy) | `ConsentExpiry(90, TimeUnit.DAYS)` |
| `consentLoggingEnabled` | `bool` | Enables the [Consent Logging](https://docs.tealium.com/consent-change-event-specifications/) feature, which sends all consent status changes to Tealium Customer Data Hub for auditing purposes. (default: enabled) | `true` |
| `consentPolicy`| [`ConsentPolicy`](#consentpolicy) | Sets the consent policy, such as CCPA or GDPR. Consent manager is only enabled if this property is set. | `ConsentPolicy.GDPR` |
| `customVisitorId` | `String` | Set a custom Visitor ID | `ALK2398LSDKJ3289SLKJ3298SLKJ3`|
| `dataSource` | `String` | CDH data source key |`abc123` |
| `deepLinkTrackingEnabled` | `bool` | Enables or disables [automatic tracking of standard deep links](https://docs.tealium.com/platforms/getting-started-mobile/deep-linking/#readout), such as links to the app from Facebook or other sources, as well as QR trace.  (default: enabled) | `false` |
| `dispatchers` | `List<Dispatchers>` | (Required) Sets the list of [`Dispatchers`](#dispatchers) to initialize the Tealium library with| `[Dispatchers.Collect]` |
| `environment` | [`TealiumEnvironment`](#tealiumenvironment) | (Required) Tealium environment name |  `TealiumEnvironment.dev` |
| `lifecycleAutotrackingEnabled` | `bool` | Enables or disables lifecycle auto tracking. (default: enabled) | `false` |
| `loglevel`| [`LogLevel`](#loglevel) | Sets the log level property, which controls how much information is logged (default: silent) | `LogLevel.DEV` |
| `memoryReportingEnabled` | `bool` | Enables or disables memory reporting in the DeviceData module (default: disabled) | `true` |
| `overrideCollectBatchURL` | `String` | Overrides the Tealium Collect batch URL to send data to a different endpoint | `https://example.com/batch-event` |
| `overrideCollectDomain` | `String` | Overrides the Tealium Collect domain | `"custom-domain.example.com"` |
| `overrideCollectProfile` | `String` | Overrides the Tealium Profile sent in the tracking data. | `custom-profile` |
| `overrideCollectURL` | `String` | Overrides the Tealium Collect URL to send data to a different endpoint. If using the event batching feature, also override the `overrideCollectBatchURL` property. | `https://example.com/event` |
| `overrideLibrarySettingsURL` | `String` | Overrides the publish settings URL. | `https://example.com/mobile.html` |
| `overrideTagManagementURL` | `String` | Overrides the default URL used by the Tag Management module. This is needed if you are self-hosting your Tealium JavaScript files | `https://example.com/mobile.html` |
| `profile` | `String` | (Required) Tealium profile name | `main` |
| `qrTraceEnabled` | `bool` | Enables or disables [QR trace](https://docs.tealium.com/platforms/getting-started-mobile/trace/#how-it-works). (default: enabled) | `false` |
| `remoteCommands` | `List<RemoteCommand>` | List of remote commands to add during initialization | `[RemoteCommand("firebase", path: "firebase.json")]` |
| `sessionCountingEnabled` | `bool` | Enables or disables session counting for Tealium iQ accounts. Use this if you are self-hosting your Tealium JavaScript files (default: enabled) | `false` |
| `useRemoteLibrarySettings`| `bool` | Enables or disables the [Mobile Publish Settings](https://docs.tealium.com/creating-a-mobile-profile/) (default: enabled). Configure the Mobile Publish Settings in iQ Tag Management, or disable the feature. | `false` |
| [`visitorIdentityKey`](#visitoridentitykey) | `String` | Specifies the data layer key that represents the customer identifier. This key can be used to enable [visitor switching](https://docs.tealium.com/platforms/getting-started-mobile/identity-resolution/#visitor-switching). | |
| `visitorServiceEnabled`| `bool` | Enables or disables the automatic retrieval of the Visitor Profile using the [Data Layer Enrichment API](https://docs.tealium.com/data-layer-enrichment-api/) (default: disabled) | `true` |
| `webViewLoggingEnabled` | `bool` | Enables or disables WebView console logging (default: disabled) | `true` |


### `Collectors`

Collectors are modules that gather supplemental information from the device and append it to the data layer before it's transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors:

| Collector Name | TealiumConfig Reference |
| --- | --- |
| `AppData` (default) | `Collectors.AppData`|
| `Connectivity` (default) | `Collectors.Connectivity`|
| `DeviceData` | `Collectors.DeviceData`|
| `Lifecycle` | `Collectors.Lifecycle`|

These modules are enabled or disabled using the [`TealiumConfig`](https://docs.tealium.com/platforms/flutter/api/tealium-config/) `collectors` property.


### `ConsentExpiry`

Defines user consent preferences expiration.

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `time` | `int` | The amount of time before expiration | `90` |
| `unit` | `TimeUnit` | The unit of time before expiration | `TimeUnit.DAYS` |

Example:

```dart
ConsentExpiry(90, TimeUnit.DAYS)
```

The following time units are available:

| Time Unit | Description |
| --- | --- |
| `TimeUnit.DAYS`| Days|
| `TimeUnit.HOURS`| Hours|
| `TimeUnit.MINUTES`| Minutes|
| `TimeUnit.MONTHS`| Months|


### `ConsentPolicy`

Defines the consent policy to adhere to. If no consent policy is defined on the [`TealiumConfig`](https://docs.tealium.com/platforms/flutter/api/tealium-config/) object, the consent manager becomes disabled.

Example:

```dart
ConsentPolicy.GDPR
```

| Consent Policy | Description |
| --- | --- |
| `ConsentPolicy.GDPR` | GDPR |
| `ConsentPolicy.CCPA` | CCPA |


### `Dispatchers`

Dispatchers are modules that send the data from your data layer to a Tealium endpoint. The following dispatchers are currently available:

| Dispatcher Name | TealiumConfig Reference |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|


<blockquote>
At least one dispatcher is required. If no dispatchers are specified, no tracking occurs.
</blockquote>



### `Expiry`

Defines the expiration time for setting a property that expires.

Example:

```dart
Expiry.session
```

The following expiry options are available:

| Value | Description |
| :-- | :-- |
| `Expiry.session` (default)| The lifetime of the current active session |
| `Expiry.forever` |  Never expires while the app is installed |
| `Expiry.untilRestart` | Until the app restarts |

### `LogLevel`

Sets the `loglevel` property, which controls how much information is logged.

The following logging levels are available:

| Value | Description |
| --- | --- |
| `LogLevel.DEV` | Informational events that highlight the progress of the application |
| `LogLevel.QA` | Debug-level events used for debugging an application |
| `LogLevel.PROD` | Error events such as critical errors and failures |
| `LogLevel.SILENT` | No Logging (default) |

Example:

```dart
LogLevel.DEV
```

### `TealiumEnvironment`

The environment is one of three default environments (Dev, QA, Prod) or any custom environments that Tealium publishes to. Select one of these environments.

Example:

```dart
TealiumEnvironment.dev
```

| Value | Description |
| --- | --- |
| `TealiumEnvironment.dev` | Development |
| `TealiumEnvironment.qa` | QA/UAT |
| `TealiumEnvironment.prod` | Production |

### `visitorIdentityKey`

Used to enable visitor switching on the specified `visitorIdentityKey` in the data layer.