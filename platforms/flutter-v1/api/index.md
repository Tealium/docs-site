---
title: API reference
description: Reference guide for classes and methods provided by Tealium for Flutter.
url: https://docs.tealium.com/platforms/flutter-v1/api/
---
<blockquote>
This is the previous version (1.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](https://docs.tealium.com/platforms/flutter/).
</blockquote>


## Class: `Tealium`

The following summarizes the commonly used methods of the Flutter `Tealium` class.

| Method | Description |
| ----- | ------ |
| `addRemoteCommand()`| Adds a remote command to the remote command manager |
| `addRemoteCommandForInstance()`| Adds a remote command to the remote command manager, for a specific Tealium instance |
| `getPersistentData()` | Gets persistent data |
| `getPersistentDataForInstance()` | Gets persistent data, for a specific Tealium instance|
| `getVolatileData()` | Gets volatile data |
| `getVolatileDataForInstance()` | Gets volatile data, for a specific Tealium instance |
| `initialize()` | Initializes the Tealium instance |
| `initializeCustom()` | Initializes the Tealium instance with custom options |
| `initializeWithConsentManager()` | Initializes the Tealium instance and enables consent management |
| `removePersistentData()` | Removes persistent data |
| `removePersistentDataForInstance()` | Removes persistent data, for a specific Tealium instance  |
| `removeRemoteCommand()` | Removes a remote command from the remote command manager |
| `removeRemoteCommandForInstance()` | Removes a remote command from the remote command manager, for a specific Tealium instance |
| `removeVolatileData()` | Removes volatile data |
| `removeVolatileDataForInstance()` | Removes volatile data, for a specific Tealium instance  |
| `setPersistentData()` | Sets persistent data |
| `setPersistentDataForInstance()` | Sets persistent data, for a specific Tealium instance  |
| `setVolatileData()` | Sets volatile data |
| `setVolatileDataForInstance()` | Sets volatile data, for a specific Tealium instance  |
| `trackEvent()` | Track non-view events |
| `trackEventForInstance()` | Track non-view events, for a specific Tealium instance |
| `trackView()` | Track screen views |
| `trackViewForInstance()` | Track screen views, for a specific Tealium instance  |

### `addRemoteCommand()`

Adds a remote command to the remote command manager.

```dart
Tealium.addRemoteCommand(commandID, description, callback);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `commandID` | `String` | Name of the command ID from the tag configuration | `"test_command"` |
| `description` | `String ` | Description of the remote command | `"Firebase remote command"` |
| `callback` | `Function ` | A callback function to execute once the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```dart
Tealium.addRemoteCommand("firebase", "Firebase Remote Command", (payload) {

  final eventName = payload["firebase_event_name"];
  final eventProperties = payload["firebase_event_properties"];

  analytics.logEvent(name: eventName, parameters: eventProperties);
});
```

### `addRemoteCommandForInstance()`

Adds a remote command to the remote command manager, for a specific Tealium instance.

```dart
Tealium.addRemoteCommandForInstance(instanceName, commandID, description, callback);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `instanceName` | `String` | Name of the Tealium instance | `"instance-2"` |
| `commandID` | `String` | Name of the command ID from the tag configuration | `"test_command"` |
| `description` | `String ` | Description of the remote command | `"Firebase remote command"` |
| `callback` | `Function ` | A callback function to execute once the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```dart
Tealium.addRemoteCommandForInstance("instance-2", "verify_email", "Verify User Email", (user) {

	print('Howdy, ${user.name}!');
	print('We sent the verification link to ${user.email}.');

	// Send data to email service to send email to user
	// ...
});
```

### `getPersistentData()`

Gets persistent data.

```dart
Tealium.getPersistentData(key)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `key` | `String` | Key name | `"key1"` |

### `getPersistentDataForInstance()`

Gets persistent data, for a specific Tealium instance.

```dart
Tealium.getPersistentDataForInstance(instance, key)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `"instance123"` |
| `key` | `String` | Key name | `"key1"` |

### `getVolatileData()`

Gets volatile data.

```dart
Tealium.getVolatileData(key)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `key` | `String` | Key name | `"key1"` |

### `getVolatileDataForInstance()`

Gets volatile data, for a specific Tealium instance.

```dart
Tealium.getVolatileDataForInstance(instance, key)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `"instance123"` |
| `key` | `String` | Key name | `"key1"` |

### `initialize()`

Initializes the Tealium instance.

```dart
Tealium.initialize(account, profile, environment,
               iosDataSource, androidDataSource,
               instance, isLifecycleEnabled)
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `account` | `String` | Tealium account name |  `"companyXYZ"` |
| `profile` | `String` | Tealium profile name |  `"main"` |
| `environment` | `String` | Tealium environment name |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDataSource` | `String` | (Optional) data source key  (Set to `null` if none) |  `"abc123"` |
| `androidDataSource` | `String` | (Optional) The Android data source key (Set to `null` if none) |  `null` |
| `instance` | `String` | (Optional) Tealium instance name (default: `"main"`) |  `"main"` |
| `isLifecycleEnabled` | `bool` | (Optional) Enable lifecycle tracking events (default: `true`)|  [`true`, `false`] |


### `initializeCustom()`

Initializes the Tealium instance with all options available.

```dart
Tealium.initializeCustom(account, profile, environment,
               iosDataSource, androidDataSource,
               instance, isLifecycleEnabled,
               overridePublishSettingsUrl,
               overrideTagManagementUrl,
               enableVdataCollectEndpointUrl,
               enableConsentManager)
```

The following additional parameters are included with this method call:


| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `account` | `String` | Tealium account name |  `"companyXYZ"` |
| `profile` | `String` | Tealium profile name |  `"main"` |
| `environment` | `String` | Tealium environment name |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDataSource` | `String` | (Optional) data source key  (Set to `null` if none) |  `"abc123"` |
| `androidDataSource` | `String` | (Optional) The Android data source key (Set to `null` if none) |  `null` |
| `instance` | `String` | (Optional) Tealium instance name (default: `"main"`) |  `"main"` |
| `isLifecycleEnabled` | `bool` | (Optional) Enable lifecycle tracking events (default: `true`)|  [`true`, `false`] |
| `overridePublishSettingsUrl` | `String` | (Optional) String representing the custom publish settings URL if overriding (Set to `null` if none)| |
| `overrideTagManagementUrl` | `String` | (Optional) String representing the custom tag management URL if overriding (Set to `null` if none)| |
| `enableVdataCollectEndpointUrl`| `String` | Toggle between data endpoints (`true` is the default in native Android and iOS libraries that send data to the Collect endpoint URL. `false` sends data to the older `vdata` endpoint (Set to `null` if none) | |
| `enableConsentManager` | `bool` | Enable the consent manager (enable: `true`, disable: `false`) | [`true`, `false`]  |

### `initializeWithConsentManager()`

Initializes the Tealium instance and enables consent management.

```dart
Tealium.initializeWithConsentManager(account, profile, environment,
               iosDataSource, androidDataSource,
               instance, isLifecycleEnabled)
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `account` | `String` | Tealium account name |  `"companyXYZ"` |
| `profile` | `String` | Tealium profile name |  `"main"` |
| `environment` | `String` | Tealium environment name |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDataSource` | `String` | (Optional) data source key  (Set to `null` if none) |  `"abc123"` |
| `androidDataSource` | `String` | (Optional) The Android data source key (Set to `null` if none) |  `null` |
| `instance` | `String` | (Optional) Tealium instance name (default: `"main"`) |  `"main"` |
| `isLifecycleEnabled` | `bool` | (Optional) Enable lifecycle tracking events (default: `true`)|  [`true`, `false`] |

### `removePersistentData()`

Removes persistent data.

```dart
Tealium.removePersistentData(keys)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `keys` | `List<String>` | List with String key names | `["persistent_var", "persistent_var2"]` |

### `removePersistentDataForInstance()`

Removes persistent data, for a specific Tealium instance.

```dart
Tealium.removePersistentDataForInstance(instance, keys)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `"instance123"` |
| `keys` | `List<String>` | List with String key names | `["persistent_var", "persistent_var2"]` |

### `removeRemoteCommand()`

Removes a remote command from the remote command manager.

```dart
Tealium.removeRemoteCommand(commandID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `commandID ` | `String` | Name of command ID to remove  | `"test_command"` |

Example:

```dart
Tealium.removeRemoteCommand("firebase");
```


### `removeRemoteCommandForInstance()`

Removes a remote command from the remote command manager, for a specific Tealium instance.

```dart
Tealium.removeRemoteCommandForInstance(instanceName, commandID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `instanceName` | `String` | Name of the Tealium instance | `"instance-2"` |
| `commandID ` | `String` | Name of the command ID to remove  | `"test_command"` |

```dart
Tealium.removeRemoteCommandForInstance("instance-2", "firebase");
```

### `removeVolatileData()`

Removes volatile data.

```dart
Tealium.removeVolatileData(keys)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `keys` | `List<String>` | List with String key names | `["volatile_var1", "volatile_var2"]` |

### `removeVolatileDataForInstance()`

Removes volatile data, for a specific Tealium instance.

```dart
Tealium.removeVolatileDataForInstance(instance, keys)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `"instance123"` |
| `keys` | `List<String>` | List with String key names | `["volatile_var1", "volatile_var2"]` |

### `setPersistentData()`

Sets persistent data.

```dart
Tealium.setPersistentData(data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `data` | `Map<String, dynamic>` | Persistent data as key-value pairs | `{"key1": "value1"}` |

### `setPersistentDataForInstance()`

Sets persistent data, for a specific Tealium instance.

```dart
Tealium.setPersistentDataForInstance(instance, data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `"instance123"` |
| `data` | `Map<String, dynamic>` | Persistent data as key-value pairs | `{"key1": "value1"}` |

### `setVolatileData()`

Sets volatile data.

```dart
Tealium.setVolatileData(data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `data` | `Map<String, dynamic>` | Volatile data as key-value pairs | `{"key1": "value1"}` |

### `setVolatileDataForInstance()`

Sets volatile data, for a specific Tealium instance.

```dart
Tealium.setVolatileDataForInstance(instance, data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `"instance123"` |
| `data` | `Map<String, dynamic>` | Volatile data as key-value pairs | `{"key1": "value1"}` |


### `trackEvent()`

Track non-view events.

```dart
Tealium.trackEvent(eventName, data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `eventName` | `String` | Name to identify the event |  `"Event button click"` |
| `data` | `Map<String, dynamic>` | (Optional) Event data as key-value pairs |  `{"key1": "value1"}` |


### `trackEventForInstance()`

Track non-view events, for a specific Tealium instance.

```dart
Tealium.trackEventForInstance(instance, eventName, data)
```
| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance` | `String` | Tealium instance name | `"instance123"` |
| `eventName` | `String` | Name to identify the event | `"Event button click"` |
| `data` | `Map<String, dynamic>` | (Optional) Event data as key-value pairs |  `{"key1": "value1"}` |


### `trackView()`

Track screen views.

```dart
Tealium.trackView(viewName, data)
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `viewName` | `String` | Name to identify screen view | `"View screen"` |
| `data` | `Map<String, dynamic>` | (Optional) Event data as key-value pairs|  `{"key1": "value1"}` |

### `trackViewForInstance()`

Track screen views, for a specific Tealium instance.

```dart
Tealium.trackViewForInstance(instance, viewName, data)
```
| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance` | `String` | Tealium instance name | `"instance123"` |
| `viewName` | `String` | Name to identify the view | `"View screen"` |
| `data` | `Map<String, dynamic>` | (Optional) Event data as key-value pairs |  `{"key1": "value1"}` |
