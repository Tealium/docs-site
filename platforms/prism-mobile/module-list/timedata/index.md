---
title: TimeData module
description: Adds timestamp data to all tracking calls.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/timedata/
---
## Data layer

The following variables are added to each tracking call while the module is enabled:

| Variable | Description | Example |
| :--- | :--- | :--- |
| `tealium_timestamp_epoch` | Unix timestamp in seconds | `1746547200` |
| `tealium_timestamp_epoch_milliseconds` | Unix timestamp in milliseconds | `1746547200000` |
| `tealium_timestamp_local` | ISO 8601 local time | `&#34;2025-05-06T07:30:45&#34;` |
| `tealium_timestamp_local_with_offset` | ISO 8601 local time with timezone offset | `&#34;2025-05-06T07:30:45-07:00&#34;` |
| `tealium_timestamp_offset` | Timezone offset in decimal hours | `-7` |
| `tealium_timestamp_timezone` | Timezone identifier | `&#34;America/Los_Angeles&#34;` |
| `tealium_timestamp_utc` | ISO 8601 UTC time | `&#34;2025-05-06T14:30:45Z&#34;` |

## Install



Add the `prism-time-data` dependency to your `build.gradle` file:

```kotlin
implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
implementation(&#34;com.tealium.prism:prism-time-data&#34;)
```


Add `TealiumPrismTimeData` as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod &#39;tealium-prism/TimeData&#39;
```



## Initialize



```kotlin
val config = TealiumConfig.Builder(
    accountName = &#34;ACCOUNT&#34;,
    profileName = &#34;PROFILE&#34;,
    environment = Environment.PROD,
    modules = listOf(
        Modules.timeData(),
        // other modules...
    )
).build()
```


Configure the module programmatically by adding it to the modules parameter in `TealiumConfig`.

For more information about module settings, see [`TimeDataSettingsBuilder`](/tealium-prism-swift/timedata.html).

```swift
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;dev&#34;,
                           modules: [
                               Modules.timeData(forcingSettings: { builder in
                                   builder.setEnabled(true)
                                          .setOrder(1)
                                          .setRules(.just(&#34;rule_id_from_settings&#34;))
                               }),
                               // other modules...
                           ])
```


