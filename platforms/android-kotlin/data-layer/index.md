---
title: Data Layer
description: Learn about managing common data layer values and the data provided by each module.
url: https://docs.tealium.com/platforms/android-kotlin/data-layer/
---
## Custom Data

It&#39;s common to need general data layer values on every event. To avoid having to add these values to every tracking call, use the `tealium.dataLayer` methods to persist data layer values that apply to all tracking calls. Once values are stored, they are automatically included in every tracked event.

Methods provided by `tealium.dataLayer` are able to read and write custom values, but do not have access to [module data](#module-data).

### Set and Get Values

There are several utility methods for setting, getting, and deleting values in the data layer. The methods to set and get custom data layer values are typed, however an untyped method is available if you don’t know the type of the variable stored in the data layer.

For example, to set a string value call [`putString()`](/platforms/android-kotlin/api/data-layer/#putstring):  
```java
tealium.dataLayer.putString(&#34;my_string&#34;, &#34;my_string_value&#34;)
```
To get a value without the type specified, call [`get()`](/platforms/android-kotlin/api/data-layer/#get):  

```java
tealium.dataLayer.get(&#34;my_string&#34;)
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
* `Array&lt;Boolean&gt;`
* `Array&lt;String&gt;`
* `Array&lt;Integer&gt;`
* `Array&lt;Long&gt;`
* `Array&lt;Double&gt;`

To set a long number value call [`putLong()`](/platforms/android-kotlin/api/data-layer/#putlong):  
```java
val launchTime = System.currentTimeMillis()
tealium.dataLayer.putLong(&#34;launch_time&#34;, launchTime)
```

To set an array of strings call [`putStringArray()`](/platforms/android-kotlin/api/data-layer/#putstringarray):  
```java
val lastThreeProductsViewed = arrayOf(&#34;SKU-1&#34;, &#34;SKU-2&#34;, &#34;SKU-3&#34;)
tealium.dataLayer.putStringArray(&#34;last_three_products&#34;, lastThreeProductsViewed)
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
val userId = &#34;my_id&#34;
tealium.dataLayer.putString(&#34;user_id&#34;, userId, Expiry.FOREVER)
```

To explicitly set a value to expire at the end of the current session (the default behavior):  
```java
val sessionProductViews = 10
tealium.dataLayer.putInt(&#34;product_views&#34;, sessionProductViews, Expiry.SESSION)
```

To set a value to expire after one day:  
```java
val frequentVisitor = tealium.dataLayer.getBoolean(&#34;frequent_visitor&#34;) ?: false

tealium.dataLayer.putBoolean(&#34;frequent_visitor&#34;,
        frequentVisitor,
        Expiry.afterTimeUnit(1, TimeUnit.DAYS))
```

### Examples

For a full list of available methods see [Class: DataLayer](/platforms/android-kotlin/api/data-layer/).

To check if the data layer contains a variable call [`contains()`](/platforms/android-kotlin/api/data-layer/#contains):

```java
tealium.dataLayer.contains(&#34;my_string&#34;)
```

To delete a value call [`remove()`](/platforms/android-kotlin/api/data-layer/#remove):  
```java
tealium.dataLayer.remove(&#34;my_string&#34;)
```

To list all key names in the data layer call [`keys()`](/platforms/android-kotlin/api/data-layer/#keys):  

```java
tealium.dataLayer.keys()
```

To get the number of variables in the data layer, call [`count()`](/platforms/android-kotlin/api/data-layer/#count):  
```java
tealium.dataLayer.count()
```

To get the expiry time of a variable call [`getExpiry()`](/platforms/android-kotlin/api/data-layer/#getexpiry):  
```java
tealium.dataLayer.getExpiry(&#34;my_string&#34;)
```

To retrieve all data layer variables call [`all()`](/platforms/android-kotlin/api/data-layer/#all), which returns a `mapOf()`:  
```java
tealium.dataLayer.all()
```

To delete all data layer variables call [`clear()`](/platforms/android-kotlin/api/data-layer/#clear):  
```java
tealium.dataLayer.clear()
```

## Module Data

### Ad Identifier

The following variables are added to the data layer by the [Ad Identifier](/platforms/android-kotlin/module-list/adid/).

| Variable | Type | Description | Example |
| --- | --- | --- | --- |     
| `google_adid` | `String` | The Google Ad Identifier | `ca-app-pub-0123456789012345~0123456789` |
| `google_limit_ad_tracking` | `Boolean` | Is `true` if limit ad tracking is enabled on the device, or `false` otherwise  | `true` |

### App Collector

The following variables are added to the data layer by the [App Collector](/platforms/android-kotlin/module-list/collectors/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `app_build` | App build version | `1`|
| `app_name` | Application name (from the [application manifest attribute `android:label`](https://developer.android.com/guide/topics/manifest/application-element.html#label)) | `My App`|
| `app_memory_usage` | Memory (MB) in use by app process | `57` |
| `app_rdns` | Reverse DNS application ID (from the [root manifest attribute `package`](https://developer.android.com/guide/topics/manifest/manifest-element.html)) | `com.example.myapp` |
| `app_uuid` | Random `uuid`. Persists for the duration of the app install, so long as one of the persistent storage modules is also enabled. Resets if app is uninstalled. | `123e4567-e89b-12d3-a456-556642440000`|
| `app_version` | Application version | `version 1.0`|

### Connectivity Collector

The following variables are added to the data layer by the [Connectivity Collector](/platforms/android-kotlin/module-list/collectors/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `carrier`                    | Mobile network carrier name| `EE`|
| `carrier_iso`                | Mobile carrier ISO| `gb`|
| `carrier_mcc`                | Carrier mobile country code| `234`|
| `carrier_mnc`                | Carrier mobile network code| `34`|
| `connection_type`            | Current connection type| `wifi`, `cellular`|

### Crash Reporter

The following variables are added to the data layer by the [Crash Reporter](/platforms/android-kotlin/module-list/crash-reporter/).

| Variable | Type | Description | Example |
| --- | --- | --- | --- |
| `crash_cause` | `String` | The exception type | `java.lang.RuntimeException` |
| `crash_count` | `Number` | An incremented counter for each crash since install | `1` |
| `crash_name` | `String` | The exception message |`&#34;Connection refused by server&#34;` |
| `crash_threads` | `[String]` | Array of JSON strings  containing data of the crashed thread, including the thread ID and stack trace| ` [&#39;{ &#34;crashed&#34;: &#34;true&#34;, &#34;state&#34;: &#34;RUNNABLE&#34;, &#34;threadNumber&#34;: &#34;1&#34;, &#34;threadId&#34;: &#34;main&#34;, &#34;priority&#34;: &#34;5&#34;, &#34;stack&#34;:  [ { &#34;fileName&#34;: &#34;MainActivity.java&#34;, &#34;className&#34;: &#34;com.tealium.libraryproject.MainActivity$1&#34;, &#34;methodName&#34;: &#34;onClick&#34;, &#34;lineNumber&#34;: &#34;38&#34; }] }&#39;]` |
| `crash_uuid` | `String` | 16-character unique ID for each crash event | `3c91d707-949e-445f-8ad1-4d6e200bfd6f` |

### Device Collector

The following variables are added to the data layer by the [Device Collector](/platforms/android-kotlin/module-list/collectors/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `device` | Device type | `Samsung G955f` |
| `device_android_runtime` | Android Runtime version | `2.1.0` |
| `device_available_external_storage` | Total available external storage on device (in bytes) | `273772544`|
| `device_available_system_storage` | Total available storage on device |`273772544` |
| `device_architecture` | Bit architecture of the device | `64` |
| `device_battery_percent` | Integer percent representation of device&#39;s remaining power | `50` |
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

The following variables are added to the data layer by the [Lifecycle Module](/platforms/android-kotlin/module-list/lifecycle-tracking/).

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
| `lifecycle_totalwakecount` | Total number of launches &#43; wakes since install (only reset if app deleted)| `563` |
| `lifecycle_type` | Type of lifecycle call.| `launch`, `wake`, `sleep`|
| `lifecycle_updatelaunchdate` | GMT timestamp of first wake/launch after a version update has been detected| `2014-09-08T18:10:01Z` |
| `lifecycle_wakecount` | Total number of launches &#43; wakes in this version of your app (resets if updated)| `29` |


### Location Collector

The following variables are added to the data layer by the [Location Collector](/platforms/android-kotlin/module-list/location/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `latitude`     | The latitude of the user&#39;s most recently recorded location | `32.906119` |
| `longitude`    | The longitude of the user&#39;s most recently recorded location | `-117.2367` |
| `location_accuracy` | The accuracy setting for the location module | `high`, `low`|
| `tealium_event`            |  The Tealium tracked geofence event | `geofence_entered`, `geofence_exited`, `geofence_dwell` |
| `geofence_name`            |  The name of the geofence region | `Tealium_San_Diego` |
| `geofence_transition_type` |  The type of geofence transition event | `geofence_entered`, `geofence_exited`, `geofence_dwell` |

### Tealium Collector

The following variables are added to the data layer by the [Tealium Collector](/platforms/android-kotlin/module-list/collectors/).

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

The following variables are added to the data layer by the [Time Collector](/platforms/android-kotlin/module-list/collectors/).

| Variable Name | Description | Example |
| --- | --- | --- |
| `timestamp` | Timestamp to seconds of event occurrence [ISO 8601 at UTC] | `2013-07-11T19:57:47Z` |
| `timestamp_local` | Local Timestamp to seconds of event occurrence (ISO 8601 without offset) | `2013-07-11T19:57:47` |
| `timestamp_offset` | Local timezone offset of device&#39;s location in hours | `-3` |
| `timestamp_unix` | GMT/UTC Unix timestamp of event occurrence |`1373498679` |
| `timestamp_unix_milliseconds` | GMT/UTC Unix timestamp in milliseconds of event occurrence | `1373498679123` |

### Deprecated

The following data layer variables from [Tealium for Android (Java)](/platforms/android-java/data-layer/) were renamed or removed in Tealium for Android (Kotlin).

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
