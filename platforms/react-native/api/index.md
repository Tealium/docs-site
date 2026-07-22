---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for React Native.
url: https://docs.tealium.com/platforms/react-native/api/
---
## Class: `Tealium`

The following summarizes the commonly used methods of the `Tealium` class for React Native library.

| Method                                                      | Description                                                           |
|:------------------------------------------------------------|:----------------------------------------------------------------------|
| [`addRemoteCommand()`](#addRemoteCommand)                   | Adds a remote command to the remote command manager                   |
| [`addData()`](#addData)                                     | Adds data to persistent data layer                                    |
| [`gatherTrackData()`](#gatherTrackData)                     | Gathers all track data from collectors and data layer                 |
| [`getData()`](#getData)                                     | Retrieves a specified value from the data layer                       |
| [`getConsentCategories()`](#getConsentCategories)           | Retrieves the user's consented categories                             |
| [`getConsentStatus()`](#getConsentStatus)                   | Retrieves the user's consent status                                   |
| [`getSessionId()`](#getSessionId)                           | Retrieves the current `tealium_session_id`                            |
| [`getVisitorId()`](#getVisitorId)                           | Retrieves the current Visitor ID                                      |
| [`initialize()`](#initialize)                               | Initializes Tealium with configuration parameters                     |
| [`joinTrace()`](#joinTrace)                                 | Joins a trace with the given ID                                       |
| [`leaveTrace()`](#leaveTrace)                               | Leaves active trace session                                           |
| [`removeData()`](#removeData)                               | Remove persistent data that has been previously set using `addData()` |
| [`removeRemoteCommand()`](#removeRemoteCommand)             | Removes a remote command from the remote command manager              |
| [`setConsentCategories()`](#setConsentCategories)           | Sets the consent categories of a user                                 |
| [`setConsentExpiryListener()`](#setConsentExpiryListener)   | Sets the consent expired listener/callback                            |
| [`setConsentStatus()`](#setConsentStatus)                   | Sets the consent status of a user                                     |
| [`setVisitorServiceListener()`](#setVisitorServiceListener) | Defines the visitor service listener/callback                         |
| [`terminateInstance()`](#terminateInstance)                 | Disables and destroys the Tealium instance                            |
| [`track()`](#track)                                         | Track an event or screen view                                         |

### `addRemoteCommand()`

Adds a remote command to the remote command manager.

```javascript
Tealium.addRemoteCommand(id, callback);
```

| Parameters | Type        | Description                                                                                                                                                     | Example          |
|:-----------|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `String`    | Name of the command ID from the tag configuration                                                                                                               | `"test_command"` |
| `callback` | `Function ` | A callback function to execute after the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example)    |

Example:

```javascript
Tealium.addRemoteCommand("firebase", payload => {

  var eventName = payload["firebase_event_name"];
  var eventProperties = payload["firebase_event_properties"];

  analytics.logEvent(eventName, eventProperties);
});
```

### `addData()`

Adds data to the persistent data storage for the given expiration.

```javascript
Tealium.addData(data, expiry);
```
| Parameters | Type                | Description                                                                                                   | Example                                   |
|:-----------|:--------------------|:--------------------------------------------------------------------------------------------------------------|:------------------------------------------|
| `data`     | `Object`            | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{"persistent_key2" : "persistent_val2"}` |
| `expiry`   | [`Expiry`](#expiry) | Length of time for which to persist the data                                                                  | `Expiry.forever`                          |

### Collectors

Collectors are modules that gather supplemental information from the device and append it to the data layer before it's transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors. Default collectors are denoted by a `*` next to the collector name.

| Collector Name   | TealiumConfig Reference     |
|:-----------------|:----------------------------|
| `AppData`*       | `Collectors.AppData`        |
| `Connectivity`*  | `Collectors.Connectivity`   |
| `Device`         | `Collectors.Device`         |
| `Lifecycle`      | `Collectors.Lifecycle`      |
| `VisitorService` | `Collectors.VisitorService` |

These modules are enabled or disabled using the [`TealiumConfig`](#tealiumconfig) `collectors` property as described below

### ConsentExpiry

Defines the consent preferences expiration

| Parameters | Type       | Description                          | Example         |
|:-----------|:-----------|:-------------------------------------|:----------------|
| `time`     | `Number`   | The amount of time before expiration | `90`            |
| `unit`     | `TimeUnit` | The unit of time before expiration   | `TimeUnit.days` |

Example:

`ConsentExpiry(90, TimeUnit.days)`

#### TimeUnit

| Value    | Description |
|:---------|:------------|
| .minutes | Minutes     |
| .hours   | Hours       |
| .months  | Months      |
| .days    | Days        |

### ConsentPolicy

Defines the consent policy to adhere to. If no consent policy is defined on the [`TealiumConfig`](#tealiumconfig) object, the consent manager will be disabled.

Example:

`ConsentPolicy.gdpr`

| Value | Description |
|:------|:------------|
| .gdpr | GDPR        |
| .ccpa | CCPA        |

### Dispatchers

Dispatchers are modules that send the data from your data layer and send it to a Tealium endpoint. The following dispatchers are currently available:

| Dispatcher Name  | TealiumConfig Reference      |
|:-----------------|:-----------------------------|
| `Collect`        | `Dispatchers.Collect`        |
| `RemoteCommands` | `Dispatchers.RemoteCommands` |
| `TagManagement`  | `Dispatchers.TagManagement`  |


<blockquote>
At least one dispatcher is required. If no dispatchers are specified, your data is not sent anywhere.
</blockquote>


### Expiry

Defines the custom data expiration

Example:

`Expiry.session`

| Parameters | Type       | Description                          | Example         |
|:-----------|:-----------|:-------------------------------------|:----------------|
| `time`     | `Number`   | The amount of time before expiration | `90`            |
| `unit`     | `TimeUnit` | The unit of time before expiration   | `TimeUnit.days` |

Example:

`ConsentExpiry(90, TimeUnit.days)`

#### TimeUnit

| Value    | Description |
|:---------|:------------|
| .minutes | Minutes     |
| .hours   | Hours       |
| .months  | Months      |
| .days    | Days        |

### `gatherTrackData()`

Gathers all track data from Collectors and data layer.

```javascript
Tealium.gatherTrackData(callback);
```

| Parameters | Type       | Description                                          | Example       |
|:-----------|:-----------|:-----------------------------------------------------|:--------------|
| `callback` | `Function` | A Callback function to use the retrieved value for key. The callback returns a JSON object. | (see example) |

Example:

```javascript
Tealium.gatherTrackData(value => {
   console.log("Track data: " + JSON.stringify(value))
});
```

### `getData()`

Retrieves the value for a specified key in the persistent data layer, then returns in the form of a callback function.

```javascript
Tealium.getData(key, callback);
```

| Parameters | Type       | Description                                          | Example       |
|:-----------|:-----------|:-----------------------------------------------------|:--------------|
| `key`      | `String`   | Key to retrieve from the data layer                  | (see example) |
| `callback` | `Function` | Callback function to use the retrieved value for key | (see example) |

Example:

```javascript
Tealium.getData('test_session_key', value => {
   console.log("Value: " + value)
});
```

### `getConsentCategories()`

Retrieves the user's consented categories.

```javascript
Tealium.getConsentCategories(callback);
```

| Parameters | Type       | Description                                     | Example       |
|:-----------|:-----------|:------------------------------------------------|:--------------|
| `callback` | `Function` | Callback function to use the consent categories | (see example) |

Example:

```javascript
Tealium.getConsentCategories(categories => {
    console.log("Consent Categories: " + categories)
});
```

### `getConsentStatus()`

Retrieves the user consent status and returns in the form of a callback function.

```javascript
Tealium.getConsentStatus(callback);
```

| Parameters | Type       | Description                                 | Example       |
|:-----------|:-----------|:--------------------------------------------|:--------------|
| `callback` | `Function` | Callback function to use the consent status | (see example) |

Example:

```javascript
Tealium.getConsentStatus(status => {
    console.log("Consent Status: " + status)
});
```

### `getSessionId()`

Retrieves the current Session ID and returns in the form of a callback function.

```javascript
Tealium.getSessionId(callback);
```

| Parameters | Type       | Description                             | Example       |
|:-----------|:-----------|:----------------------------------------|:--------------|
| `callback` | `Function` | Callback function to use the Session ID | (see example) |

Example:

```javascript
Tealium.getSessionId(value => {
    console.log("Sesssion ID: " + value)
});
```

### `getVisitorId()`

Retrieves the user's visitor ID and returns in the form of a callback function.

```javascript
Tealium.getVisitorId(callback);
```

| Parameters | Type       | Description                             | Example       |
|:-----------|:-----------|:----------------------------------------|:--------------|
| `callback` | `Function` | Callback function to use the Visitor ID | (see example) |

Example:

```javascript
Tealium.getVisitorId(value => {
    console.log("Visitor ID: " + value)
});
```

### `initialize()`

Initialize Tealium before calling any other method.

```javascript
Tealium.initialize(config);
```

| Parameters | Type                              | Description                                                      | Example       |
|:-----------|:----------------------------------|:-----------------------------------------------------------------|:--------------|
| `config`   | [`TealiumConfig`](#tealiumconfig) | Tealium configuration parameters                                 | (see example) |
| `callback` | `Function`                        | (Optional) Callback function after the Tealium instance is ready | (see example) |

Example:

```javascript
let config: TealiumConfig =
{
	account: 'tealiummobile',
	profile: 'demo',
	environment: TealiumEnvironment.dev,
	dispatchers: [Dispatchers.Collect,
	 			  Dispatchers.TagManagement,
	  			  Dispatchers.RemoteCommands],
	collectors: [Collectors.AppData,
				 Collectors.DeviceData,
				 Collectors.Lifecycle,
				 Collectors.Connectivity],
	consentLoggingEnabled: true,
	consentPolicy: ConsentPolicy.gdpr,
	visitorServiceEnabled: true
};

Tealium.initialize(config, success => {
    if (!success) {
        // error creating instance.
    }
    // do something on-ready
});
```

### `joinTrace()`

Joins a trace with the specified ID. Learn more about the [Trace](https://docs.tealium.com/manage-traces/) feature in the Tealium Customer Data Hub.

```javascript
Tealium.joinTrace(id);
```

| Parameters | Type     | Description                     | Example    |
|:-----------|:---------|:--------------------------------|:-----------|
| `id`       | `String` | Trace ID retrieved from the CDH | `abc123xy` |

### `leaveTrace()`

A trace remains active for the duration of the app session until the `leaveTrace()` method is called, which leaves a previously joined trace and ends the visitor session.

```javascript
Tealium.leaveTrace();
```

### LogLevel

Sets the log level property, which controls how much information is logged, to one of the following values:

| Value     | Description                                                         |
|:----------|:--------------------------------------------------------------------|
| `.dev`    | Informational events that highlight the progress of the application |
| `.qa`     | Debug-level events used for debugging an application                |
| `.prod`   | Error events such as critical errors and failures                   |
| `.silent` | No Logging (default)                                                |

Example:

`LogLevel.dev`

### `setConsentCategories()`

Sets the consent categories of a user. Pass in an array of Strings to set the categories. Default is an empty array until `ConsentStatus` is set to `.consented`. If the consent status is `.consented` and no categories are specified with the `setConsentCategories()` method, then all categories are set.

```javascript
Tealium.setConsentCategories(categories);
```

| Parameters   | Type                  | Description                       | Example                                                        |
|:-------------|:----------------------|:----------------------------------|:---------------------------------------------------------------|
| `categories` | `ConsentCategories[]` | Array of  user consent categories | `[ConsentCategories.email, ConsentCategories.personalization]` |

Example:

```javascript
Tealium.setConsentCategories([ConsentCategories.analytics, ConsentCategories.email]);
```

#### ConsentCategories

| Value             | Description     |
|:------------------|:----------------|
| `analytics`       | Analytics       |
| `affiliates`      | Affiliates      |
| `displayAds`      | Display Ads     |
| `email`           | Email           |
| `personalization` | Personalization |
| `search`          | Search          |
| `social`          | Social          |
| `bigData`         | Big Data        |
| `mobile`          | Mobile          |
| `engagement`      | Engagement      |
| `monitoring`      | Monitoring      |
| `crm`             | CRM             |
| `cdp`             | CDP             |
| `cookieMatch`     | Cookie Match    |
| `misc`            | Misc            |

### `setConsentExpiryListener()`

Defines a callback to execute after the user's consent preferences have expired according the [`ConsentExpiry`](#consentexpiry).

```javascript
Tealium.setConsentExpiryListener(callback);
```

| Parameters | Type       | Description                           | Example       |
|:-----------|:-----------|:--------------------------------------|:--------------|
| `callback` | `Function` | Code to execute after consent expires | (see example) |

Example:

```javascript
Tealium.setConsentExpiryListener(() => {
    console.log("Consent Expired");
});
```

### `setConsentStatus()`

Sets the consent status of a user. Default is `.unknown` until changed.

```javascript
Tealium.setConsentStatus(status);
```

| Parameters | Type            | Description         | Example                   |
|:-----------|:----------------|:--------------------|:--------------------------|
| `status`   | `ConsentStatus` | User consent status | `ConsentStatus.consented` |

Example:

```javascript
Tealium.setConsentStatus(ConsentStatus.consented);
```

#### ConsentStatus

| Value           | Description   |
|:----------------|:--------------|
| `.consented`    | Consented     |
| `.notConsented` | Not Consented |
| `.unknown`      | Unknown       |

### `setVisitorServiceListener()`

Defines a callback to execute when the visitor profile has been updated. The updated [`VisitorProfile`](#visitorprofile) is provided in the callback response.

The VisitorService module implements the [Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/) feature of the Tealium Customer Data Hub.

Usage of this module is recommended if you are licensed for Tealium AudienceStream and you want to use the visitor profile to enhance the user experience in your mobile application. If you are not licensed for AudienceStream, usage of this module is not recommended as no visitor profile is returned.

```javascript
Tealium.setVisitorServiceListener(callback);
```

| Parameters | Type       | Description                                                   | Example       |
|:-----------|:-----------|:--------------------------------------------------------------|:--------------|
| `callback` | `Function` | Code to execute after the updated visitor profile is returned | (see example) |

Example:

```javascript
Tealium.setVisitorServiceListener(profile => {
    console.log(JSON.stringify(profile["audiences"]));
});
```

### `removeData()`

Remove persistent data that has been previously set using `Tealium.setPersistentData()`.

```javascript
Tealium.removeData(keys);
```

| Parameters | Type       | Description        | Example          |
|:-----------|:-----------|:-------------------|:-----------------|
| `keys`     | `String[]` | Array of key names | `["foo", "bar"]` |

### `removeRemoteCommand()`

Removes a remote command from the remote command manager.

```javascript
Tealium.removeRemoteCommand(id);
```

| Parameters | Type     | Description                      | Example          |
|:-----------|:---------|:---------------------------------|:-----------------|
| `id`       | `String` | Name of the command ID to remove | `"test_command"` |

Example:

```javascript
Tealium.removeRemoteCommand("firebase");
```

### TealiumEnvironment

The environment is one of three default environments (Dev, QA, Prod) or any custom environments that Tealium publishes to. Select one of these environments.

Example:

`TealiumEnvironment.dev`

| Value   | Description |
|:--------|:------------|
| `.dev`  | Development |
| `.qa`   | QA/UAT      |
| `.prod` | Production  |

### TealiumConfig

The following summarizes the properties of the `TealiumConfig` class.

| Parameters                     | Type                                        | Description                                                                                                                                                                                                                                                 | Example                                                                                                       |
|:-------------------------------|:--------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `account`                      | `String`                                    | (Required) Tealium account name                                                                                                                                                                                                                             | `"companyXYZ" `                                                                                               |
| `profile`                      | `String`                                    | (Required) Tealium profile name                                                                                                                                                                                                                             | `"main"`                                                                                                      |
| `environment`                  | [`TealiumEnvironment`](#tealiumenvironment) | (Required) Tealium environment name                                                                                                                                                                                                                         | `"TealiumEnvironment.dev"`                                                                                    |
| `dataSource`                   | `String`                                    | CDH data source key                                                                                                                                                                                                                                         | `"abc123"`                                                                                                    |
| `collectors`                   | `Collectors[]`                              | (Required) Sets the list of [`Collectors`](#collectors) to initialize the Tealium library with                                                                                                                                                              | `[Collectors.AppData]`                                                                                        |
| `dispatchers`                  | `Dispatchers[]`                             | (Required) Sets the list of [`Dispatchers`](#dispatchers) to initialize the Tealium library with                                                                                                                                                            | `[Dispatchers.Collect]`                                                                                       |
| `customVisitorId`              | `String`                                    | Sets a custom Visitor ID                                                                                                                                                                                                                                    | `ALK2398LSDKJ3289SLKJ3298SLKJ3`                                                                               |
| `memoryReportingEnabled`       | `Boolean`                                   | Enables or disables memory reporting in the DeviceData module (default: disabled).                                                                                                                                                                          | `true`                                                                                                        |
| `overrideCollectURL`           | `String`                                    | Overrides the Tealium Collect URL to send data to a different endpoint. If using the event batching feature, also override the `overrideCollectBatchURL` property.                                                                                          | `https://custom-domain.com/event`                                                                             |
| `overrideCollectBatchURL`      | `String`                                    | Overrides the Tealium Collect batch URL to send data to a different endpoint.                                                                                                                                                                               | `https://custom-domain.com/batch-event`                                                                       |
| `overrideCollectProfile`       | `String`                                    | Overrides the Tealium Collect profile to send data to a different Tealium profile.                                                                                                                                                                                               | `custom-profile`                                                                                              |
| `overrideCollectDomain`        | `String`                                    | Overrides the domain name in the Tealium Collect URL to send data to a different endpoint.                                                                                                                                                                                                 | `custom-domain`                                                                                              |
| `overrideLibrarySettingsURL`   | `String`                                    | Overrides the publish settings URL.                                                                                                                                                                                                                         | `https://custom-domain.com/mobile.html`                                                                       |
| `overrideTagManagementURL`     | `String`                                    | Overrides the default URL used by the Tag Management module. This is needed if you are self-hosting your Tealium JavaScript files.                                                                                                                          | `https://custom-domain.com/path/env/utag.js`                                                                  |
| `deepLinkTrackingEnabled`      | `Boolean`                                   | Enables or disables [automatic tracking of standard deep links](https://docs.tealium.com/platforms/getting-started-mobile/deep-linking/#readout), such as links to the app from Facebook or other sources, as well as QR trace.  (default: enabled)                                        | `false`                                                                                                       |
| `qrTraceEnabled`               | `Boolean`                                   | Enables or disables [QR trace](https://docs.tealium.com/platforms/getting-started-mobile/trace/#how-it-works). (default: enabled)                                                                                                                                                           | `false`                                                                                                       |
| `loglevel`                     | [`LogLevel`](#loglevel)                     | Sets the log level property, which controls how much information is logged (default: silent)                                                                                                                                                                | `LogLevel.dev`                                                                                                |
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)           | Sets the expiration of the user's consent preferences. (defaults dependent upon policy)                                                                                                                                                                     | `ConsentExpiry(90, TimeUnit.days)`                                                                            |
| `consentLoggingEnabled`        | `Boolean`                                   | Enables the [Consent Logging](https://docs.tealium.com/consent-change-event-specifications/) feature, which sends all consent status changes to Tealium Customer Data Hub for auditing purposes. (default: enabled)   | true                                                                                                          |
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)           | Sets the consent policy, such as CCPA or GDPR. Consent manager is only enabled if this property is set.                                                                                                                                                        | `ConsentPolicy.gdpr`                                                                                          |
| `lifecycleAutotrackingEnabled` | `Boolean`                                   | Enables or disables lifecycle auto tracking. (default: enabled)                                                                                                                                                                                             | `false`                                                                                                       |
| `useRemoteLibrarySettings`     | `Boolean`                                   | Enables or disables the [Mobile Publish Settings](https://docs.tealium.com/creating-a-mobile-profile/) (default: enabled) Configure the Mobile Publish Settings in Tealium iQ Tag Management, or disable the feature. | `false`                                                                                                       |
| `visitorServiceEnabled`        | `Boolean`                                   | Enables or disables the automatic retrieval of the Visitor Profile using the [Data Layer Enrichment API](https://docs.tealium.com/data-layer-enrichment-api/) (default: disabled)                                | `true`                                                                                                        |
| `sessionCountingEnabled`       | `Boolean`                                   | Enables or disables session counting for Tealium iQ accounts. Set this to `false` if you are self-hosting your Tealium JavaScript files. (default: enabled)                                                                                                            | `false`                                                                                                        |
| `remoteCommands`               | `RemoteCommand[]`                           | Sets a list of [RemoteCommand](#RemoteCommand) objects to add when the instance is ready                                                                                                                                                                    | `[{ id: "hello-world", callback: (payload) => { console.log("hello-world: " + JSON.stringify(payload)); } }]` |


### `terminateIntance()`

Disables the Tealium library and removes all module references. Re-enable by creating a new Tealium instance if required.

`Tealium.terminateIntance();`

### `track()`

Track an event with either a `TealiumEvent` or `TealiumView` dispatch.

`Tealium.track(dispatch);`

| Parameters | Type      | Description      | 
|:-----------|:----------|:-----------------|
| `tealEvent` | [`TealiumDispatch`](#tealiumdispatch) | Tealium dispatch with the event name and data layer | 

```javascript
let tealEvent = new TealiumEvent(
    'cart_add', 
    {
        "customer_id": "abc123", 
        "product_id": ["PROD123", "PROD456"], 
        "product_price": [4.00, 6.00]
    }
);
Tealium.track(tealEvent);
```

### VisitorProfile

The visitor profile is an object that contains friendly names for each attribute. There is a `currentVisit` property that lets you distinguish visitor/visit attribute types. Access each attribute value by ID using a subscript. If the attribute does not exist, `null` is returned. See the below list for examples.

**Attribute Types**

| Parameters         | Properties                                                                                                       | Value                                                                                                                             |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: String, value: Boolean[]                                                                                     | `id: "5129", value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: Number[]                                                                                      | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: String[]                                                                                      | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: String, value: String                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | id: String, value: Boolean                                                                                       | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: String, value: Boolean                                                                                       | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | All attributes for current visit visitorProfile. The current visit profile does not contain Audiences or Badges. | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: String, value: Number                                                                                        | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Number                                                                                        | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String, value: Set(String)                                                                                   | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `strings`          | id: String, value: String                                                                                        | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: String, value: Object                                                                                        | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: String, value: Number                                                                                        | `["category 1": 2.0]`                                                                                                             |

### RemoteCommand

An interface that defines a configured Remote Command

| Value      | Description                                        |
|:-----------|:---------------------------------------------------|
| `id`       | The unique identifier name for the RemoteCommand   |
| `path`     | (Optional) local file to use for mappings          |
| `url`      | (Optional) remote file to use for mappings         |
| `callback` | (Optional) callback function for the RemoteCommand |

The path and URL are optional, but either provide only one or the other, or omit both in the case where the mappings are handled by a tag in Tealium iQ Tag Management.

Provide the callback if the command is to be handled within the scope of your React Native app. Omit the callback if the handler has already been registered natively.

The following example is a local mappings file for a command handled by Javascript:   
```javascript
let localCommand: RemoteCommand = {
    id: "hello-world",
    path: "hello-mappings.json",
    callback: (payload) => {
        //...
    }
}
```

The following example is a remote mappings file for a command handled natively:   
```javascript
let remoteNativeCommand: RemoteCommand = {
    id: "hello-world",
    url: "https://you.domain.com/hello-mappings.json"
}
```

## Interface: `TealiumDispatch`

An interface that defines the type of event to be tracked. The following classes implement `TealiumDispatch`:

### Class: `TealiumEvent`

To track a user's interaction with a screen, pass an instance of `TealiumEvent(tealiumEvent, dataLayer)` to the [`track()`](#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional event data object.

```javascript
let tealEvent = TealiumEvent(tealiumEvent, {eventData})
tealium?.track(tealEvent)
```

| Parameters  | Type    | Description      |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | The event name, passed as the `tealium_event` attribute  |
| `eventData` | `object` | (Optional) Data to be sent with the event in key-value format. | 

Example:

```javascript
let tealEvent = new TealiumEvent(
    'cart_add', 
    {
        "customer_id": "abc123", 
        "product_id": ["PROD123", "PROD456"], 
        "product_price": [4.00, 6.00]
    }
);
Tealium.track(tealEvent);
```

### Class: `TealiumView`

To track screen views, pass an instance of `TealiumView(tealiumEvent, dataLayer)` to the [`Track()`](#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```swift
let screenView = TealiumView(tealiumEvent, {eventData})
tealium?.track(screenView)
```

| Parameters  | Type    | Description      | Example    |
|:------------|:--------|:-----------------|:-----------|
| `tealiumEvent`  | `string`                     | `tealium_event` name of view event or screen.          | `purchase`                                                 |
| `eventData` | `Dictionary<string, object>` | (Optional) Data to be sent with the event in key-value format. | `'purchase', {"customer_id", "abc123", "order_total": 10.00, "product_id": ["PROD123", "PROD456"], "order_id": "0123456789"}` |

Example:

```javascript
let screenView = new TealiumView(
    'purchase', 
    {
        "customer_id": "abc123", 
        "order_total": 10.00, 
        "product_id": ["PROD123", "PROD456"], 
        "order_id": "0123456789"
    }
);
Tealium.track(screenView);
```