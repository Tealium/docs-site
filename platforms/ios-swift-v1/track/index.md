---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/ios-swift-v1/track/
---This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](/platforms/ios-swift/).

## Track Views

The [`trackView()`](/platforms/ios-swift-v1/api/tealium/#trackview) method tracks a screen view with associated data and, optionally, triggers a callback function.

```swift
let mydata = [&#34;KEY&#34;: &#34;VALUE&#34;]
// track call with type specified and completion block
tealium?.trackView(title: &#34;EVENT_NAME&#34;,
      data: mydata,
      completion: { (success: Bool, info: [String: Any]?, error: Error?) in
//...
})
```

The value passed to `title` will appear in the data layer as the variable `tealium_event`.

## Track Events

The [`track()`](/platforms/ios-swift-v1/api/tealium/#track) method tracks an event with associated data and, optionally, triggers a callback function.

```swift
let mydata = [&#34;KEY&#34;: &#34;VALUE&#34;]
// track call with type specified and completion block
tealium?.track(title: &#34;EVENT_NAME&#34;,
      data: mydata,
      completion: { (success: Bool, info: [String: Any]?, error: Error?) in
 //...
})
```

The value passed to `title` will appear in the data layer as the variable `tealium_event`.

## Trace

### Join Trace

The [`joinTrace()`](/platforms/ios-swift-v1/api/tealium/#jointrace) method joins a trace with the specified ID. [Learn more]() about the Trace feature in the Tealium Customer Data Hub.


```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	func joinTrace(traceId id: String) {
		tealium?.joinTrace(traceId: &#34;TRACE_ID&#34;)
		// ...
	}
}
```

### Leave trace

A trace remains active for the duration of the app session until the [`leaveTrace()`](/platforms/ios-swift-v1/api/tealium/#leavetrace) method is called, which leaves a previously joined trace and ends the visitor session.

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	func leaveTrace() {
		tealium?.leaveTrace()
		// ...
	}
}
```

Connector actions set to run at &#34;End of Visit&#34; does not run until the session expires.

To preserve the trace visitor session when leaving the trace, pass the optional argument `false`, as shown in the following example:

```swift
tealium?.leaveTrace(killVisitorSession: false)
```
