---
title: User Location and Geofencing
description: Learn about the location tracking and geofencing features for mobile.
url: https://docs.tealium.com/platforms/getting-started-mobile/location/
---
## Supported Platforms

The following platforms support location tracking and geofencing:

- [Android](/platforms/android-java/module-list/location/)
- [iOS](/platforms/ios-swift/module-list/location/)

## Location Tracking

Location tracking is the ability to identify the geographic location (latitude and longitude) of a user&#39;s device.  Permission must be granted to your app to allow for location tracking.

Location updates can be provided continuously, which results in higher accuracy, but requires more battery consumption.

If continuous tracking is disabled or not available, the user&#39;s last known location can be retrieved with an explicit method call. This approach uses less battery and can be used in apps that do not require real-time location monitoring.

The following variables are added to the data layer for each location tracking call:

| Variable Name | Type | Description | Example             |
|---------------|-----|-------------|----------------------|
| `latitude`     | `String` | The latitude of the user&#39;s most recently recorded location | `&#34;32.9072&#34;` |
| `longitude`    | `String` | The longitude of the user&#39;s most recently recorded location | `&#34;-117.2367&#34;` |
| `location_accuracy` | `String` | The accuracy setting, such as `&#34;high&#34;` or `&#34;low&#34;` | `&#34;high&#34;`|

## Geofencing

Geofencing is a location tracking service that combines awareness of the user&#39;s location with the user&#39;s proximity to a _geofence_. A geofence is a virtual perimeter surrounding an area of interest, specified by latitude, longitude, and a radius.

Geofencing uses three transition states to track a user&#39;s interaction with a geofence. These transition states trigger tracking calls in the Tealium library. The following transition states are monitored:

| Transition       | Tealium Event             | Description |
|------------------|-------------------------------------| --- |
| Geofence entered | `tealium_event=&#34;geofence_entered&#34;`  | The user entered a geofence |
| Geofence exited | `tealium_event=&#34;geofence_exited&#34;`  | The user exited a geofence |
| Dwelled | `tealium_event=&#34;geofence_dwell&#34;` (Android only)  | The user stops for a defined duration within a geofence |

The specifics of your geofencing is defined in a [geofences file](#file-format) and provided to your app during initialization.

The following variables are tracked during geofencing transition states:

| Variable Name | Type | Description | Example             |
|----------------------------|----------|-------------|----------------------|
| `tealium_event`            | `String` |  The Tealium tracked geofence event: `&#34;geofence_entered&#34;`, `&#34;geofence_exited&#34;`, or `&#34;geofence_dwell&#34;` (Android only) | `&#34;geofence_entered&#34;` |
| `geofence_name`            | `String` | The name of the geofence region | `&#34;Tealium San Diego&#34;` |
| `geofence_transition_type` | `String` | The type of geofence transition event | `&#34;geofence_entered&#34;`, `&#34;geofence_exited&#34;`, or `&#34;geofence_dwell&#34;`(Android) |
| `movement_speed`  (iOS only)         | `String` | The instantaneous speed of the user, measured in meters per second | `&#34;1.0&#34;` |
| `location_timestamp` (iOS only)     | `String` | The recorded date/time (GMT) the user entered/exited the geofence region | `&#34;2020-01-28 16:29:46 &#43;0000&#34;`|

## Geofence File

Geofencing is enabled when a geofence file is provided during app initialization. A geofence file contains coordinates of points of interest and which transition states to track in JSON format.

There are two options when providing the geofences file: a local file or a hosted URL.   

### File Format

When creating your geofence file, name the file `geofences.json`. Geofences are written as key-value pairs with the variables listed in the table below.

 ```json
[{
  &#34;name&#34;: &#34;Geofence_Name&#34;,
  &#34;latitude&#34;: 0.000,
  &#34;longitude&#34;: 0.000,
  &#34;radius&#34;: 100,
  &#34;expire_after&#34;: -1,
  &#34;trigger_on_enter&#34;: true,
  &#34;trigger_on_exit&#34;: false,
  &#34;minimum_dwell_time&#34;: 0 },
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
| `radius` | `Number` | The geofence radius value, in meters. Recommended value: `100`&#43;   | `100` |
| `expire_after` | `Number` | The time, in milliseconds, that the geofence expires after. (Set to -1 to not expire) | `-1` |
| `trigger_on_enter` | `Boolean` | Defines whether the geofence fires a tracking event when a user enters the area. | `true` |
| `trigger_on_exit` | `Boolean` | Defines whether the geofence fires a tracking event when a user exits the area.| `true` |
| `minimum_dwell_time` | `Number` | The time, in milliseconds, a tracking event is fired when a user enters and stays in the geofence. Recommended for most use cases to avoid events repeatedly firing if a user keeps entering and exiting a geofence. (Set to `0` if `trigger_on_enter` is set to `true`)  | `0` |
