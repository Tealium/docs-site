---
title: DeepLinkHandler module
description: Track deep links and attribute them to campaigns or referrers.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/deep-link/
---
The DeepLinkHandler module tracks incoming deep links for attribution and trace management. When your app is launched from a deep link, the module captures the URL and extracts its query parameters into the data layer. Deep link handling runs automatically by default.

## How it works

When a deep link opens your app, the module adds the full URL to the data layer as `deep_link_url`. Each query parameter is extracted and added separately using the prefix `deep_link_param_`. For example, `https://example.com/?campaign_code=SUMMER` produces:

```
deep_link_url = &#34;https://example.com/?campaign_code=SUMMER&#34;
deep_link_param_campaign_code = &#34;SUMMER&#34;
```

Deep link data layer attributes are only stored for the session.

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
pod &#39;tealium-prism/Core&#39;
```

To install the full Prism library instead:

```ruby
pod &#39;tealium-prism&#39;
```



## Initialize

Add the module to the `modules` list in your `TealiumConfig`.



```kotlin
val config = TealiumConfig.Builder(
    accountName = &#34;ACCOUNT&#34;,
    profileName = &#34;PROFILE&#34;,
    environment = Environment.PROD,
    modules = listOf(
        Modules.deepLink(),
        // other modules...
    )
).build()
```


```swift
let config = TealiumConfig(
    account: &#34;ACCOUNT&#34;,
    profile: &#34;PROFILE&#34;,
    environment: &#34;prod&#34;,
    modules: [
        Modules.deepLink(),
        // other modules...
    ]
)
```



## Handle deep links manually

To handle deep links manually, call `handle` on the deep link property of the `Tealium` instance.



```kotlin
tealium.deeplink.handle(uri).subscribe { result -&gt;
    // Optionally handle result here
}

// With a referrer URL:
tealium.deeplink.handle(uri, referrerUri).subscribe { result -&gt;
    // Optionally handle result here
}
```


```swift
tealium.deepLink.handle(link: url, referrer: .fromUrl(referrerUrl)).subscribe { result in
    // Optionally handle result here
}
```



## Configururation

### Disable automatic deep link tracking

By default, the module handles deep links automatically when the app is launched from a deep link.

To disable automatic deep link tracking:



```kotlin
Modules.deepLink { settings -&gt;
    settings.setAutomaticDeepLinkTrackingEnabled(false)
}
```


Add the key `TealiumAutotrackingDeepLinkEnabled` with the value `false` to your app&#39;s `Info.plist` file.



### Enable deep link events

By default, the module does not send a separate tracking event when a deep link is handled. When you enable deep link events, the module also tracks a `deep_link` event each time a deep link is opened.



```kotlin
Modules.deepLink { settings -&gt;
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
Modules.deepLink { settings -&gt;
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
    &#34;modules&#34;: {
        &#34;DeepLink&#34;: {
            &#34;module_type&#34;: &#34;DeepLink&#34;,
            &#34;enabled&#34;: true,
            &#34;configuration&#34;: {
                &#34;deep_link_trace_enabled&#34;: true,
                &#34;send_deep_link_event&#34;: false
            }
        }
    }
}
```

## Settings builder reference



For more information, see [`DeepLinkSettingsBuilder`](/tealium-prism-kotlin/core/com.tealium.prism.core.api.settings.modules/-deep-link-settings-builder/).

| Method | Description |
| :--- | :--- |
| `setAutomaticDeepLinkTrackingEnabled(enabled: Boolean)` | Enables or disables automatic deep link handling. |
| `setDeepLinkTraceEnabled(enabled: Boolean)` | Enables or disables trace functionality from deep links. Default: `true`. |
| `setSendDeepLinkEventEnabled(enabled: Boolean)` | Enables or disables sending a `deep_link` event when a deep link is opened. Default: `false`. |
| `setEnabled(enabled: Boolean)` | Permanently enables or disables the module. |
| `setOrder(order: Int)` | Sets the order in which the module is initialized. |


For more information, see [`DeepLinkSettingsBuilder`](/tealium-prism-swift/TealiumPrismCore/Classes/DeepLinkSettingsBuilder.html).

| Method | Description |
| :--- | :--- |
| `setDeepLinkTraceEnabled(_:)` | Enables or disables trace functionality from deep links. Default: `true`. |
| `setSendDeepLinkEvent(_:)` | Enables or disables sending a `deep_link` event when a deep link is opened. Default: `false`. |
| `setEnabled(_:)` | Permanently enables or disables the module. |
| `setOrder(_:)` | Sets the order in which the module is initialized. |
| `setRules(_:)` | Sets the rules that determine when the module runs. |


