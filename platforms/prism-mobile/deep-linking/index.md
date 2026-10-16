---
title: Deep linking
description: Learn how to handle deep links for attribution tracking and trace management with the Tealium Prism SDK.
url: https://docs.tealium.com/platforms/prism-mobile/deep-linking/
---
The DeepLink module automatically handles incoming deep links for attribution tracking and trace management. It captures deep link URLs, extracts query parameters, manages referrer information, and integrates with the Trace module for debugging.

On iOS, the module automatically listens for deep link events unless explicitly disabled.

## Collected data points

When a deep link is handled, the DeepLink module collects the following data:

| Data point | Key | Description |
|:-----------|:----|:------------|
| Deep link URL | `deep_link_url` | The complete URL of the deep link |
| Query parameters | `deep_link_param_*` | Each query parameter prefixed with `deep_link_param_` |
| Referrer URL | `deep_link_referrer_url` | The URL that referred to this deep link |
| Referrer app | `deep_link_referrer_app` | The app identifier that opened this deep link |

## Installation

The DeepLink module can be configured using programmatic, remote JSON, or local JSON settings.


<blockquote>
The DeepLink module is not configurable in React Native. The native Prism SDK handles deep links automatically on both iOS and Android.
</blockquote>




Add the DeepLink module to your Tealium configuration:

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev"
)
.addModule(Modules.deepLink())
.build()
```

To configure with enforced settings:

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev"
)
.addModule(Modules.deepLink {
    setEnabled(true)
    setDeepLinkTraceEnabled(true)
    setSendDeepLinkEvent(false)
})
.build()
```


Add the DeepLink module to your Tealium configuration:

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.deepLink(),
                              // other modules...
                          ])
```

To configure with enforced settings:

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.deepLink(forcingSettings: { builder in
                                  builder.setEnabled(true)
                                         .setDeepLinkTraceEnabled(true)
                                         .setSendDeepLinkEvent(false)
                              }),
                              // other modules...
                          ])
```



### JSON configuration

Configure the DeepLink module in your local or remote settings JSON file:

```json
{
    "modules": {
        "DeepLink": {
            "module_type": "DeepLink",
            "enabled": true,
            "configuration": {
                "deep_link_trace_enabled": true,
                "send_deep_link_event": false
            }
        }
    }
}
```

## Configuration options

| Setting | Key | Description | Default |
|:--------|:----|:------------|:--------|
| Deep link trace enabled | `deep_link_trace_enabled` | Enable or disable trace from deep links. When enabled, QR codes from the QR Trace tool automatically join traces. | `true` |
| Send deep link event | `send_deep_link_event` | Enable or disable sending deep link events. When enabled, a deep link event is tracked automatically. | `false` |

## Handle deep links manually


<blockquote>
`tealium.deepLink.handle()` is not available in React Native. Deep links are handled automatically by the native SDK.
</blockquote>




```kotlin
tealium.deepLink.handle(url, referrer)
    .subscribe { result ->
        // Optionally handle result here
    }
```


```swift
tealium.deepLink.handle(link: url, referrer: .fromUrl(referrerUrl)).subscribe { result in
    // Optionally handle result here
}
```



### Disable automatic tracking (iOS)

On iOS, deep links are tracked automatically by default. To disable automatic deep link tracking, set the `TealiumAutotrackingDeepLinkEnabled` key to `false` in your `Info.plist`.

## API reference

For detailed class and method signatures, see the API reference documentation:

* [DeepLinkHandler (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DeepLinkHandler.html)
* [DeepLinkSettingsBuilder (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/DeepLinkSettingsBuilder.html)
* [DeepLink (Kotlin)](https://docs.tealium.com/tealium-prism-kotlin/)
