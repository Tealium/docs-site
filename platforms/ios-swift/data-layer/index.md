---
title: Data Layer
description: Learn about managing common data layer values and the data provided by each module.
url: https://docs.tealium.com/platforms/ios-swift/data-layer/
---
## Custom Data

It&#39;s common to need general data layer values on every event. To avoid having to add these values to every tracking call, use the `tealium.dataLayer` methods to persist data layer values that apply to all tracking calls. Once values are stored, they are automatically included in every tracked event.

### Data Expiration

Data layer values have an expiration and are removed from the data layer when they expire. When you set a custom data layer value you can optionally set the expiration time for the value. The default expiration length is the current session.

The following expiration types are available:

| Type                                     | Value           | Description               |
|:-----------------------------------------|:----------------|:--------------------------|
| [Session](#session-data) (default)       | `.session`      | Expires at the end of the current session |
| [Restart](#restart-data)                 | `.untilRestart` | Expires when the app is closed or restarted |
| [Forever](#forever-data)                 | `.forever`      | Never expires             |
| [Custom Date](#custom-date-data)         | `.after`        | Expires on the date specified |
| [Custom Duration](#custom-duration-data) | `.afterCustom`  | Expires on the duration specified by the following time units: `.minutes`, `.hours`, `.days`, `.months`, `.years` |

Use [add()](/platforms/ios-swift/api/tealium-data-layer/#add) to store data in the data layer, based on the expiration type.

#### Session Data

Session data values are persisted for the session. A session is determined by user activity within a given time frame. The session expires after 30 minutes of user inactivity.  

To persist a data layer value that expires after the session:  
```swift
tealium?.dataLayer.add(key: &#34;mysessionvar&#34;, value: &#34;hello&#34;, expiry: .session)
```

To retrieve all session data:  
```swift
let sessionData = tealium?.dataLayer.allSessionData
```

#### Restart Data

Restart data values are persisted for each event. The data is removed when the app is closed or restarted.

To persist a data layer value until the next app restart:  
```swift
tealium?.dataLayer.add(key: &#34;myrestartvar&#34;, value: &#34;foo&#34;, expiry: .untilRestart)
```

#### Forever Data

Forever data values are persisted for the lifetime of the current app version. The data is removed from the data layer when the app is uninstalled or updated.

To persist forever data:  
```swift
tealium?.dataLayer.add(key: &#34;myforevervar&#34;, value: &#34;world&#34;, expiry: .forever)
```

#### Custom Date Data

Custom date data values are persisted by a specified date.

To persist data layer values with a custom date expiration:  
```swift
tealium?.dataLayer.add(key: &#34;customdate&#34;, value: &#34;bar&#34;, expiry: .after(yourDate))
```

#### Custom Duration Data

Custom duration data values are persisted by a specified duration of time.

To persist data layer values which expire after 1 day:  
```swift
tealium?.dataLayer.add(key: &#34;lengthoftime&#34;, value: &#34;days&#34;, expiry: .afterCustom((.days, 1)))
```

To persist data layer values which expire after 1 month:  
```swift
tealium?.dataLayer.add(key: &#34;lengthoftime&#34;, value: &#34;months&#34;, expiry: .afterCustom((.months, 1)))
```

### Retrieve All Data

To retrieve all the currently stored data in the data layer, use the [all()](/platforms/ios-swift/api/tealium-data-layer/#all) method:  

```swift
let data: [String: Any] = tealium?.dataLayer.all
```

See also [`Tealium.gatherTrackData()`](/platforms/ios-swift/api/tealium/#gathertrackdata).

### Clear Data

To clear data for specific keys, use the [delete()](/platforms/ios-swift/api/tealium-data-layer/#delete) method:

- Multiple: `dataLayer.delete(forKeys:)`
- Single: `dataLayer.delete(forKey:)`

To clear all data, use the [`deleteAll()`](/platforms/ios-swift/api/tealium-data-layer/#delete) method.

### Example

The following example demonstrates the above methods:  
```swift
class TealiumHelper {
	var tealium: Tealium?
	let config = TealiumConfig(...)
	tealium = Tealium(config: config) { [weak self] _ in
		guard let self = self, let teal = self.tealium else { return }

		teal.dataLayer.add(key: &#34;mysessionvar&#34;, value: 123456)

		teal.dataLayer.add(key: &#34;myvarforever&#34;, value: &#34;hello&#34;, expiry: .forever)

		teal.dataLayer.add(key: &#34;campaign&#34;, value: &#34;summer&#34;, expiry: .afterCustom((.months, 3)))

		print(&#34;All event data: \(teal.dataLayer.all)&#34;)
		print(&#34;All session data: \(teal.dataLayer.allSessionData)&#34;)
		print(&#34;Single event data key `campaign`: \(teal.dataLayer.all[&#34;campaign&#34;])&#34;)

		teal.dataLayer.delete(forKeys: [&#34;myvarforever&#34;])

		teal.dataLayer.deleteAll()
	}
}
```

## Module Data

### App Data Collector

The following variables are added to the data layer by the [`AppData`](/platforms/ios-swift/module-list/appdata/) module.

| Variable Name        | Description                                                                                                                                                  | Example |
|:---------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|:--|
| `app_build`          | Minor build version of the app                                                                                                                               | `2213` |
| `app_name`           | Name of the app (typically the App Store name)                                                                                                               | `Digital Velocity` |
| `app_rdns`           | Fully-qualified name of the app bundle                                                                                                                       | `com.tealium.digitalvelocity` |
| `app_uuid`           | Random `uuid`. Persists for the duration of the app install, so long as one of the persistent storage modules is also enabled. Resets if app is uninstalled. | `123e4567-e89b-12d3-a456-556642440000` |
| `app_version`        | Version of the app bundle                                                                                                                                    | `1.0` |
| `tealium_vid`        | Persistent Tealium visitor ID                                                                                                                                | `t3aL...1uM` |
| `tealium_visitor_id` | Same as `tealium_vid` and included for legacy reasons                                                                                                        | `t3aL...1uM` |

### Attribution Collector

The following variables are added to the data layer by the [`Attribution`](/platforms/ios-swift/module-list/attribution/) module.

| Variable Name                   | Description                                                                                                                                                                                                            | Example |
|:--------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--|
| `ad_campaign_id`                | The corresponding ad&#39;s campaign ID                                                                                                                                                                                     | `1234567890` |
| `ad_campaign_name`              | The corresponding ad&#39;s campaign name                                                                                                                                                                                   | `CampaignName` |
| `ad_creativeset_id`             | The ID of the Creative Set which the corresponding ad was part of.                                                                                                                                                     | `456093` |
| `ad_creativeset_name`           | The name of the Creative Set which the corresponding ad was part of.                                                                                                                                                   | `Beast Images` |
| `ad_group_id`                   | The corresponding ad&#39;s campaign group ID                                                                                                                                                                               | `1234567890` |
| `ad_group_name`                 | The corresponding ad&#39;s campaign group name                                                                                                                                                                             | `AdGroupName` |
| `ad_keyword`                    | The keyword that drove the ad impression which led to the corresponding ad click                                                                                                                                       | `Keyword` |
| `ad_keyword_matchtype`          | Either be Broad, Exact or Search Match.                                                                                                                                                                                | `Exact` |
| `ad_org_id`                     | The corresponding ad&#39;s campaign organization ID                                                                                                                                                                        | `OrgID` |
| `ad_org_name`                   | The corresponding ad&#39;s campaign organization name                                                                                                                                                                      | `OrgName` |
| `ad_purchase_date`              | Date and time the user first downloaded your app. In the case where `iadconversion-type = &#34;Redownload&#34;`, this represents the original purchase date. This may or may not have been associated with an Apple Search Ad. | `2016-12-05T17:31:40Z` |
| `ad_region`                     | Identifies the country or region associated with the campaign which drove this install.                                                                                                                                | `US` |
| `ad_user_clicked_last_30_days`  | Boolean indicating if user clicked on a Search Ads impression within 30 days prior to app download                                                                                                                     | `true` |
| `ad_user_conversion _type`      | Identifies new download or redownload of the app                                                                                                                                                                       | `Download` |
| `ad_user_date_clicked`          | Date and time the user clicked on a corresponding ad                                                                                                                                                                   | `2016-12-05T17:31:40Z` |
| `ad_user_date_converted`        | Date and time the user downloaded the app                                                                                                                                                                              | `2016-12-05T17:31:40Z` |
| `device_advertising_enabled`    | Boolean indicating if the user allowed ad tracking (if `false`, the advertising ID appears as a string of zeroes)                                                                                                      | `true` |
| `device_advertising_id`         | User-resettable advertising identifier (IDFA)                                                                                                                                                                          | `6D92078A-8246...` |
| `device_advertising_vendor_id`  | Unique ID guaranteed to be the same across all apps on the same device from a single vendor (apps with the same first two parts of the RDNS bundle identifier. For example, com.tealium or com.acme)                       | `6D92078A-8246...` |
| `device_tracking_authorization` | The tracking [authorization status](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus) that is added to the dispatch payload                                     | `authorized` |

### Autotracking Collector

The following variables are added to the data layer by the [`Autotracking`](/platforms/ios-swift/module-list/autotracking/) module.

| Variable Name | Description                                                | Example |
|:--------------|:-----------------------------------------------------------|:--------|
| `autotracked` | Set to `true` and added to each auto-tracked tracking call | `true`  |

### Collect Dispatcher

The following variables are added to the data layer by the [`Collect`](/platforms/ios-swift/module-list/collect/) dispatcher.

| Variable Name        | Description                                                        | Example |
|:---------------------|:-------------------------------------------------------------------|:--|
| `dispatch_service`   | Static string to indicate which module the tracking call came from | `collect` |
| `tealium_event_type` | String to indicate which event type is being dispatched            | `view` or `event` |

### Consent Manager Module

The following variables are added to the data layer by the [`ConsentManager`](/platforms/ios-swift/consent-management/) module if enabled.

| Variable Name        | Description                                                          | Example |
|:---------------------|:---------------------------------------------------------------------|:--|
| `consent_categories` | An array of the user&#39;s selected consent categories                   | `[&#34;analytics&#34;, &#34;cdp&#34;]` |
| `consent_status`     | The user&#39;s current consent status                                    | `consented`, `notConsented` |
| `policy`             | Consent Policy                                                       | `gdpr`, `ccpa` |
| `do_not_sell`        | Whether or not the user has asked not to sell their data (CCPA only) | `true` |

### Core

The following variables are added to the data layer by the `Core` module.

| Variable Name                  | Description                                                                                                                                         | Example |
|:-------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|:--|
| `enabled_modules`              | List of all currently-enabled modules                                                                                                               | `tagmanagement`, `collect` |
| `screen_title`                 | Screen title passed to trackView call                                                                                                               | `homescreen ` |
| `tealium_datasource`           | Specifies the data source name (added to every dispatch)                                                                                            | `a1b2c3` |
| `tealium_event`                | The name of the event being tracked                                                                                                                 | `checkout` |
| `queue_reason`                 | Added to the track call if the tracking request was queued due to lack of connectivity. Only present for queued events; absent for all other events | `connectivity` |
| `was_queued`                   | Indicates whether a tracking call was queued due to no connectivity. Only present for queued events; absent for all other events                    | `true` |
| `tealium_account`              | Current Tealium account (from TealiumConfig object)                                                                                                 | `tealium` |
| `tealium_environment`          | Current Tealium environment (from TealiumConfig object)                                                                                             | `dev` |
| `tealium_library_name`         | Tealium library name                                                                                                                                | `swift` |
| `tealium_library_version`      | Tealium library version                                                                                                                             | `1.8.0` |
| `tealium_profile`              | Current Tealium profile (from TealiumConfig object)                                                                                                 | `mobile` |
| `tealium_random`               | Random number                                                                                                                                       | `8449989974958830` |
| `tealium_session_id`           | Tealium Session ID                                                                                                                                  | `1511262829677` |
| `tealium_timestamp_epoch`      | Current Unix timestamp (1970 epoch) in seconds                                                                                                      | `1511262829` |
| `timestamp`                    | Event timestamp in ISO 8601 UTC                                                                                                         | `2017-11-20T14:48:00Z` |
| `timestamp_local`              | Event timestamp in ISO 8601 local timezone                                                                                                           | `2017-11-20T06:48:00` |
| `timestamp_offset`             | Current offset from UTC in hours                                                                                                                    | `-8` |
| `timestamp_unix`               | Current Unix timestamp (1970 epoch) in seconds                                                                                                      | `1511189280` |
| `timestamp_unix_milliseconds`  | Current Unix timestamp (1970 epoch) in milliseconds                                                                                                 | `1511189280337` |
| `deep_link_url`                | `String`                                                                                                                                            | The full URL of the deep link that opened the app, including query parameters. | `https://example.com/?campaign_code=SUMMER` |
| `deep_link_param_X`            | `String`                                                                                                                                            | Each query parameter of the deep link URL, where `X` is the name of the parameter, such as `deep_link_param_campaign_code`.| `SUMMER` |
| `deep_link_referrer_url` (iOS) | `String`                                                                                                                                            | The full URL of the browser page where the deep link was clicked. | `https://www.example.com/referring/page` |
| `deep_link_referrer_app` (iOS) | `String`                                                                                                                                            | The identifier of the referrer app when the deep link comes from a custom schema in another app signed by the same team. | `com.example.appId` |


### Crash Collector

The following variables are added to the data layer by the [`CrashReporter`](/platforms/ios-swift/module-list/crash-reporter/) module.

| Variable Name             | Description                                                           | Example |
|:--------------------------|:----------------------------------------------------------------------|:--|
| `app_memory_usage`        | Current memory used by the app on the device at the time of the crash | `143.57MB` |
| `crash_cause`             | Cause of the crash                                                    | `Crash Reason` |
| `crash_name`              | Friendly name of the crash, if available                              | `Crash Name` |
| `crash_libraries`         | List of loaded libraries at the time of the crash                     | `{ &#34;baseAddress&#34;: &#34;0xa3e0000&#34;, &#34;codeType&#34;: { &#34;arch&#34;: 64, &#34;typeEncoding&#34;: &#34;Mach&#34;}, &#34;imageName&#34;: &#34;/Applications/Xcode9.3.app/ Contents/Developer/Platforms/ iPhoneOS.platform/Developer/ Library/CoreSimulator/Profiles/ Runtimes/iOS.simruntime/ Contents/Resources/ RuntimeRoot/usr/lib/dyld_sim&#34;, &#34;imageSize&#34;: 212992, &#34;imageUuid&#34;: &#34;4015e9b70bde&#34; }` |
| `crash_process_id`        | PID of the app at time of crash                                       | `84351` |
| `crash_process_path`      | Path the app was running under                                        | `/DemoApp.app/DemoApp` |
| `crash_parent_process`    | Parent process that launched the app                                  | `launchd_sim` |
| `crash_parent_process_id` | Parent process PID                                                    | `83183` |
| `crash_signal_address`    | Signal address of the crash                                           | `4572945982` |
| `crash_signal_code`       | Signal code causing the crash                                         | `#0` |
| `crash_signal_name`       | Signal name causing the crash                                         | `SIGABRT` |
| `crash_threads`           | Returns all active threads at the time of the crash                   | `{&#34;crashed&#34;: 1,&#34;registers&#34;: {&#34;cs&#34;: &#34;0x07&#34;},&#34;stack&#34;: {&#34;instructionPointer&#34;: 4572945982,&#34;symbolInfo&#34;: {&#34;symbolName&#34;: &#34;&#34;,&#34;symbolStartAddr&#34;: 0},&#34;threadId&#34;: &#34;&#34;}}` |
| `crash_uuid`              | Unique identifier for this specific crash                             | `CC2DA0E9-E544-429A-AC5E-A268FC62F02A` |
| `device_memory_usage`     | Current memory used by the app on the device at the time of the crash | `143.57MB` |
| `device_memory_available` | Free memory on device at the time of the crash                        | `1068.88MB` |
| `device_os_build`         | Current OS build number                                               | `15E217` |
| `memory_free`             | Free memory on device at the time of the crash                        | `1068.88MB` |

### Device Data Collector

The following variables are added to the data layer by the [`DeviceData`](/platforms/ios-swift/module-list/device-data/) module.

| Variable Name                 | Description                                                                           | Example |
|:------------------------------|:--------------------------------------------------------------------------------------|:--|
| `app_memory_usage`            | Memory being used by the current process/app in Megabytes                             | `35.75MB` |
| `carrier`                     | Mobile network carrier name                                                           | `EE` |
| `carrier_iso`                 | Mobile carrier ISO                                                                    | `gb` |
| `carrier_mcc`                 | Carrier mobile country code                                                           | `234` |
| `carrier_mnc`                 | Carrier mobile network code                                                           | `34` |
| `connection_type`             | Current connection type                                                               | `wifi`, `cellular` |
| `device`                      | Consumer device name                                                                  | `iPhone 7 Plus` |
| `device_architecture`         | Device architecture                                                                   | `64` |
| `device_battery_percent`      | Current battery percentage at time of track call                                      | `58` |
| `device_cputype`              | Device CPU type                                                                       | `ARM64v8` |
| `device_ischarging`           | Boolean to indicate if device is currently charging at time of track call             | `true` |
| `device_language`             | Current device language                                                               | `en-US` |
| `device_orientation`          | Simple orientation                                                                    | `Portrait`, `Landscape` |
| `device_orientation_extended` | Full orientation                                                                      | `Face Up` |
| `device_os_version`           | Operating system version                                                              | `11.1` |
| `device_resolution`           | Physical screen resolution in pixels (width x height)                                 | `828x1792` |
| `device_logical_resolution`   | Logical screen resolution in points (width x height)                                  | `414x896` |
| `device_type`                 | Apple internal device identifier                                                      | `iPhone12,1` |
| `memory_active*`              | Total active memory on the device                                                     | `997.78MB` |
| `memory_compressed*`          | Total compressed memory on the device                                                 | `153.39MB` |
| `memory_free*`                | Total free memory on the device                                                       | `120.81MB` |
| `memory_inactive*`            | Total inactive memory on the device                                                   | `441.83MB` |
| `memory_physical*`            | Total physical memory on the device (RAM) in Megabytes                                | `2013.50MB` |
| `memory_wired*`               | Total wired memory on the device                                                      | `207.12MB` |
| `model_name`                  | Model name                                                                            | `iPhone 7 Plus` |
| `model_variant`               | Model variant (generally indicates which radio technology is available on the device) | `CDMA`, `GSM`, `WiFi`, `Cellular` |
| `network_iso_country_code`    | Mobile network ISO country code                                                       | `gb` |
| `os_name`                     | Operating System Name                                                                 | `iOS`, `tvOS`, `watchOS`, `macOS` |
| `platform`                    | Operating System Name                                                                 | `iOS`, `tvOS`, `watchOS`, `macOS` |


### Lifecycle Collector

The following variables are added to the data layer by the [`Lifecycle`](/platforms/ios-swift/module-list/lifecycle/) module.

| Variable Name                        | Description                                                                                                                              | Example |
|:-------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------|:--|
| `lifecycle_dayofweek_local`          | Local day of week that call was made, such as 1=Sunday, 2=Monday                                                                         | `4` |
| `lifecycle_dayssincelastwake`        | Days since last detected wake in integer increments                                                                                      | `1` |
| `lifecycle_dayssincelaunch`          | Days since first launch in integer increments                                                                                            | `23` |
| `lifecycle_dayssinceupdate`          | Days since the last detected app version update in integer increments                                                                    | `46` |
| `lifecycle_diddetect_crash`          | Was a crash detected during this launch/wake event (populated only if `true`)                                                            | `true` |
| `lifecycle_firstlaunchdate`          | GMT timestamp of the first detected launch/wake in ISO 8601 format from UTC                                                         | `2013-07-11T17:55:04Z` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | GMT Timestamp formatted as MM/DD/YYYY                                                                                                    | `01/17/2012 ` |
| `lifecycle_hourofday_local`          | Local hour of day that call was made (24 hour format)                                                                                    | `true` |
| `lifecycle_isfirstlaunch`            | Only present if call is the first launch/wake call                                                                                       | `true` |
| `lifecycle_isfirstlaunchupdate`      | Only present if call is first launch/wake after a detected updated                                                                       | `true`, `false` |
| `lifecycle_isfirstwakemonth`         | Only present if call is first launch/wake of the month                                                                                   | `true` |
| `lifecycle_isfirstwaketoday`         | Only present if call is first launch/wake of the day                                                                                     | `true` |
| `lifecycle_launchcount`              | Total number of launches this version of your app (since the last update)                                                                | `3` |
| `lifecycle_priorsecondsawake`        | Whole seconds app was awake since last launch only. Aggregates total from all wakes prior. Sent only with `lifecycle_type:launch` calls. | `126` |
| `lifecycle_secondsawake`             | Whole seconds app was awake since most recent wake/launch                                                                                | `30` |
| `lifecycle_sleepcount`               | Total number of times your app has gone to sleep (resets if updated)                                                                     | `5` |
| `lifecycle_totalcrashcount`          | Total number of crashes counted since install (only reset if app deleted)                                                                | `21` |
| `lifecycle_totallaunchcount`         | Total number of launches since install (only reset if app deleted)                                                                       | `3` |
| `lifecycle_totalsecondsawake`        | Total number of seconds your app has been in a woken/active state since app install (only reset if app deleted)                          | `36` |
| `lifecycle_totalsleepcount`          | Total number of times your app has gone into the background since app install (only reset if app deleted)                                | `400` |
| `lifecycle_totalwakecount`           | Total number of launches &#43; wakes since install (only reset if app deleted)                                                               | `563` |
| `lifecycle_type`                     | Type of lifecycle call.                                                                                                                  | `launch`, `wake`, `sleep` |
| `lifecycle_updatelaunchdate`         | GMT timestamp of first wake/launch after a version update has been detected                                                              | `2014-09-08T18:10:01Z` |
| `lifecycle_wakecount`                | Total number of launches &#43; wakes in this version of your app (resets if updated)                                                         | `29` |

### Location Collector

The following variables are added to the data layer by the [`Location`](/platforms/ios-swift/module-list/location/) module.

| Variable  Name             | Description                                                              | Example |
|:---------------------------|:-------------------------------------------------------------------------|:--|
| `geofence_name`            | The name of the geofence region                                          | `Tealium_San_Diego` |
| `geofence_transition_type` | The type of geofence transition event                                    | `entered`,`exited` |
| `location_timestamp`       | The recorded date/time (GMT) the user entered/exited the geofence region | `2020-01-28 16:29:46 &#43;0000` |
| `latitude`                 | The latitude of the user&#39;s most recently recorded location               | `32.906119` |
| `longitude`                | The longitude of the user&#39;s most recently recorded location              | `-117.23791632509666` |
| `movement_speed`           | The instantaneous speed of the device, measured in meters per second     | `1.0` |
| `location_accuracy`        | String	The accuracy setting for the location module                       | `high`, `low` |

### Tag Management

The following variables are added to the data layer by the [`Tag Management`](/platforms/ios-swift/module-list/tag-management/) module.

| Variable Name        | Description                                                        | Example |
|:---------------------|:-------------------------------------------------------------------|:--|
| `dispatch_service`   | Static string to indicate which module the tracking call came from | `tagmanagement` |
| `tealium_event_type` | String to indicate which event type is being dispatched            | `view` or `event` |

