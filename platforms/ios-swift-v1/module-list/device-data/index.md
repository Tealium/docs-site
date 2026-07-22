---
title: DeviceData Module
description: Gathers information about the current device and adds to the tracking call/dispatch.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/device-data/
---## Usage
The DeviceData module gathers information about the current device and adds to the tracking call/dispatch. Usage of this module is recommended.

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

Install the DeviceData module with CocoaPods or Carthage.

### CocoaPods

To install the DeviceData module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod 'tealium-swift/TealiumDeviceData'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.


### Carthage

To install the DeviceData module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```ruby
      TealiumDeviceData.framework
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable Name | Description  | Example |
|---|---| --- |
| `app_memory_usage`   | Memory being used by the current process/app in Megabytes| `35.75MB`          |
| `app_orientation`    | Orientation of the app (from statusBarOrientation; may differ from device orientation if app is locked in a specific orientation)| `Portrait`       |
| `app_orientation_ extended` | Extended Orientation of the app (from statusBarOrientation; may differ from device orientation if app is locked in a specific orientation)| `Portrait Upside Down` |
| `battery_percent`            | Current battery percentage at time of track call| `58`|
| `carrier`                    | Mobile network carrier name| `EE`|
| `carrier_iso`                | Mobile network ISO country code| `gb`|
| `carrier_mcc`                | [Mobile network country code](https://en.wikipedia.org/wiki/Mobilecountrycode)| `234`|
| `carrier_mnc`                | [Mobile network code](https://en.wikipedia.org/wiki/Mobilecountrycode)| `34`|
| `connection_type`           | Current connection type| [`wifi`, `cellular`]|
| `cpu_architecture`           | CPU architecture| `64`|
| `cpu_type`                   | CPU type| `ARM64v8`|
| `device_battery_percent`     | Current battery percentage at time of track call| `58`|
| `device_architecture`        | CPU architecture| `64`|
| `device`                     | Consumer device name| `iPhone 7 Plus`|
| `device_cputype`             | CPU type| `ARM64v8`|
| `device_is_charging`         | Boolean to indicate if device is currently charging at time of track call| [`true`, `false`]|
| `device_language`            | Current device language| `en`|
| `device_orientation`         | Simple orientation| [`Portrait`, `Landscape`]|
| `device_orientation_ extended`| Full orientation| `Face Up`|
| `device_os_version`          | Operating system version| `11.1`|
| `device_resolution`          | Screen resolution| `1080x1920`|
| `device_type`            | Apple internal device identifier| `iPhone8,4`|
| `memory_active*`             | Total active memory on the device| `997.78MB`|
| `memory_compressed*`         | Total compressed memory on the device| `153.39MB`|
| `memory_free*`               | Total free memory on the device| `120.81MB`|
| `memory_inactive*`           | Total inactive memory on the device| `441.83MB`|
| `memory_physical*`           | Total physical memory on the device (RAM) in Megabytes| `2013.50MB`|
| `memory_wired*`              | Total wired memory on the device| `207.12MB`|
| `model_name`                 | Consumer device name| `iPhone 7 Plus`|
| `model_variant`              | Model variant (generally indicates which radio technology is available on the device)| [`CDMA`, `GSM`, `WiFi`, `Cellular`]|
| `network_connection_ type`    | Current connection type| [`wifi`, `cellular`]|
| `network_iso_ country_code`   | Mobile network ISO country code| `gb`|
| `network_mcc`                | [Mobile network Country Code](https://en.wikipedia.org/wiki/Mobilecountrycode)| `234`|
| `network_mnc`                | [Mobile network code](https://en.wikipedia.org/wiki/Mobilecountrycode)| `34`|
| `network_name`               | Mobile network carrier name| `EE`|
| `os_build`                   | Operating System Build Version| `15J580`|
| `os_name`                    | Operating System Name| [`iOS`, `tvOS`, `watchOS`, `macOS`]|
| `os_version`                 | Operating system version| `11.1`|
| `platform`                   | Operating System Name| [`iOS`, `tvOS`, `watchOS`, `macOS`]|
| `user_locale`                | Current device language| `en`|

* These variables are only transmitted if you explicitly enable memory data collection with the `TealiumConfig` object. They are disabled by default.
* These variables are duplicated for backward-compatibility with previous releases.
