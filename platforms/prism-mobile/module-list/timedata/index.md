---
title: TimeData module
description: Adds timestamp data to all tracking calls.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/timedata/
---
The TimeData module adds timestamp and timezone information to every tracking call.

## Data layer

The following variables are added to each tracking call while the module is enabled:

| Variable | Description | Example |
| :--- | :--- | :--- |
| `tealium_timestamp_epoch` | Unix timestamp in seconds | `1746547200` |
| `tealium_timestamp_epoch_milliseconds` | Unix timestamp in milliseconds | `1746547200000` |
| `tealium_timestamp_local` | ISO 8601 local time | `"2025-05-06T07:30:45"` |
| `tealium_timestamp_local_with_offset` | ISO 8601 local time with timezone offset | `"2025-05-06T07:30:45-07:00"` |
| `tealium_timestamp_offset` | Timezone offset in decimal hours | `-7` |
| `tealium_timestamp_timezone` | Timezone identifier | `"America/Los_Angeles"` |
| `tealium_timestamp_utc` | ISO 8601 UTC time | `"2025-05-06T14:30:45Z"` |

## Install



Add the `prism-time-data` dependency to your `build.gradle` file:

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-time-data")
```


Add `TealiumPrismTimeData` as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod 'tealium-prism/TimeData'
```



## Initialize



```kotlin
val config = TealiumConfig.Builder(
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.timeData(),
        // other modules...
    )
).build()
```


Configure the module programmatically by adding it to the modules parameter in `TealiumConfig`.

For more information about module settings, see [`TimeDataSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/timedata.html).

```swift
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "dev",
                           modules: [
                               Modules.timeData(forcingSettings: { builder in
                                   builder.setEnabled(true)
                                          .setOrder(1)
                                          .setRules(.just("rule_id_from_settings"))
                               }),
                               // other modules...
                           ])
```


