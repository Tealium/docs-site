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
| `device` | Consumer device name | `"iPhone 13 Pro Max"` |
| `device_architecture` | CPU architecture | `"64"` |
| `device_cputype` | Detailed CPU type | `"ARM64e"` |
| `device_language` | Primary device language | `"en-US"` |
| `device_manufacturer` | Device manufacturer | `"Apple"` |
| `device_model` | Consumer device name | `"iPhone 13 Pro Max"` |
| `device_os_build` | OS build number | `"20A372"` |
| `device_os_version` | Operating system version | `"17.0"` |
| `device_type` | Platform model identifier | `"iPhone14,3"` |
| `model_variant` | Model variant identifier | `"A2484"` |
| `origin` | Device category | `"mobile"` |
| `os_name` | Operating system name | `"iOS"` |
| `platform` | Lowercase OS name | `"ios"` |


### Battery and screen

The following battery and screen attributes can be enabled or disabled based on your builder settings. For more information, see [Initialize](#initialize).

| Variable | Description | Example |
| :--- | :--- | :--- |
| `device_battery_percent` | (iOS only) Battery charge percentage | `"58"` |
| `device_ischarging` | (iOS only) Whether the device is charging | `"true"` |
| `device_logical_resolution` | Logical screen resolution | `"390x844"` |
| `device_orientation` | Device orientation | `"Portrait"` |
| `device_orientation_extended` | Detailed orientation | `"Face Up"` |
| `device_resolution` | Physical screen resolution | `"1170x2532"` |

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
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-device-data")
```


Add `TealiumPrismDeviceData` as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod 'tealium-prism/DeviceData'
```



## Initialize

The DeviceData module initializes automatically when it is configured. No code changes are required for most integrations. Configure the module in the Tealium platform UI, or bundle a local JSON configuration file with your app.



```kotlin
val config = TealiumConfig.Builder(
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.deviceData(),
        // other modules...
    )
).build()
```


Use the `DeviceDataSettingsBuilder` to enable or disable device data types.
For more information, see [`DeviceDataSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/DeviceDataSettingsBuilder.html).
```swift
let config = TealiumConfig(account: "ACCOUNT",
                          profile: "PROFILE", 
                          environment: "dev",
                          modules: [
                              Modules.deviceData(forcingSettings: { builder in
                                  builder.setDeviceNamesUrl("https://custom-endpoint.example.com/device_names.json")
                                         .setMemoryReportingEnabled(true)
                                         .setBatteryReportingEnabled(false)
                                         .setScreenReportingEnabled(true)
                                         .setEnabled(true)
                                         .setOrder(1)
                                        .setRules(.just("rule_id_from_settings"))
                              }),
                              // other modules...
                          ])
```



