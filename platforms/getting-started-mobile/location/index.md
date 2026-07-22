---
title: User Location and Geofencing
description: Learn about the location tracking and geofencing features for mobile.
url: https://docs.tealium.com/platforms/getting-started-mobile/location/
---
## Supported Platforms

The following platforms support location tracking and geofencing:

- [Android](https://docs.tealium.com/platforms/android-java/module-list/location/)
- [iOS](https://docs.tealium.com/platforms/ios-swift/module-list/location/)

## Location Tracking

Location tracking is the ability to identify the geographic location (latitude and longitude) of a user's device.  Permission must be granted to your app to allow for location tracking.

Location updates can be provided continuously, which results in higher accuracy, but requires more battery consumption.

If continuous tracking is disabled or not available, the user's last known location can be retrieved with an explicit method call. This approach uses less battery and can be used in apps that do not require real-time location monitoring.

The following variables are added to the data layer for each location tracking call:

| Variable Name | Type | Description | Example             |
|---------------|-----|-------------|----------------------|
| `latitude`     | `String` | The latitude of the user's most recently recorded location | `"32.9072"` |
| `longitude`    | `String` | The longitude of the user's most recently recorded location | `"-117.2367"` |
| `location_accuracy` | `String` | The accuracy setting, such as `"high"` or `"low"` | `"high"`|

## Geofencing

Geofencing is a location tracking service that combines awareness of the user's location with the user's proximity to a _geofence_. A geofence is a virtual perimeter surrounding an area of interest, specified by latitude, longitude, and a radius.

Geofencing uses three transition states to track a user's interaction with a geofence. These transition states trigger tracking calls in the Tealium library. The following transition states are monitored:

| Transition       | Tealium Event             | Description |
|------------------|-------------------------------------| --- |
| Geofence entered | `tealium_event="geofence_entered"`  | The user entered a geofence |
| Geofence exited | `tealium_event="geofence_exited"`  | The user exited a geofence |
| Dwelled | `tealium_event="geofence_dwell"` (Android only)  | The user stops for a defined duration within a geofence |

The specifics of your geofencing is defined in a [geofences file](#file-format) and provided to your app during initialization.

The following variables are tracked during geofencing transition states:

| Variable Name | Type | Description | Example             |
|----------------------------|----------|-------------|----------------------|
| `tealium_event`            | `String` |  The Tealium tracked geofence event: `"geofence_entered"`, `"geofence_exited"`, or `"geofence_dwell"` (Android only) | `"geofence_entered"` |
| `geofence_name`            | `String` | The name of the geofence region | `"Tealium San Diego"` |
| `geofence_transition_type` | `String` | The type of geofence transition event | `"geofence_entered"`, `"geofence_exited"`, or `"geofence_dwell"`(Android) |
| `movement_speed`  (iOS only)         | `String` | The instantaneous speed of the user, measured in meters per second | `"1.0"` |
| `location_timestamp` (iOS only)     | `String` | The recorded date/time (GMT) the user entered/exited the geofence region | `"2020-01-28 16:29:46 +0000"`|

## Geofence File

Geofencing is enabled when a geofence file is provided during app initialization. A geofence file contains coordinates of points of interest and which transition states to track in JSON format.

There are two options when providing the geofences file: a local file or a hosted URL.   

### File Format

When creating your geofence file, name the file `geofences.json`. Geofences are written as key-value pairs with the variables listed in the table below.

 ```json
[{
  "name": "Geofence_Name",
  "latitude": 0.000,
  "longitude": 0.000,
  "radius": 100,
  "expire_after": -1,
  "trigger_on_enter": true,
  "trigger_on_exit": false,
  "minimum_dwell_time": 0 },
 {
    ...
 }]
```

The following properties define each geofence:

| Parameter | Type | Description | Example |
| :-------  | :--- | :---------- | :------ |
| `name` | `String` | The geofence name as a unique string with words separated by underscores. Avoid using spaces, emojis and characters not supported by UTF-8 encoding. | `Geofence_Name` |
| `latitude` | `Number` | The latitude coordinate of the center of the geofence as a decimal value between `-90.0` and `90.0`. | `0.000` |
| `longitude` | `Number` | The longitude coordinate of the center of the geofence as a decimal value between `-180.0` and `180.0`. | `0.000` |
| `radius` | `Number` | The geofence radius value, in meters. Recommended value: `100`+   | `100` |
| `expire_after` | `Number` | The time, in milliseconds, that the geofence expires after. (Set to -1 to not expire) | `-1` |
| `trigger_on_enter` | `Boolean` | Defines whether the geofence fires a tracking event when a user enters the area. | `true` |
| `trigger_on_exit` | `Boolean` | Defines whether the geofence fires a tracking event when a user exits the area.| `true` |
| `minimum_dwell_time` | `Number` | The time, in milliseconds, a tracking event is fired when a user enters and stays in the geofence. Recommended for most use cases to avoid events repeatedly firing if a user keeps entering and exiting a geofence. (Set to `0` if `trigger_on_enter` is set to `true`)  | `0` |
