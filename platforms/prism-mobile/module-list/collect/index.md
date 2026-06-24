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
    &#34;modules&#34;: {
        &#34;Collect&#34;: {
            &#34;module_type&#34;: &#34;Collect&#34;
        }
    }
}
```

**Custom configuration:**
```json
{
    &#34;modules&#34;: {
        &#34;Collect&#34;: {
            &#34;module_type&#34;: &#34;Collect&#34;,
            &#34;enabled&#34;: true,
            &#34;order&#34;: 1,
            &#34;configuration&#34;: {
                &#34;url&#34;: &#34;https://custom.collect.example.com/event&#34;,
                &#34;batch_url&#34;: &#34;https://custom.collect.example.com/bulk-event&#34;,
                &#34;override_profile&#34;: &#34;custom-profile&#34;,
                &#34;override_domain&#34;: &#34;custom-domain.example.com&#34;
            }
        }
    }
}
```

### Programmatic settings

Configure the module programmatically by adding it to the modules in `TealiumConfig`.

Programmatic settings always take precedence over local and remote settings.



```kotlin
val config = TealiumConfig.Builder(
    application,
    &#34;ACCOUNT&#34;,
    &#34;PROFILE&#34;,
    Environment.DEV,
    listOf(Modules.collect { builder -&gt;
        builder.setUrl(&#34;https://custom.collect.example.com/event&#34;)
              .setBatchUrl(&#34;https://custom.collect.example.com/bulk-event&#34;)
              .setProfile(&#34;custom-profile&#34;)
              .setDomain(&#34;custom-domain.example.com&#34;)
              .setEnabled(true)
              .setOrder(1)
    })
).build()
```


```swift
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                          profile: &#34;PROFILE&#34;,
                          environment: &#34;dev&#34;,
                          modules: [
                              Modules.collect(forcingSettings: { builder in
                                  builder.setUrl(&#34;https://custom.collect.example.com/event&#34;)
                                         .setBatchUrl(&#34;https://custom.collect.example.com/bulk-event&#34;)
                                         .setOverrideProfile(&#34;custom-profile&#34;)
                                         .setOverrideDomain(&#34;custom-domain.example.com&#34;)
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
    &#34;ACCOUNT&#34;,
    &#34;PROFILE&#34;,
    Environment.DEV
).addModule(Modules.collect(
    { builder -&gt;
        builder.setModuleId(&#34;PrimaryCollect&#34;)
              .setUrl(&#34;https://primary.collect.example.com/event&#34;)
    },
    { builder -&gt;
        builder.setModuleId(&#34;SecondaryCollect&#34;)
              .setUrl(&#34;https://secondary.collect.example.com/event&#34;)
              .setRules(Rule.just(&#34;purchase_rule_id&#34;))
    }
)).build()
```


```swift
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                          profile: &#34;PROFILE&#34;,
                          environment: &#34;dev&#34;,
                          modules: [
                              Modules.collect(
                                  forcingSettings: { builder in
                                      builder.setModuleId(&#34;PrimaryCollect&#34;)
                                             .setUrl(&#34;https://primary.collect.example.com/event&#34;)
                                  },
                                  { builder in
                                      builder.setModuleId(&#34;SecondaryCollect&#34;)
                                             .setUrl(&#34;https://secondary.collect.example.com/event&#34;)
                                             .setRules(.just([&#34;purchase_rule_id&#34;]))
                                  }
                              ),
                              // other modules...
                          ])
```



The equivalent configuration in JSON format:

```json
{
    &#34;modules&#34;: {
        &#34;PrimaryCollect&#34;: {
            &#34;module_type&#34;: &#34;Collect&#34;,
            &#34;module_id&#34;: &#34;PrimaryCollect&#34;,
            &#34;configuration&#34;: {
                &#34;url&#34;: &#34;https://primary.collect.example.com/event&#34;
            }
        },
        &#34;SecondaryCollect&#34;: {
            &#34;module_type&#34;: &#34;Collect&#34;,
            &#34;module_id&#34;: &#34;SecondaryCollect&#34;,
            &#34;configuration&#34;: {
                &#34;url&#34;: &#34;https://secondary.collect.example.com/event&#34;
            },
            &#34;rules&#34;: {
                &#34;operator&#34;: &#34;just&#34;,
                &#34;children&#34;: [
                    &#34;purchase_rule_id&#34;
                ]
            }
        }
    }
}
```

## Settings builder reference

The Collect module uses the `CollectSettingsBuilder` for configuration. The following methods are available:



For more information, see [`CollectSettingsBuilder`](/tealium-prism-kotlin/core/com.tealium.prism.core.api.settings.modules/-collect-settings-builder/).


| Method | Description |
|---|---|
| `setUrl(url: String)` | Sets the URL used to send individual events. |
| `setBatchUrl(url: String)` | Sets the URL used to send batches of events. |
| `setProfile(profile: String)` | Sets the Tealium profile to use when sending events. |
| `setDomain(domain: String)` | Sets the domain to use in place of the default single and batch URL. |
| `setModuleId(moduleId: String)` | Sets a unique identifier for this module instance. |
| `setEnabled(enabled: Boolean)` | Permanently enables or disables the module. |
| `setOrder(order: Int)` | Sets the order in which the module is initialized. |
| `setRules(rules: Rule&lt;String&gt;)` | Sets the rules that this module must match to process an event. |
| `setMappings(mappings: ...)` | Sets the mappings for this module. |


For more information, see [`CollectSettingsBuilder`](/tealium-prism-swift/TealiumPrismCore/Classes/CollectSettingsBuilder.html).

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


