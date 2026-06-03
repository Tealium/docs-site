---
title: TealiumLocation
description: Reference guide for TealiumLocation class and methods provided by Tealium for Android.
url: https://docs.tealium.com/platforms/android-java/api/tealium-location/
---

## Class: `TealiumLocation`

The following summarizes the commonly used methods of the `TealiumLocation` class.

| Method | Description |
| ----- | ------ |
| `requestDeviceLastLocation()` | Returns the last known location of a user&#39;s device |
| `setupInstance()` | Sets the Tealium geolocation instance with geofencing disabled |
| `setupInstanceWithConfig()` | Sets the Tealium geolocation instance with geofences provided from a Tealium Config file (hosted with Tealium&#39;s hosted data layer) |
| `setupInstanceWithFile()` | Sets the Tealium geolocation instance with geofences provided from a JSON file in assets |
| `setupInstanceWithUrl()` | Sets the Tealium geolocation instance with geofences provided from a URL hosting a raw JSON file |
| `startLocationUpdates()` | Sets the accuracy of location updates and the update interval time for continuous tracking |
| `stopLocationUpdates()` | Stops/disables continuous location tracking updates |


### `requestDeviceLastLocation()`

Returns the last known location of a user&#39;s device. This method relies on the location client being used by other apps on the device for accuracy. If no other apps are receiving location updates, then the method returns the last known location. Returns `null` if a location is not available.

```java
TealiumLocation.getInstance().requestDeviceLastLocation();
```

### `setupInstance()`

Sets the Tealium geolocation instance with geofencing disabled.

```java
TealiumLocation.setupInstance(applicationContext, tealiumInstances);
```

### `setupInstanceWithConfig()`

Sets the Tealium geolocation instance with geofences provided from a Tealium Config file (hosted with Tealium&#39;s hosted data layer). It creates a custom URL in the following format: `&#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/geofences.json&#34;`.

```java
TealiumLocation.setupInstanceWithConfig(this, tealiumInstances, mTealiumConfig);
```  

### `setupInstanceWithFile()`

Sets the Tealium geolocation instance with geofences provided from a JSON file in assets.

```java
TealiumLocation.setupInstanceWithFile(this, tealiumInstances, &#34;geofences.json&#34;);
```

### `setupInstanceWithUrl()`

Sets the Tealium geolocation instance with geofences provided from a URL hosting a raw JSON file. This option is recommended if you have overridden the publish settings URL.

```java
TealiumLocation.setupInstanceWithUrl(this, tealiumInstances, url);
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `url` | `String` | The URL pointing to your hosted JSON file, such as `geofences.json` | `&#34;https://DOMAIN/PATH/FILE.json&#34;` |


### `startLocationUpdates()`

Sets the accuracy of location updates and the update interval time for continuous tracking. Enabling pin-point location accuracy and frequent updates provides higher accuracy, but at the cost of more battery consumption. Enabling &#34;block&#34; accuracy requests location precision to within a city block, which is an accuracy of approximately 100 meters.

```java
TealiumLocation.getInstance().startLocationUpdates(isHighAccuracy, updateInterval);
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `isHighAccuracy` | `boolean` |Set to `true` for pin-point location accuracy, or `false` for &#34;block&#34; accuracy. | `true` |
| `updateInterval` | `double` | Time (ms) that location updates are retrieved. Recommended value: `10000` ms (10 seconds) | `10000` |

### `stopLocationUpdates()`

Disables continuous location tracking updates.

```java
TealiumLocation.getInstance().stopLocationUpdates();
```
