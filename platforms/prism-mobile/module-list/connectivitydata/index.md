---
title: ConnectivityData module
description: Monitors network connectivity and adds connection information to all tracking events.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/connectivitydata/
---

## Data layer

The following variables are added to each tracking call while the module is enabled:

| Variable | Description | Example |
| :--- | :--- | :--- |
| `connection_type` | A list of current network connection types.&lt;br&gt;Possible values: `wifi`, `cellular`, `ethernet`, `none` | `[&#34;wifi&#34;, &#34;cellular&#34;]` |

## Install



The ConnectivityData module is included in `TealiumPrismCore`. Add it as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod &#39;tealium-prism/Core&#39;
```



## Initialize



Configure the module programmatically by adding it to the modules parameter in `TealiumConfig`.

For more information about module settings, see [`ModuleSettingsBuilder`](/tealium-prism-swift/TealiumPrismCore/Classes/ModuleSettingsBuilder.html).

```swift
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                          profile: &#34;PROFILE&#34;, 
                          environment: &#34;dev&#34;,
                          modules: [
                              Modules.connectivityData(forcingSettings: { builder in
                                  builder.setEnabled(true)
                                         .setOrder(1)
                                         .setRules(.and([&#34;rule_id_from_settings&#34;]))
                              }),
                              // other modules...
                          ])
```


