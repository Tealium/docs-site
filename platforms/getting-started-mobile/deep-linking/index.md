---
title: Deep Links
description: Learn about deep linking for mobile.
url: https://docs.tealium.com/platforms/getting-started-mobile/deep-linking/
---
A deep link is a hyperlink that launches a mobile app and, optionally, delivers specific content within the app. Deep links are often used to measure the performance of advertisement campaigns or promotional emails that link users to your app.

## Supported platforms

The following platforms support deep link tracking:

- [Android (Kotlin)](/platforms/android-kotlin/)
- [iOS (Swift v2.x)](/platforms/ios-swift/)

## How it works

When your app is launched from a deep link, the Tealium library adds the URL to the data layer as the attribute `deep_link_url`.

The deep link&#39;s query parameters are added to the data layer with attribute names in the format `deep_link_param_&lt;param name&gt;`.

For example, `https://example.com/?campaign_code=SUMMER` becomes:  
```javascript
deep_link_url = &#34;https://example.com/?campaign_code=SUMMER&#34;
deep_link_param_campaign_code = &#34;SUMMER&#34;
```

Deep link data layer attributes are only stored for the session.

## Configuration

### Android Kotlin

Deep link tracking is automatically enabled in Tealium for Android (Kotlin).

Disable automatic tracking of deep links by setting the [`deepLinkTrackingEnabled`](/platforms/android-kotlin/api/tealium-config/#deeplinktrackingenabled) property to `false`.

### Swift v2.x

Automatic deep link tracking is enabled by default in Tealium for iOS (Swift v2.x) through the method swizzling technique. Method swizzling is the dynamic swapping of one method implementation for another during a program&#39;s runtime.

If you do not want to use method swizzling or don&#39;t want deep links to be tracked automatically, you can disable automatic deep link tracking with the `info.plist` key `TealiumAutotrackingDeepLinkEnabled` set to `false`.

If you want to track deep links without method swizzling and you are using `SwiftUI`, after disabling the automatic tracking in the `info.plist`, use the `TealiumAppTrackable` wrapper around your application content&#39;s `View`:

```swift
var body: some Scene {
    WindowGroup {
        TealiumAppTrackable {
            ContentView()
        }
    }
}
```

If you are using `UIKit`, you can instead call the `handleDeeplink` method on the `tealium` instance manually.

### Swift v1.x

Tealium for iOS (Swift v1.x) requires a single line of code to be added to your app&#39;s `AppDelegate` class to enable deep linking.  

```swift
func application(_ app: UIApplication,
                 open url: URL,
                 options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -&gt; Bool {
  tealium?.handleDeepLink(url)
  return true
}
```

## Data Layer

The following properties are added to your data layer when your app is launched from a deep link:

| Event Attribute | Type | Description | Example |
| :-- | :-- | :-- | :-- |
| `deep_link_url` | `String` | The full URL of the deep link that opened the app, including query parameters. | `https://example.com/?campaign_code=SUMMER` |
| `deep_link_param_X` | `String` | Each query parameter of the deep link URL, where `X` is the name of the parameter, such as `deep_link_param_campaign_code`.| `SUMMER` |
| `deep_link_referrer_url` (iOS) | `String` | The full URL of the browser page where the deep link was clicked. | `https://www.example.com/referring/page` |
| `deep_link_referrer_app` (iOS) | `String` | The identifier of the referrer app when the deep link comes from a custom schema in another app signed by the same team. | `com.example.appId` |
