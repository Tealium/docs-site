---
title: API reference
description: Reference guide for classes and methods provided by Tealium for Flutter.
url: https://docs.tealium.com/platforms/flutter-v1/api/
---This is the previous version (1.x) of Tealium for Flutter. For the latest version, see [Tealium for Flutter](/platforms/flutter/).

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
| `commandID` | `String` | Name of the command ID from the tag configuration | `&#34;test_command&#34;` |
| `description` | `String ` | Description of the remote command | `&#34;Firebase remote command&#34;` |
| `callback` | `Function ` | A callback function to execute once the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```dart
Tealium.addRemoteCommand(&#34;firebase&#34;, &#34;Firebase Remote Command&#34;, (payload) {

  final eventName = payload[&#34;firebase_event_name&#34;];
  final eventProperties = payload[&#34;firebase_event_properties&#34;];

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
| `instanceName` | `String` | Name of the Tealium instance | `&#34;instance-2&#34;` |
| `commandID` | `String` | Name of the command ID from the tag configuration | `&#34;test_command&#34;` |
| `description` | `String ` | Description of the remote command | `&#34;Firebase remote command&#34;` |
| `callback` | `Function ` | A callback function to execute once the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```dart
Tealium.addRemoteCommandForInstance(&#34;instance-2&#34;, &#34;verify_email&#34;, &#34;Verify User Email&#34;, (user) {

	print(&#39;Howdy, ${user.name}!&#39;);
	print(&#39;We sent the verification link to ${user.email}.&#39;);

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
| `key` | `String` | Key name | `&#34;key1&#34;` |

### `getPersistentDataForInstance()`

Gets persistent data, for a specific Tealium instance.

```dart
Tealium.getPersistentDataForInstance(instance, key)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `&#34;instance123&#34;` |
| `key` | `String` | Key name | `&#34;key1&#34;` |

### `getVolatileData()`

Gets volatile data.

```dart
Tealium.getVolatileData(key)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `key` | `String` | Key name | `&#34;key1&#34;` |

### `getVolatileDataForInstance()`

Gets volatile data, for a specific Tealium instance.

```dart
Tealium.getVolatileDataForInstance(instance, key)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `&#34;instance123&#34;` |
| `key` | `String` | Key name | `&#34;key1&#34;` |

### `initialize()`

Initializes the Tealium instance.

```dart
Tealium.initialize(account, profile, environment,
               iosDataSource, androidDataSource,
               instance, isLifecycleEnabled)
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `account` | `String` | Tealium account name |  `&#34;companyXYZ&#34;` |
| `profile` | `String` | Tealium profile name |  `&#34;main&#34;` |
| `environment` | `String` | Tealium environment name |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `iosDataSource` | `String` | (Optional) data source key  (Set to `null` if none) |  `&#34;abc123&#34;` |
| `androidDataSource` | `String` | (Optional) The Android data source key (Set to `null` if none) |  `null` |
| `instance` | `String` | (Optional) Tealium instance name (default: `&#34;main&#34;`) |  `&#34;main&#34;` |
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
| `account` | `String` | Tealium account name |  `&#34;companyXYZ&#34;` |
| `profile` | `String` | Tealium profile name |  `&#34;main&#34;` |
| `environment` | `String` | Tealium environment name |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `iosDataSource` | `String` | (Optional) data source key  (Set to `null` if none) |  `&#34;abc123&#34;` |
| `androidDataSource` | `String` | (Optional) The Android data source key (Set to `null` if none) |  `null` |
| `instance` | `String` | (Optional) Tealium instance name (default: `&#34;main&#34;`) |  `&#34;main&#34;` |
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
| `account` | `String` | Tealium account name |  `&#34;companyXYZ&#34;` |
| `profile` | `String` | Tealium profile name |  `&#34;main&#34;` |
| `environment` | `String` | Tealium environment name |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `iosDataSource` | `String` | (Optional) data source key  (Set to `null` if none) |  `&#34;abc123&#34;` |
| `androidDataSource` | `String` | (Optional) The Android data source key (Set to `null` if none) |  `null` |
| `instance` | `String` | (Optional) Tealium instance name (default: `&#34;main&#34;`) |  `&#34;main&#34;` |
| `isLifecycleEnabled` | `bool` | (Optional) Enable lifecycle tracking events (default: `true`)|  [`true`, `false`] |

### `removePersistentData()`

Removes persistent data.

```dart
Tealium.removePersistentData(keys)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `keys` | `List&lt;String&gt;` | List with String key names | `[&#34;persistent_var&#34;, &#34;persistent_var2&#34;]` |

### `removePersistentDataForInstance()`

Removes persistent data, for a specific Tealium instance.

```dart
Tealium.removePersistentDataForInstance(instance, keys)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `&#34;instance123&#34;` |
| `keys` | `List&lt;String&gt;` | List with String key names | `[&#34;persistent_var&#34;, &#34;persistent_var2&#34;]` |

### `removeRemoteCommand()`

Removes a remote command from the remote command manager.

```dart
Tealium.removeRemoteCommand(commandID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `commandID ` | `String` | Name of command ID to remove  | `&#34;test_command&#34;` |

Example:

```dart
Tealium.removeRemoteCommand(&#34;firebase&#34;);
```


### `removeRemoteCommandForInstance()`

Removes a remote command from the remote command manager, for a specific Tealium instance.

```dart
Tealium.removeRemoteCommandForInstance(instanceName, commandID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `instanceName` | `String` | Name of the Tealium instance | `&#34;instance-2&#34;` |
| `commandID ` | `String` | Name of the command ID to remove  | `&#34;test_command&#34;` |

```dart
Tealium.removeRemoteCommandForInstance(&#34;instance-2&#34;, &#34;firebase&#34;);
```

### `removeVolatileData()`

Removes volatile data.

```dart
Tealium.removeVolatileData(keys)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `keys` | `List&lt;String&gt;` | List with String key names | `[&#34;volatile_var1&#34;, &#34;volatile_var2&#34;]` |

### `removeVolatileDataForInstance()`

Removes volatile data, for a specific Tealium instance.

```dart
Tealium.removeVolatileDataForInstance(instance, keys)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `&#34;instance123&#34;` |
| `keys` | `List&lt;String&gt;` | List with String key names | `[&#34;volatile_var1&#34;, &#34;volatile_var2&#34;]` |

### `setPersistentData()`

Sets persistent data.

```dart
Tealium.setPersistentData(data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `data` | `Map&lt;String, dynamic&gt;` | Persistent data as key-value pairs | `{&#34;key1&#34;: &#34;value1&#34;}` |

### `setPersistentDataForInstance()`

Sets persistent data, for a specific Tealium instance.

```dart
Tealium.setPersistentDataForInstance(instance, data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `&#34;instance123&#34;` |
| `data` | `Map&lt;String, dynamic&gt;` | Persistent data as key-value pairs | `{&#34;key1&#34;: &#34;value1&#34;}` |

### `setVolatileData()`

Sets volatile data.

```dart
Tealium.setVolatileData(data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `data` | `Map&lt;String, dynamic&gt;` | Volatile data as key-value pairs | `{&#34;key1&#34;: &#34;value1&#34;}` |

### `setVolatileDataForInstance()`

Sets volatile data, for a specific Tealium instance.

```dart
Tealium.setVolatileDataForInstance(instance, data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | Specific Tealium instance name | `&#34;instance123&#34;` |
| `data` | `Map&lt;String, dynamic&gt;` | Volatile data as key-value pairs | `{&#34;key1&#34;: &#34;value1&#34;}` |


### `trackEvent()`

Track non-view events.

```dart
Tealium.trackEvent(eventName, data)
```

| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `eventName` | `String` | Name to identify the event |  `&#34;Event button click&#34;` |
| `data` | `Map&lt;String, dynamic&gt;` | (Optional) Event data as key-value pairs |  `{&#34;key1&#34;: &#34;value1&#34;}` |


### `trackEventForInstance()`

Track non-view events, for a specific Tealium instance.

```dart
Tealium.trackEventForInstance(instance, eventName, data)
```
| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance` | `String` | Tealium instance name | `&#34;instance123&#34;` |
| `eventName` | `String` | Name to identify the event | `&#34;Event button click&#34;` |
| `data` | `Map&lt;String, dynamic&gt;` | (Optional) Event data as key-value pairs |  `{&#34;key1&#34;: &#34;value1&#34;}` |


### `trackView()`

Track screen views.

```dart
Tealium.trackView(viewName, data)
```

| Parameter | Type | Description |  Example |
|-----------|-------------| ---- | ------- |
| `viewName` | `String` | Name to identify screen view | `&#34;View screen&#34;` |
| `data` | `Map&lt;String, dynamic&gt;` | (Optional) Event data as key-value pairs|  `{&#34;key1&#34;: &#34;value1&#34;}` |

### `trackViewForInstance()`

Track screen views, for a specific Tealium instance.

```dart
Tealium.trackViewForInstance(instance, viewName, data)
```
| Parameter | Type | Description | Example |
|-----------|-------------| ---- | ------- |
| `instance` | `String` | Tealium instance name | `&#34;instance123&#34;` |
| `viewName` | `String` | Name to identify the view | `&#34;View screen&#34;` |
| `data` | `Map&lt;String, dynamic&gt;` | (Optional) Event data as key-value pairs |  `{&#34;key1&#34;: &#34;value1&#34;}` |
