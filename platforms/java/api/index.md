---
title: API Reference
description: Reference guide for classes methods provided by Tealium for Java.
url: https://docs.tealium.com/platforms/java/api/
---
## Class: `Tealium`

The following summarizes the commonly used methods of the Java `Tealium` class.

| Method | Description |
| ----- | ------ |
| `addPersistentData()` | Use the `DataManager` to make data available across multiple app sessions |
| `deletePersistentData()` | Use the `DataManager` to delete previously persisted data by providing a list of keys to delete |
| `getDataManager()` | Get the `DataManager` object which processes call time data and handles persistent data |
| `getPersistentData()` | Use the `DataManager` to retrieve data that has been persisted |
| `getSessionId()` | Use the `DataManager` to fetch the current session ID  |
| `resetSessionId()` | Use the `DataManager` to reset the session ID |
| `track()` | Track events |

### `addPersistentData()`

Use the `DataManager` to make data available across multiple app sessions.

```java
addPersistentData(data)
```

| Parameters | Type | Description  | Example |
| --- | --- | --- | --- |
| `data` | `Map<String, Object>` | Required map data to add to the existing persistent `Udo` | `["key":"value"]` |

```java
Udo data = new Udo();
data.put("KEY", "VALUE");
tealium.getDataManager().addPersistentData(data);
```

### `deletePersistentData()`

Use the `DataManager` to delete previously persisted data by providing a list of keys to delete.

```java
deletePersistentData(list)
```

| Parameters |  Type |Description | Example |
| --- | --- | --- | --- |
| `list` |  `List<String>` | List of keys as Strings | `["key1", "key2"]` |

```java
List<String> list = new List<>();
list.append("key_to_delete");
tealium.getDataManager().deletePersistentData(list);
```

### `getDataManager()`

Get the `DataManager` object which processes call time data and handles persistent data.

```java
getDataManager()
```

| Return Type | Description |
| --- | --- |
| `DataManager` | Instance of the Tealium `DataManager` object |

```java
DataManager dm = tealium.getDataManager()
```


### `getPersistentData()`

Use the `DataManager` to retrieve data that has been persisted.

```java
getPersistentData()
```

| Return Type | Description | Example |
| --- | --- | --- |
| `Udo` | Universal Data Object (UDO) of persistent data | `["key1", "key2"]` |

```java
Udo persistentData = tealium.getDataManager().getPersistentData()
```

### `getSessionId()`

Use the `DataManager` to fetch the current session ID. A session ID is created on initialization of the `Tealium` object.

```java
getSessionId()
```

| Return Type | Description | Example  |
| --- | --- | --- |
| `String` | Representation of a timestamp in milliseconds | `"1473371215123"` |

```java
tealium.getDataManager().getSessionId() 
```


### `resetSessionId()`

Use the `DataManager` to reset the session ID. Used when you need to start a new session other than at app start time.

```java
resetSessionId()
```

| Return Type | Description | Example |
| --- | --- | --- |
| `String` | New String representation of a timestamp in milliseconds that is added to all dispatches for the remainder of the current session. The returned String is for monitoring convenience as it is automatically added to the volatile data store when this method is called. | `"1473371215123"` |

```java
tealium.getDataManager().resetSessionId()
```


### `track()`

Track events.

```java
track(eventTitle)
```

Track events with optional parameters for data and a callback.

```java
track(eventTitle, data, callback)
```

| Parameter | Type | Description |  Example |
|-----------|-------------|------| --- |
| `eventTitle` | `String` |Title of event (becomes the `tealium_event` and `event_name` event attribute values) |  `"Some Event"` |
| `data`    | `Udo` |  (Optional) Universal Data Object (UDO) with event data as key-value pairs| `udoObject` |
| `callback`| `DispatchCallback` |(Optional) Object with a function assigned to the "callback" key | `dispatchCallbackObject` |


## Class: `Tealium.Builder`

The following summarizes the commonly used methods of the Java `Tealium.Builder` class.

| Method | Description |
| ----- | ------ |
| `build()` | Executes the build, and sets the persistent data and collect dispatcher |
| `Builder()` | Constructor to instantiate a Tealium object |
| `setDatasource()` | Data source key |
| `setEnvironment()` | Sets the Tealium environment name |  
| `setPersistentData()` | Sets the persistent data |

### `build()`

Executes the build. Sets the persistent data if it hasn't been explicitly set with the `setPersistentData()` method. Sets the collect dispatcher if it hasn't been explicitly set with the setCollectDispatcher() method.

```java
tealium.build();
```

### `Builder()`

Constructor to instantiate a Tealium object.

```java
Tealium.Builder(account, profile, environment).build()
```

```java
// Init Tealium
Tealium tealium = new Tealium.Builder(account, profile)
    .setEnvironment(environment)
    .setDatasource(datasource)
    .build();
```

| Parameters |  Type | Description |  Example |
| --- | --- | --- | --- |
| `account` |  `String` |Tealium account name | `"companyXYZ"` |
| `profile` |  `String` |Tealium profile name  | `"main"` |
| `environment` |  `String` |Tealium environment name  | [`"dev"`, `"qa"`, `"prod"`] |
| `datasource` |  `String` |(Optional) data source key (Set to `null` if none)  | `"abc123"` |

### `setDatasource() `  

Sets the data source key. Set to `null` if none.

```java
tealium.setEnvironment(datasource);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `datasource` | `String` | Data source key (Set to `null` if none)  |  `"abc123"` |

### `setEnvironment()`   

Sets the Tealium environment name

```java
tealium.setEnvironment(environment);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `environment` | `String` |Tealium environment name |  [`"dev"`, `"qa"`, `"prod"`] |


### `setPersistentData()`   

Sets the persistent data.

```java
tealium.setPersistentData(persistentData);
```

| Parameters | Type | Description |  Example |
| --- | --- | --- | --- |
| `persistentData` | `PersistentUdo` | Persistent Udo data object | `persistentUdoObj` |
