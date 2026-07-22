---
title: LocationManager
description: Reference guide for LocationManager class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/location-manager/
---
## Class: LocationManager

The `LocationManager` class provides methods for gathering location data, creating and monitoring geofences. The following summarizes the commonly used methods of the `LocationManager` class for Tealium Kotlin. For additional details, see the [Location module](https://docs.tealium.com/platforms/android-kotlin/module-list/location/).

| Method | Description |
| ----- | ------ |
| [`addGeofence()`](#addgeofence) | Creates and adds a new `GeofenceLocation` to allGeofenceLocations. |
| [`allGeofenceNames()`](#allgeofencenames) | Returns a list of all `GeofenceLocation` names. |
| [`lastLocation()`](#lastlocation) | Returns last known location result for user's device. |
| [`lastLocationLatitude()`](#lastlocationlatitude) | Returns latitude for last location result. |
| [`lastLocationLongitude()`](#lastlocationlongitude) | Returns longitude for last location result. |
| [`startLocationTracking()`](#startlocationtracking) | Starts location tracking based on the accuracy and interval updates you want. |
| [`stopLocationTracking()`](#stoplocationtracking) | Stops location tracking updates.  |

### `addGeofence()`

Provides to ability to manually create and add geofences for monitoring.

```java
tealiumInstance.location?.addGeofence(
							"Tealium-HQ",
							45.0, // latitude
							100.0, // longitude
							100, // radius
							-1, // expiry duration
							0, // loiter duration
							true, // events triggered on entry of geofence
							true) // events triggered on exit of geofence
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Name of location | `"Tealium-HQ"` |
| `latitude` | `Double` | Latitude of location | `45.0` |
| `longitude` | `Double` | Longitude of location | `100.0` |
| `radius` | `Int` | Radius in meters of geofence | `100` |
| `expireTime` | `Int` | Sets expiration duration in milliseconds for geofence | `-1` |
| `loiterTime` | `Int` | Sets duration in milliseconds for time delay between entering and dwelling a geofence | `0` |
| `triggerEnter` | `Boolean` | Enables events being triggered upon entering a geofence  | `true` |
| `triggerExit` | `Boolean` | Enables events being triggered upon exiting a geofence | `true` |

### `allGeofenceNames()`

Returns a list of all geofence names to be observed.

```java
tealiumInstance.location?.allGeofenceNames()
```

### `lastLocation()`

Returns most recent location recorded for a user's device or `null` if location is not available.

```java
val location = tealiumInstance.location?.lastLocation()
```

### `lastLocationLatitude()`

Returns the latitude for the most recent location recorded for a user's device.

```java
val latitude = tealiumInstance.location?.lastLocationLatitude()
```

### `lastLocationLongitude()`

Returns the longitude for the most recent location recorded for a user's device.

```java
val longitude = tealiumInstance.location?.lastLocationLongitude()
```

### `startLocationTracking()`

Starts continuous location tracking, as well as sets the accuracy and interval in milliseconds you want for location updates. Enabling precise location and frequent location update intervals may be costly to battery consumption.

```java
tealiumInstance.location?.startLocationTracking(true, 1000)
```
| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `isHighAcuracy` | `Boolean` | Set to 'true' for high precision location tracking, or `false` for accuracy within 100 meters  | `true` |
| `updateInterval` | `Int` | Interval in milliseconds for preferred location update frequency | `10000` |

### `stopLocationTracking()`

Halts continuous location tracking updates.

```java
tealiumInstance.location?.stopLocationTracking()
```
