---
title: VolatileData Module
description: Allows data variables to be stored in main memory (RAM). Data is stored and added to all dispatches/tracking calls until the app is restarted.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/volatile-data/
---
## Usage

The VolatileData module allows data variables to be stored in main memory (RAM). Data is stored and added to all dispatches/tracking calls until the app is restarted.

Usage of this module is mandatory. If you do not implement it, vital variables become missing from tracking calls.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Install

Install the VolatileData module with CocoaPods or Carthage.

### CocoaPods

To install the VolatileData module with CocoaPods, add the following pod to your Podfile:  

```ruby
pod &#39;tealium-swift/TealiumVolatileData&#39;
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.

### Carthage

To install the VolatileData module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```ruby
      TealiumVolatileData.framework
      ```
3. To store volatile data through the VolatileData API, add the following required import statement to your project:  
      ```swift
      import TealiumVolatileData
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Included Variables
| Variable              | Description                                             | Example    | Supported Platforms       |
|---------------------------|---------------------------------------------------------|------------------|---------------------------|
| `tealium_random`          | Random number                                           | `&#34;8449989974958830&#34;` | iOS, tvOS, watchOS, macOS |
| `tealium_session_id`      | Tealium Session ID                                      | `&#34;1511262829677&#34;` | iOS, tvOS, watchOS, macOS |
| `tealium_timestamp_epoch` | Current Unix timestamp (1970 epoch) in seconds                    | `&#34;1511262829&#34;` | iOS, tvOS, watchOS, macOS |
| `tealium_account`         | Current Tealium account (from TealiumConfig object)     | `&#34;tealium&#34;`          | iOS, tvOS, watchOS, macOS |
| `tealium_profile`         | Current Tealium profile (from TealiumConfig object)     | `&#34;mobile&#34;`           | iOS, tvOS, watchOS, macOS |
| `tealium_environment`     | Current Tealium environment (from TealiumConfig object) | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`]              | iOS, tvOS, watchOS, macOS |
| `tealium_library_name`    | Tealium library name                                    | `&#34;swift&#34;`            | iOS, tvOS, watchOS, macOS |
| `tealium_library_version` | Tealium library version                                 | `&#34;1.4.0&#34;`            | iOS, tvOS, watchOS, macOS |
| `event_timestamp_iso* `                  | Event timestamp in ISO 8601 UTC, UTC                                                   | `&#34;2017-11-20T14:48:00Z&#34;`      | iOS, tvOS, watchOS, macOS |
| `timestamp`                   | Event timestamp in ISO 8601 UTC, UTC                                                   | `&#34;2017-11-20T14:48:00Z&#34;`      | iOS, tvOS, watchOS, macOS |
| `event_timestamp_local_iso*`            | Event timestamp in ISO 8601 local timezone                                        | `&#34;2017-11-20T06:48:00&#34;`       | iOS, tvOS, watchOS, macOS |
| `timestamp_local`            | Event timestamp in ISO 8601 local timezone                                        | `&#34;2017-11-20T06:48:00&#34;`       | iOS, tvOS, watchOS, macOS |
| `event_timestamp_offset_hours*`           | Current offset from UTC in hours                                    | `-8`                        | iOS, tvOS, watchOS, macOS |
| `timestamp_offset`           | Current offset from UTC in hours                                                 | `-8`                        | iOS, tvOS, watchOS, macOS |
| `event_timestamp_unix_millis*`            | Current Unix timestamp (1970 epoch) in milliseconds                 | `1511189280337`             | iOS, tvOS, watchOS, macOS |
| `timestamp_unix_milliseconds`             | Current Unix timestamp (1970 epoch) in milliseconds                 | `1511189280337`             | iOS, tvOS, watchOS, macOS |
| `event_timestamp_unix*`             | Current Unix timestamp (1970 epoch) in seconds                            | `1511189280`             | iOS, tvOS, watchOS, macOS |
| `timestamp_unix`             | Current Unix timestamp (1970 epoch) in seconds                                   | `1511189280`             | iOS, tvOS, watchOS, macOS |

## API Reference

See the [`TealiumVolatileData`](/platforms/ios-swift-v1/api/tealium-volatile-data/) class in the iOS (Swift) API.
