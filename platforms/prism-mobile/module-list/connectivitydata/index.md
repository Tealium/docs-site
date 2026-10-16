---
title: ConnectivityData module
description: Monitors network connectivity and adds connection information to all tracking events.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/connectivitydata/
---
The ConnectivityData module monitors network connectivity and adds the current connection type to every tracking event.

## Data layer

The following variables are added to each tracking call while the module is enabled:

| Variable | Description | Example |
| :--- | :--- | :--- |
| `connection_type` | A list of current network connection types.<br>Possible values: `wifi`, `cellular`, `ethernet`, `none` | `["wifi", "cellular"]` |

## Install



The ConnectivityData module is included in `TealiumPrismCore`. Add it as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod 'tealium-prism/Core'
```



## Initialize



Configure the module programmatically by adding it to the modules parameter in `TealiumConfig`.

For more information about module settings, see [`ModuleSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/ModuleSettingsBuilder.html).

```swift
let config = TealiumConfig(account: "ACCOUNT",
                          profile: "PROFILE", 
                          environment: "dev",
                          modules: [
                              Modules.connectivityData(forcingSettings: { builder in
                                  builder.setEnabled(true)
                                         .setOrder(1)
                                         .setRules(.and(["rule_id_from_settings"]))
                              }),
                              // other modules...
                          ])
```


