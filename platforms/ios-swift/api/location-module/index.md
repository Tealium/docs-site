---
title: LocationModule
description: Reference guide for LocationModule class and methods provided by Tealium for iOS (Swift).
url: https://docs.tealium.com/platforms/ios-swift/api/location-module/
---
## Class: LocationModule

The `LocationModule` class provides methods for gathering location data, creating and monitoring geofences. The following summarizes methods of the `LocationModule` class for Tealium iOS (Swift) which can be used to make custom changes to the default behavior of the Location Module. For additional details, explore [Location](https://docs.tealium.com/platforms/ios-swift/module-list/location/).

| Method | Description |
| ----- | ------ |
| [`clearMonitoredGeofences()`](#clearmonitoredgeofences) | Removes all currently monitored geofences from the location client |
| [`getCreatedGeofences()`](#getcreatedgeofences) | Returns the names of all the created geofences (those currently being monitored and those that are not) |
| [`getLastLocation()`](#getlastlocation) | Gets the last known location for a user's device |
| [`getMonitoredGeofences()`](#getmonitoredgeofences) | Returns the names of all currently monitored geofences |
| [`requestAuthorization()`](#requestauthorization) | Prompts the user to enable permission for location servies |
| [`requestTemporaryFullAccuracyAuthorization()`](#requesttemporaryfullaccuracyauthorization) | Automatically requests temporary full accuracy if precise accuracy is disabled |
| [`startLocationUpdates()`](#startlocationupdates) | Enables regular updates of location data through the location client |
| [`stopLocationUpdates()`](#stoplocationupdates) | Stops the updating of location data through the location client |
| [`startMonitoring()`](#startmonitoring) | Adds geofences to the location client to be monitored |
| [`stopMonitoring()`](#stopmonitoring) | Removes geofences from being monitored by the location client |


### `clearMonitoredGeofences()`

Removes all currently monitored geofences from the location client.

```swift
tealium.location?.clearMonitoredGeofences()
```


### `getCreatedGeofences()`

Returns the names of all the created geofences (those currently being monitored and those that are not).

```swift
tealium.location?.getCreatedGeofences(completion: { createdGeofences in
            if let createdGeofences = createdGeofences {
                // use geofences here
            }
        })
```


### `getLastLocation()`

Gets the last known location for a user's device.

```swift
tealium.location?.getLastLocation(completion: { lastLocation in
            if let lastLocation = lastLocation {
                // use last location here
            }
        })
```

### `getMonitoredGeofences()`

Returns the names of all currently monitored geofences.

```swift
tealium.location?.getMonitoredGeofences(completion: { monitoredGeofences in
            if let monitoredGeofences = monitoredGeofences {
                // use monitored geofences here
            }
        })
```

### `requestAuthorization()`

Prompts the user to enable permission for location servies.

```swift
tealium.location?.requestAuthorization()
```

### `requestTemporaryFullAccuracyAuthorization()`

Automatically requests temporary full accuracy if precise accuracy is disabled.

```swift
let purposeKey = "a key in the NSLocationTemporaryUsageDescriptionDictionary"
tealium.location?.requestTemporaryFullAccuracyAuthorization(purposeKey: purposeKey)
```

| Parameters    | Type     | Description                               |
|:--------------|:---------|:------------------------------------------|
| `purposeKey`  | `String` | A key in the `NSLocationTemporaryUsageDescriptionDictionary` dictionary of the app’s `Info.plist` file |


### `startLocationUpdates()`

Enables regular updates of location data through the location client. Update frequency is dependent on `config.useHighAccuracy`, a parameter passed on initialization of this class.

```swift
tealium.location?.startLocationUpdates()
```

### `stopLocationUpdates()`

Stops the updating of location data through the location client.

```swift
tealium.location?.stopLocationUpdates()
```

### `startMonitoring()`

Adds geofences to the location client to be monitored.

```swift
let myGeofences = [CLCircularRegion]() // Store your self-managed geofences somewhere if you want to stop them later
tealium.location?.startMonitoring(geofences: myGeofences)
```

| Parameters    | Type     | Description                          |
|:--------------|:---------|:-------------------------------------|
| `geofences`  | `[CLCircularRegion]()` | Geofences to be added |


### `stopMonitoring()`

Removes geofences from being monitored by the location client.

```swift
tealium.location?.stopMonitoring(geofences: myGeofences)
```

| Parameters    | Type     | Description                          |
|:--------------|:---------|:-------------------------------------|
| `geofences`  | `[CLCircularRegion]()` | Geofences to be removed |