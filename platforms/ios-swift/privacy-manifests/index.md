---
title: Privacy Manifests on iOS
description: This article describes Privacy Manifests and how to comply with Apple's new requirements while using the Tealium libraries.
url: https://docs.tealium.com/platforms/ios-swift/privacy-manifests/
---
## Apple Privacy Manifest files

Apple Privacy Manifests are files that allow an app to declare potentially privacy-impacting APIs that it uses. Apple introduced Privacy Manifest files to help app developers be more transparent to their users regarding the privacy-sensitive data that they collect and the privacy-sensitive APIs that their app uses. In addition to apps, third-party SDKs also have the ability to implement privacy manifest files. For more information, see [App privacy details on the App Store](https://developer.apple.com/app-store/app-privacy-details) and [Privacy Manifest files](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files) at Apple.

## Tealium privacy manifest

Tealium Swift SDK version 2.12.0 and later include [a privacy manifest](https://github.com/Tealium/tealium-swift/blob/main/tealium/core/PrivacyInfo.xcprivacy), which highlights the required reason APIs used by the Tealium Swift SDK. 

### Required Reason APIs

The Tealium Swift SDK uses 2 APIs from the "Required Reason" list: User Defaults and Disk Space. These are included in the privacy manifest distributed with the SDK, and their usage is within the scope of the allowed reasons.

Apps might use "Required Reason" APIs for their own purposes, which app developers must specify in their own privacy manifests.

### Data collection definition

In the [Data Collection section of App privacy details on the App Store](https://developer.apple.com/app-store/app-privacy-details/#data-collection), Apple defines the term *collect* as:

> “Collect” refers to transmitting data off the device in a way that allows you and/or your third-party partners to access it for a period longer than what is necessary to service the transmitted request in real time.

In addition to this definition, Apple elaborates in the [Additional Guidance section](https://developer.apple.com/app-store/app-privacy-details/#additional-guidance):

> "Collect" refers to transmitting data off the device and storing it in a readable form for longer than the time it takes you and/or your third-party partners to service the request. For example, if an authentication token or IP address is sent on a server call and not retained, or if data is sent to your servers then immediately discarded after servicing the request, you do not need to disclose this in your answers in App Store Connect.

According to this definition, data is "collected" only if it is stored in a readable format for longer than it takes to service a request. Following this definition, none of the data that is sent by the Tealium SDK is being collected by our SDK. Therefore, no data use has been reported in our privacy manifest.

However, Tealium's product offering is diverse, and in some cases it is possible that Tealium customers could be "collecting" data according to Apple's definition. For example, if a Tealium customer decided to save an app user's IP address in their visitor profile in Audiencestream or store it for later use through some Event Stream Connector, this action would fall under the "Collect" definition. Tealium customers are ultimately responsible for determining if they are collecting any data and disclosing this behavior in their own privacy manifest. Tealium customers should also check if they are sending any data to third parties through EventStream or AudienceStream that might fall into the "collect" definition

When deciding what to declare in your app's privacy manifest, you should consider data that is automatically sent by the Tealium Swift SDK, as well as other types of data that the app is collecting and through the Tealium Swift SDK. The only exception would be if the impacted data is stripped out (for example, using a transformation or extension) before being stored.

### Tracking definition

In the [Tracking](https://developer.apple.com/app-store/app-privacy-details/#user-tracking) section of App privacy details on the App Store, Apple  defines the term *tracking* as:

> “Tracking” refers to linking data collected from your app about a particular end-user or device, such as a user ID, device ID, or profile, with Third-Party Data for targeted advertising or advertising measurement purposes, or sharing data collected from your app about a particular end-user or device with a data broker.

> “Third-Party Data” refers to any data about a particular end-user or device collected from apps, websites, or offline properties not owned by you.

## Data use by TealiumSwift library

Due to the flexibility of the Tealium SDKs, and the fact that Tealium cannot dictate what data Tealium customers choose to send or collect, it's not possible to provide a generic privacy manifest for all apps. The APIs included in the bundled privacy manifest are the minimum required to use the SDKs, and Tealium customers may need additional privacy manifest entries, depending on how they are using the data the SDK sends.

The following tables list the data that is sent by the Tealium Swift SDK, divided by modules with relative sections as defined by Apple. Tealium customers can add the sections that include the data that they actually collect from the modules that they use.


<blockquote>
You do not need to report all of these categories, unless the data sent to the CDP is actually stored or sent to a third party that stores or sells it.
</blockquote>


### Tealium Core

|Data Key|Description|Apple Data Type|
|--|--|--|
| `tealium_event` | Event sent to track the user activity in the app | `NSPrivacyCollectedDataTypeProductInteraction` |
| `screen_title` | The page that the user is viewing | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_name` | An event to which we are tracking the time to complete | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_start` | The start of an event duration timing | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_end` | The end of an event duration timing | `NSPrivacyCollectedDataTypeProductInteraction` |
| `timed_event_duration` | The duration of an event timing | `NSPrivacyCollectedDataTypeProductInteraction` |
| `tealium_visitor_id` | The ID used for AudienceStream | `NSPrivacyCollectedDataTypeUserID` |
| `app_uuid` | A constant ID for an App installed on a specific device | `NSPrivacyCollectedDataTypeDeviceID` |
| `device_battery_percent` | Current battery charge percentage | `NSPrivacyCollectedDataTypePerformanceData` |
| `app_memory_usage` | How much memory is the app using | `NSPrivacyCollectedDataTypePerformanceData` |
| `memory_free` | How much memory is available | `NSPrivacyCollectedDataTypePerformanceData` |
| `device_ischarging` | If the device is charging | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_active` | If the memory is active | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_inactive` | If the memory is inactive | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_compressed` | If the memory is compressed | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_wired` | If the memory is wired | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `memory_physical` | If the memory is physical | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_orientation` | The device orientation | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_orientation_extended` | The extended device orientation | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `model_name` | The device model | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `model_variant` | The device variant | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_type` | The device type | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_architecture` | The device architecture | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_cputype` | The device CPU type | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_language` | The device language | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `os_name` | The OS name | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_build` | The app build number | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_name` | The app name | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_rdns` | The app RDNS | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `app_version` | The app version | `NSPrivacyCollectedDataTypeOtherDiagnosticData` |
| `device_resolution` | The device resolution | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `device_logical_resolution` | The device logical resolution | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_url` | The deeplink URL | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_param` | Each deeplink's query parameters | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_referrer_url` | The deeplink referrer URL | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `deep_link_referrer_app` | The deeplink referrer app | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier` | The carrier | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier_mnc` | The carrier MNC | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier_mcc` | The carrier MCC | `NSPrivacyCollectedDataTypeOtherDataTypes` |
| `carrier_iso` | The carrier ISO | `NSPrivacyCollectedDataTypeOtherDataTypes` |

### Tealium Attribution

|Data Key|Description|Apple Data Type|
|--|--|--|
| `device_advertising_id` | The IDFA | `NSPrivacyCollectedDataTypeDeviceID` |
| `device_advertising_vendor_id` | The IDFV | `NSPrivacyCollectedDataTypeDeviceID` |

### Tealium Location

|Data Key|Description|Apple Data Type|
|--|--|--|
| `latitude` | The latitude (precision based on configuration) | `NSPrivacyCollectedDataTypePreciseLocation` or `NSPrivacyCollectedDataTypeCoarseLocation` |
| `longitude` | The longitude (precision based on configuration) | `NSPrivacyCollectedDataTypePreciseLocation` or `NSPrivacyCollectedDataTypeCoarseLocation` |
| `geofence_name` | The geofences that are entered or exited by the user | `NSPrivacyCollectedDataTypeCoarseLocation` |

### Tealium Crash

|Data Key|Description|Apple Data Type|
|--|--|--|
| `crash_count` | The amount of crashes occurred for this app on this device | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_threads` | The crash threads | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_libraries` | The crash libraries  | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_signal_address` | The crash signal address | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_signal_name` | The crash signal name | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_signal_code` | The crash signal code | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_name` | The crash name | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_parent_process_id` | The crash parent process ID | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_parent_process` | The crash parent process | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_process_path` | The crash process path | `NSPrivacyCollectedDataTypeCrashData` |
| `crash_process_id` | The crash process ID | `NSPrivacyCollectedDataTypeCrashData` |
| `device_os_build` | The device OS build | `NSPrivacyCollectedDataTypeCrashData` |

### Tealium Lifecycle

|Data Key|Description|Apple Data Type|
|--|--|--|
| `lifecycle_type` | The lifecycle event type | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayofweek_local` | The lifecycle event's current day of the week | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayssincelaunch` | The lifecycle event's count of days since the first launch  | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayssinceupdate` | The lifecycle event's count of days since the last update | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_dayssincelastwake` | The lifecycle event's count of days since the last wake | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_diddetectcrash` | If the lifecycle detected a crash | `NSPrivacyCollectedDataTypeCrashData` |
| `lifecycle_firstlaunchdate` | The first launch date | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | The first launch date | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_hourofday_local` | The lifecycle event's hours of day | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstlaunch` | If the lifecycle event is a first launch | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstlaunchupdate` | If the lifecycle event is the first launch after an update | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstwakemonth` | If the lifecycle event is the first wake of the month | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_isfirstwaketoday` | If the lifecycle event is the first wake of the day | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastlaunchdate` | The lifecycle event's last launch date | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastsleepdate` | The lifecycle event's last sleep date | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastwakedate` | The lifecycle event's last wake date | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_lastupdatedate` | The lifecycle event's last update date | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_launchcount` | The lifecycle event's launches count | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_priorsecondsawake` | The lifecycle event's seconds of awake on last launch | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_secondsawake` | The lifecycle event's seconds being awake count | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_sleepcount` | The lifecycle event's count of sleeps | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalcrashcount` | The lifecycle event's total crash count | `NSPrivacyCollectedDataTypeCrashData` |
| `lifecycle_totallaunchcount` | The lifecycle event's total launch count | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalwakecount` | The lifecycle event's total wake count | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalsleepcount` | The lifecycle event's total sleep count | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_totalsecondsawake` | The lifecycle event's total seconds being awake | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_updatelaunchdate` | The lifecycle event's first launch after last update date | `NSPrivacyCollectedDataTypeProductInteraction` |
| `lifecycle_wakecount` | The lifecycle event's wake count | `NSPrivacyCollectedDataTypeProductInteraction` |

## Examples

The following examples demonstrate use cases in which data is sent by the Tealium Swift SDK and which types of data should be reported in privacy manifests.


<blockquote>
An app might send more data than what is automatically sent by the Tealium Swift SDK, whether by adding it to the DataLayer or by enriching the track requests with more data. Therefore, this list of data types is not an exhaustive list of everything an app might need to report.
</blockquote>


For each data type that the app is collecting and must be reported, you must also specify the reason for collecting them. You must also specify if the data is specifically linked to the visitor or if it is used for tracking. For more information, see [Report the reasons your app or third-party SDK collects data](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests#4250556) on Apple's Developer site.

### Audience Stream use case

An app using AudienceStream uses the `tealium_visitor_id` variable to store and fetch the visitor profile, and may use the `tealium_event` and `screen_name` variables to detect what is the visitor doing inside of the app. AudienceStream changes the visitor profile according to those events and screens the visitor navigated to.

This app might also use the Lifecycle module to infer some information about the visitor, such as how often and for how long the visitor has been using the app.

Finally, this app uses location data to determine the generic location of the visitor and establish the country they live in, which AudienceStream saves in the visitor profile.

With those use cases in mind, we can determine the `NSPrivacyCollectedDataType` data objects they should report in their manifest files:

* `NSPrivacyCollectedDataTypeUserID`
* `NSPrivacyCollectedDataTypeProductInteraction`
* `NSPrivacyCollectedDataTypeCoarseLocation`

### Event DB use case

An app using EventDB and storing everything that is sent from the SDK, without stripping anything from the data layer with extension or transformation, must report all of the data types for all of the modules that it uses. 

If the app is using only Core and Attribution modules, the manifest file must include:

* `NSPrivacyCollectedDataTypeProductInteraction`
* `NSPrivacyCollectedDataTypeUserID`
* `NSPrivacyCollectedDataTypeDeviceID`
* `NSPrivacyCollectedDataTypePerformanceData`
* `NSPrivacyCollectedDataTypeOtherDiagnosticData`
* `NSPrivacyCollectedDataTypeOtherDataTypes`

If the app also uses the Location, Crash, and Lifecyle modules, the manifest file must also include:

* `NSPrivacyCollectedDataTypeCoarseLocation` and/or `NSPrivacyCollectedDataTypePreciseLocation`
* `NSPrivacyCollectedDataTypeCrashData`

## Tracking and TrackingDomains

The app privacy manifest files includes two more properties that might be related to Tealium:

* `NSPrivacyTracking`
* `NSPrivacyTrackingDomains`

These two properties refer to Apple's definition of tracking, so they do not include Tealium's SDK activity. However, some Tealium customers may still be tracking visitors with the data that is sent through the Tealium Swift SDK. In such cases, it might be required to specify Tealium's domain as a tracking domain, and that their app is actively tracking their visitors. 

If you list Tealium's domain as tracking domain, Apple will actively block Tealium from receiving tracking data for visitors who deny the authorization for tracking.

If the tracking happens only through a specific vendor tag or a RemoteCommand, then add the vendor's tracking endpoint to the list of tracking domains instead of Tealium's domain. This practice allows all the other Tealium functionality to work as expected, even if the visitor denied the authorization.

