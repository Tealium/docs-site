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
| `data` | `Map&lt;String, Object&gt;` | Required map data to add to the existing persistent `Udo` | `[&#34;key&#34;:&#34;value&#34;]` |

```java
Udo data = new Udo();
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);
tealium.getDataManager().addPersistentData(data);
```

### `deletePersistentData()`

Use the `DataManager` to delete previously persisted data by providing a list of keys to delete.

```java
deletePersistentData(list)
```

| Parameters |  Type |Description | Example |
| --- | --- | --- | --- |
| `list` |  `List&lt;String&gt;` | List of keys as Strings | `[&#34;key1&#34;, &#34;key2&#34;]` |

```java
List&lt;String&gt; list = new List&lt;&gt;();
list.append(&#34;key_to_delete&#34;);
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
| `Udo` | Universal Data Object (UDO) of persistent data | `[&#34;key1&#34;, &#34;key2&#34;]` |

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
| `String` | Representation of a timestamp in milliseconds | `&#34;1473371215123&#34;` |

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
| `String` | New String representation of a timestamp in milliseconds that is added to all dispatches for the remainder of the current session. The returned String is for monitoring convenience as it is automatically added to the volatile data store when this method is called. | `&#34;1473371215123&#34;` |

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
| `eventTitle` | `String` |Title of event (becomes the `tealium_event` and `event_name` event attribute values) |  `&#34;Some Event&#34;` |
| `data`    | `Udo` |  (Optional) Universal Data Object (UDO) with event data as key-value pairs| `udoObject` |
| `callback`| `DispatchCallback` |(Optional) Object with a function assigned to the &#34;callback&#34; key | `dispatchCallbackObject` |


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

Executes the build. Sets the persistent data if it hasn&#39;t been explicitly set with the `setPersistentData()` method. Sets the collect dispatcher if it hasn&#39;t been explicitly set with the setCollectDispatcher() method.

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
| `account` |  `String` |Tealium account name | `&#34;companyXYZ&#34;` |
| `profile` |  `String` |Tealium profile name  | `&#34;main&#34;` |
| `environment` |  `String` |Tealium environment name  | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `datasource` |  `String` |(Optional) data source key (Set to `null` if none)  | `&#34;abc123&#34;` |

### `setDatasource() `  

Sets the data source key. Set to `null` if none.

```java
tealium.setEnvironment(datasource);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `datasource` | `String` | Data source key (Set to `null` if none)  |  `&#34;abc123&#34;` |

### `setEnvironment()`   

Sets the Tealium environment name

```java
tealium.setEnvironment(environment);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `environment` | `String` |Tealium environment name |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |


### `setPersistentData()`   

Sets the persistent data.

```java
tealium.setPersistentData(persistentData);
```

| Parameters | Type | Description |  Example |
| --- | --- | --- | --- |
| `persistentData` | `PersistentUdo` | Persistent Udo data object | `persistentUdoObj` |
