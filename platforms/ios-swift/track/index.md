---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/ios-swift/track/
---
## Track Views

To track screen views, pass an instance of `TealiumView(tealiumEvent:dataLayer:)` to the [`track()`](/platforms/ios-swift/api/tealium/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

#### Example

```swift
let screenView = TealiumView(
	&#34;purchase&#34;,
	dataLayer: [
		&#34;customer_id&#34;: &#34;abc123&#34;, 
		&#34;order_total&#34;: 10.00, 
		&#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
		&#34;order_id&#34;: &#34;0123456789&#34;
	]
)
tealium?.track(screenView)
```

## Track Events

To track non-view events, pass an instance of `TealiumEvent(tealiumEvent:dataLayer:)` to the [`track()`](/platforms/ios-swift/api/tealium/#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

#### Example

```swift
let tealEvent = TealiumEvent(
	&#34;cart_add&#34;, 
	dataLayer: [
		&#34;customer_id&#34;: &#34;abc123&#34;, 
		&#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
		&#34;product_price&#34;: [4.00, 6.00]
	]
)
tealium?.track(tealEvent)
```

## Timed Events

[Timed events](/platforms/getting-started-mobile/timed-events/) measure the duration of a single event or the time between two events. Timed events are triggered automatically or manually.

### Automatic Triggers

Automatically track the duration between events by setting [`timedEventTriggers`](/platforms/ios-swift/api/tealium-config/#timedeventtriggers) to a list of `TimedEventTrigger` objects, specifying the names of the start and stop events.

The following is an example of tracking a timed event with an automatic trigger:

```swift
config.timedEventTriggers = [TimedEventTrigger(
    start: &#34;cart_add&#34;,
    stop: &#34;purchase&#34;)]
```

### Manual Triggers

Manually track the duration of an event by starting and stopping the timed event based on your custom logic.

Start tracking the duration of an event with [`startTimedEvent()`](/platforms/android-kotlin/api/tealium/#starttimedevent):  
```swift
tealium.startTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

Stop a timed event with [`stopTimedEvent()`](/platforms/android-kotlin/api/tealium/#stoptimedevent):    
```swift
tealium.stopTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

Cancel a previously started timed event with [`cancelTimedEvent()`](/platforms/android-kotlin/api/tealium/#canceltimedevent):    
```swift
tealium.cancelTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

Clear all previously started timed events with [`clearAllTimedEvents()`](/platforms/ios-swift/api/tealium/#clearalltimedevents):    
```swift
tealium?.clearAllTimedEvents()
```

## Trace

### Join Trace

The [`joinTrace()`](/platforms/ios-swift/api/tealium/#jointrace) method joins a trace with the specified ID. Learn more about the [Trace]() feature in the Tealium Customer Data Hub.

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	func joinTrace(traceId id: String) {
		tealium?.joinTrace(id: &#34;TRACE_ID&#34;)
		// ...
	}
}
```
Replace `TRACE_ID` with the ID of the trace you want to join. 

### Leave trace

A trace remains active for the duration of the app session until the [`leaveTrace()`](/platforms/ios-swift/api/tealium/#leavetrace) method is called, which leaves a previously joined trace and ends the visitor session.

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

Connector actions set to run at `&#34;End of Visit&#34;` do not run until the session expires.

To preserve the trace visitor session when leaving the trace, pass the optional argument `false`, as shown in the following example:

```swift
tealium?.leaveTrace(killVisitorSession: false)
```
