---
title: Data Layer
description: Learn the differences between versions 4.x and 5.x of the Tealium for iOS libraries and how to migrate to the latest version.
url: https://docs.tealium.com/platforms/ios-objective-c/data-layer/
---The following variables are populated by the Tealium iOS Library as part of the mobile data layer. These variables are included automatically in each tracking call from the library and used in your iQ or Tealium EventStream configurations.

Addition variables are available in the [Lifecycle Tracking Module](/platforms/ios-objective-c/module-list/lifecycle-tracking/) for 5.0.x.

| Variable | iOS Version | Description | Example |
| --- | --- | --- | --- |
| `app_name` | 1.0&#43; | Application name. | [any string] |
| `app_rdns` | 3.2&#43; | Reverse DNS Bundle Id/Package ID. | `com.tealium.sampleApp` |
| `app_uuid` | 5.1&#43; | (Universally Unique Identifier) Unique for each installation of an app on a device (was formerly uuid). | [any string] |
| `app_version` | 1.0&#43; | Application version. | [any string] |
| `call_type` | 2.2&#43; | Call type. | [`view`, `link`]|
| `carrier` | 2.0&#43; | Carrier device is currently on. | `Verizon` |
| `carrier_iso` | 2.2&#43; | Carrier iso country code. | `ISO 3166-1` |
| `carrier_mcc` | 2.2&#43; | Mobile country code.| `ITU-T Recommendation E.212` |
| `carrier_mnc` | 2.2&#43; | Mobile network code. | |
| `connection_type` | 1.0&#43; | Connection type. | `wifi`|
| `device` | 1.0&#43; | iphone |
| `device_architecture` | 3.2&#43; | Bit architecture of the device. |`64` |
| `device_battery_percent` | 4.0&#43; | Whole number percent representation of device&#39;s remaining power. |`50` |
| `device_cputype` | 3.2&#43; | CPU type. | `arm7s` |
| `device_ischarging` | 4.0&#43; | Is the device actively charging? | [`true`, `false`] |
| `device_language` | 3.2&#43; | Two-letter ISO 639-1 language setting identifier., |`en` |
| `device_orientation` | 5.0&#43; | Orientation of device at time of call. | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, or `Unknown` |
| `device_os_version` | 5.0&#43; | Operating System version on device.| `7.0` |
| `event_name` | 5.0&#43; | `mobile_link` required by vdata. | [any string]|
| `library_version` | 2.0&#43; | The version of the Tealium library your app has installed. | |
| `link_id` | 1.0&#43; | (EVENT CALLS ONLY) General event or link title - such as a button title or an object&#39;s Tealium ID. | [any string] |
| `~~orientation~~` | 2.0&#43; | **DEPRECATED** Orientation of device at time of call. | `Portrait`, `Landscape Left`, `Landscape Right`, `Portrait UpsideDown`, `Face Up`, `Face Down`, or `Unknown` |
| `origin` | 3.2&#43; | Constant used in mapping to distinguish mobile from web implementations.  | `mobile` |
| `os_version` | 1.0&#43; | Operating System version on device. | `7.0` |
| `page_type` | 5.0&#43; | &#34;mobile_view&#34; constant used in mapping to distinguish mobile view / page changes from mobile or web events - required by vdata. | |
| `platform` | 1.0&#43; | Platform of device | `iOS` |
| `screen_title` | 1.0&#43; | (VIEW CALLS ONLY) General view title. | [any string] |
| `timestamp` | 2.0&#43; | Timestamp to seconds of event occurrence. | `2013-07-11T19:57:47Z` [ISO 8601 at UTC] |
| `timestamp_local` | 2.2&#43; | Local Timestamp to seconds of event occurrence. | `2013-07-11T19:57:47` [ISO 8601 without offset] |
| `timestamp_offset` | 2.2&#43; | Local timezone offset of device&#39;s location in hours. | `-3` |
| `timestamp_unix` | 2.2&#43; | GMT/UTC Unix timestamp of any occurrence. | `1373498679` |
| `timestamp_unix_milliseconds` |  5.4.5&#43; |  GMT/UTC Unix timestamp in milliseconds of event occurrence. | `1373498679123` |
| `visitor_id` | 5.0&#43; | Tealium-generated visitor ID. | |
| `was_queued` | 4.1&#43; | Whether this dispatch was queued or batched prior to sending. | [`true`, `false`] |
