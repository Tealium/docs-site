---
title: Collectors Module
description: Learn about the different data collectors available in the Tealium Kotlin library to include in your app.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/collectors/
---
## Usage

Collectors modules are available in the core library. The data gathered from each Collector module is added to the data layer and sent in each track call. Usage of these collectors is recommended, but not required. Excluding a collector omits the data variables from your data layer for that given collector.

To add a Collector module to your app implementation, add a `collectors` parameter when creating the `TealiumConfig` instance:

```kotlin
val config = TealiumConfig(application,
                 &#34;ACCOUNT&#34;,
                 &#34;PROFILE&#34;,
                 Environment.DEV,
                 collectors = mutableSetOf(
                     Collectors.Tealium,
                     Collectors.Time,
                     Collectors.App,
                     Collectors.Device,
                     Collectors.Connectivity
                 )
          )
```

### Tealium Collector

Gathers information about your Tealium account.

| Variable Name | Description | Example |
| --- | --- | --- |
| `tealium_account` | Tealium account name from `TealiumConfig` | `tealium` |
| `tealium_profile` | Tealium profile name from `TealiumConfig` | `mobile` |
| `tealium_environment` | Tealium environment from `TealiumConfig` | `dev` |
| `tealium_datasource`| Identifies Tealium data source name from `TealiumConfig` | `abc123` |
| `tealium_visitor_id` | Tealium visitor ID | `t3aL...1uM` |
| `tealium_random` | A random number for each event | `1234567890` |
| `was_queued` | Indicates whether this event was ever queued on the device | `true` |

### App Collector

Gathers information about your app package.

| Variable Name | Description | Example |
| --- | --- | --- |
| `app_build` | App build version | `1`|
| `app_name` | Application name (from the [application manifest attribute `android:label`](https://developer.android.com/guide/topics/manifest/application-element.html#label)) | `My App`|
| `app_memory_usage` | Memory (MB) in use by app process | `57` |
| `app_rdns` | Reverse DNS application ID (from the [root manifest attribute `package`](https://developer.android.com/guide/topics/manifest/manifest-element.html)) | `com.example.myapp` |
| `app_uuid` | Random `uuid`. Persists for the duration of the app install, so long as one of the persistent storage modules is also enabled. Resets if app is uninstalled. | `123e4567-e89b-12d3-a456-556642440000`|
| `app_version` | Application version | `version 1.0`|

### Connectivity Collector

Gathers information about device network and carrier.

| Variable Name | Description | Example |
| --- | --- | --- |
| `carrier` | The device&#39;s mobile carrier | `Verizon` |
| `carrier_iso` | Carrier ISO country code| `gb` |
| `carrier_mcc` | Mobile country code| `ITU-T Recommendation E.212` |
| `carrier_mnc` | Mobile network code | `34` |
| `connection_type` | Connection type | `wifi` |

### Device Collector

Gathers information about your user&#39;s device.

| Variable Name | Description | Example |
| --- | --- | --- |
| `device` | Retail device name (manufacturer&#43;model) | `Google Pixel 8`, `Sony Xperia 1 V` |
| `device_android_runtime` | Android Runtime version | `2.1.0` |
| `device_architecture` | Bit architecture of the device | `64` |
| `device_battery_percent` | Integer percent representation of device&#39;s remaining power | `50` |
| `device_cputype` | CPU type | `arm7s` |
| `device_free_external_storage` | Total available external storage on device | |
| `device_free_system_storage` | Total available storage on device |`273772544` |
| `device_ischarging` | Indicates whether the device is actively charging | `true`, `false` |
| `device_language` | Two-letter ISO 639-1 language setting identifier | `en` |
| `device_logical_resolution` | Logical screen resolution in points (width x height) | `414x896` |
| `device_manufacturer` | The manufacturer of the product/hardware | `Google`, `Sony` |
| `device_model` | The end-user-visible name for the end product | `Pixel 8`, `Xperia 1 V` |
| `device_orientation` | Orientation of device at time of call | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, `Unknown` |
| `device_os_build` | Operating System build version | `4499259` |
| `device_os_version` | Operating System version on device | `7.0` |
| `device_resolution` | Display resolution size in pixels | `1920x1080` |
| `origin` | Constant used in mapping to distinguish mobile from web implementations | `mobile` |
| `os_name` | The name of the operating system | `Android` |
| `platform` | Mobile platform | `android` |

### Time Collector

Gathers timestamps information when a track call occurs.

| Variable Name | Description | Example |
| --- | --- | --- |
| `timestamp` | Timestamp to seconds of event occurrence [ISO 8601 at UTC] | `2013-07-11T19:57:47Z` |
| `timestamp_local` | Local Timestamp to seconds of event occurrence (ISO 8601 without offset) | `2013-07-11T19:57:47` |
| `timestamp_offset` | Local timezone offset of device&#39;s location in hours | `-3` |
| `timestamp_unix` | GMT/UTC Unix timestamp of event occurrence |`1373498679` |
| `timestamp_unix_milliseconds` | 5.5.1 | GMT/UTC Unix timestamp in milliseconds of event occurrence | `1373498679123` |
