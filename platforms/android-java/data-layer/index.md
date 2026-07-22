---
title: Data Layer
description: Learn about the data layer variables from the Android library.
url: https://docs.tealium.com/platforms/android-java/data-layer/
---The following variables are populated by the Tealium Android Library as part of the mobile data layer. These variables are included automatically in each tracking call from the library and are useable in your Tealium Customer Data Hub configuration.


<blockquote>
These variables are added to your Tealium iQ Tag Management account when you [activate the profile for mobile use](https://docs.tealium.com/creating-a-mobile-profile/).
</blockquote>


Addition variables are available in the [Lifecycle Tracking Module](https://docs.tealium.com/platforms/android/lifecycle-tracking-module/) for 5.0.x.

| Variable Name | Android Version | Description | Example |
| --- | --- | --- | --- |
| `app_build` | 5.4+ | App build version | `1 `|
| `app_name` | 1.1+ | Application name (from the [application manifest attribute `android:label`](https://developer.android.com/guide/topics/manifest/application-element.html#label)) | `My App`|
| `app_memory_usage` | 5.4+ | Memory (MB) in use by app process | `57` |
| `app_rdns` | 3.0+ | Reverse DNS application ID (from the [root manifest attribute `package`](https://developer.android.com/guide/topics/manifest/manifest-element.html)) | `com.example.myapp` |
| `app_version` | 1.1+ | Application version | `version 1.0 `|
| `call_type` | 2.0+ | Call type. | [`view`, `link`] |
| `carrier` | 1.1+ | The device's mobile carrier | `Verizon` |
| `carrier_iso` | 1.1+ | Carrier ISO country code| `ISO 3166-1` |
| `carrier_mcc` | 1.1+ | Mobile country code| `ITU-T Recommendation E.212` |
| `carrier_mnc` | 1.1+ | Mobile network code |
| `connection_type` | 1.1+ | Connection type | `wifi` |
| `device` | 1.1+ | Device type. | iPhone, iPad |
| `device_android_runtime` | 5.4+ | Android Runtime version | `2.1.0` |
| `device_available_external_storage` | 5.4+ | Total available external storage on device | |
| `device_available_system_storage` | 5.4+ | Total available storage on device |` 273772544` |
| `device_architecture` | 3.0+ | Bit architecture of the device | `64` |
| `device_battery_percent` | 4.0+ | Integer percent representation of device's remaining power | `50` |
| `device_cputype` | 3.0+ | CPU type | `arm7s` |
| `device_ischarging` | 4.0+ | Is the device actively charging? | [`true`, `false`] |
| `device_language` | 3.0+ | Two-letter ISO 639-1 language setting identifier | `en` |
| `device_orientation` | 5.0+ | Orientation of device at time of call | [`Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown`] |
| `device_os_build` | 5.4+ | Operating System build version | `4499259` |
| `device_os_version` | 5.0+ | Operating System version on device | `7.0` |
| `event_name` | 5.0+ | `mobile_link` required by vdata | |
| `library_version` | 1.2+ | The version of the Tealium library your app has installed | `1.2` |
| `lifecycle_dayofweeklocal*` | 1.2+ | Local day of week that call was made | `1`=Sunday, `2`=Monday |
| `lifecycle_dayssincelastwake*` | 1.2+ | Days since last detected wake in integer increments | |
| `lifecycle_dayssincelaunch*` | 1.2+ | Days since first launch in integer increments | |
| `lifecycle_dayssinceupdate*` | 1.2+ | Days since the last detected app version update in integer increments | |
| `lifecycle_diddetectcrash*` | 5.0.3+ | Was there a crash determined on launch event? | `true` |
| `lifecycle_firstlaunchdate*` | 1.2+ | GMT timestamp of the first detected launch/wake in ISO 8601 format from UTC | `2013-07-11T17:55:04Z` |
| `lifecycle_firstlaunchdate_MMDDYYYY*` | 1.2+ | GMT Timestamp formatted as MM/DD/YYYY | `01/17/2012` |
| `lifecycle_hourofday_local*` | 1.2+ | Local hour of day that call was made (24 hour format) | |
| `lifecycle_isfirstlaunch*` | 1.2+ | Is call the first launch/wake call? | [`true`, `false`]  |
| `lifecycle_isfirstlaunchupdate*` | 1.2+ | Is call the first launch/wake after a detected updated? | [`true`, `false`]  |
| `lifecycle_isfirstwakemonth*` | 1.2+ | Is call the first launch/wake of the month? | [`true`, `false`] |
| `lifecycle_isfirstwaketoday*` | 1.2+ | Is call the first launch/wake of the day? | [`true`, `false`]  |
| `lifecycle_lastlaunchdate*` | 1.2+ | GMT timestamp of last recorded launch in ISO 8601 format from UTC | `2013-01-17T17:55:04Z` |
| `lifecycle_lastsleepdate*` | 1.2+ | GMT timestamp of last recorded sleep in ISO 8601 format from UTC |`2013-07-11T17:55:04Z` |
| `lifecycle_lastwakedate*` | 1.2+ | GMT timestamp of last recorded wake in ISO 8601 format from UTC | `2013-07-11T17:55:04Z` |
| `lifecycle_launchcount*` | 1.2+ | Total number of launches this version of your app (resets if app version updates) | |
| `lifecycle_priorsecondsawake*` | 1.2+ | Whole seconds app was awake since last launch only (aggregates total from all wakes prior, and only sent with `lifecycle_type:launch` calls) | |
| `lifecycle_secondsawake*` | 1.2+ | Whole seconds app was awake since last wake/launch (sent only with `lifecycle_type:sleep`) | |
| `lifecycle_sleepcount*` | 1.2+ | Total number of times your app has gone to sleep (resets if app version updates) | |
| `lifecycle_totalcrashcount*` | 5.0.4+ | Total number of times crashes were detected. Does not reset unless app reinstalled | |
| `lifecycle_totallaunchcount*` | 1.2+ | Total number of launches since install. Does not reset unless app reinstalled | |
| `lifecycle_totalsecondsawake*`| 1.2+ | Total number of seconds your app has been in a woken/active state  (does not reset unless app reinstalled) | |
| `lifecycle_totalsleepcount*` | 1.2+ | Total number of times your app has gone into the background since install (does not reset unless app reinstalled) | |
| `lifecycle_totalwakecount*` | 1.2+ | Total number of launches + wakes since install (does not reset unless app reinstalled) |
| `lifecycle_type*` | 1.2+ | Type of lifecycle call | [`launch`, `wake`, `sleep`] |
| lifecycle_updatelaunchdate*` | 1.2+ | GMT timestamp of first wake/launch after a version update has been detected. ISO 8601 format from UTC | `2013-01-17T17:55:04Z` |
| lifecycle_wakecount* | 1.2+ | Total number of launches + wakes in this version of your app (resets if app version updates) |
| `link_id` | 1.0+ | (EVENT CALLS ONLY) General event or link title - such as a button title or an object's Tealium ID | [any string] |
| `~orientation~` | 2.0+ | **DEPRECATED** Orientation of device at time of call | [`Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown`] |
| `origin` | 3.0+ | Constant used in mapping to distinguish mobile from web implementations | `mobile` |
| `os_version` | 1.1+ | Operating System version on device | `7.0` |
| `page_type` | 5.0+ | `mobile_view` constant used in mapping to distinguish mobile view / page changes from mobile or web events - required by vdata | |
| `platform` | 1.0+ | Mobile platform | `Android` |
| `screen_title` | 1.0+ | (VIEW CALLS ONLY) General view title | [any string] |
| `timestamp` | 1.1+ | Timestamp to seconds of event occurrence [ISO 8601 at UTC] | `2013-07-11T19:57:47Z` |
| `timestamp_local` | 2.0+ | Local Timestamp to seconds of event occurrence (ISO 8601 without offset) | `2013-07-11T19:57:47` |
| `timestamp_offset` | 2.0+ | Local timezone offset of device's location in hours | `-3` |
| `timestamp_unix` | 1.1+ | GMT/UTC Unix timestamp of event occurrence |`1373498679` |
| `timestamp_unix_milliseconds` | 5.5.1 | GMT/UTC Unix timestamp in milliseconds of event occurrence | `1373498679123` |
| `uuid` | 1.2+ | (Universally Unique Identifier) Unique for each installation of an app on a device | [any string] |
| `visitor_id` | 5.0+ | Tealium-generated visitor ID | |
