---
title: TealiumVolatileData
description: Provides methods for accessing volatile data.
url: https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-volatile-data/
---
## Class: `TealiumVolatileData`


The following summarizes the commonly used methods of the iOS (Swift) `TealiumVolatileData` class.

| Method | Description |
| ----- | ------ |
| `add()` | Add data to all dispatches for the remainder of an active session |
| `deleteAllData()` | Deletes all data in the volatile data store |
| `deleteData()` | Deletes data for a specific set of known keys from the volatile data store |
| `getData()` | Returns all volatile data previously set with the `add()` method |
| `resetSessionId()` | Reset the session ID for current session |
| `setSessionId()` | Override the existing session ID for current session |

### `add()`

Add data to all dispatches for the remainder of an active session.

```swift
tealium?.volatileData()?.add(data)
```

| Parameter  | Type       | Description       | Example |
|------------  |-----------|-------------------| --- |
| `data`| `[String: Any]`  | Dictionary of data to add as key-value pairs | `data: [&#34;session_id&#34;:&#34;1234567890232&#34;]` |  

### `deleteAllData()`

Deletes all data in the volatile data store.

```swift
tealium?.volatileData()?.deleteAllData()
```


### `deleteData()`

Deletes data for a specific set of known keys from the volatile data store.

```swift
tealium?.volatileData()?.deleteData(forKeys)
```

| Parameter  | Type       | Description       | Example |
|------------  |-----------|-------------------| --- |
| `forKeys`| `[String]`  | Array of keys to remove from the internal volatile data store | `forKeys: [&#34;a&#34;, &#34;b&#34;]` |  


### `getData()`

Returns all volatile data previously set with the `add()` method.

```swift
let data = tealium?.volatileData()?.getData()
```

| Returns | Return Type |
| ------- | ----------- |
| Volatile data as key-value pairs | `[String:Any]` |

### `resetSessionId()`
Reset the session ID for current session.

```swift
tealium?.volatileData()?.resetSessionId()
```


### `setSessionId()`
Override the existing session ID for current session.

```swift
tealium?.volatileData()?.setSessionId(sessionId)
```

| Parameters | Type | Description                      | Example              |
|------------|-----|-----------------------------|---------------------------|
| `sessionId`  | `String` | Override the session ID for the current session | `&#34;123456123456009&#34;` |
