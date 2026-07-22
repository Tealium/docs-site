---
title: Tealium
description: The Tealium class serves as the main API entry point for all modules.
url: https://docs.tealium.com/platforms/flutter-v2/api/tealium/
---
<blockquote>
This is the previous version (2.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](https://docs.tealium.com/platforms/flutter/).
</blockquote>


## Class: `Tealium`

The following summarizes the commonly used methods of the Flutter `Tealium` class.

| Method | Description |
| ----- | ------ |
| [`addCustomRemoteCommand()`](#addcustomremotecommand)| Adds a remote command callback to the remote command manager. |
| [`addRemoteCommand()`](#addremotecommand)| Adds a remote command to the remote command manager |
| [`addToDataLayer()`](#addtodatalayer) | Adds data to persistent data layer |
| [`clearStoredVisitorIds()`](#clearstoredvisitorids)       | Deletes the stored cache of visitor IDs and calls `resetVisitorId`. |
| [`gatherTrackData()`](#gathertrackdata) | Gathers data from all collectors and data layer |
| [`getFromDataLayer()`](#getfromdatalayer) | Gets the value for a specified key in the persistent data layer |
| [`getConsentCategories()`](#getconsentcategories) | Gets the user's consented categories |
| [`getConsentStatus()`](#getconsentstatus) | Gets the user's consent status |
| [`getVisitorId()`](#getvisitorid) | Gets the user's visitor ID |
| [`initialize()`](#initialize) | 	Initializes Tealium with configuration parameters |
| [`joinTrace()`](#jointrace) | Joins a trace with the given ID |
| [`leaveTrace()`](#leavetrace) | Leaves a previously joined traced and ends the visitor session |
| [`removeFromDataLayer()`](#removefromdatalayer) | Removes a list of persistent data keys-value pairs that was previously set using `addToDataLayer()` |
| [`removeRemoteCommand()`](#removeremotecommand) | Removes a remote command from the remote command manager |
| [`resetVisitorId()`](#resetvisitorid) | Generates a new visitor ID for the user. |
| [`setConsentCategories()`](#setconsentcategories) | Sets the consent categories of a user |
| [`setConsentExpiryListener()`](#setconsentexpirylistener) | Sets the consent expired listener/callback |
| [`setConsentStatus()`](#setconsentstatus) | Sets the user's consent status |
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
| `id` | `String` | Name of the command ID from the tag configuration | `"test_command"` |
| `callback` | `Function ` | A callback function to execute after receiving the response from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```dart
Tealium.addCustomRemoteCommand('CUSTOM_COMMAND_ID', (payload) {
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
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, path: "firebase.json")); // local
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, url: "www.tealium.com/path_to_remote_command/firebase.json")); // remote
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName)); // webview
```

### `addToDataLayer()`

Adds data to the persistent data layer for the given expiration.

```dart
Tealium.addToDataLayer(data, expiry);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | `Map<String, Object>` | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{'persistent_key' : 'persistent_val'}` |
| `expiry` | `Expiry` | Length of time for which to persist the data | `Expiry.forever` |

### `clearStoredVisitorIds()`

Clears all previously stored visitor IDs and hashed customer identifiers.

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
| `N/A` | `Future<dynamic>` | Future succeeds after value was successfully retrieved from `Tealium.dataLayer` |

Example:

```dart
Tealium.getFromDataLayer('key')
    .then((value) => print('Value From data layer: $value'));
```


### `getConsentCategories()`

Gets the user's consented categories.

```dart
Tealium.getConsentCategories();
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `N/A` | `Future<List<dynamic>>` | Future completes after the consent categories have been successfully retrieved from the `Tealium.ConsentManager` |

Example:

```dart
Tealium.getConsentCategories()
  .then((categories) =>
      print('Consent Categories: ' + categories.join(",")));
```


### `getConsentStatus()`

Gets the user's consent status as a callback function.

```dart
Tealium.getConsentStatus();
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `N/A` | `Future<String>` | Future completes after the consent status was successfully retrieved from the `Tealium.ConsentManager` |

Example:

```dart
Tealium.getConsentStatus()
  .then((status) => print('Consent Status: $status'));
```

### `getVisitorId()`

Gets the user's visitor ID as a callback function.

```dart
Tealium.getVisitorId();
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `N/A` | `Future<String>` | Future returns after the `Tealium.visitorId` was successfully retrieved |

### `initialize()`

Initialize Tealium before calling any other method.

```dart
Tealium.initialize(config);
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `config`  | `TealiumConfig` | Configuration |
| `N/A` | `Future<bool>` | Future completes after the Tealium initialization is successful |


Example:

```dart
final config = TealiumConfig(
    'ACCOUNT',
    'PROFILE',
    TealiumEnvironment.dev,
    [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity,
    ],
    [
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands,
    ],
    loglevel: LogLevel.DEV,
    consentLoggingEnabled: true,
    consentPolicy: ConsentPolicy.GDPR,
    visitorServiceEnabled: true);

Tealium.initialize(config).then((_) {
    print('Tealium Initialized');
    Tealium.setConsentStatus(ConsentStatus.consented);
    Tealium.setConsentExpiryListener(() => print('Consent Expired'));
});
```


### `joinTrace()`

Joins a trace with the specified ID. Learn more about [Trace](https://docs.tealium.com/platforms/getting-started-mobile/trace/).

```dart
Tealium.joinTrace(id);
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `id` | `String` | Trace ID retrieved from the CDH |  `"abc123xy"` |

### `leaveTrace()`

Leaves a previously joined traced and ends the visitor session. The trace remains active for the duration of the app session until this method is called.

```dart
Tealium.leaveTrace();
```

### `removeFromDataLayer()`

Remove persistent data that was previously set using `addToDataLayer()`.

```dart
Tealium.removeFromDataLayer(keys);
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `keys` | `List<String>` | Array of key names |  `["key1", "key2"]` |

### `removeRemoteCommand()`

Removes a remote command from the remote command manager.

```dart
Tealium.removeRemoteCommand(id);
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `id` | `String` | Name of the command ID to remove |  `"test_command"` |

Example:

```dart
Tealium.removeRemoteCommand('test_command');
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
| `categories` | `List<ConsentCategories>` | Array of user consent categories | `[ConsentCategories.email, ConsentCategories.personalization]` |

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

Sets a callback to execute after the user's consent preferences have expired according the `ConsentExpiry`.

```dart
Tealium.setConsentExpiryListener(callback);
```

| Parameter | Type | Description |
|-----------|-------------| ---- |
| `callback`  | `Function` | Code to execute after consent expires |

```dart
Tealium.setConsentExpiryListener(() {
    print('Consent Expired');
});
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
Tealium.setVisitorIdListener((newVisitorId) {
    print(newVisitorId);
});
```


### `setVisitorServiceListener()`

Sets a callback to execute when the visitor profile is updated. The updated `VisitorProfile` is provided in the callback response.

The VisitorService module implements the [Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/) feature of the Tealium Customer Data Hub.

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
  'cart_add',
  {
    'customer_id': 'abc123',
    'product_id': ["PROD123", "PROD456"],
    'product_price': [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```

### `gatherTrackData()`

Gathers all data from all collectors and data layer.

Example:

```dart
Tealium.gatherTrackData()
  .then((data) => print('Gather track data: $data'));
```

## Interface: `TealiumDispatch`

An interface that defines the type of dispatch to be tracked. The following classes implement `TealiumDispatch`:

### Class: `TealiumEvent`

To track a user's interaction with a screen or a screen view, pass an instance of `TealiumEvent(eventName, dataLayer)` to the [`track()`](#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```dart
final tealEvent = TealiumEvent(eventName, dataLayer);
Tealium.track(tealEvent);
```

| Parameters  | Type    | Description      |
|:------------|:--------|:-----------------|
| `eventName` | `String` | The event name, passed as the `tealium_event` attribute.  |
| `dataLayer` | `Map<String, Object>` | (Optional) Data to be sent with the event in key-value format. |

Example:

```dart
final tealEvent = TealiumEvent(
  'cart_add',
  {
    'customer_id': 'abc123',
    'product_id': ["PROD123", "PROD456"],
    'product_price': [4.00, 6.00]
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
| `dataLayer` | `Map<String, Object>` | (Optional) Data to be sent with the event in key-value format. |

Example:

```dart
final screenView = TealiumView(
  'purchase',
  {
    'customer_id': 'abc123',
    'order_total': 10.00,
    'product_id': ["PROD123", "PROD456"],
    'order_id': '0123456789'
  }
);
Tealium.track(screenView);
```
