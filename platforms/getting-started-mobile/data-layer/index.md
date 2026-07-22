---
title: Data Layer
description: The list of data layer variables available on mobile installations.
url: https://docs.tealium.com/platforms/getting-started-mobile/data-layer/
---
Each mobile component adds variables to the data layer. The following sections list every variable in each module.

All values are converted to strings. However, numbers can be coerced back into a numeric type as needed using iQ extensions or Tealium EventStream enrichments.


<blockquote>
All auto-tracked events set the attribute: `autotracked="true"`
</blockquote>


## App data

Properties of the host application.

| Event Attribute | Type | Description | Example |
| :-- | :-- | :-- | :-- |
| `app_name` | `String` | Application name | `"Digital Velocity"` |
| `app_rdns` | `String` | Reverse DNS Bundle id/package name | `"com.digitalvelocity.alpha"` |
| `app_version` | `String` | Application version |  `"1.2.0"` |

## Collect

Dispatches tracking calls as network requests to Tealium's Collect service using the platform's native URL communications service.

| Event Attribute | Type | Value |
| :-- | :-- | :-- |
| `dispatch_service` | `String` | `"collect"` |

## Carrier data

Provides information regarding the mobile carrier. 

| Event Attribute | Type | Description |Example |
| :-- | :-- | :-- | :-- |
| `carrier` | `String` |Name of the Carrier |`"AT&T"` |
| `carrier_iso` | `String` |Carrier ISO 3166-1 country code  |`"us"` |
| `carrier_mcc` | `String` |Mobile ITU-T E.212 country code | `"us"` |
| `carrier_mnc` | `String` |Mobile Network Code  | `"410"` |

## Consent management

Provides information about consent tracking preferences. 

| Event Attribute | Type | Description | Example |
| :-- | :-- | :-- | :-- |
| `policy` | `String` |The policy under which consent was collected |`"gdpr"` |
| `consent_status` | `String` |The user's current consent status |`"consented"` |
| `consent_categories` | `[String]` |An array of the user's selected consent categories | `["analytics", "cdp"]` |


## Device data

Provides information regarding the host device.

| Event Attribute | Type | Description | Example |
| :-- | :-- | :-- | :-- |
| `device` |`String` | Name of the device |`"iPhone 6s"` |
| `device_architecture` |`Number` | Bit architecture of device (32, 64, etc.)| `64` |
| `device_advertising_id` |`String` | Optional Advertising identifier. Not automatically available for all devices |`"03402320-245A-4ED4-BEAE-A1F50E21C55E"` |
| `device_battery_percent` |`Number` | Whole number percent representation of device's remaining battery power| `100` |
| `device_cputype` | `String` |Central Processor Unit type (arm6, arm7, etc.) |`"ARM64"` |
| `device_ischarging ` | `String` |Is the device actively charging (true/false)| `"false"` |
| `device_language ` | `String` |Two-letter IOS-639-1 language identifier (en, ja, etc.) |`"en"` |
| `device_orientation` | `String` |Orientation of device at time of event (portrait, landscape, etc.)  |`"Portrait"` |
| `device_resolution ` | `String` | Resolution of a device |`"750x1334"` |



## Lifecycle events

Provides automatic tracking for the following application lifecycle events: launch, wake, and sleep.

| Event Attribute | Type | Description | Example |
| :-- | :-- | :-- | :-- |
| `lifecycle_ dayofweek_local` | `Number` |Local day of week (1=Sunday, 2=Monday, etc) | `3` |
| `lifecycle_ dayssincelaunch` | `Number` | Days since first launch in whole number increments | `0` (24 hours have not yet elapsed) |
| `lifecycle_ dayssinceupdate` | `String` |Days since the app was updated in whole number increments|`"1"` |
| `lifecycle_ diddetectcrash` | `String` | Was there a crash was determined at time of launch?  |`"true"` |
| `lifecycle_ firstlaunchdate` | `String` |GMT timestamp of very first detected launch (ISO 8601 format for UTC) | `"2016-05-16T16:32:04Z"` |
| `lifecycle_ firstlaunchdate_ MMDDYYYY` | `String` |GMT timestamp of very first detected launch (MM/DD/YYYY format) |`"5/16/2016"` |
| `lifecycle_ hourofday_local` | `Number` |Local hour of day (24 hour format)  | `13` |
| `lifecycle_ isfirstlaunch` | `String` |`"true"` if launch is very first (otherwise not populated)|  `"true"` |
| `lifecycle_ isfirstlaunchupdate` | `String` |`"true"` if launch is very first after a detected app version update (otherwise not populated) |`"true"` |
| `lifecycle_ isfirstwakemonth` | `String` |`"true"` if launch event is the first for the current month (otherwise not populated) | `"true"` |
| `lifecycle_ isfirstwaketoday ` | `String` |`"true"` if launch/wake event is the first for current day (otherwise not populated) | `"true"` |
| `lifecycle_ lastlaunchdate ` | `String` |GMT timestamp of prior recorded launch (ISO 8601 format for UTC) (Not populated if it is within the first session) | `"2013-07-11T17:55:04Z"` |
| `lifecycle_ lastsleepdate ` | `String` | GMT timestamp of prior recorded sleep event (ISO 8601 format for UTC) |`"2013-07-11T17:55:04Z"` |
| `lifecycle_ lastwakedate ` | `String` |GMT timestamp of prior recorded wake event (ISO 8601 format for UTC) |`"2013-07-11T17:55:04Z"` |
| `lifecycle_ launchcount ` | `Number` |Total whole number of launches for application since most recent version update (restarts when a new version detected) |`3` |
| `lifecycle_ priorsecondsawake` | `Number` |Populated only during launch events. Whole seconds application was awake between wakes and sleeps. Aggregate of all these wakes & sleeps until a launch event. | `148` |
| `lifecycle_ secondsawake ` | `Number` |Populated only during sleep events. Whole seconds application has been awake from most recent wake to the sleep event.  |`480` |
| `lifecycle_ sleepcount ` | `Number` | Total number of times app was detected to have gone to sleep/background.  |`3` |
| `lifecycle_ totallaunchcount` | `Number` |Total number of launches since app was installed. Only resets if application deleted and reinstalled.  |`5` |
| `lifecycle_ totalsecondsawake ` | `Number` | Total number of seconds application has been awake. Only resets if application deleted and reinstalled.  |`800` |
| `lifecycle_ totalsleepcount ` | `Number` |Total number of times application was detected to have gone to sleep. Only resets if application deleted and reinstalled. |`8` |
| `lifecycle_ totalcrashcount` | `Number` |Total number of times an application failed to properly log a sleep event, resulting in a lifecycle sequence discrepancy caused by a crash. Only resets if application deleted and reinstalled.  |`2` |
| `lifecycle_ totalwakecount ` | `Number` | Total number of launches and wakes. Only resets if application deleted and reinstalled.  |`7` |
| `lifecycle_type`  | `String` |Lifecycle event type |  [`"launch"`, `"wake"`, `"sleep"`] |
| `lifecycle_ updatelaunchdate` | `String` |GMT timestamp of first launch/wake after an app version update detected. ISO 8601 format for UTC.|`"2016-05-16T16:32:04Z"` |
| `lifecycle_ wakecount` | `Number` |Total number of launches and wakes for this application version. Resets if a new host application version detected. |`34` |


## Offline queuing

Preserves event dispatch data for later delivery when, for example, a device has momentarily lost network connectivity.

Populates the following Event Attribute within the dispatch data that was queued: 

| Event Attribute | Value |
| :-- | :-- |
| `was_queued` | `"true"` |


## Tag management

Runs vendor tags configured in Tealium iQ Tag Management in a hidden webview.

| Event Attribute | Value |
| :-- | :-- |
| `dispatch_service` | `"tagmanagement"` |

## Tealium data

Default event attributes that are present in all libraries.

| Event Attribute | Type | Description |Example |
| :-- | :-- | :-- | :-- |
| `tealium_event` | `String` |Title of the event. Value populated by the 'title' argument of the Tealium provided track calls. Does NOT need to be unique. | `"button_tapped"` |
| `tealium_random` | `Number` |Random 16 digit number generated per event. Pre-padded with zeroes to maintain 16 digit length.| `1234567890123456` |
| `tealium_account` | `String` |Tealium account name used to initialize a Tealium integration library.  |`"companyXYZ"` |
| `tealium_environment` | `String` |Tealium TIQ environment used to initialize a Tealium integration library. | [`"dev"`, `"qa"`, `"prod"`] |
| `tealium_library_name` | `String` |Name of the platform integration library.  |`"swift"` |
| `tealium_library_version` | `String` |Version of the platform integration library. |  `"1.2.0"` |
| `tealium_profile` | `String` |Tealium profile name used to initialize a Tealium integration library.  |`"main"` |
| `tealium_datasource` | `String` |6 digit alphanumeric identifier provided by the Tealium Customer Data Hub |`"abc123"` |
| `tealium_session_id` | `Number` |Unix epoch timestamp in milliseconds, no decimals, of first event. Resets after a new session starts, typically a new launch.  |`1496350751928` |
| `tealium_visitor_id` | `String` | Unique app-device visitor id that differentiates users. Required by the Collect service. |(32 character alpha-numeric) |
| `tealium_timestamp_epoch` | `Number` |Unix timestamp at UTC.  |`1496350751` |
