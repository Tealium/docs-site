---
title: TealiumDataLayer
description: Reference guide for DataLayer class and methods provided by Tealium for iOS (Swift).
url: https://docs.tealium.com/platforms/ios-swift/api/tealium-data-layer/
---
## Class: `DataLayer`

The following summarizes the commonly used methods and properties of the iOS (Swift) `DataLayer` class.

| Method/Property | Description |
| ----- | ------ |
| [`add()`](#add) | Adds data to the data layer, based on expiration type. |
| [`all`](#all) | Returns all data stored on the data layer. |
| [`allSessionData`](#allsessiondata) | Returns all data stored on the data layer for the active session. |
| [`delete()`](#delete) | Deletes the specified values from storage. |
| [`deleteAll()`](#deleteall) | Deletes all values from storage. |
| [`persistentDataStorage`](#persistentdatastorage) | Returns all event data stored in persistent storage. |

### `add()`

Adds data to the data layer, based on [expiration type](https://docs.tealium.com/platforms/ios-swift/data-layer/#data-expiration).  If the `expiry` parameter is not provided, the expiration type defaults to` .session`.

```swift
tealium?.dataLayer.add(key, value, expiry)
```

| Parameter             | Type     | Description               |
|-----------------------|----------|---------------------------|
| `key`                 | `String` | Name of key to be stored  |
| `value`               | `Any`    | Data to be stored         |
| `expiry` (Optional)   | `Expiry` | Data expiration level     |

### `all`

Returns all data stored on the data layer.

```swift
let data: [String: Any] = tealium?.dataLayer.all
```

| Return Type | Description                       |
|-------------|-----------------------------------|
| `[String]`  | All data stored on the data layer |


### `allSessionData`

Returns all data stored on the data layer for the active session.

```swift
let data: [String: Any] = tealium?.dataLayer.allSessionData
```

| Return Type | Description                       |
|-------------|-----------------------------------|
| `[String]`  | All data stored on the data layer for the active session |


### `delete()`

Deletes specified value from storage based on a specific key.

```swift
tealium?.dataLayer.delete(for key)
```

| Parameter | Type                   | Description                               |
|-----------|------------------------|-------------------------------------------|
| `key` | `String` | Key of value to delete |

To delete multiple values from storage based on multiple keys:

```swift
tealium?.dataLayer.delete(for keys)
```

| Parameter | Type                   | Description                               |
|-----------|------------------------|-------------------------------------------|
| `keys` | `[String]` | Keys of values to delete |


### `deleteAll()`

Deletes all values from storage.

```swift
tealium?.dataLayer.deleteAll()
```

### `persistentDataStorage`

Returns all event data stored in persistent storage.

```swift
let data: Set<DataLayerItem> = tealium?.dataLayer.persistentDataStorage
```

| Return Type | Description                       |
|-------------|-----------------------------------|
| `Set<DataLayerItem>`  | All event data stored in persistent storage |
