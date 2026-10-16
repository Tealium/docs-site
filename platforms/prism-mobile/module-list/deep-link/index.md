---
title: DeepLinkHandler module
description: Track deep links and attribute them to campaigns or referrers.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/deep-link/
---
The DeepLinkHandler module tracks incoming deep links for attribution and trace management. When your app is launched from a deep link, the module captures the URL and extracts its query parameters into the data layer. Deep link handling runs automatically by default.

## How it works

When a deep link opens your app, the module adds the full URL to the data layer as `deep_link_url`. Each query parameter is extracted and added separately using the prefix `deep_link_param_`. For example, `https://example.com/?campaign_code=SUMMER` produces:

```
deep_link_url = "https://example.com/?campaign_code=SUMMER"
deep_link_param_campaign_code = "SUMMER"
```


<blockquote>
Deep link data layer attributes are only stored for the session.
</blockquote>


## Data layer

The following attributes are added to the data layer when a deep link is handled:

| Attribute | Type | Description |
| :--- | :--- | :--- |
| `deep_link_url` | `String` | The full URL of the deep link, including query parameters. |
| `deep_link_param_X` | `String` | Each query parameter of the deep link URL, where `X` is the parameter name. |
| `deep_link_referrer_url` | `String` | The URL of the page or resource that referred to this deep link. |
| `deep_link_referrer_app` (iOS only) | `String` | The bundle identifier of the app that opened this deep link via a custom URL scheme. |

## Install



The DeepLinkHandler module is included with `prism-core`, which is a transitive dependency of all other Prism modules.


The DeepLinkHandler module is included in `TealiumPrismCore`. Add it as a Swift Package Manager dependency using the repository URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod 'tealium-prism/Core'
```

To install the full Prism library instead:

```ruby
pod 'tealium-prism'
```



## Initialize

Add the module to the `modules` list in your `TealiumConfig`.



```kotlin
val config = TealiumConfig.Builder(
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.deepLink(),
        // other modules...
    )
).build()
```


```swift
let config = TealiumConfig(
    account: "ACCOUNT",
    profile: "PROFILE",
    environment: "prod",
    modules: [
        Modules.deepLink(),
        // other modules...
    ]
)
```



## Handle deep links manually

To handle deep links manually, call `handle` on the deep link property of the `Tealium` instance.



```kotlin
tealium.deeplink.handle(uri).subscribe { result ->
    // Optionally handle result here
}

// With a referrer URL:
tealium.deeplink.handle(uri, referrerUri).subscribe { result ->
    // Optionally handle result here
}
```


```swift
tealium.deepLink.handle(link: url, referrer: .fromUrl(referrerUrl)).subscribe { result in
    // Optionally handle result here
}
```



## Configuration

### Disable automatic deep link tracking

By default, the module handles deep links automatically when the app is launched from a deep link.

To disable automatic deep link tracking:



```kotlin
Modules.deepLink { settings ->
    settings.setAutomaticDeepLinkTrackingEnabled(false)
}
```


Add the key `TealiumAutotrackingDeepLinkEnabled` with the value `false` to your app's `Info.plist` file.



### Enable deep link events

By default, the module does not send a separate tracking event when a deep link is handled. When you enable deep link events, the module also tracks a `deep_link` event each time a deep link is opened.



```kotlin
Modules.deepLink { settings ->
    settings.setSendDeepLinkEventEnabled(true)
}
```


```swift
Modules.deepLink(forcingSettings: { builder in
    builder.setSendDeepLinkEvent(true)
})
```



### Enable trace via deep link

By default, scanning a QR code from the Tealium QR Trace tool automatically joins a trace session.

To disable the ability to join a trace using deep links:



```kotlin
Modules.deepLink { settings ->
    settings.setDeepLinkTraceEnabled(false)
}
```


```swift
Modules.deepLink(forcingSettings: { builder in
    builder.setDeepLinkTraceEnabled(false)
})
```



### JSON configuration

Configure the module in your local or remote settings JSON file:

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

## Settings builder reference



For more information, see [`DeepLinkSettingsBuilder`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.settings.modules/-deep-link-settings-builder/).

| Method | Description |
| :--- | :--- |
| `setAutomaticDeepLinkTrackingEnabled(enabled: Boolean)` | Enables or disables automatic deep link handling. |
| `setDeepLinkTraceEnabled(enabled: Boolean)` | Enables or disables trace functionality from deep links. Default: `true`. |
| `setSendDeepLinkEventEnabled(enabled: Boolean)` | Enables or disables sending a `deep_link` event when a deep link is opened. Default: `false`. |
| `setEnabled(enabled: Boolean)` | Permanently enables or disables the module. |
| `setOrder(order: Int)` | Sets the order in which the module is initialized. |


For more information, see [`DeepLinkSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/DeepLinkSettingsBuilder.html).

| Method | Description |
| :--- | :--- |
| `setDeepLinkTraceEnabled(_:)` | Enables or disables trace functionality from deep links. Default: `true`. |
| `setSendDeepLinkEvent(_:)` | Enables or disables sending a `deep_link` event when a deep link is opened. Default: `false`. |
| `setEnabled(_:)` | Permanently enables or disables the module. |
| `setOrder(_:)` | Sets the order in which the module is initialized. |
| `setRules(_:)` | Sets the rules that determine when the module runs. |


