---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/ios-swift-v1/track/
---
<blockquote>
This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](https://docs.tealium.com/platforms/ios-swift/).
</blockquote>


## Track Views

The [`trackView()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium/#trackview) method tracks a screen view with associated data and, optionally, triggers a callback function.

```swift
let mydata = ["KEY": "VALUE"]
// track call with type specified and completion block
tealium?.trackView(title: "EVENT_NAME",
      data: mydata,
      completion: { (success: Bool, info: [String: Any]?, error: Error?) in
//...
})
```


<blockquote>
The value passed to `title` will appear in the data layer as the variable `tealium_event`.
</blockquote>


## Track Events

The [`track()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium/#track) method tracks an event with associated data and, optionally, triggers a callback function.

```swift
let mydata = ["KEY": "VALUE"]
// track call with type specified and completion block
tealium?.track(title: "EVENT_NAME",
      data: mydata,
      completion: { (success: Bool, info: [String: Any]?, error: Error?) in
 //...
})
```


<blockquote>
The value passed to `title` will appear in the data layer as the variable `tealium_event`.
</blockquote>


## Trace

### Join Trace

The [`joinTrace()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium/#jointrace) method joins a trace with the specified ID. [Learn more](https://docs.tealium.com/manage-traces/) about the Trace feature in the Tealium Customer Data Hub.


```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	func joinTrace(traceId id: String) {
		tealium?.joinTrace(traceId: "TRACE_ID")
		// ...
	}
}
```

### Leave trace

A trace remains active for the duration of the app session until the [`leaveTrace()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium/#leavetrace) method is called, which leaves a previously joined trace and ends the visitor session.

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

Connector actions set to run at "End of Visit" does not run until the session expires.

To preserve the trace visitor session when leaving the trace, pass the optional argument `false`, as shown in the following example:

```swift
tealium?.leaveTrace(killVisitorSession: false)
```
