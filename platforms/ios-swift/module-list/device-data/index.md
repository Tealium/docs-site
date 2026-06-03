---
title: DeviceData Module
description: Adds information about the device to the data layer.
url: https://docs.tealium.com/platforms/ios-swift/module-list/device-data/
---
## Usage
The DeviceData module gathers information about the current device and adds it to the data layer. Usage of this module is recommended.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Requirements

* UIKit
* Darwin
* CoreTelephony
* WatchKit

## Install

This module is included as part of the Core library and does not require separate installation.

## Initialize

To initialize the module, verify that it&#39;s specified on the `TealiumConfig` [`collectors`](/platforms/ios-swift/api/tealium-config/#collectors) property

```swift
config.collectors = [Collectors.DeviceData]
```

Review the [Collectors](/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.

## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable Name | Description  | Example |
|---|---| --- |
| `app_memory_usage`   | Memory being used by the current process/app in Megabytes| `35.75MB`|
| `carrier`                    | Mobile network carrier name| `EE`|
| `carrier_iso`                | Mobile carrier ISO| `gb`|
| `carrier_mcc`                | Carrier mobile country code| `234`|
| `carrier_mnc`                | Carrier mobile network code| `34`|
| `connection_type`            | Current connection type| `wifi`, `cellular`|
| `device`                     | Consumer device name| `iPhone 7 Plus`|
| `device_architecture`        | Device architecture| `64`|
| `device_battery_percent`     | Current battery percentage at time of track call| `58`|
| `device_cputype`             | Device CPU type| `ARM64v8`|
| `device_ischarging`          | Boolean to indicate if device is currently charging at time of track call| `true`|
| `device_language`            | Current device language| `en-US`|
| `device_logical_resolution`            | Screen dimensions in points (not pixels)| `430x932`|
| `device_manufacturer`            | Product/hardware manufacturer| `Apple`|
| `device_orientation`         | Simple orientation| `Portrait`, `Landscape`|
| `device_orientation_extended`| Full orientation| `Face Up`|
| `device_os_build`          | Operating system build| `20A372`|
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
| `model_variant`              | Model variant (generally indicates which radio technology is available on the device)| `CDMA`, `GSM`, `WiFi`, `Cellular`|
| `network_iso_country_code`   | Mobile network ISO country code| `gb`|
| `os_name`                    | Operating System Name| `iOS`, `tvOS`, `watchOS`, `macOS`|
| `platform`                   | Operating System Name (lowercased)| `ios`, `tvos`, `watchos`, `macos`|

\* These variables are only transmitted if you explicitly enable memory data collection through the `TealiumConfig` object. They are disabled by default.
