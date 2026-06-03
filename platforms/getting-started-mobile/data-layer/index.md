---
title: Data Layer
description: The list of data layer variables available on mobile installations.
url: https://docs.tealium.com/platforms/getting-started-mobile/data-layer/
---
Each mobile component adds variables to the data layer. The following sections list every variable in each module.

All values are converted to strings. However, numbers can be coerced back into a numeric type as needed using iQ extensions or Tealium EventStream enrichments.

 All auto-tracked events set the attribute: `autotracked=&#34;true&#34;` 

## App data

Properties of the host application.

| Event Attribute | Type | Description | Example |
| :-- | :-- | :-- | :-- |
| `app_name` | `String` | Application name | `&#34;Digital Velocity&#34;` |
| `app_rdns` | `String` | Reverse DNS Bundle id/package name | `&#34;com.digitalvelocity.alpha&#34;` |
| `app_version` | `String` | Application version |  `&#34;1.2.0&#34;` |

## Collect

Dispatches tracking calls as network requests to Tealium&#39;s Collect service using the platform&#39;s native URL communications service.

| Event Attribute | Type | Value |
| :-- | :-- | :-- |
| `dispatch_service` | `String` | `&#34;collect&#34;` |

## Carrier data

Provides information regarding the mobile carrier. 

| Event Attribute | Type | Description |Example |
| :-- | :-- | :-- | :-- |
| `carrier` | `String` |Name of the Carrier |`&#34;AT&amp;T&#34;` |
| `carrier_iso` | `String` |Carrier ISO 3166-1 country code  |`&#34;us&#34;` |
| `carrier_mcc` | `String` |Mobile ITU-T E.212 country code | `&#34;us&#34;` |
| `carrier_mnc` | `String` |Mobile Network Code  | `&#34;410&#34;` |

## Consent management

Provides information about consent tracking preferences. 

| Event Attribute | Type | Description | Example |
| :-- | :-- | :-- | :-- |
| `policy` | `String` |The policy under which consent was collected |`&#34;gdpr&#34;` |
| `consent_status` | `String` |The user&#39;s current consent status |`&#34;consented&#34;` |
| `consent_categories` | `[String]` |An array of the user&#39;s selected consent categories | `[&#34;analytics&#34;, &#34;cdp&#34;]` |


## Device data

Provides information regarding the host device.

| Event Attribute | Type | Description | Example |
| :-- | :-- | :-- | :-- |
| `device` |`String` | Name of the device |`&#34;iPhone 6s&#34;` |
| `device_architecture` |`Number` | Bit architecture of device (32, 64, etc.)| `64` |
| `device_advertising_id` |`String` | Optional Advertising identifier. Not automatically available for all devices |`&#34;03402320-245A-4ED4-BEAE-A1F50E21C55E&#34;` |
| `device_battery_percent` |`Number` | Whole number percent representation of device&#39;s remaining battery power| `100` |
| `device_cputype` | `String` |Central Processor Unit type (arm6, arm7, etc.) |`&#34;ARM64&#34;` |
| `device_ischarging ` | `String` |Is the device actively charging (true/false)| `&#34;false&#34;` |
| `device_language ` | `String` |Two-letter IOS-639-1 language identifier (en, ja, etc.) |`&#34;en&#34;` |
| `device_orientation` | `String` |Orientation of device at time of event (portrait, landscape, etc.)  |`&#34;Portrait&#34;` |
| `device_resolution ` | `String` | Resolution of a device |`&#34;750x1334&#34;` |



## Lifecycle events

Provides automatic tracking for the following application lifecycle events: launch, wake, and sleep.

| Event Attribute | Type | Description | Example |
| :-- | :-- | :-- | :-- |
| `lifecycle_ dayofweek_local` | `Number` |Local day of week (1=Sunday, 2=Monday, etc) | `3` |
| `lifecycle_ dayssincelaunch` | `Number` | Days since first launch in whole number increments | `0` (24 hours have not yet elapsed) |
| `lifecycle_ dayssinceupdate` | `String` |Days since the app was updated in whole number increments|`&#34;1&#34;` |
| `lifecycle_ diddetectcrash` | `String` | Was there a crash was determined at time of launch?  |`&#34;true&#34;` |
| `lifecycle_ firstlaunchdate` | `String` |GMT timestamp of very first detected launch (ISO 8601 format for UTC) | `&#34;2016-05-16T16:32:04Z&#34;` |
| `lifecycle_ firstlaunchdate_ MMDDYYYY` | `String` |GMT timestamp of very first detected launch (MM/DD/YYYY format) |`&#34;5/16/2016&#34;` |
| `lifecycle_ hourofday_local` | `Number` |Local hour of day (24 hour format)  | `13` |
| `lifecycle_ isfirstlaunch` | `String` |`&#34;true&#34;` if launch is very first (otherwise not populated)|  `&#34;true&#34;` |
| `lifecycle_ isfirstlaunchupdate` | `String` |`&#34;true&#34;` if launch is very first after a detected app version update (otherwise not populated) |`&#34;true&#34;` |
| `lifecycle_ isfirstwakemonth` | `String` |`&#34;true&#34;` if launch event is the first for the current month (otherwise not populated) | `&#34;true&#34;` |
| `lifecycle_ isfirstwaketoday ` | `String` |`&#34;true&#34;` if launch/wake event is the first for current day (otherwise not populated) | `&#34;true&#34;` |
| `lifecycle_ lastlaunchdate ` | `String` |GMT timestamp of prior recorded launch (ISO 8601 format for UTC) (Not populated if it is within the first session) | `&#34;2013-07-11T17:55:04Z&#34;` |
| `lifecycle_ lastsleepdate ` | `String` | GMT timestamp of prior recorded sleep event (ISO 8601 format for UTC) |`&#34;2013-07-11T17:55:04Z&#34;` |
| `lifecycle_ lastwakedate ` | `String` |GMT timestamp of prior recorded wake event (ISO 8601 format for UTC) |`&#34;2013-07-11T17:55:04Z&#34;` |
| `lifecycle_ launchcount ` | `Number` |Total whole number of launches for application since most recent version update (restarts when a new version detected) |`3` |
| `lifecycle_ priorsecondsawake` | `Number` |Populated only during launch events. Whole seconds application was awake between wakes and sleeps. Aggregate of all these wakes &amp; sleeps until a launch event. | `148` |
| `lifecycle_ secondsawake ` | `Number` |Populated only during sleep events. Whole seconds application has been awake from most recent wake to the sleep event.  |`480` |
| `lifecycle_ sleepcount ` | `Number` | Total number of times app was detected to have gone to sleep/background.  |`3` |
| `lifecycle_ totallaunchcount` | `Number` |Total number of launches since app was installed. Only resets if application deleted and reinstalled.  |`5` |
| `lifecycle_ totalsecondsawake ` | `Number` | Total number of seconds application has been awake. Only resets if application deleted and reinstalled.  |`800` |
| `lifecycle_ totalsleepcount ` | `Number` |Total number of times application was detected to have gone to sleep. Only resets if application deleted and reinstalled. |`8` |
| `lifecycle_ totalcrashcount` | `Number` |Total number of times an application failed to properly log a sleep event, resulting in a lifecycle sequence discrepancy caused by a crash. Only resets if application deleted and reinstalled.  |`2` |
| `lifecycle_ totalwakecount ` | `Number` | Total number of launches and wakes. Only resets if application deleted and reinstalled.  |`7` |
| `lifecycle_type`  | `String` |Lifecycle event type |  [`&#34;launch&#34;`, `&#34;wake&#34;`, `&#34;sleep&#34;`] |
| `lifecycle_ updatelaunchdate` | `String` |GMT timestamp of first launch/wake after an app version update detected. ISO 8601 format for UTC.|`&#34;2016-05-16T16:32:04Z&#34;` |
| `lifecycle_ wakecount` | `Number` |Total number of launches and wakes for this application version. Resets if a new host application version detected. |`34` |


## Offline queuing

Preserves event dispatch data for later delivery when, for example, a device has momentarily lost network connectivity.

Populates the following Event Attribute within the dispatch data that was queued: 

| Event Attribute | Value |
| :-- | :-- |
| `was_queued` | `&#34;true&#34;` |


## Tag management

Runs vendor tags configured in Tealium iQ Tag Management in a hidden webview.

| Event Attribute | Value |
| :-- | :-- |
| `dispatch_service` | `&#34;tagmanagement&#34;` |

## Tealium data

Default event attributes that are present in all libraries.

| Event Attribute | Type | Description |Example |
| :-- | :-- | :-- | :-- |
| `tealium_event` | `String` |Title of the event. Value populated by the &#39;title&#39; argument of the Tealium provided track calls. Does NOT need to be unique. | `&#34;button_tapped&#34;` |
| `tealium_random` | `Number` |Random 16 digit number generated per event. Pre-padded with zeroes to maintain 16 digit length.| `1234567890123456` |
| `tealium_account` | `String` |Tealium account name used to initialize a Tealium integration library.  |`&#34;companyXYZ&#34;` |
| `tealium_environment` | `String` |Tealium TIQ environment used to initialize a Tealium integration library. | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `tealium_library_name` | `String` |Name of the platform integration library.  |`&#34;swift&#34;` |
| `tealium_library_version` | `String` |Version of the platform integration library. |  `&#34;1.2.0&#34;` |
| `tealium_profile` | `String` |Tealium profile name used to initialize a Tealium integration library.  |`&#34;main&#34;` |
| `tealium_datasource` | `String` |6 digit alphanumeric identifier provided by the Tealium Customer Data Hub |`&#34;abc123&#34;` |
| `tealium_session_id` | `Number` |Unix epoch timestamp in milliseconds, no decimals, of first event. Resets after a new session starts, typically a new launch.  |`1496350751928` |
| `tealium_visitor_id` | `String` | Unique app-device visitor id that differentiates users. Required by the Collect service. |(32 character alpha-numeric) |
| `tealium_timestamp_epoch` | `Number` |Unix timestamp at UTC.  |`1496350751` |
