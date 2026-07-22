---
title: Data Layer
description: Learn about managing common data layer values and the data provided by each module.
url: https://docs.tealium.com/platforms/android-kotlin/data-layer/
---
## Custom Data

It's common to need general data layer values on every event. To avoid having to add these values to every tracking call, use the `tealium.dataLayer` methods to persist data layer values that apply to all tracking calls. Once values are stored, they are automatically included in every tracked event.


<blockquote>
Methods provided by `tealium.dataLayer` are able to read and write custom values, but do not have access to [module data](#module-data).
</blockquote>


### Set and Get Values

There are several utility methods for setting, getting, and deleting values in the data layer. The methods to set and get custom data layer values are typed, however an untyped method is available if you don’t know the type of the variable stored in the data layer.

For example, to set a string value call [`putString()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#putstring):  
```java
tealium.dataLayer.putString("my_string", "my_string_value")
```
To get a value without the type specified, call [`get()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#get):  

```java
tealium.dataLayer.get("my_string")
```

### Data Types

The data layer supports the following data types:

* `Boolean`
* `String`
* `Integer`
* `Long`
* `Double`
* `JSONObject`
* `JSONArray`
* `Array<Boolean>`
* `Array<String>`
* `Array<Integer>`
* `Array<Long>`
* `Array<Double>`

To set a long number value call [`putLong()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#putlong):  
```java
val launchTime = System.currentTimeMillis()
tealium.dataLayer.putLong("launch_time", launchTime)
```

To set an array of strings call [`putStringArray()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#putstringarray):  
```java
val lastThreeProductsViewed = arrayOf("SKU-1", "SKU-2", "SKU-3")
tealium.dataLayer.putStringArray("last_three_products", lastThreeProductsViewed)
```

### Data Expiration

Data layer values have an expiration and are removed from the data layer when they expire. When you set a custom data layer value you can optionally set the expiration time for the value. The default expiration length is the current session.

The following expiration types are available:

| Type | Value | Description |
| :-- | :-- | :-- |
| Session (default) | `Expiry.SESSION` | Expires at the end of the current session |
| Forever  | `Expiry.FOREVER` | Never expires while the app is installed |
| Custom Duration | `Expiry.afterTimeUnit(time, units)` | Expires after the duration specified by the following time units: `NANOSECONDS`, `MICROSECONDS`, `MILLISECONDS`, `SECONDS`, `MINUTES`, `HOURS`, `DAYS` |

#### Session Data

Session data values are persisted for the session. A session is determined by user activity within a given time frame. The session expires after 30 minutes of user inactivity.

For example, to set a value to never expire:  
```java
val userId = "my_id"
tealium.dataLayer.putString("user_id", userId, Expiry.FOREVER)
```

To explicitly set a value to expire at the end of the current session (the default behavior):  
```java
val sessionProductViews = 10
tealium.dataLayer.putInt("product_views", sessionProductViews, Expiry.SESSION)
```

To set a value to expire after one day:  
```java
val frequentVisitor = tealium.dataLayer.getBoolean("frequent_visitor") ?: false

tealium.dataLayer.putBoolean("frequent_visitor",
        frequentVisitor,
        Expiry.afterTimeUnit(1, TimeUnit.DAYS))
```

### Examples

For a full list of available methods see [Class: DataLayer](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/).

To check if the data layer contains a variable call [`contains()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#contains):

```java
tealium.dataLayer.contains("my_string")
```

To delete a value call [`remove()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#remove):  
```java
tealium.dataLayer.remove("my_string")
```

To list all key names in the data layer call [`keys()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#keys):  

```java
tealium.dataLayer.keys()
```

To get the number of variables in the data layer, call [`count()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#count):  
```java
tealium.dataLayer.count()
```

To get the expiry time of a variable call [`getExpiry()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#getexpiry):  
```java
tealium.dataLayer.getExpiry("my_string")
```

To retrieve all data layer variables call [`all()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#all), which returns a `mapOf()`:  
```java
tealium.dataLayer.all()
```

To delete all data layer variables call [`clear()`](https://docs.tealium.com/platforms/android-kotlin/api/data-layer/#clear):  
```java
tealium.dataLayer.clear()
```

## Module Data

### Ad Identifier

The following variables are added to the data layer by the [Ad Identifier](https://docs.tealium.com/platforms/android-kotlin/module-list/adid/).

| Variable | Type | Description | Example |
| --- | --- | --- | --- |     
| `google_adid` | `String` | The Google Ad Identifier | `ca-app-pub-0123456789012345~0123456789` |
| `google_limit_ad_tracking` | `Boolean` | Is `true` if limit ad tracking is enabled on the device, or `false` otherwise  | `true` |

### App Collector

The following variables are added to the data layer by the [App Collector](https://docs.tealium.com/platforms/android-kotlin/module-list/collectors/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `app_build` | App build version | `1`|
| `app_name` | Application name (from the [application manifest attribute `android:label`](https://developer.android.com/guide/topics/manifest/application-element.html#label)) | `My App`|
| `app_memory_usage` | Memory (MB) in use by app process | `57` |
| `app_rdns` | Reverse DNS application ID (from the [root manifest attribute `package`](https://developer.android.com/guide/topics/manifest/manifest-element.html)) | `com.example.myapp` |
| `app_uuid` | Random `uuid`. Persists for the duration of the app install, so long as one of the persistent storage modules is also enabled. Resets if app is uninstalled. | `123e4567-e89b-12d3-a456-556642440000`|
| `app_version` | Application version | `version 1.0`|

### Connectivity Collector

The following variables are added to the data layer by the [Connectivity Collector](https://docs.tealium.com/platforms/android-kotlin/module-list/collectors/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `carrier`                    | Mobile network carrier name| `EE`|
| `carrier_iso`                | Mobile carrier ISO| `gb`|
| `carrier_mcc`                | Carrier mobile country code| `234`|
| `carrier_mnc`                | Carrier mobile network code| `34`|
| `connection_type`            | Current connection type| `wifi`, `cellular`|

### Crash Reporter

The following variables are added to the data layer by the [Crash Reporter](https://docs.tealium.com/platforms/android-kotlin/module-list/crash-reporter/).

| Variable | Type | Description | Example |
| --- | --- | --- | --- |
| `crash_cause` | `String` | The exception type | `java.lang.RuntimeException` |
| `crash_count` | `Number` | An incremented counter for each crash since install | `1` |
| `crash_name` | `String` | The exception message |`"Connection refused by server"` |
| `crash_threads` | `[String]` | Array of JSON strings  containing data of the crashed thread, including the thread ID and stack trace| ` ['{ "crashed": "true", "state": "RUNNABLE", "threadNumber": "1", "threadId": "main", "priority": "5", "stack":  [ { "fileName": "MainActivity.java", "className": "com.tealium.libraryproject.MainActivity$1", "methodName": "onClick", "lineNumber": "38" }] }']` |
| `crash_uuid` | `String` | 16-character unique ID for each crash event | `3c91d707-949e-445f-8ad1-4d6e200bfd6f` |

### Device Collector

The following variables are added to the data layer by the [Device Collector](https://docs.tealium.com/platforms/android-kotlin/module-list/collectors/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `device` | Device type | `Samsung G955f` |
| `device_android_runtime` | Android Runtime version | `2.1.0` |
| `device_available_external_storage` | Total available external storage on device (in bytes) | `273772544`|
| `device_available_system_storage` | Total available storage on device |`273772544` |
| `device_architecture` | Bit architecture of the device | `64` |
| `device_battery_percent` | Integer percent representation of device's remaining power | `50` |
| `device_cputype` | CPU type | `i686` |
| `device_free_external_storage` | Total available external storage on device (in bytes) | `273772544`|
| `device_free_system_storage` | Total available storage on device |`273772544` |
| `device_ischarging` | Is the device actively charging? | `true`, `false` |
| `device_language` | Current device language | `en-US` |
| `device_logical_resolution` | Logical screen resolution in points (width x height) | `414x896` |
| `device_orientation` | Orientation of device at time of call | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown` |
| `device_os_build` | Operating System build version | `4499259` |
| `device_os_version` | Operating System version on device | `7.0` |
| `device_resolution` | Display resolution size in pixels | `1920x1080` |
| `origin` | Constant used in mapping to distinguish mobile from web implementations | `mobile` |
| `platform` | Mobile platform | `Android` |

### Core

The following variables are added to the data layer by the `Core Library`.

| Variable Name | Description | Example |
| --- | --- | --- |
| `tealium_event` | The name of the event being tracked| `cart_add`|
| `tealium_event_type` | String to indicate which event type is being dispatched | `view` or `event` |
| `tealium_library_name` | The name of the Tealium library your app has installed | `android-kotlin` |
| `tealium_library_version` | The version of the Tealium library your app has installed | `1.2` |

### Lifecycle Module

The following variables are added to the data layer by the [Lifecycle Module](https://docs.tealium.com/platforms/android-kotlin/module-list/lifecycle-tracking/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `lifecycle_dayofweek_local` | Local day of week that call was made, such as 1=Sunday, 2=Monday| `4` |
| `lifecycle_dayssincelastwake` | Days since last detected wake in integer increments| `1` |
| `lifecycle_dayssincelaunch` | Days since first launch in integer increments| `23` |
| `lifecycle_dayssinceupdate` | Days since the last detected app version update in integer increments| `46` |
| `lifecycle_diddetect_crash` | Was a crash detected during this launch/wake event (populated only if `true`)| `true` |
| `lifecycle_firstlaunchdate` | GMT timestamp of the first detected launch/wake in ISO 8601 format from UTC | `2013-07-11T17:55:04Z` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | GMT Timestamp formatted as MM/DD/YYYY| `01/17/2012 `|
| `lifecycle_hourofday_local` | Local hour of day that call was made (24 hour format)| `true` |
| `lifecycle_isfirstlaunch` | Only present if call is the first launch/wake call| `true` |
| `lifecycle_isfirstlaunchupdate` | Only present if call is first launch/wake after a detected updated| `true`, `false` |
| `lifecycle_isfirstwakemonth` | Only present if call is first launch/wake of the month| `true` |
| `lifecycle_isfirstwaketoday` | Only present if call is first launch/wake of the day| `true` |
| `lifecycle_launchcount` | Total number of launches this version of your app (since the last update)| `3` |
| `lifecycle_priorsecondsawake` | Whole seconds app was awake since last launch only. Aggregates total from all wakes prior. Sent only with `lifecycle_type:launch` calls.| `126` |
| `lifecycle_secondsawake` | Whole seconds app was awake since most recent wake/launch| `30` |
| `lifecycle_sleepcount` | Total number of times your app has gone to sleep (resets if updated)| `5` |
| `lifecycle_totalcrashcount` | Total number of crashes counted since install (only reset if app deleted)| `21` |
| `lifecycle_totallaunchcount` | Total number of launches since install (only reset if app deleted)| `3` |
| `lifecycle_totalsecondsawake` | Total number of seconds your app has been in a woken/active state since app install (only reset if app deleted)| `36` |
| `lifecycle_totalsleepcount` | Total number of times your app has gone into the background since app install (only reset if app deleted)| `400` |
| `lifecycle_totalwakecount` | Total number of launches + wakes since install (only reset if app deleted)| `563` |
| `lifecycle_type` | Type of lifecycle call.| `launch`, `wake`, `sleep`|
| `lifecycle_updatelaunchdate` | GMT timestamp of first wake/launch after a version update has been detected| `2014-09-08T18:10:01Z` |
| `lifecycle_wakecount` | Total number of launches + wakes in this version of your app (resets if updated)| `29` |


### Location Collector

The following variables are added to the data layer by the [Location Collector](https://docs.tealium.com/platforms/android-kotlin/module-list/location/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `latitude`     | The latitude of the user's most recently recorded location | `32.906119` |
| `longitude`    | The longitude of the user's most recently recorded location | `-117.2367` |
| `location_accuracy` | The accuracy setting for the location module | `high`, `low`|
| `tealium_event`            |  The Tealium tracked geofence event | `geofence_entered`, `geofence_exited`, `geofence_dwell` |
| `geofence_name`            |  The name of the geofence region | `Tealium_San_Diego` |
| `geofence_transition_type` |  The type of geofence transition event | `geofence_entered`, `geofence_exited`, `geofence_dwell` |

### Tealium Collector

The following variables are added to the data layer by the [Tealium Collector](https://docs.tealium.com/platforms/android-kotlin/module-list/collectors/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `tealium_account` | Tealium account name from `TealiumConfig` | `tealium` |
| `tealium_profile` | Tealium profile name from `TealiumConfig` | `mobile` |
| `tealium_environment` | Tealium environment from `TealiumConfig` | `dev` |
| `tealium_datasource` | Identifies Tealium data source name from `TealiumConfig` | `abc123` |
| `tealium_visitor_id` | Tealium visitor ID | `t3aL...1uM` |
| `tealium_random` | A random number for each event | `1234567890` |
| `was_queued` | Indicates whether this event was ever queued on the device | `true` |

### Time Collector

The following variables are added to the data layer by the [Time Collector](https://docs.tealium.com/platforms/android-kotlin/module-list/collectors/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `timestamp` | Timestamp to seconds of event occurrence [ISO 8601 at UTC] | `2013-07-11T19:57:47Z` |
| `timestamp_local` | Local Timestamp to seconds of event occurrence (ISO 8601 without offset) | `2013-07-11T19:57:47` |
| `timestamp_offset` | Local timezone offset of device's location in hours | `-3` |
| `timestamp_unix` | GMT/UTC Unix timestamp of event occurrence |`1373498679` |
| `timestamp_unix_milliseconds` | GMT/UTC Unix timestamp in milliseconds of event occurrence | `1373498679123` |

### Deprecated

The following data layer variables from [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/data-layer/) were renamed or removed in Tealium for Android (Kotlin).

| Tealium for Android (Java) | Tealium for Android (Kotlin) |
|:---------------|:---------------------|
| `call_type`    | `tealium_event_type` |
| `event_name`   | `tealium_event`      |
| `link_id`      | `tealium_event`      |
| `orientation`  | `device_orientation` |
| `os_version`   | `device_os_version`  |
| `page_type`    | (not included)       |
| `tealium_vid`  | `tealium_visitor_id` |
| `uuid`         | `app_uuid`           |
| `visitor_id`   | `tealium_visitor_id` |
