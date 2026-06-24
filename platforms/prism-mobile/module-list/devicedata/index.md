---
title: DeviceData module
description: Automatically adds device information to all tracking events.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/devicedata/
---
The DeviceData module gathers static device characteristics such as model, CPU type, and OS version, as well as dynamic information such as battery status and screen orientation, and makes them available to all tracking events.

## Data layer

### Device

The following device attributes are added to each tracking call while the module is enabled:

| Variable | Description | Example |
| :--- | :--- | :--- |
| `device` | Consumer device name | `&#34;iPhone 13 Pro Max&#34;` |
| `device_architecture` | CPU architecture | `&#34;64&#34;` |
| `device_cputype` | Detailed CPU type | `&#34;ARM64e&#34;` |
| `device_language` | Primary device language | `&#34;en-US&#34;` |
| `device_manufacturer` | Device manufacturer | `&#34;Apple&#34;` |
| `device_model` | Consumer device name | `&#34;iPhone 13 Pro Max&#34;` |
| `device_os_build` | OS build number | `&#34;20A372&#34;` |
| `device_os_version` | Operating system version | `&#34;17.0&#34;` |
| `device_type` | Platform model identifier | `&#34;iPhone14,3&#34;` |
| `model_variant` | Model variant identifier | `&#34;A2484&#34;` |
| `origin` | Device category | `&#34;mobile&#34;` |
| `os_name` | Operating system name | `&#34;iOS&#34;` |
| `platform` | Lowercase OS name | `&#34;ios&#34;` |


### Battery and screen

The following battery and screen attributes can be enabled or disabled based on your builder settings. For more information, see [Initialize](#initialize).

| Variable | Description | Example |
| :--- | :--- | :--- |
| `device_battery_percent` | (iOS only) Battery charge percentage | `&#34;58&#34;` |
| `device_ischarging` | (iOS only) Whether the device is charging | `&#34;true&#34;` |
| `device_logical_resolution` | Logical screen resolution | `&#34;390x844&#34;` |
| `device_orientation` | Device orientation | `&#34;Portrait&#34;` |
| `device_orientation_extended` | Detailed orientation | `&#34;Face Up&#34;` |
| `device_resolution` | Physical screen resolution | `&#34;1170x2532&#34;` |

### Memory (iOS only)

iOS apps can enable attributes to track memory usage. These memory attributes are disabled by default. For more information, see [Initialize](#initialize).

| Variable | Description |
| :--- | :--- |
| `memory_active` | Active memory |
| `memory_compressed` | Compressed memory |
| `memory_free` | Free memory |
| `memory_inactive` | Inactive memory |
| `memory_physical` | Total physical memory (RAM) |
| `memory_wired` | Wired memory |

## Install



Add the `prism-device-data` dependency to your `build.gradle` file:

```kotlin
implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
implementation(&#34;com.tealium.prism:prism-device-data&#34;)
```


Add `TealiumPrismDeviceData` as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod &#39;tealium-prism/DeviceData&#39;
```



## Initialize

The DeviceData module initializes automatically when it is configured. No code changes are required for most integrations. Configure the module in the Tealium platform UI, or bundle a local JSON configuration file with your app.



```kotlin
val config = TealiumConfig.Builder(
    accountName = &#34;ACCOUNT&#34;,
    profileName = &#34;PROFILE&#34;,
    environment = Environment.PROD,
    modules = listOf(
        Modules.deviceData(),
        // other modules...
    )
).build()
```


Use the `DeviceDataSettingsBuilder` to enable or disable device data types.
For more information, see [`DeviceDataSettingsBuilder`](/tealium-prism-swift/TealiumPrismCore/Classes/DeviceDataSettingsBuilder.html).
```swift
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                          profile: &#34;PROFILE&#34;, 
                          environment: &#34;dev&#34;,
                          modules: [
                              Modules.deviceData(forcingSettings: { builder in
                                  builder.setDeviceNamesUrl(&#34;https://custom-endpoint.example.com/device_names.json&#34;)
                                         .setMemoryReportingEnabled(true)
                                         .setBatteryReportingEnabled(false)
                                         .setScreenReportingEnabled(true)
                                         .setEnabled(true)
                                         .setOrder(1)
                                        .setRules(.just(&#34;rule_id_from_settings&#34;))
                              }),
                              // other modules...
                          ])
```



