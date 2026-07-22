---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Cordova.
url: https://docs.tealium.com/platforms/cordova/api/
---
## Class: `Tealium`

The following summarizes the commonly used methods of the Cordova `Tealium` class.

| Method                                                      | Description                                                                        |
|:------------------------------------------------------------|:-----------------------------------------------------------------------------------|
| [`addRemoteCommand()`](#addremotecommand)                   | Adds a remote command to the remote command manager.                               |
| [`addData()`](#adddata)                                     | Adds data to persistent data layer.                                                |
| [`gatherTrackData()`](#gathertrackdata)                     | Gathers all track data from collectors and data layer.                             |
| [`getData()`](#getdata)                                     | Retrieves a specified value from the data layer.                                   |
| [`getConsentCategories()`](#getconsentcategories)           | Retrieves the user's consented categories.                                         |
| [`getConsentStatus()`](#getconsentwtatus)                   | Retrieves the user's consent status.                                               |
| [`getVisitorId()`](#getvisitorid)                           | Retrieves the current Visitor ID.                                                  |
| [`initialize()`](#initialize)                               | Initializes Tealium with configuration parameters.                                 |
| [`joinTrace()`](#joinTrace)                                 | Joins a trace with the given ID.                                                   |
| [`leaveTrace()`](#leavetrace)                               | Leaves active trace session.                                                       |
| [`removeData()`](#removedata)                               | Remove persistent data that has been previously set using [`addData()`](#adddata). |
| [`removeRemoteCommand()`](#removeremotecommand)             | Removes a remote command from the remote command manager.                          |
| [`setConsentCategories()`](#setconsentcategories)           | Sets the consent categories of a user.                                             |
| [`setConsentExpiryListener()`](#setconsentexpirylistener)   | Sets the consent expired listener or callback.                                     |
| [`setConsentStatus()`](#setconsentstatus)                   | Sets the consent status of a user.                                                 |
| [`setVisitorServiceListener()`](#setvisitorservicelistener) | Defines the visitor service listener or callback.                                  |
| [`terminateInstance()`](#terminateinstance)                 | Disables and destroys the Tealium instance.                                        |
| [`track()`](#track)                                         | Track an event or screen view                                                      |

### `addRemoteCommand()`

Adds a remote command to the remote command manager.

```javascript
tealium.addRemoteCommand(id, callback);
```

| Parameters | Type        | Description                                                                                                                                                     | Example          |
|:-----------|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `String`    | Name of the command ID from the tag configuration                                                                                                               | `"test_command"` |
| `callback` | `Function ` | A callback function to execute after the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example)    |

Example:

```javascript
tealium.addRemoteCommand("firebase", (payload) => {

  var eventName = payload["firebase_event_name"];
  var eventProperties = payload["firebase_event_properties"];

  analytics.logEvent(eventName, eventProperties);
});
```

### `addData()`
Adds data to the persistent data storage for the given expiration.

```javascript
tealium.addData(data, expiry);
```
| Parameters | Type                | Description                                                                                                   | Example                                   |
|:-----------|:--------------------|:--------------------------------------------------------------------------------------------------------------|:------------------------------------------|
| `data`     | `Object`            | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{"persistent_key2" : "persistent_val2"}` |
| `expiry`   | [`Expiry`](#expiry) | Length of time for which to persist the data                                                                  | `Expiry.forever`                          |

### Collectors

Collectors are modules that gather supplemental information from the device and append it to the data layer before it's transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors. Default collectors are denoted by a `*` next to the collector name.

| Collector Name  | TealiumConfig Reference   |
|:----------------|:--------------------------|
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

These modules are enabled or disabled using the `collectors` property of your config object, and the constant values are available from `window.tealium.utils.Collectors`.

### ConsentExpiry

Defines the consent preferences expiration

| Parameters | Type       | Description                          | Example         |
|:-----------|:-----------|:-------------------------------------|:----------------|
| `time`     | `Number`   | The amount of time before expiration | `90`            |
| `unit`     | `TimeUnit` | The unit of time before expiration   | `TimeUnit.days` |

Example:

```javascript
var ConsentExpiry = tealium.utils.ConsentExpiry
var TimeUnit = tealium.utils.TimeUnit
ConsentExpiry.create(90, TimeUnit.days)
```

#### TimeUnit

| Value    | Description |
|:---------|:------------|
| .minutes | Minutes     |
| .hours   | Hours       |
| .months  | Months      |
| .days    | Days        |

### ConsentPolicy

Defines the consent policy to adhere to. If no consent policy is defined on the `config` object, the consent manager becomes disabled. Constants are available from `window.tealium.utils.ConsentPolicy`.

Example:

```javascript
var ConsentPolicy = tealium.utils.ConsentPolicy
var gdpr = ConsentPolicy.gdpr
```

| Value | Description |
|:------|:------------|
| .gdpr | GDPR        |
| .ccpa | CCPA        |

### Dispatchers

Dispatchers are modules that send the data from your data layer and send it to a Tealium endpoint. The following dispatchers are currently available - Constants are available from `window.tealium.utils.Dispatchers`.

| Dispatcher Name  | TealiumConfig Reference      |
|:-----------------|:-----------------------------|
| `Collect`        | `Dispatchers.Collect`        |
| `RemoteCommands` | `Dispatchers.RemoteCommands` |
| `TagManagement`  | `Dispatchers.TagManagement`  |


<blockquote>
At least one dispatcher is required. If no dispatchers are specified, your data is not sent anywhere.
</blockquote>


### Expiry

Defines the custom data expiration.

Example:

```javascript
Expiry.session
```

| Value          | Description                                 |
|:---------------|:--------------------------------------------|
| `session`      | The lifetime of the current active session. |
| `untilRestart` | Until the app restarts.                     |
| `forever`      | For the lifetime of the app, until deleted. |

Example:

```javascript
var Expiry = tealium.utils.Expiry
var session = Expiry.session
```

### `gatherTrackData()`

Gathers all track data from collectors and data layer.

```javascript
tealium.gatherTrackData(callback)
```

| Parameters | Type       | Description                                          |
|:-----------|:-----------|:-----------------------------------------------------|
| `callback` | `Function` | Callback function to use the track data object       |

Example:

```javascript
  tealium.gatherTrackData(function(data) {
    console.log(data)
  });
```

### `getData()`

Retrieves the value for a specified key in the persistent data layer, then returns in the form of a callback function.

```javascript
tealium.getData(key, callback);
```

| Parameters | Type       | Description                                          |
|:-----------|:-----------|:-----------------------------------------------------|
| `key`      | `String`   | Key to retrieve from the data layer                  |
| `callback` | `Function` | Callback function to use the retrieved value for key |

Example:

```javascript
tealium.getData(key, function(data) {
  console.log(data)
});
```

### `getConsentCategories()`
Retrieves the user's consented categories.

```javascript
tealium.getConsentCategories(callback);
```

| Parameters | Type       | Description                                     |
|:-----------|:-----------|:------------------------------------------------|
| `callback` | `Function` | Callback function to use the consent categories |

Example:

```javascript
tealium.getConsentCategories(categories => {
    console.log("Consent Categories: " + categories)
});
```

### `getConsentStatus()`
Retrieves the user's visitor ID and returns in the form of a callback function.

```javascript
tealium.getConsentStatus(callback);
```

| Parameters | Type       | Description                                 |
|:-----------|:-----------|:--------------------------------------------|
| `callback` | `Function` | Callback function to use the consent status |

Example:

```javascript
tealium.getConsentStatus(function(categories) {
  console.log("Consent Status: " + status)
})
```

### `getVisitorId()`
Retrieves the user's visitor ID and returns in the form of a callback function.

```javascript
tealium.getVisitorId(callback);
```

| Parameters | Type       | Description                             | Example       |
|:-----------|:-----------|:----------------------------------------|:--------------|
| `callback` | `Function` | Callback function to use the Visitor ID | (see example) |

Example:

```javascript
tealium.getVisitorId(function(visitorId) {
  console.log("VisitorId: " + visitorId)
})
```

### `initialize()`

Initialize Tealium before calling any other method.

```javascript
tealium.initialize(config);
```

| Parameters | Type                              | Description                                                      | Example       |
|:-----------|:----------------------------------|:-----------------------------------------------------------------|:--------------|
| `config`   | [`TealiumConfig`](#tealiumconfig) | Tealium configuration parameters                                 | (see example) |
| `callback` | `Function`                        | (Optional) Callback function after the Tealium instance is ready | (see example) |

Example:

```javascript
let Environment = tealium.utils.Environment;
let Collectors = tealium.utils.Collectors;
let Dispatchers = tealium.utils.Dispatchers;
let ConsentPolicy = tealium.utils.ConsentPolicy;
let Expiry = tealium.utils.Expiry;

let config = {
    account: 'tealiummobile',
    profile: 'demo',
    environment: Environment.dev,
    dispatchers: [
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands
    ],
    collectors: [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity
    ],
    consentLoggingEnabled: true,
    // consentExpiry: {
    //     'time': 10,
    //     'unit': 'days'
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    batchingEnabled: false,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: false
};

window.tealium.initialize(config, function(success) {
    console.log("Init was: " + success)
    if(success) {
        tealium.setVisitorServiceListener(logVisitorUpdated)
        tealium.setConsentExpiryListener(logConsentExpired)
        tealium.addRemoteCommand("hello-world", logRemoteCommand)
    }
})
```

### `joinTrace()`

Joins a trace with the specified ID. Learn more about the [Trace](https://docs.tealium.com/manage-traces/) feature in the Tealium Customer Data Hub.

```javascript
tealium.joinTrace(id);
```

| Parameters | Type     | Description                     | Example    |
|:-----------|:---------|:--------------------------------|:-----------|
| `id`       | `String` | Trace ID retrieved from the CDH | `abc123xy` |

### `leaveTrace()`

A trace remains active for the duration of the app session until the `leaveTrace()` method is called, which leaves a previously joined trace and ends the visitor session.

```javascript
tealium.leaveTrace();
```

### LogLevel

Sets the log level property, which controls how much information is logged, to one of the following values:

| Value             | Description                                                         |
|:------------------|:--------------------------------------------------------------------|
| `LogLevel.dev`    | Informational events that highlight the progress of the application |
| `LogLevel.qa`     | Debug-level events used for debugging an application                |
| `LogLevel.prod`   | Error events such as critical errors and failures                   |
| `LogLevel.silent` | No Logging (default)                                                |

Example:

`LogLevel.dev`

### `setConsentCategories()`
Sets the consent categories of a user. Pass in an array of Strings to set the categories. Default is an empty array until `ConsentStatus` is set to `.consented`. If the consent status is `.consented` and no categories are specified with the `setConsentCategories()` method, then all categories are set.

```javascript
tealium.setConsentCategories(categories);
```

| Parameters   | Type                  | Description                       | Example                                                        |
|:-------------|:----------------------|:----------------------------------|:---------------------------------------------------------------|
| `categories` | `ConsentCategories[]` | Array of  user consent categories | `[ConsentCategories.email, ConsentCategories.personalization]` |

Example:

```javascript
var ConsentCategories = tealium.utils.ConsentCategories;

tealium.setConsentCategories([ConsentCategories.analytics, ConsentCategories.email]);
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
tealium.setConsentExpiryListener(callback);
```

| Parameters | Type       | Description                           |
|:-----------|:-----------|:--------------------------------------|
| `callback` | `Function` | Code to execute after consent expires |

Example:

```javascript
tealium.setConsentExpiryListener(() => {
    print("Consent Expired");
});
```

### `setConsentStatus()`

Sets the consent status of a user. Default is `.unknown` until changed.

```javascript
tealium.setConsentStatus(status);
```

| Parameters | Type     | Description         | Example                   |
|:-----------|:---------|:--------------------|:--------------------------|
| `status`   | `String` | User consent status | `ConsentStatus.consented` |

Example:

```javascript
var ConsentStatus = window.tealium.utils.ConsentStatus

tealium.setConsentStatus(ConsentStatus.consented);
```

#### ConsentStatus

| Value           | Description                    |
|:----------------|:-------------------------------|
| `.consented`    | User has consented.            |
| `.notConsented` | User has not consented.        |
| `.unknown`      | Unknown if user has consented. |

### `setVisitorServiceListener()`
Defines a callback to execute when the visitor profile has been updated. The updated [`VisitorProfile`](#visitorprofile) is provided in the callback response.

The VisitorService module implements the [Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/) feature of the Tealium Customer Data Hub.

Usage of this module is recommended if you are licensed for Tealium AudienceStream and you want to use the visitor profile to enhance the user experience in your mobile application. If you are not licensed for AudienceStream, usage of this module is not recommended as no visitor profile is returned.

```javascript
tealium.setVisitorServiceListener(callback);
```

| Parameters | Type       | Description                                                   |
|:-----------|:-----------|:--------------------------------------------------------------|
| `callback` | `Function` | Code to execute after the updated visitor profile is returned |

Example:

```javascript
tealium.setVisitorServiceListener((profile) => {
    console.log(JSON.stringify(profile));
});
```

### `removeData()`
Remove persistent data that has been previously set using `tealium.addData()`.

```javascript
tealium.removeData(keys);
```

| Parameters | Type              | Description        | Example          |
|:-----------|:------------------|:-------------------|:-----------------|
| `keys`     | `Array (Strings)` | Array of key names | `["foo", "bar"]` |

### `removeRemoteCommand()`

Removes a remote command from the remote command manager.

```javascript
tealium.removeRemoteCommand(id);
```

| Parameters | Type     | Description                      | Example          |
|:-----------|:---------|:---------------------------------|:-----------------|
| `id`       | `String` | Name of the command ID to remove | `"test_command"` |

Example:

```javascript
tealium.removeRemoteCommand("firebase");
```

### TealiumEnvironment

The environment is one of three default environments (Dev, QA, Prod) or any custom environments that Tealium publishes to. Select one of these environments. Constants are available from `window.tealium.utils.Environment`.

Example:

```javascript
Environment.dev
```

| Value   | Description |
|:--------|:------------|
| `.dev`  | Development |
| `.qa`   | QA/UAT      |
| `.prod` | Production  |

### Config

The following summarizes the properties of the `config` options and their keys.

| Parameters                     | Type                                        | Description                                                                                                                                                                                                                                                 | Example                                                                                                       |
|:-------------------------------|:--------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `account`                      | `String`                                    | (Required) Tealium account name                                                                                                                                                                                                                             | `"companyXYZ" `                                                                                               |
| `profile`                      | `String`                                    | (Required) Tealium profile name                                                                                                                                                                                                                             | `"main"`                                                                                                      |
| `environment`                  | [`TealiumEnvironment`](#tealiumenvironment) | (Required) Tealium environment name                                                                                                                                                                                                                         | `"Environment.dev"`                                                                                           |
| `dataSource`                   | `String`                                    | CDH data source key                                                                                                                                                                                                                                         | `"abc123"`                                                                                                    |
| `collectors`                   | `Collectors[]`                              | (Required) Sets the list of [`Collectors`](#collectors) to initialize the Tealium library with                                                                                                                                                              | `[Collectors.AppData]`                                                                                        |
| `dispatchers`                  | `Dispatchers[]`                             | (Required) Sets the list of [`Dispatchers`](#dispatchers) to initialize the Tealium library with                                                                                                                                                            | `[Dispatchers.Collect]`                                                                                       |
| `customVisitorId`              | `String`                                    | Sets a custom Visitor ID                                                                                                                                                                                                                                    | `ALK2398LSDKJ3289SLKJ3298SLKJ3`                                                                               |
| `memoryReportingEnabled`       | `Boolean`                                   | Enables or disables memory reporting in the DeviceData module (default: disabled).                                                                                                                                                                          | `true`                                                                                                        |
| `overrideCollectURL`           | `String`                                    | Overrides the Tealium Collect URL to send data to a different endpoint. If using the event batching feature, also override the `overrideCollectBatchURL` property.                                                                                          | `https://custom-domain.com/event`                                                                             |
| `overrideCollectBatchURL`      | `String`                                    | Overrides the Tealium Collect batch URL to send data to a different endpoint.                                                                                                                                                                               | `https://custom-domain.com/batch-event`                                                                       |
| `overrideCollectProfile`       | `String`                                    | Overrides the Tealium Collect profile to send data to a different Tealium profile.                                                                                                                                                                          | `custom-profile`                                                                                              |
| `overrideCollectDomain`        | `String`                                    | Overrides the domain name in the Tealium Collect URL to send data to a different endpoint.                                                                                                                                                                  | `custom-domain`                                                                                               |
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
| `remoteCommands`               | `RemoteCommand[]`                           | Sets a list of [RemoteCommand](#RemoteCommand) objects to add when the instance is ready                                                                                                                                                                    | `[{ id: "hello-world", callback: (payload) => { console.log("hello-world: " + JSON.stringify(payload)); } }]` |
| `sessionCountingEnabled`       | `Boolean`                                   | Enables or disables session counting for Tealium iQ accounts. Set this to `false` if you are self-hosting your Tealium JavaScript files. (default: enabled)                                                                                                 | `false`                                                                                                       |

### Dispatch

An interface that defines the type of dispatch to be tracked.

#### View

To track a screen view, pass an object wit `viewName` and optional `dataLayer` to the [`track()`](#track) method. These may be supplied manually or through the utility methods at `tealium.utils.Dispatch.view(viewName, dataLayer)`.

```javascript
var Dispatch = tealium.utils.Dispatch;
var screenView = Dispatch.view(tealiumEvent, eventData);
tealium.track(screenView);
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | The event name, passed as the `tealium_event` attribute.  | 
| `eventData` | `<string, object>` | (Optional) Data to be sent with the event in key-value format. | 


```javascript
var Dispatch = tealium.utils.Dispatch;

var screenView = Dispatch.view(
  'purchase', 
  {
    "customer_id": "abc123", 
    "order_total": 10.00, 
    "product_id": ["PROD123", "PROD456"], 
    "order_id": "0123456789"
  }
);
tealium.track(screenView);

// the following is equivalent
tealium.track({
  type: "view",
  viewName: "purchase",
  dataLayer: {
    "customer_id": "abc123", 
    "order_total": 10.00, 
    "product_id": ["PROD123", "PROD456"], 
    "order_id": "0123345789"
  }
})
```

#### Event

To track non-view events, pass an object with `eventName` and optional `eventData` to the [`track()`](#track) method. These may be supplied manually or through the utility methods at `tealium.utils.Dispatch.event(eventName, dataLayer)`.

```javascript
var Dispatch = tealium.utils.Dispatch;
var tealiumEvent= Dispatch.view(tealiumEvent, eventData);
tealium.track(tealiumEvent);
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| The event name, passed as the `tealium_event` attribute. | 
| `eventData` | `Dictionary<string, object>` | (Optional) Data to be sent with the event in key-value format. | 

```javascript
var Dispatch = tealium.utils.Dispatch
var tealEvent = Dispatch.event(
  "cart_add", 
  {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
)
tealium.track(tealEvent)

// the following is equivalent
tealium.track({
  type: "event",
  eventName: "cart_add",
  dataLayer: {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
})
```

### `terminateIntance()`

Disables the Tealium library and removes all module references. Re-enable by creating a new Tealium instance if required.

```javascript
tealium.terminateIntance();
```

### `track()`

Tracks a screen view or event with optional associated data.

```javascript
tealium.track(tealiumEvent)
```

| Parameters | Type     | Description| 
|:-----------|:---------|:------------|
| `tealiumEvent` | `Object` | Tealium [`Dispatch`](#dispatch) with event name, passed as the `tealium_event` attribute, and an optional event data object. | 

To track events, pass a [`TealiumEvent`](#event) object to the `track()` method:

```javascript
var Dispatch = tealium.utils.Dispatch
var tealEvent = Dispatch.event(
  "cart_add", 
  {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
)
tealium.track(tealEvent)

// the following is equivalent
tealium.track({
  type: "event",
  eventName: "cart_add",
  dataLayer: {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
})
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
