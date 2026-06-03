---
title: TealiumConfig
description: A class to set configuration options for the main Tealium class. Individual modules provide their own extensions for the TealiumConfig class if they are enabled.
url: https://docs.tealium.com/platforms/nativescript/api/tealium-config/
---
## `TealiumConfig`

The following summarizes the properties of the `TealiumConfig` class.

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `String` | (Required) Tealium account name | `companyXYZ`|
| `collectors` | `Collectors[]` | (Required) Sets the list of [`Collectors`](#collectors) to initialize the Tealium library with | `[Collectors.AppData]` |
| `consentExpiry`| [`ConsentExpiry`](#consentexpiry) | Sets the expiration of the user&#39;s consent preferences. (default is dependent upon policy) | `new ConsentExpiry(90, TimeUnit.days)` |
| `consentLoggingEnabled`| `Boolean` | Enables the [Consent Logging]() feature, which sends all consent status changes to Tealium Customer Data Hub for auditing purposes. (default: enabled) | `true` |
| `consentPolicy`| [`ConsentPolicy`](#consentpolicy) | Sets the consent policy, such as CCPA or GDPR. Consent manager is only enabled if this property is set. | `ConsentPolicy.gdpr` |
| `customVisitorId` | `String` | Sets a custom Visitor Id | `ALK2398LSDKJ3289SLKJ3298SLKJ3` |
| `dataSource` | `String` | CDH data source key | `abc123` |
| `deepLinkTrackingEnabled` | `Boolean` | Enables or disables [automatic tracking of standard deep links](/platforms/getting-started-mobile/deep-linking/#readout), such as links to the app from Facebook or other sources, as well as QR trace.  (default: enabled) | `false` |
| `dispatchers` | `Dispatchers[]` | (Required) Sets the list of [`Dispatchers`](#dispatchers) to initialize the Tealium library with| `[Dispatchers.Collect]` |
| `environment` | [`TealiumEnvironment`](#tealiumenvironment) | (Required) Tealium environment name |  `TealiumEnvironment.dev` |
| `loglevel`| [`LogLevel`](#loglevel) | Sets the log level property, which controls how much information is logged (default: silent) | `LogLevel.dev` |
| `lifecycleAutotrackingEnabled`| `Boolean` | Enables or disables lifecycle auto tracking. (default: enabled) | `false` |
| `memoryReportingEnabled` | `Boolean` | Enables or disables memory reporting in the DeviceData module (default: disabled). | `true` |
| `overrideCollectURL`| `String` | Overrides the Tealium Collect URL to send data to a different endpoint. If using the event batching feature, also override the `overrideCollectBatchURL` property. | `https://custom-domain.com/event` |
| `overrideCollectBatchURL`| `String` | Overrides the Tealium Collect batch URL to send data to a different endpoint. | `https://custom-domain.com/batch-event` |
| [`overrideCollectProfile`](#overridecollectprofile)| `String` | Overrides the Tealium Collect profile to send data to a different Tealium profile. | `custom-profile` |
| [`overrideCollectDomain`](#overridecollectdomain)| `String` | Overrides the domain name in the Tealium Collect URL to send data to a different endpoint. | `custom-domain` |
| `overrideLibrarySettingsURL` | `String` | Overrides the publish settings URL. | `https://custom-domain.com/mobile.html` |
| `overrideTagManagementURL` | `String` | Overrides the default URL used by the Tag Management module. This is needed if you are self-hosting your Tealium JavaScript files. | `https://custom-domain.com/path/env/utag.js` |
| `profile` | `String` | (Required) Tealium profile name | `main` |
| `qrTraceEnabled` | `Boolean` | Enables or disables [QR trace](/platforms/getting-started-mobile/trace/#mobile-trace-tool). (default: enabled) | `false` |
| [`sessionCountingEnabled`](#sessioncountingenabled) | `Boolean` | Enables or disables session counting for Tealium iQ accounts. Set this to `false` if you are self-hosting your Tealium JavaScript files. (default: enabled) | `false` |
| `useRemoteLibrarySettings`| `Boolean` | Enables or disables the [Mobile Publish Settings]() (default: enabled) Configure the Mobile Publish Settings in iQ Tag Management, or disable the feature. | `false` |
| `visitorServiceEnabled`| `Boolean` | Enables or disables the automatic retrieval of the Visitor Profile using the [Data Layer Enrichment API]() (default: disabled) | `true` |
| `visitorServiceRefreshInterval`| `String` | Sets the number of minutes between visitor profile refreshes. Only integers are supported, for example, &#34;2&#34; would be 2 minutes. | `&#34;2&#34;` |


### `Collectors`

Collectors are modules that gather supplemental information from the device and append it to the data layer before it&#39;s transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors. Default collectors are denoted by a `*` next to the collector name.

| Collector Name | TealiumConfig Reference |
| --- | --- |
| `AppData`* | `Collectors.AppData`|
| `Connectivity`* | `Collectors.Connectivity`|
| `Device` | `Collectors.Device`|
| `Lifecycle` | `Collectors.Lifecycle`|

These modules are enabled or disabled using the [`TealiumConfig`](/platforms/nativescript/api/tealium-config/) `collectors` property.


### `ConsentPolicy`

Defines the consent policy to adhere to. If no consent policy is defined on the [`TealiumConfig`](/platforms/nativescript/api/tealium-config/) object, the consent manager becomes disabled.

Example:

`ConsentPolicy.gdpr`

The following consent policies are available:

| Value | Description |
| --- | --- |
| `.gdpr` | GDPR |
| `.ccpa` | CCPA |


### `ConsentExpiry`

Defines user consent preferences expiration.

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `time` | `Number` | The amount of time before expiration | `90` |
| `unit` | `TimeUnit` | The unit of time before expiration | `TimeUnit.days` |

Example:

`new ConsentExpiry(90, TimeUnit.days)`

#### TimeUnit

The following time units are available:

| Value | Description |
| --- | --- |
| `.minutes` | Minutes |
| `.hours` | Hours |
| `.days` | Days |
| `.months` | Months |


### `Dispatchers`

Dispatchers are modules that send the data from your data layer to a Tealium endpoint. The following dispatchers are currently available:

| Dispatcher Name | TealiumConfig Reference |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|

At least one dispatcher is required. If no dispatchers are specified, no tracking occurs.


### `LogLevel`

Sets the `logLevel` property, which controls how much information is logged.

The following logging levels are available:

| Value | Description |
| --- | --- |
| `LogLevel.dev` | Informational events that highlight the progress of the application |
| `LogLevel.qa` | Debug-level events used for debugging an application |
| `LogLevel.prod` | Error events such as critical errors and failures |
| `LogLevel.silent` | No Logging (default) |

### `overrideCollectProfile`

Overrides the Tealium Collect profile to send data to a different Tealium profile.

```swift
config.overrideCollectProfile = &#34;main&#34;
```

### `overrideCollectDomain`

Overrides the domain name in the Tealium Collect URL to send data to a different endpoint.

```swift
config.overrideCollectDomain = &#34;my-company.com&#34;
```

### `sessionCountingEnabled`
Enables or disables session counting for Tealium iQ accounts. Set this to `false` if you are self-hosting your Tealium JavaScript files (default: enabled).                         

```swift
config.sessionCountingEnabled = false
```

### `TealiumEnvironment`

The environment is one of three default environments (Dev, QA, Prod) or any custom environments that Tealium publishes to. Select one of these environments.

Example:

`TealiumEnvironment.dev`

| Value | Description |
| --- | --- |
| `.dev` | Development |
| `.qa` | QA/UAT |
| `.prod` | Production |


### `VisitorProfile`

The visitor profile is an object that contains friendly names for each attribute. There is a `currentVisit` property that lets you distinguish visitor/visit attribute types. Access each attribute value by ID using a subscript. If the attribute does not exist, `null` is returned. See the below list for examples.

**Attribute Types**

| Parameters | Properties | Value |
| --- | --- | --- |
| `arraysOfBooleans` | id: String, value: Boolean[]   | `id: &#34;5129&#34;, value: [true,false,true,true]` |
| `arraysOfNumbers`  | id: String, value: Number[]    | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]` |
| `arraysOfStrings`  | id: String, value: String[]    | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]` |
| `audiences`        | id: String, value: String      | `id: &#34;tealiummobile\_demo\_103&#34;, value: &#34;iOS Users&#34;` |
| `badges`           | id: String, value: Boolean     | `id: &#34;2815&#34;, value: true` |
| `booleans`         | id: String, value: Boolean     | `id: &#34;4868&#34;, value: true` |
| `currentVisit`     | All attributes for current visit visitorProfile. The current visit profile does not contain Audiences or Badges. | `TealiumCurrentVisitProfile(dates: [&#34;5376&#34;: 1567536668080, &#34;10&#34;: 1567536668000], booleans: [&#34;4530&#34;: true], numbers: [&#34;32&#34;: 3.8])`  |
| `dates`            | id: String, value: Number      | `id: &#34;22&#34;, value: 1567120112000` |
| `numbers`          | id: String, value: Number      | `id: &#34;5728&#34;, value: 4.82125` |
| `setOfStrings`     | id: String, value: Set(String) | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]` |
| `strings`          | id: String, value: String      | `id: &#34;5380&#34;, value: &#34;green shirts&#34;` |
| `tallies`          | id: String, value: Object      | `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]` |
| `tallyValue`       | id: String, value: Number      | `[&#34;category 1&#34;: 2.0]` |
