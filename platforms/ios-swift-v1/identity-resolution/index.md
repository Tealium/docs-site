---
title: Identity Resolution
description: Learn about identity resolution.
url: https://docs.tealium.com/platforms/ios-swift-v1/identity-resolution/
---This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](/platforms/ios-swift/).

## How it Works

The Tealium Swift library generates a randomized and unique persistent visitor ID the first time it is launched with the [`getVisitorId()`](/platforms/ios-swift-v1/api/tealium/#getvisitorid) method. This value is included in each tracked event as the attribute `tealium_visitor_id`. This value is the primary visitor ID used in Tealium AudienceStream. You can include secondary visitor ID attributes as needed by adding them to the persistent data storage.

If you are using AudienceStream, this will become the main first-party visitor ID that&#39;s associated with this visitor. You may provide additional known visitor IDs as needed, by sending them as variables in your tracking calls.

[Learn more]() about configuring visitor IDs in AudienceStream.

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	// Retrieve Tealium&#39;s first party visitor ID, if needed
	func getVisitorId() -&gt; String? {
		return self.tealium?.visitorId
	}

	// adds a known visitor ID (such as an email address) to the persistent data store
	func setKnownVisitorId(_ id: String) {
		self.tealium?.persistentData()?.addPersistentData([&#34;customer_id&#34;: id])
	}

}
```
