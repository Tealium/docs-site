---
title: TealiumPersistentData
description: Provides methods for accessing persistent data.
url: https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-persistent-data/
---
## Class: `TealiumPersistentData`


The following summarizes the commonly used methods of the iOS (Swift) `TealiumPersistentData` class.

| Method | Description |
| ----- | ------ |
| `add()` | Adds additional persistent data that will be available to all track calls for lifetime of app. Values will overwrite any pre-existing values for a given ke |
| `deleteAllData()` | Deletes all data in the persistent data store |
| `deleteData()` | Deletes data for a specific set of known keys from the persistent data store |
| `getData()` | Gets data from the persistent data store |


### `add()`

Adds additional persistent data that will be available to all track calls for lifetime of app. Values will overwrite any pre-existing values for a given key.

```swift
tealium?.persistentData()?.add(data: [String: Any])
```

| Parameter  | Type       | Description       | Example |
|------------  |-----------|-------------------| --- |
| `Any`| `[String: Any]`  | Dictionary of data to add | `data: ["customer_id":"1234567890-a"]` |  


### `deleteAllData()`

Deletes all data in the persistent data store.

```swift
tealium?.persistentData()?.deleteAllData()
```


### `deleteData()`

Deletes data for a specific set of known keys from the persistent data store.

```swift
tealium?.persistentData()?.deleteDate(forKeys: [String])
```

| Parameter  | Type       | Description       | Example |
|------------  |-----------|-------------------| --- |
| `forKeys`| `[String]`  | Array of keys to remove | `forKeys: ["customer_id"]` |  


### `getData()`

Gets data from the persistent data store.

```swift
let data = tealium?.persistentData()?.getData()
```
