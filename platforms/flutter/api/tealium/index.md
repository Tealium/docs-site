---
title: Tealium
description: The Tealium class serves as the main API entry point for all modules.
url: https://docs.tealium.com/platforms/flutter/api/tealium/
---
## Class: `Tealium`

The following summarizes the commonly used methods of the Flutter `Tealium` class.

| Method | Description |
| ----- | ------ |
| [`addCustomRemoteCommand()`](#addcustomremotecommand)| Adds a remote command callback to the remote command manager. |
| [`addRemoteCommand()`](#addremotecommand)| Adds a remote command to the remote command manager |
| [`addToDataLayer()`](#addtodatalayer) | Adds data to persistent data layer |
| [`clearStoredVisitorIds()`](#clearstoredvisitorids) | Clears all previously stored visitor IDs and hashed customer identifiers. As a result, a new visitor ID is generated and becomes the active visitor ID. |
| [`gatherTrackData()`](#gathertrackdata) | Gathers data from all collectors and data layer |
| [`getFromDataLayer()`](#getfromdatalayer) | Gets the value for a specified key in the persistent data layer |
| [`getConsentCategories()`](#getconsentcategories) | Gets the user&#39;s consented categories |
| [`getConsentStatus()`](#getconsentstatus) | Gets the user&#39;s consent status |
| [`getVisitorId()`](#getvisitorid) | Gets the user&#39;s visitor ID |
| [`initialize()`](#initialize) | Initializes Tealium with configuration parameters |
| [`joinTrace()`](#jointrace) | Joins a trace with the given ID |
| [`leaveTrace()`](#leavetrace) | Leaves a previously joined traced and ends the visitor session |
| [`removeFromDataLayer()`](#removefromdatalayer) | Removes a list of persistent data keys-value pairs that was previously set using `addToDataLayer()` |
| [`removeRemoteCommand()`](#removeremotecommand) | Removes a remote command from the remote command manager |
| [`resetVisitorId()`](#resetvisitorid) | Generates a new visitor ID for the user. |
| [`setConsentCategories()`](#setconsentcategories) | Sets the consent categories of a user |
| [`setConsentExpiryListener()`](#setconsentexpirylistener) | Sets the consent expired listener/callback |
| [`setConsentStatus()`](#setconsentstatus) | Sets the user&#39;s consent status |
| [`setVisitorIdListener()`](#setvisitoridlistener) | Add a listener for changes on `visitorId`. |
| [`setVisitorServiceListener()`](#setvisitorservicelistener) | Sets the visitor service listener/callback |
| [`terminateInstance()`](#terminateinstance) | Terminates the Tealium instance by disabling the Tealium library and removing all module references |
| [`track()`](#track) | Track an event or screen view |

### `addCustomRemoteCommand()`

Adds a custom remote command to the remote command manager, backed up by a Tag on Tealium iQ Tag Management.

```dart
Tealium.addCustomRemoteCommand(id, callback);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `id` | `String` | Name of the command ID from the tag configuration | `&#34;test_command&#34;` |
| `callback` | `Function ` | A callback function to execute after receiving the response from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```dart
Tealium.addCustomRemoteCommand(&#39;CUSTOM_COMMAND_ID&#39;, (payload) {
  print(JsonEncoder().convert(payload));
});
```

### `addRemoteCommand()`

Adds a remote command to the remote command manager.

```dart
Tealium.addRemoteCommand(remoteCommand);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `remoteCommand` | `RemoteCommand` | A prebuilt remote command with either path, URL, or webview configurations. | See example below. |

Example:

```dart
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, path: &#34;firebase.json&#34;)); // local
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, url: &#34;www.tealium.com/path_to_remote_command/firebase.json&#34;)); // remote
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName)); // webview
```

### `addToDataLayer()`

Adds data to the persistent data layer for the given expiration.

```dart
Tealium.addToDataLayer(data, expiry);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | `Map&lt;String, Object&gt;` | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{&#39;persistent_key&#39; : &#39;persistent_val&#39;}` |
| `expiry` | `Expiry` | Length of time for which to persist the data | `Expiry.forever` |

### `clearStoredVisitorIds()`

Clears all previously stored visitor IDs and hashed customer identifiers. As a result, a new visitor ID is generated and becomes the active visitor ID.

```dart
Tealium.clearStoredVisitorIds();
```


### `getFromDataLayer()`

Gets the value for a specified key in the persistent data layer as a callback function.

```dart
Tealium.getFromDataLayer(key);
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `key` | `String` | Key to retrieve from the data layer|
| `N/A` | `Future&lt;dynamic&gt;` | Future succeeds after value was successfully retrieved from `Tealium.dataLayer` |

Example:

```dart
Tealium.getFromDataLayer(&#39;key&#39;)
    .then((value) =&gt; print(&#39;Value From data layer: $value&#39;));
```


### `getConsentCategories()`

Gets the user&#39;s consented categories.

```dart
Tealium.getConsentCategories();
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `N/A` | `Future&lt;List&lt;dynamic&gt;&gt;` | Future completes after the consent categories have been successfully retrieved from the `Tealium.ConsentManager` |

Example:

```dart
Tealium.getConsentCategories()
  .then((categories) =&gt;
      print(&#39;Consent Categories: &#39; &#43; categories.join(&#34;,&#34;)));
```


### `getConsentStatus()`

Gets the user&#39;s consent status as a callback function.

```dart
Tealium.getConsentStatus();
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `N/A` | `Future&lt;String&gt;` | Future completes after the consent status was successfully retrieved from the `Tealium.ConsentManager` |

Example:

```dart
Tealium.getConsentStatus()
  .then((status) =&gt; print(&#39;Consent Status: $status&#39;));
```

### `getVisitorId()`

Gets the user&#39;s visitor ID.

```dart
Tealium.getVisitorId();
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `N/A` | `Future&lt;String&gt;` | Future returns after the `Tealium.visitorId` was successfully retrieved |

Example:

```dart
final visitorId = await Tealium.getVisitorId();
```

### `initialize()`

Initialize Tealium before calling any other method.

```dart
Tealium.initialize(config);
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `config`  | `TealiumConfig` | Configuration |
| `N/A` | `Future&lt;void&gt;` | Future completes when Tealium is successfully initialized. Throws `PlatformException` on failure. |


Example:

```dart
final config = TealiumConfig(
    &#39;ACCOUNT&#39;,
    &#39;PROFILE&#39;,
    TealiumEnvironment.dev,
    [Collectors.AppData, Collectors.DeviceData, Collectors.Lifecycle, Collectors.Connectivity],
    [Dispatchers.Collect, Dispatchers.TagManagement, Dispatchers.RemoteCommands],
    loglevel: LogLevel.DEV,
    consentLoggingEnabled: true,
    consentPolicy: ConsentPolicy.GDPR,
    visitorServiceEnabled: true);

try {
    await Tealium.initialize(config);
    Tealium.setConsentStatus(ConsentStatus.consented);
    Tealium.setConsentExpiryListener(() =&gt; print(&#39;Consent Expired&#39;));
} on PlatformException catch (e) {
    print(&#39;Tealium initialization error: ${e.message}&#39;);
}
```


### `joinTrace()`

Joins a trace with the specified ID. Learn more about [Trace](/platforms/getting-started-mobile/trace/).

```dart
Tealium.joinTrace(id);
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `id` | `String` | Trace ID retrieved from the CDH |  `&#34;abc123xy&#34;` |

### `leaveTrace()`

Leaves a previously joined traced and ends the visitor session. The trace remains active for the duration of the app session until this method is called.

```dart
Tealium.leaveTrace();
```

### `removeFromDataLayer()`

Remove persistent data that was previously set using `Tealium.addToDataLayer()`.

```dart
Tealium.removeFromDataLayer(keys);
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `keys` | `List&lt;String&gt;` | Array of key names |  `[&#34;key1&#34;, &#34;key2&#34;]` |

### `removeRemoteCommand()`

Removes a remote command from the remote command manager.

```dart
Tealium.removeRemoteCommand(id);
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `id` | `String` | Name of the command ID to remove |  `&#34;test_command&#34;` |

Example:

```dart
Tealium.removeRemoteCommand(&#39;test_command&#39;);
```

### `resetVisitorId()`

Generates a new visitor ID for the user.

```dart
Tealium.resetVisitorId();
```

### `setConsentCategories()`

Sets the consent categories of a user. Pass in an array of Strings to set the categories. Default is an empty array until `ConsentStatus` is set to `ConsentStatus.consented`. If the consent status is `ConsentStatus.consented` and no categories are specified with the `setConsentCategories()` method, then all categories are set.

```dart
Tealium.setConsentCategories(categories);
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `categories` | `List&lt;ConsentCategories&gt;` | Array of user consent categories | `[ConsentCategories.email, ConsentCategories.personalization]` |

Example:

```dart
Tealium.setConsentCategories([ConsentCategories.analytics, ConsentCategories.email]);
```

#### Consent categories

The following consent categories are available:

| Value | Description |
| ----- | ----------- |
| `analytics` |  Analytics |
| `affiliates` |  Affiliates |
| `displayAds` | Display ads  |
| `email` | Email |
| `personalization` | Personalization |
| `search` | Search |
| `social`  |  Social |
| `bigData` | Big data |
| `mobile` | Mobile  |
| `engagement` | Engagement |
| `monitoring` | Monitoring |
| `crm` | CRM |
| `cdp` | CDP |
| `cookieMatch` | Cookie match |
| `misc` | Misc |

### `setConsentExpiryListener()`

Sets a callback to execute after the user&#39;s consent preferences have expired according the `ConsentExpiry`.

```dart
Tealium.setConsentExpiryListener(callback);
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `callback`  | `Function` | Code to execute after consent expires |

```dart
Tealium.setConsentExpiryListener(() =&gt; print(&#39;Consent Expired&#39;));
```

### `setConsentStatus()`

Sets the consent status of a user. Default is `ConsentStatus.unknown` until the status is updated.

```dart
Tealium.setConsentStatus(status);
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `status`  | `ConsentStatus` | Consent status |

Example:

```dart
Tealium.setConsentStatus(ConsentStatus.consented);
```

#### Consent status

The following consent statuses are available:  

| Value | Description |
| ----- | ----------- |
| `ConsentStatus.consented` |  Consented |
| `ConsentStatus.notConsented` |  Not consented |
| `ConsentStatus.unknown` |  Unknown |

### `setVisitorIdListener()`

Sets a callback to execute when the visitor ID changes.

```dart
Tealium.setVisitorIdListener(callback);
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `callback`  | `Function` | Code to execute with the updated `visitorId`. |

Example:

```dart
Tealium.setVisitorIdListener((newVisitorId) =&gt; print(newVisitorId));
```


### `setVisitorServiceListener()`

Sets a callback to execute when the visitor profile is updated. The updated `VisitorProfile` is provided in the callback response.

The VisitorService module implements the [Data Layer Enrichment]() feature of the Tealium Customer Data Hub.

Usage of this module is recommended if you are licensed for Tealium AudienceStream and you want to use the visitor profile to enhance the user experience in your mobile application. If you are not licensed for AudienceStream, usage of this module is not recommended as no visitor profile is returned.

```dart
Tealium.setVisitorServiceListener(callback);
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `callback`  | `Function` | Code to execute after the updated visitor profile returns |

Example:

```dart
Tealium.setVisitorServiceListener((profile) {
    print(JsonEncoder().convert(profile));
});
```

### `terminateInstance()`

Terminates the Tealium instance by disabling the Tealium library and removing all module references. Re-enable by creating a new Tealium instance, if required.

```dart
Tealium.terminateInstance();
```

### `track()`

Tracks a screen view or event with optional event data.

```dart
Tealium.track(tealEvent);
```

| Parameter | Type | Description |  
|-----------|-------------| ---- |
| `tealEvent` | `TealiumDispatch` | Tealium dispatch with the event name and event data. |

To track view or events, pass an instance of [`TealiumView`](#class-tealiumview) or [`TealiumEvent`](#class-tealiumevent) to the `track()` method:

```dart
final tealEvent = TealiumEvent(
  &#39;cart_add&#39;, 
  {
    &#39;customer_id&#39;: &#39;abc123&#39;, 
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#39;product_price&#39;: [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```

### `gatherTrackData()`

Gathers all data from all collectors and data layer.

Example:

```dart
Tealium.gatherTrackData()
  .then((data) =&gt; print(&#39;Gather track data: $data&#39;));
```

## Interface: `TealiumDispatch`

An interface that defines the type of dispatch to be tracked. The following classes implement `TealiumDispatch`:

### Class: `TealiumEvent`

To track a user&#39;s interaction with a screen or a screen view, pass an instance of `TealiumEvent(eventName, dataLayer)` to the [`track()`](#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```dart
final tealEvent = TealiumEvent(eventName, dataLayer);
Tealium.track(tealEvent);
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `eventName` | `String` | The event name, passed as the `tealium_event` attribute.  |
| `dataLayer` | `Map&lt;String, Object&gt;` | (Optional) Data to be sent with the event in key-value format. |

Example:

```dart
final tealEvent = TealiumEvent(
  &#39;cart_add&#39;, 
  {
    &#39;customer_id&#39;: &#39;abc123&#39;, 
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#39;product_price&#39;: [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```

### Class: `TealiumView`

To track screen views, pass an instance of `TealiumView(viewName, dataLayer)` to the [`track()`](#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data object.

```dart
final screenView = TealiumView(viewName, dataLayer);
Tealium.track(screenView);
```

| Parameters  | Type    | Description      |
|:------------|:--------|:-----------------|
| `viewName`  | `String`| The view name, passed as the `tealium_event` attribute.|
| `dataLayer` | `Map&lt;String, Object&gt;` | (Optional) Data to be sent with the event in key-value format. | 

Example:

```dart
final screenView = TealiumView(
  &#39;purchase&#39;, 
  {
    &#39;customer_id&#39;: &#39;abc123&#39;, 
    &#39;order_total&#39;: 10.00, 
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#39;order_id&#39;: &#39;0123456789&#39;
  }
);
Tealium.track(screenView);
```