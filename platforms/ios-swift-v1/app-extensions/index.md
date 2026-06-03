---
title: App Extensions
description: Learn about app extensions.
url: https://docs.tealium.com/platforms/ios-swift-v1/app-extensions/
---This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](/platforms/ios-swift/).

## Today Extensions

**Today Extensions** are widgets that appear on the device&#39;s &#34;Today&#34; screen. These app extensions are allowed very limited resources by the OS, and may be terminated if they consume too much memory or processing power.

Use the Swift library as normal inside a Today Extension but, to keep the memory footprint low, we recommend using only the [Collect module](/platforms/ios-swift-v1/module-list/collect/) to transmit data. The [Tag Management module](/platforms/ios-swift-v1/module-list/tag-management/) may be too resource intensive and result in your widget being terminated.

Regardless of the option chosen, it is important to thoroughly test and ensure your widget performs as expected. Embedding fewer Tealium modules in your widget results in greater performance and a lower memory footprint.

## watchOS Extensions and Independent Apps

If you are adding a watchOS target to an iOS project that already has Tealium installed then add the necessary modules, `TealiumHelper` to the Watch Extension target, and necessary tracking calls. The Tag Management module is not supported on watchOS, due to the dependency on `WKWebView`; the Collect module is the only supported method of data collection on watchOS.

Alternatively, you could use the `WatchConnectivty` framework&#39;s `WCSession` API to send a message to the host iOS app each time you want to send a tracking call. This allows the event to be tracked by the Tag Management module if you are using it, but is not an option for an independent watchOS app.

## Visitor ID in App Extensions

App Extensions have their own sandboxed data storage, which is not shared with the host iOS app (if available). Therefore, by default, a new persistent visitor ID is generated when the app is started for the first time.

An issue causing 3 distinct visitor IDs for the same visitor arises when you have an iOS app, Today widget, and the watchOS extension. This is not an issue if you are using visitor stitching and already have a known visitor ID for the app user. Avoid this situation by synchronizing the visitor IDs across the app and its extensions. This is done by passing the current Tealium first party visitor ID in the `TealiumConfig` object of the app extension when initializing Tealium. The ID is stored and used for future launches of the app, without being regenerated.

```swift
class TealiumHelper {

	var tealium: Tealium?

	// ...

	// Return the current visitor ID from the Tealium Swift library on the iOS app
	func getVisitorId() -&gt; String? {
		return self.tealium.visitorId
	}

	// On the app extension, pass the ID retrieved from the iOS app in the config object
	private func initTealium(existingVisitorId id: String) {
		let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
 	       		                 profile: &#34;PROFILE&#34;,
        	   	                 environment: &#34;ENVIRONMENT&#34;,
           		                 datasource: &#34;DATASOURCE&#34;)

		// existing ID is used as the first party ID in the app extension
        config.existingVisitorId = id
        self.tealium = Tealium(config: config)
	}

}
```

Alternatively, generate a visitor ID centrally and pass it to each Tealium instance at initialization. It is recommended to use a UUID.

Do not use a simple ID, such as email address, for your first party visitor ID.
