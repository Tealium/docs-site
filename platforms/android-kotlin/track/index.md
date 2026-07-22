---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/android-kotlin/track/
---
## Track Views

To track screen views, pass an instance of `TealiumView(viewName:mutableMapOf)` to the [`track()`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

The following is an example:

```java
val screenView = TealiumView(
  "purchase", 
  mutableMapOf(
    "customer_id" to "abc123", 
    "order_total" to 10.00, 
    "product_id" to listOf("PROD123", "PROD456"),
    "order_id" to "0123456789"
  )
)
tealium.track(screenView);
```

## Track Events

To track non-view events, pass an instance of `TealiumEvent(eventName:mutableMapOf)` to the [`track()`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#track) method.  `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

The following is an example:

```java
val tealEvent = TealiumEvent(
  "cart_add", 
  mutableMapOf(
    "customer_id" to "abc123", 
    "product_id" to listOf("PROD123", "PROD456"), 
    "product_price" to listOf(4.00, 6.00)
  )
)
tealium.track(tealEvent);
```

## Timed Events

[Timed events](https://docs.tealium.com/platforms/getting-started-mobile/timed-events/) measure the duration of an event or the duration between two events. Timed events are triggered automatically or manually.

### Automatic Triggers

Automatically track the duration between events by setting [`timedEventTriggers`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#timedeventtriggers) to a list of `EventTrigger` objects, specifying the names of the start and stop events.

The following is an example of tracking a timed event with an automatic trigger:

```java
timedEventTriggers = mutableListOf(EventTrigger.forEventName(
    "cart_add",
    "purchase"))
```

### Manual Triggers

Manually track the duration of an event by starting and stopping the timed event based on your custom logic.

Start tracking the duration of an event with [`startTimedEvent()`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#starttimedevent).  
```java
tealium.startTimedEvent(name: "TimeSpentViewingProduct")
```

Stop a timed event with [`stopTimedEvent()`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#stoptimedevent):  
```java
tealium.stopTimedEvent(name: "TimeSpentViewingProduct")
```

Cancel a previously started timed event with [`cancelTimedEvent()`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#canceltimedevent):  
```java
tealium.cancelTimedEvent(name: "TimeSpentViewingProduct")
```

## Trace

### Join Trace

Join a trace with the specified ID by calling [`joinTrace()`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#jointrace). Learn more about the [Trace](https://docs.tealium.com/manage-traces/) feature in the Tealium Customer Data Hub.

```java
Tealium["INSTANCE_NAME"]?.joinTrace("TRACE_ID")
```
Replace the following:
* `INSTANCE_NAME`: the instance name you used when initializing the Tealium Kotlin library.
* `TRACE_ID`: the ID of the trace you want to join.

### Leave trace

A trace remains active for the duration of the app session until you call [`leaveTrace()`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#leavetrace), which leaves a previously joined trace and ends the visitor session.

```java
Tealium["INSTANCE_NAME"]?.leaveTrace()
```

End the visitor session remotely with [`endTraceVisitorSession()`](https://docs.tealium.com/platforms/android-kotlin/api/tealium/#endtracevisitorsession), which does not terminate the SDK session or reset the session ID.


```java
Tealium["INSTANCE_NAME"]?.endTraceVisitorSession()
```
