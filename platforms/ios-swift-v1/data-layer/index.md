---
title: Data Layer
description: A full list of the data layer variables provided by each module.
url: https://docs.tealium.com/platforms/ios-swift-v1/data-layer/
---
<blockquote>
This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](https://docs.tealium.com/platforms/ios-swift/).
</blockquote>


## AppData

The following variables are added to the data layer by the [`AppData`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/appdata/) module.

| Variable Name | Description | Example |
| --- | --- | --- |
| `app_build` | Minor build version of the app | `2213` |
| `app_name` | Name of the app (typically the App Store name)| `Digital Velocity` |
| `app_rdns` | Fully-qualified name of the app bundle| `com.tealium. digitalvelocity` |
| `app_uuid` | Random `uuid`. Persists for the duration of the app install, so long as one of the persistent storage modules is also enabled. Resets if app is uninstalled.| `t3aL...1uM` |
| `app_version` | Version of the app bundle | `1.0` |
| `tealium_vid` | Persistent Tealium visitor ID| `t3aL...1uM` |
| `tealium_visitor_id` | Same as `tealium_vid` and included for legacy reasons| `t3aL...1uM` |

## Attribution

The following variables are added to the data layer by the [`Attribution`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/attribution/) module.

| Variable Name | Description | Example |
| --- | --- | --- |
| `ad_campaign_id` | The corresponding ad's campaign ID | `1234567890` |
| `ad_campaign_name` |  The corresponding ad's campaign name | `CampaignName` |
| `ad_creativeset_id` | The ID of the Creative Set which the corresponding ad was part of. | `456093` |
| `ad_creativeset_name` | The name of the Creative Set which the corresponding ad was part of.| `Beast Images` |
| `ad_group_id` |  The corresponding ad's campaign group ID | `1234567890` |
| `ad_group_name` |  The corresponding ad's campaign group name| `AdGroupName` |
| `ad_keyword` | The keyword that drove the ad impression which led to the corresponding ad click| `Keyword` |
| `ad_keyword_matchtype` | Either be Broad, Exact or Search Match. | `Exact` |
| `ad_org_id` |  The corresponding ad's campaign organization ID | `OrgID` |
| `ad_org_name` |  The corresponding ad's campaign organization name | `OrgName` |
| `ad_purchase_date` | Date and time the user first downloaded your app. In the case where `iadconversion-type = "Redownload"`, this represents the original purchase date. This may or may not have been associated with an Apple Search Ad.| `2016-12-05T17:31:40Z` |
| `ad_region` | Identifies the country or region associated with the campaign which drove this install. | `US` |
| `ad_user_clicked_last_30_days` | Boolean indicating if user clicked on a Search Ads impression within 30 days prior to app download | [`true`, `false`] |
| `ad_user_conversion _type` | Identifies new download or redownload of the app| `Download` |
| `ad_user_date_clicked` | Date and time the user clicked on a corresponding ad| `2016-12-05T17:31:40Z` |
| `ad_user_date_converted` | Date and time the user downloaded the app| `2016-12-05T17:31:40Z` |
| `device_advertising_enabled` | Boolean indicating if the user allowed ad tracking (if `false`, the advertising ID appears as a string of zeroes)| [`true`, `false`] |
| `device_advertising_id` | User-resettable advertising identifier (IDFA)| `6D92078A-8246...` |
| `device_advertising_vendor_id` | Unique ID guaranteed to be the same across all apps on the same device from a single vendor (apps with the same first two parts of the RDNS bundle identifier. For example, com.tealium or com.acme)| `6D92078A-8246...` |

## Autotracking

The following variables are added to the data layer by the [`Autotracking`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/autotracking/) module.

| Variable Name | Description | Example |
| --- | --- | --- |
| `autotracked` | Set to true and added to each autotracked tracking call| [`true`, `false`] |

## ConsentManager

The following variables are added to the data layer by the [`ConsentManager`](https://docs.tealium.com/platforms/ios-swift-v1/consent-management/) module.

| Variable Name | Description | Example |
| --- | --- | --- |
| `consent_categories` | An array of the user's selected consent categories| [`"analytics"`, `"cdp"`] |
| `consent_status` | The user's current consent status| [`consented`, `notConsented`] |
| `policy` | Consent Policy| `"gdpr"` |

## Connectivity

The following variables are added to the data layer by the [`Connectivity`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/connectivity/) module.

| Variable Name | Description | Example |
| --- | --- | --- |
| `queue_reason` | Added to the track call if the tracking request was queued due to lack of connectivity. Only present for queued events; absent for all other events| `connectivity` |
| `was_queued` | Indicates whether a tracking call was queued due to no connectivity. Only present for queued events; absent for all other events| [`true`, `false`] |

##  Core

The following variables are added to the data layer by the `Core` module.

| Variable Name | Description | Example |
| --- | --- |  --- |
| `enabled_modules` | List of all currently-enabled modules| `["tagmanagement", "collect"]` |
| `screen_title` | Screen title passed to trackView call| `"homescreen" `|
| `tealium_datasource` | Specifies the data source name (added to every dispatch)| `"a1b2c3"` |
| `tealium_event` | The name of the event being tracked| `"checkout"` |


##  Crash Reporter

The following variables are added to the data layer by the [`CrashReporter`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/crash-reporter/) module.

| Variable Name | Description | Example |
| --- | --- | --- |
| `app_memory_usage` | Current memory used by the app on the device at the time of the crash| `143.57MB` |
| `crash_cause` | Cause of the crash| `Crash Reason` |
| `crash_name` | Friendly name of the crash, if available| `Crash Name` |
| `crash_libraries` | List of loaded libraries at the time of the crash| `[{ "baseAddress": "0xa3e0000", "codeType": { "arch": 64, "typeEncoding": "Mach"}, "imageName": "/Applications/Xcode9.3.app/ Contents/Developer/Platforms/ iPhoneOS.platform/Developer/ Library/CoreSimulator/Profiles/ Runtimes/iOS.simruntime/ Contents/Resources/ RuntimeRoot/usr/lib/dyld_sim", "imageSize": 212992, "imageUuid": "4015e9b70bde" }]` |
| `crash_process_id` | PID of the app at time of crash| `84351` |
| `crash_process_path` | Path the app was running under| `/DemoApp.app/DemoApp` |
| `crash_parent_process` | Parent process that launched the app| `launchd_sim` |
| `crash_parent_process_id`| Parent process PID | `83183` |
| `crash_signal_address` | Signal address of the crash| `4572945982` |
| `crash_signal_code` | Signal code causing the crash| `#0` |
| `crash_signal_name` | Signal name causing the crash| `SIGABRT` |
| `crash_threads` | Returns all active threads at the time of the crash| `{"crashed": 1,"registers": {"cs": "0x07"},"stack": {"instructionPointer": 4572945982,"symbolInfo": {"symbolName": "","symbolStartAddr": 0},"threadId": ""}}` |
| `crash_uuid` | Unique identifier for this specific crash| `CC2DA0E9-E544-429A-AC5E-A268FC62F02A` |
| `device_memory_usage` | Current memory used by the app on the device at the time of the crash| `143.57MB` |
| `device_memory_available` | Free memory on device at the time of the crash| `1068.88MB` |
| `device_os_build` | Current OS build number| `15E217` |
| `memory_free` | Free memory on device at the time of the crash| `1068.88MB` |

## DeviceData

The following variables are added to the data layer by the [`DeviceData`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/device-data/) module.

| Variable Name | Description  | Example |
|---|---| --- |
| `app_memory_usage`   | Memory being used by the current process/app in Megabytes| `35.75MB`          |
| `app_orientation`    | Orientation of the app (from statusBarOrientation; may differ from device orientation if app is locked in a specific orientation)| `Portrait`       |
| `app_orientation_extended` | Extended Orientation of the app (from statusBarOrientation; may differ from device orientation if app is locked in a specific orientation)| `Portrait Upside Down` |
| `carrier`                    | Mobile network carrier name| `EE`|
| `carrier_iso`                | Mobile carrier ISO| `gb`|
| `carrier_mcc`                | [Carrier mobile country code](https://en.wikipedia.org/wiki/Mobilecountrycode)| `234`|
| `carrier_mnc`                | Carrier mobile network code| `34`|
| `cpu_architecture`           | CPU architecture| `64`|
| `cpu_type`                   | CPU type| `ARM64v8`|
| `device`                     | Consumer device name| `iPhone 7 Plus`|
| `device_architecture`        | Device architecture| `64`|
| `device_battery_percent`     | Current battery percentage at time of track call| `58`|
| `device_cputype`             | Device CPU type| `Intel`|
| `device_ischarging`          | Boolean to indicate if device is currently charging at time of track call| [`true`, `false`]|
| `device_language`            | Current device language| `en`|
| `device_orientation`         | Simple orientation| [`Portrait`, `Landscape`]|
| `device_orientation_extended`| Full orientation| `Face Up`|
| `device_os_version`          | Operating system version| `11.1`|
| `device_resolution`          | Screen resolution| `1080x1920`|
| `device_type`            | Apple internal device identifier| `iPhone8,4`|
| `memory_active*`             | Total active memory on the device| `997.78MB`|
| `memory_compressed*`         | Total compressed memory on the device| `153.39MB`|
| `memory_free*`               | Total free memory on the device| `120.81MB`|
| `memory_inactive*`           | Total inactive memory on the device| `441.83MB`|
| `memory_physical*`           | Total physical memory on the device (RAM) in Megabytes| `2013.50MB`|
| `memory_wired*`              | Total wired memory on the device| `207.12MB`|
| `model_name`                 | Model name| `iPhone 7 Plus`|
| `model_variant`              | Model variant (generally indicates which radio technology is available on the device)| [`CDMA`, `GSM`, `WiFi`, `Cellular`]|
| `network_connection_type`    | Current connection type| [`wifi`, `cellular`]|
| `_connection_type`           | Current connection type| [`wifi`, `cellular`]|
| `network_iso_country_code`   | Mobile network ISO country code| `gb`|
| `network_mcc`                | [Network mobile country code](https://en.wikipedia.org/wiki/Mobilecountrycode)| `234`|
| `network_mnc`                | [Network mobile network code](https://en.wikipedia.org/wiki/Mobilecountrycode)| `34`|
| `network_name`               | Mobile network carrier name| `EE`|
| `os_build`                   | Operating System Build Version| `15J580`|
| `os_name`                    | Operating System Name| [`iOS`, `tvOS`, `watchOS`, `macOS`]|
| `os_version`                 | Operating system version| `11.1`|
| `platform`                   | Operating System Name| [`iOS`, `tvOS`, `watchOS`, `macOS`]|
| `user_locale`                | Current device language| `en`|

## DispatchQueue

The following variables are added to the data layer by the [`DispatchQueue`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/dispatch-queue/) module.

| Variable Name | Description | Example |
| --- | --- | --- |
| `queue_reason` | Added to the track call if the tracking request was queued due to event batching. Only present for queued events; absent for all other events| `batching_enabled` |
| `was_queued` | Indicates whether a tracking call was queued due to no event batching. Only present for queued events; absent for all other events| [`true`, `false`] |

## Lifecycle

The following variables are added to the data layer by the [`Lifecycle`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/lifecycle/) module.

| Variable Name | Description | Example |
| --- | --- | --- |
| `lifecycle_dayofweek_local` | Local day of week that call was made, such as 1=Sunday, 2=Monday| `4` |
| `lifecycle_dayssincelastwake` | Days since last detected wake in integer increments| `1` |
| `lifecycle_dayssincelaunch` | Days since first launch in integer increments| `23` |
| `lifecycle_dayssinceupdate` | Days since the last detected app version update in integer increments| `46` |
| `lifecycle_diddetect_crash` | Was a crash detected during this launch/wake event (populated only if `true`)| [`true`, `false`] |
| `lifecycle_firstlaunchdate` | GMT timestamp of the first detected launch/wake in ISO 8601 format from UTC | `2013-07-11T17:55:04Z` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | GMT Timestamp formatted as MM/DD/YYYY| `01/17/2012 `|
| `lifecycle_hourofday_local` | Local hour of day that call was made (24 hour format)| [`true`, `false`] |
| `lifecycle_isfirstlaunch` | Only present if call is the first launch/wake call| [`true`, `false`] |
| `lifecycle_isfirstlaunchupdate` | Only present if call is first launch/wake after a detected updated| [`true`, `false`] |
| `lifecycle_isfirstwakemonth` | Only present if call is first launch/wake of the month| [`true`, `false`] |
| `lifecycle_isfirstwaketoday` | Only present if call is first launch/wake of the day| [`true`, `false`] |
| `lifecycle_launchcount` | Total number of launches this version of your app (since the last update)| `3` |
| `lifecycle_priorsecondsawake` | Whole seconds app was awake since last launch only. Aggregates total from all wakes prior. Sent only with `lifecycle_type:launch` calls.| `126` |
| `lifecycle_secondsawake` | Whole seconds app was awake since most recent wake/launch| `30` |
| `lifecycle_sleepcount` | Total number of times your app has gone to sleep (resets if updated)| `5` |
| `lifecycle_totalcrashcount` | Total number of crashes counted since install (only reset if app deleted)| `21` |
| `lifecycle_totallaunchcount` | Total number of launches since install (only reset if app deleted)| `3` |
| `lifecycle_totalsecondsawake` | Total number of seconds your app has been in a woken/active state since app install (only reset if app deleted)| `36` |
| `lifecycle_totalsleepcount` | Total number of times your app has gone into the background since app install (only reset if app deleted)| `"400"` |
| `lifecycle_totalwakecount` | Total number of launches + wakes since install (only reset if app deleted)| `"563"` |
| `lifecycle_type` | Type of lifecycle call.| [`"launch"`, `"wake"`, `"sleep"` ]|
| `lifecycle_updatelaunchdate` | GMT timestamp of first wake/launch after a version update has been detected| `2014-09-08T18:10:01Z` |
| `lifecycle_wakecount` | Total number of launches + wakes in this version of your app (resets if updated)| `"29"` |

## Location

The following variables are added to the data layer by the [`Location`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/location/) module.

| Variable  Name                     | Description| Example              |
|------------------------------------|---------|----------------------|
| `geofence_name`     | The name of the geofence region| `"Tealium_San_Diego"`|
| `geofence_transition_type` | The type of geofence transition event| `"entered"` or `"exited"`|
| `latitude`          | The latitude of the user's most recently recorded location| `"32.906119"`|
| `location_timestamp` | The recorded date/time (GMT) the user entered/exited the geofence region| `"2020-01-28 16:29:46 +0000"`|
| `longitude`        | The longitude of the user's most recently recorded location| `"-117.23791632509666"`|
| `movement_speed` | The instantaneous speed of the device, measured in meters per second| `"1.0"`|

## TagManagement

The following variables are added to the data layer by the [`TagManagement`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/tag-management/) module.

| Variable Name | Description | Example |
| --- | --- | --- |
| `dispatch_service` | Static string to indicate which module the tracking call came from | `collect/tagmanagement` |

## VolatileData

The following variables are added to the data layer by the [`VolatileData`](https://docs.tealium.com/platforms/ios-swift-v1/module-list/volatile-data/) module.

| Variable Name                   | Description | Example |
|---------------------------------|-------------| ---|
| `event_timestamp_iso`           | Event timestamp in ISO 8601 UTC| `2017-11-20T14:48:00Z`  |
| `event_timestamp_local_iso`     | Event timestamp in ISO 8601 local timezone| `2017-11-20T06:48:00`     |
| `event_timestamp_offset_hours`  | Current offset from UTC in hours| `-8`                               |
| `event_timestamp_unix`          | Current Unix timestamp (1970 epoch) in seconds| `1511189280`         |
| `event_timestamp_unix_millis`   | Current Unix timestamp (1970 epoch) in milliseconds| `1511189280337` |
| `tealium_account`               | Current Tealium account (from TealiumConfig object)| `tealium`       |
| `tealium_environment`           | Current Tealium environment (from TealiumConfig object)| `dev`       |
| `tealium_library_name`          | Tealium library name| `swift`                                        |
| `tealium_library_version`       | Tealium library version| `1.8.0`                                     |
| `tealium_profile`               | Current Tealium profile (from TealiumConfig object)| `mobile`        |
| `tealium_random`                | Random number| `8449989974958830`                                    |
| `tealium_session_id`            | Tealium Session ID| `1511262829677`                                  |
| `tealium_timestamp_epoch`       | Current Unix timestamp (1970 epoch) in seconds| `1511262829`         |
| `timestamp`                     | Event timestamp in ISO 8601 UTC| `2017-11-20T14:48:00Z`  |
| `timestamp_local`               | Event timestamp in ISO 8601 local timezone| `2017-11-20T06:48:00`     |
| `timestamp_offset`              | Current offset from UTC in hours| `-8`                               |
| `timestamp_unix`                | Current Unix timestamp (1970 epoch) in seconds| `1511189280`         |
| `timestamp_unix_milliseconds`   | Current Unix timestamp (1970 epoch) in milliseconds| `1511189280337` |
