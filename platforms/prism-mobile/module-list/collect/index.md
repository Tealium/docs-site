---
title: Collect module
description: Dispatches tracking calls to the Tealium Collect service.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/collect/
---
## How it works

The Collect module is a Dispatcher that sends tracking events to the Tealium Collect service. It handles both single event dispatching and batch event processing, automatically optimizing delivery based on the number of events and visitor IDs. It supports customizable endpoints, profile overrides, and domain configuration.

## Configuration

The Collect module provides the following configuration options:

| Setting            | JSON Key             | Description                                                                 | Default value                                |
|--------------------|----------------------|-----------------------------------------------------------------------------|----------------------------------------------|
| URL                | `url`                | The URL used to send single events.                                         | `https://collect.tealiumiq.com/event`        |
| Batch URL          | `batch_url`          | The URL used to send a batch of events.                                     | `https://collect.tealiumiq.com/bulk-event`   |
| Override Profile   | `override_profile`   | Profile to override the `TealiumConfig.profile` in event data.              | None                                         |
| Override Domain    | `override_domain`    | Domain to replace default URL domains (does not override explicit URLs).    | None                                         |

Configure the module using JSON settings files, programmatically, or a combination of both.

### JSON file settings

To use a local settings file, pass the filename to `settingsFile` in `TealiumConfig`. To use remote settings, pass a URL to `settingsUrl`. You can use both at the same time.

The following examples show the supported JSON structure.

**Default configuration:**
```json
{
    "modules": {
        "Collect": {
            "module_type": "Collect"
        }
    }
}
```

**Custom configuration:**
```json
{
    "modules": {
        "Collect": {
            "module_type": "Collect",
            "enabled": true,
            "order": 1,
            "configuration": {
                "url": "https://custom.collect.example.com/event",
                "batch_url": "https://custom.collect.example.com/bulk-event",
                "override_profile": "custom-profile",
                "override_domain": "custom-domain.example.com"
            }
        }
    }
}
```

### Programmatic settings

Configure the module programmatically by adding it to the modules in `TealiumConfig`.


<blockquote>
Programmatic settings always take precedence over local and remote settings.
</blockquote>




```kotlin
val config = TealiumConfig.Builder(
    application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV,
    listOf(Modules.collect { builder ->
        builder.setUrl("https://custom.collect.example.com/event")
              .setBatchUrl("https://custom.collect.example.com/bulk-event")
              .setProfile("custom-profile")
              .setDomain("custom-domain.example.com")
              .setEnabled(true)
              .setOrder(1)
    })
).build()
```


```swift
let config = TealiumConfig(account: "ACCOUNT",
                          profile: "PROFILE",
                          environment: "dev",
                          modules: [
                              Modules.collect(forcingSettings: { builder in
                                  builder.setUrl("https://custom.collect.example.com/event")
                                         .setBatchUrl("https://custom.collect.example.com/bulk-event")
                                         .setOverrideProfile("custom-profile")
                                         .setOverrideDomain("custom-domain.example.com")
                                         .setEnabled(true)
                                         .setOrder(1)
                              }),
                              // other modules...
                          ])
```



### Multiple instances

Use multiple Collect instances when you need to send events to different endpoints with different configurations. For example, to send all events to a primary endpoint and route a subset of events, filtered by rules, to a secondary endpoint.

Each instance requires a unique `moduleId`. Use rules to control which events each instance processes.



```kotlin
val config = TealiumConfig.Builder(
    application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV
).addModule(Modules.collect(
    { builder ->
        builder.setModuleId("PrimaryCollect")
              .setUrl("https://primary.collect.example.com/event")
    },
    { builder ->
        builder.setModuleId("SecondaryCollect")
              .setUrl("https://secondary.collect.example.com/event")
              .setRules(Rule.just("purchase_rule_id"))
    }
)).build()
```


```swift
let config = TealiumConfig(account: "ACCOUNT",
                          profile: "PROFILE",
                          environment: "dev",
                          modules: [
                              Modules.collect(
                                  forcingSettings: { builder in
                                      builder.setModuleId("PrimaryCollect")
                                             .setUrl("https://primary.collect.example.com/event")
                                  },
                                  { builder in
                                      builder.setModuleId("SecondaryCollect")
                                             .setUrl("https://secondary.collect.example.com/event")
                                             .setRules(.just(["purchase_rule_id"]))
                                  }
                              ),
                              // other modules...
                          ])
```



The equivalent configuration in JSON format:

```json
{
    "modules": {
        "PrimaryCollect": {
            "module_type": "Collect",
            "module_id": "PrimaryCollect",
            "configuration": {
                "url": "https://primary.collect.example.com/event"
            }
        },
        "SecondaryCollect": {
            "module_type": "Collect",
            "module_id": "SecondaryCollect",
            "configuration": {
                "url": "https://secondary.collect.example.com/event"
            },
            "rules": {
                "operator": "just",
                "children": [
                    "purchase_rule_id"
                ]
            }
        }
    }
}
```

## Settings builder reference

The Collect module uses the `CollectSettingsBuilder` for configuration. The following methods are available:



For more information, see [`CollectSettingsBuilder`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.settings.modules/-collect-settings-builder/).


| Method | Description |
|---|---|
| `setUrl(url: String)` | Sets the URL used to send individual events. |
| `setBatchUrl(url: String)` | Sets the URL used to send batches of events. |
| `setProfile(profile: String)` | Sets the Tealium profile to use when sending events. |
| `setDomain(domain: String)` | Sets the domain to use in place of the default single and batch URL. |
| `setModuleId(moduleId: String)` | Sets a unique identifier for this module instance. |
| `setEnabled(enabled: Boolean)` | Permanently enables or disables the module. |
| `setOrder(order: Int)` | Sets the order in which the module is initialized. |
| `setRules(rules: Rule<String>)` | Sets the rules that this module must match to process an event. |
| `setMappings(mappings: ...)` | Sets the mappings for this module. |


For more information, see [`CollectSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CollectSettingsBuilder.html).

| Method | Description |
|---|---|
| `setUrl(_:)` | Sets the URL used to send individual events. |
| `setBatchUrl(_:)` | Sets the URL used to send batches of events. |
| `setOverrideProfile(_:)` | Sets the profile to override the `TealiumConfig.profile` in event data. |
| `setOverrideDomain(_:)` | Sets the domain to replace default URL domains. |
| `setModuleId(_:)` | Sets a unique identifier for this module instance. |
| `setEnabled(_:)` | Permanently enables or disables the module. |
| `setOrder(_:)` | Sets the order in which the module is initialized. |
| `setRules(_:)` | Sets the rules that this module must match to process an event. |
| `setMappings(_:)` | Sets the mappings for this module. |


