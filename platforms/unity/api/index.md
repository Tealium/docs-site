---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Unity.
url: https://docs.tealium.com/platforms/unity/api/
---
## Class: `Tealium`

The following summarizes the commonly used methods of the `Tealium` class for the Unity library.

| Method                                                      | Description                                                                   |
|:------------------------------------------------------------|:------------------------------------------------------------------------------|
| [`AddRemoteCommand()`](#addRemoteCommand)                   | Adds a remote command to the remote command manager.                          |
| [`AddToDataLayer()`](#addtodatalayer)                       | Adds data to persistent data layer.                                           |
| [`GatherTrackData()`](#gathertrackdata)                     | Gathers all track data from collectors and data layer                         |
| [`GetFromDataLayer()`](#getfromdatalayer)                   | Gets a specified value from the data layer.                                   |
| [`GetConsentCategories()`](#getConsentCategories)           | Gets the user's consented categories.                                         |
| [`GetConsentStatus()`](#getConsentStatus)                   | Gets the user's consent status.                                               |
| [`GetVisitorId()`](#getVisitorId)                           | Gets the current visitor ID.                                                  |
| [`Initialize()`](#initialize)                               | Initializes Tealium with configuration parameters.                            |
| [`JoinTrace()`](#joinTrace)                                 | Joins a trace with the given ID.                                              |
| [`LeaveTrace()`](#leaveTrace)                               | Leaves an active trace and ends the visitor session.                          |
| [`RemoveFromDataLayer()`](#removefromdatalayer)             | Remove persistent data that has been previously set using `AddToDataLayer()`. |
| [`RemoveRemoteCommand()`](#removeRemoteCommand)             | Removes a remote command from the remote command manager.                     |
| [`SetConsentCategories()`](#setConsentCategories)           | Sets the consent categories of a user.                                        |
| [`SetConsentExpiryListener()`](#setConsentExpiryListener)   | Sets the consent expired listener or callback.                                |
| [`SetConsentStatus()`](#setConsentStatus)                   | Sets the consent status of a user.                                            |
| [`SetVisitorServiceListener()`](#setVisitorServiceListener) | Sets the visitor service listener or callback.                                |
| [`Terminate()`](#terminate)                                 | Disables and destroys the Tealium instance.                                   |
| [`Track()`](#track)                                         | Track a user's interaction with a game or a game view.                        |

### `AddRemoteCommand()`

Adds a remote command to the remote command manager.

```javascript
TealiumUnityPlugin.AddRemoteCommand(id, callback);
```

| Parameters | Type             | Description                                                                                                                                                     | Example          |
|:-----------|:-----------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `string`         | Name of the command ID from the tag configuration.                                                                                                              | `"test_command"` |
| `callback` | `Action<string>` | A callback function to execute after the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example)    |

Example:

```swift
TealiumUnityPlugin.AddRemoteCommand("firebase", (payload) => {

  string? eventName = (string)payload["firebase_event_name"];
  Dictionary<string, object>? eventProperties =
      (Dictionary<string, object>)payload["firebase_event_properties"];

  if (eventName != null) {
    analytics().logEvent(eventName, eventProperties);
  }
});
```

### `AddToDataLayer()`

Adds data to the persistent data storage for the given expiration.

```javascript
TealiumUnityPlugin.AddToDataLayer(data, expiry);
```

| Parameters | Type                         | Description                                                                                                    | Example                                             |
|:-----------|:-----------------------------|:---------------------------------------------------------------------------------------------------------------|:----------------------------------------------------|
| `data`     | `Dictionary<string, object>` | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings. | `new Dictionary<string, object> {{"KEY", "VALUE"}}` |
| `expiry`   | [`Expiry`](#expiry)          | Length of time for which to persist the data.                                                                  | `Expiry.Forever`                                    |

### `Collectors`

Collectors are modules that gather supplemental information from the device and append it to the data layer before it's transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors. Default collectors are denoted by a `*` next to the collector name.

| Collector Name   | `TealiumConfig` Reference   |
|:-----------------|:----------------------------|
| `AppData`*       | `Collectors.AppData`        |
| `Connectivity`*  | `Collectors.Connectivity`   |
| `Device`         | `Collectors.Device`         |
| `Lifecycle`      | `Collectors.Lifecycle`      |
| `VisitorService` | `Collectors.VisitorService` |

### `ConsentExpiry`

Defines the consent preferences expiration.

```javascript
ConsentExpiry(time, unit)
```

| Parameters | Type       | Description                           | Example         |
|:-----------|:-----------|:--------------------------------------|:----------------|
| `time`     | `Number`   | The amount of time before expiration. | `90`            |
| `unit`     | `TimeUnit` | The unit of time before expiration.   | `TimeUnit.Days` |

Example:

```javascript
new ConsentExpiry(90, TimeUnit.Days)
```

#### TimeUnit

The following are the time unit values:

| Value                   | Description               |
|:------------------------|:--------------------------|
| `ConsentExpiry.Minutes` | The time unit in minutes. |
| `ConsentExpiry.Hours`   | The time unit in hours.   |
| `ConsentExpiry.Months`  | The time unit in months.  |
| `ConsentExpiry.Days`    | The time unit in days.    |

### `ConsentPolicy`

Defines the consent policy to adhere to. If no consent policy is defined on the [`TealiumConfig`](#class-tealiumconfig) object, the consent manager is be disabled.

| Value                | Description              |
|:---------------------|:-------------------------|
| `ConsentPolicy.GDPR` | The GDPR consent policy. |
| `ConsentPolicy.CCPA` | The CCPA consent policy. |

Example:

```javascript
ConsentPolicy.GDPR
```

### `Dispatchers`

Dispatchers are modules that send the data from your data layer and send it to a Tealium endpoint. The following dispatchers are currently available:

| Dispatcher Name  | `TealiumConfig` Reference    |
|:-----------------|:-----------------------------|
| `Collect`        | `Dispatchers.Collect`        |
| `RemoteCommands` | `Dispatchers.RemoteCommands` |
| `TagManagement`  | `Dispatchers.TagManagement`  |


<blockquote>
At least one dispatcher is required. If no dispatchers are specified, your data is not sent to the data layer.
</blockquote>


### `Expiry`

Defines the custom data expiration.

| Value          | Description                                            |
|:---------------|:-------------------------------------------------------|
| `Session`      | The lifetime of the current active session.            |
| `UntilRestart` | Until the app restarts.                                |
| `Forever`      | For the lifetime of the app, until the app is deleted. |

Example:

```javascript
Expiry.session
```

### `GatherTrackData()`
Gathers all track data from collectors and data layer.

```javascript
Tealium.GatherTrackData(callback);
```

| Parameters | Type       | Description                                          | Example       |
|:-----------|:-----------|:-----------------------------------------------------|:--------------|
| `callback` | `Function` | A callback function to receive and process the tracking data. The callback returns a JSON object. | (see example) |

Example:

```javascript
Tealium.GatherTrackData(callback => {
  string? serializedPayload = JsonConvert.SerializeObject(callback);
  if (serializedPayload != null) {
      TealiumLogger.Log($"Track Data: {serializedPayload}");
  }
});
```

### `GetFromDataLayer()`

Gets the value for a specified key in the persistent data layer, then returns in the form of a callback function.

```javascript
TealiumUnityPlugin.GetFromDataLayer(key);
```

| Parameters | Type                                                                 | Description                          |
|:-----------|:---------------------------------------------------------------------|:-------------------------------------|
| `key`      | `string`                                                             | Key to retrieve from the data layer. |
| `callback` | Returns an `object` type that needs to be cast to the expected type. | Value from data layer key.           |

Example:

```bash
string? stringValue =
    (string)TealiumUnityPlugin.GetFromDataLayer("test_string");
```

### `GetConsentCategories()`

Gets the user's consented categories.

```javascript
TealiumUnityPlugin.GetConsentCategories();
```

| Return Type               | Description                                                     |
|:--------------------------|:----------------------------------------------------------------|
| `List<ConsentCategories>` | A list of `ConsentCategories` for which the user has consented. |

Example:

```javascript
List<string> caetgories = TealiumUnityPlugin.GetConsentCategories();
TealiumLogger.Log("Consent Categories: ");
caetgories.ForEach(category => TealiumLogger.Log(category.Value + " "));
```


### `GetConsentStatus()`

Gets the user's consent status.

```javascript
TealiumUnityPlugin.GetConsentStatus();
```

| Return Type     | Description                |
|:----------------|:---------------------------|
| `ConsentStatus` | The user's consent status. |
Example:

```javascript
TealiumLogger.Log("Consent Status: "
    + TealiumUnityPlugin.GetConsentStatus().Value);
```

### `GetVisitorId()`

Gets the user's visitor ID.

```javascript
TealiumUnityPlugin.GetVisitorId()
```

| Return Type | Description             |
|:------------|:------------------------|
| `string`    | The Tealium visitor ID. |

Example:

```javascript
TealiumLogger.Log("Visitor Id: " + TealiumUnityPlugin.GetVisitorId())
```

### `Initialize()`

Initialize Tealium before calling any other method. Optionally, pass in an `Action<bool>` callback that executes after the Tealium’s initialization is complete

```javascript
TealiumUnityPlugin.Initialize(config, callback);
```

| Parameters | Type                                    | Description                                                                                  |
|:-----------|:----------------------------------------|:---------------------------------------------------------------------------------------------|
| `config`   | [`TealiumConfig`](#class-tealiumconfig) | Tealium configuration parameters.                                                            |
| `callback` | `Action<bool>`                          | Returns `true` if the Tealium initialization is successful and `false` if there is an error. |


Example:

```javascript
private TealiumConfig config =
      new TealiumConfig("tealiummobile",
      "demo",
      TealiumEnvironment.DEV,
      new List<Dispatchers> {
        Dispatchers.TagManagement,
        Dispatchers.Collect,
        Dispatchers.RemoteCommands },
      new List<Collectors> {
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity },
      consentPolicy: ConsentPolicy.GDPR,
      consentExpiry: new ConsentExpiry(10, TimeUnit.Minutes));

TealiumUnityPlugin.Initialize(config, success => {
    if (success) {
        TealiumLogger.Log("TealiumUnityPlugin Initialized");
        TealiumUnityPlugin.SetConsentStatus(ConsentStatus.Consented);
        TealiumUnityPlugin.SetConsentExpiryListener(() =>
            TealiumLogger.Log("Consent Expired!!"));
    } else {
        TealiumLogger.Log("TealiumUnityPlugin Failed to Initialize");
    }
});
```

### `JoinTrace()()`

Joins a trace with the specified ID. Learn more about the [Trace](https://docs.tealium.com/manage-traces/) feature in the Tealium Customer Data Hub.

```javascript
TealiumUnityPlugin.JoinTrace(id);
```

| Parameters | Type     | Description                      | Example    |
|:-----------|:---------|:---------------------------------|:-----------|
| `id`       | `string` | Trace ID retrieved from the CDH. | `abc123xy` |

### `LeaveTrace()`

Leaves an active trace and ends the visitor session. A trace remains active for the duration of the app session until this method is called.

```javascript
TealiumUnityPlugin.LeaveTrace();
```

### `LogLevel`

Sets the log level property, which controls how much information is logged, to one of the following values:

| Value             | Description                                                          |
|:------------------|:---------------------------------------------------------------------|
| `LogLevel.Dev`    | Informational events that highlight the progress of the application. |
| `LogLevel.Qa`     | Debug-level events used for debugging an application.                |
| `LogLevel.Prod`   | Error events such as critical errors and failures.                   |
| `LogLevel.Silent` | No Logging (default).                                                |

Example:

```javascript
LogLevel.Dev
```

### `SetConsentCategories()`

Sets the consent categories of a user. Pass in an array of strings to set the categories. Default is an empty array until `ConsentStatus` is set to `.Consented`. If the consent status is `.Consented` and no categories are specified with the `SetConsentCategories()` method, then all categories are set.

```javascript
TealiumUnityPlugin.setConsentCategories(categories);
```

| Parameters   | Type                      | Description                      | Example                                                        |
|:-------------|:--------------------------|:---------------------------------|:---------------------------------------------------------------|
| `categories` | `List<ConsentCategories>` | Array of user consent categories | `[ConsentCategories.email, ConsentCategories.personalization]` |

Example:

```javascript
TealiumUnityPlugin.SetConsentCategories(new List<ConsentCategories>(){ConsentCategories.Analytics, ConsentCategories.Email});
```

#### ConsentCategories

| Value             | Description                       |
|:------------------|:----------------------------------|
| `Analytics`       | Analytics consent category.       |
| `Affiliates`      | Affiliates consent category.      |
| `DisplayAds`      | Display Ads consent category.     |
| `Email`           | Email consent category.           |
| `Personalization` | Personalization consent category. |
| `Search`          | Search consent category.          |
| `Social`          | Social consent category.          |
| `BigData`         | Big Data consent category.        |
| `Mobile`          | Mobile consent category.          |
| `Engagement`      | Engagement consent category.      |
| `Monitoring`      | Monitoring consent category.      |
| `Crm`             | CRM consent category.             |
| `Cdp`             | CDP consent category.             |
| `CookieMatch`     | Cookie Match consent category.    |
| `Misc`            | Misc consent category.            |

### `SetConsentExpiryListener()`

Defines a callback to execute after the user's consent preferences have expired according the [`ConsentExpiry`](#consentexpiry). It is recommended to define this listener in the Initialization callback to ensure Tealium is fully initialized.

```javascript
TealiumUnityPlugin.SetConsentExpiryListener(callback);
```

| Parameters | Type     | Description                                |
|:-----------|:---------|:-------------------------------------------|
| `callback` | `Action` | The code to execute after consent expires. |

Example:

```javascript
TealiumUnityPlugin.SetConsentExpiryListener(()
    => TealiumLogger.Log("Consent Expired!!"));
```

### `SetConsentStatus()`

Sets the consent status of a user. Default is `.Unknown`.

```javascript
TealiumUnityPlugin.SetConsentStatus(status);
```

| Parameters | Type            | Description              | Example                   |
|:-----------|:----------------|:-------------------------|:--------------------------|
| `status`   | `ConsentStatus` | The user consent status. | `ConsentStatus.Consented` |

Example:

```javascript
TealiumUnityPlugin.SetConsentStatus(ConsentStatus.Consented);
```

#### `ConsentStatus`

| Value           | Description                   |
|:----------------|:------------------------------|
| `.Consented`    | Consented consent status.     |
| `.NotConsented` | Not consented consent status. |
| `.Unknown`      | Unknown consent status.       |

### `SetVisitorServiceListener()`

Defines a callback to execute when the visitor profile has been updated. The updated [`VisitorProfile`](#visitorprofile) is provided in the callback response.

The VisitorService module implements the [Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/) feature of the Tealium Customer Data Hub.

Usage of this module is recommended if you are licensed for Tealium AudienceStream and you want to use the visitor profile to enhance the user experience in your mobile application. If you are not licensed for AudienceStream, usage of this module is not recommended as no visitor profile is returned.

```javascript
TealiumUnityPlugin.setVisitorServiceListener(callback);
```

| Parameters | Type                                 | Description                                                    |
|:-----------|:-------------------------------------|:---------------------------------------------------------------|
| `callback` | `Action<Dictionary<string, object>>` | Code to execute after the updated visitor profile is returned. |

Example:

```javascript
TealiumUnityPlugin.setVisitorServiceListener((profile) => {
  string? serializedProfile = JsonConvert.SerializeObject(profile);
  if (serializedProfile != null) {
      TealiumLogger.Log(serializedProfile);
  }
});
```

### `RemoveFromDataLayer()`

Remove persistent data that has been previously set using `TealiumUnityPlugin.AddToDataLayer()`.

```javascript
TealiumUnityPlugin.RemoveFromDataLayer(keys);
```

| Parameters | Type           | Description         | Example                            |
|:-----------|:---------------|:--------------------|:-----------------------------------|
| `keys`     | `List<string>` | Array of key names. | `new List<string>(){"foo", "bar"}` |

### `RemoveRemoteCommand()`

Removes a remote command from the remote command manager.

```javascript
TealiumUnityPlugin.RemoveRemoteCommand(id);
```

| Parameters | Type     | Description                       | Example        |
|:-----------|:---------|:----------------------------------|:---------------|
| `id`       | `string` | Name of the command ID to remove. | `test_command` |

Example:

```javascript
TealiumUnityPlugin.RemoveRemoteCommand("firebase");
```


### `Track()`

Track a user's interaction with a game or a game view.

```javascript
TealiumUnityPlugin.Track(dispatch);
```

| Parameters | Type                                            | Description                                          | Example                        |
|:-----------|:------------------------------------------------|:-----------------------------------------------------|:-------------------------------|
| `dispatch` | [`TealiumDispatch`](#interface-tealiumdispatch) | Tealium dispatch with the event name and data layer. | `TealiumEvent("button_click")` |

To track game events, create a [`TealiumEvent`](#class-tealiumevent) object, and pass it to the `track()` method:

```javascript
TealiumEvent event = TealiumEvent('GAME_EVENT_NAME', new Dictionary<string, object> {{"KEY", "VALUE"}});
TealiumUnityPlugin.Track(event);
```

To track game screen views, create a [`TealiumView`](#class-tealiumview) object, and pass it to the `track()` method:  

```javascript
TealiumView view = new TealiumView("VIEW_NAME", new Dictionary<string, object> {{"KEY", "VALUE"}})
TealiumUnityPlugin.Track(view);
```

### `Terminate()`

Disables the Tealium library and removes all module references. Re-enable by creating a new Tealium instance if required.

```javascript
TealiumUnityPlugin.Terminate();
```

### `VisitorProfile`

The visitor profile is an object that contains friendly names for each attribute. There is a `currentVisit` property that lets you distinguish visitor or visit attribute types. Access each attribute value by ID using a subscript. If the attribute does not exist, `null` is returned.

**Attribute Types**

| Parameters         | Properties                                                                                                       | Value                                                                                                                             |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: `string`, value: `bool`                                                                                      | id: "5129" value: [true,false,true,true]                                                                                         |
| `arraysOfNumbers`  | id: `string`, value: `double[]`                                                                                  | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: `string`, value: `string[]`                                                                                  | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: string, value: string                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | id: `string`, value: `bool`                                                                                      | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: `string`, value: `bool`                                                                                      | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | All attributes for current visit visitorProfile. The current visit profile does not contain Audiences or Badges. | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: `string`, value: `int`                                                                                       | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: `string`, value: `double`                                                                                    | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: `string`, value: `string[]`                                                                                  | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `string`           | id: `string`, value: `string`                                                                                    | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: `string`, value: `Dictionary<string, float>`                                                                 | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: `string`, value: `float`                                                                                     | `["category 1": 2.0]`                                                                                                             |

## Class: `TealiumConfig`

The following summarizes the properties of the `TealiumConfig` class.

| Parameters                     | Type                                              | Description                                                                                                                                                                                                                                                  | Example                                      |
|:-------------------------------|:--------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|
| `account`                      | `string`                                          | (Required) Tealium account name.                                                                                                                                                                                                                             | `companyXYZ`                                 |
| `profile`                      | `string`                                          | (Required) Tealium profile name.                                                                                                                                                                                                                             | `main`                                       |
| `environment`                  | [`TealiumEnvironment`](#class-tealiumenvironment) | (Required) Tealium environment name.                                                                                                                                                                                                                         | `TealiumEnvironment.Dev`                     |
| `dataSource`                   | `string`                                          | CDH data source key.                                                                                                                                                                                                                                         | `abc123`                                     |
| `collectors`                   | `List<Collectors>`                                | (Required) Sets the list of [`Collectors`](#collectors) to initialize the Tealium library with.                                                                                                                                                              | `new List<Collectors>(){Collectors.AppData}` |
| `dispatchers`                  | `List<Dispatchers>`                               | (Required) Sets the list of [`Dispatchers`](#dispatchers) to initialize the Tealium library with.                                                                                                                                                            | `new List<Collectors>(){Dispatchers.Collec}` |
| `customVisitorId`              | `string`                                          | Sets a custom visitor ID.                                                                                                                                                                                                                                    | `ALK2398LSDKJ3289SLKJ3298SLKJ3`              |
| `memoryReportingEnabled`       | `bool`                                            | Enables or disables memory reporting in the DeviceData module (default: disabled).                                                                                                                                                                           | `true`                                       |
| `overrideCollectURL`           | `string`                                          | Overrides the Tealium Collect URL to send data to a different endpoint. If using the event batching feature, also override the `overrideCollectBatchURL` property.                                                                                           | `https://custom-domain.com/event`            |
| `overrideCollectBatchURL`      | `string`                                          | Overrides the Tealium Collect batch URL to send data to a different endpoint.                                                                                                                                                                                | `https://custom-domain.com/batch-event`      |
| `overrideCollectProfile`       | `String`                                    | Overrides the Tealium Collect profile to send data to a different Tealium profile.
| `custom-profile`                                                                                              |
| `overrideLibrarySettingsURL`   | `string`                                          | Overrides the publish settings URL.                                                                                                                                                                                                                          | `https://custom-domain.com/mobile.html`      |
| `overrideTagManagementURL`     | `string`                                          | Overrides the default URL used by the Tag Management module. This is needed if you are self-hosting your Tealium JavaScript files.                                                                                                                           | `https://custom-domain.com/path/env/utag.js` |
| `deepLinkTrackingEnabled`      | `bool`                                            | Enables or disables [automatic tracking of standard deep links](https://docs.tealium.com/platforms/getting-started-mobile/deep-linking/#readout), such as links to the app from Facebook or other sources, as well as QR trace (default: enabled).                                          | `false`                                      |
| `qrTraceEnabled`               | `bool`                                            | Enables or disables [QR trace](https://docs.tealium.com/platforms/getting-started-mobile/trace/#how-it-works). (default: enabled)                                                                                                                                                            | `false`                                      |
| `loglevel`                     | [`LogLevel`](#loglevel)                           | Sets the log level property, which controls how much information is logged (default: silent).                                                                                                                                                                | `LogLevel.dev`                               |
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)                 | Sets the expiration of the user's consent preferences. (defaults dependent upon policy)                                                                                                                                                                      | `ConsentExpiry(90, TimeUnit.days)`           |
| `consentLoggingEnabled`        | `bool`                                            | Enables the [Consent Logging](https://docs.tealium.com/consent-change-event-specifications/) feature, which sends all consent status changes to Tealium Customer Data Hub for auditing purposes. (default: enabled)    | `true`                                       |
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)                 | Sets the consent policy to either CCPA or GDPR. Consent manager is only enabled if this property is set.                                                                                                                                                     | `ConsentPolicy.GDPR`                         |
| `lifecycleAutotrackingEnabled` | `bool`                                            | Enables or disables lifecycle auto tracking (default: enabled).                                                                                                                                                                                              | `false`                                      |
| `useRemoteLibrarySettings`     | `bool`                                            | Enables or disables the [Mobile Publish Settings](https://docs.tealium.com/creating-a-mobile-profile/) (default: enabled). Configure the Mobile Publish Settings in Tealium iQ Tag Management, or disable the feature. | `false`                                      |
| `visitorServiceEnabled`        | `bool`                                            | Enables or disables the automatic retrieval of the Visitor Profile using the [Data Layer Enrichment API](https://docs.tealium.com/data-layer-enrichment-api/) (default: disabled).                                | `true`                                       |
| `sessionCountingEnabled`       | `Boolean`                                   | Enables or disables session counting for Tealium iQ accounts. Set this to `false` if you are self-hosting your Tealium JavaScript files. (default: enabled)                                                                                                            | `false`                                                                                                        |


## Class: `TealiumEnvironment`

`TealiumEnvironment` is one of three default environments (Dev, QA, Prod), or may be a custom environment that Tealium publishes to.

Example:

```javascript
TealiumEnvironment.Dev
```

The following environments are available:

| Value   | Description              |
|:--------|:-------------------------|
| `.Dev`  | Development environment. |
| `.Qa`   | QA or UAT environment.   |
| `.Prod` | Production environment.  |


## Interface: `TealiumDispatch`

An interface that defines the type of dispatch to be tracked. The following classes implement `TealiumDispatch`:

### Class: `TealiumEvent`

To track a user's interaction with a game or game view, pass an instance of `TealiumEvent(eventName, dataLayer)` to the [`Track()`](#track) method. `TealiumEvent` is comprised of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
TealiumEvent(viewName, dataLayer)
```

| Parameters  | Type                         | Description                                | Example                                                                                           |
|:------------|:-----------------------------|:-------------------------------------------|:--------------------------------------------------------------------------------------------------|
| `eventName` | `string`                     | Name of game event.                        | `level_completed`                                                                                 |
| `dataLayer` | `Dictionary<string, object>` | (Optional) Data to be sent with the event. | `new Dictionary<string, object> {{"user_id", "gamer123"}, {"level": 2}, {"total_points": 17500}}` |

Example:

```javascript
TealiumEvent event = TealiumEvent('EVENT_NAME',
    new Dictionary<string, object> {{"KEY", "VALUE"}});
TealiumUnityPlugin.Track(event);
```

### Class: `TealiumView`

To track screen views in a game, pass an instance of `TealiumView(viewName, dataLayer)` to the [`Track()`](#track) method. `TealiumView` is comprised of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
TealiumView(viewName, dataLayer)
```

| Parameters  | Type                         | Description                                | Example                                                      |
|:------------|:-----------------------------|:-------------------------------------------|:-------------------------------------------------------------|
| `viewName`  | `string`                     | Name of view or screen in a game.          | `login_view`                                                 |
| `dataLayer` | `Dictionary<string, object>` | (Optional) Data to be sent with the event. | `new Dictionary<string, object> {{"customer_id", "abc123"}}` |

Example:

```javascript
TealiumView view = new TealiumView("VIEW_NAME",
    new Dictionary<string, object> {{"KEY", "VALUE"}})
TealiumUnityPlugin.Track(view);
```
