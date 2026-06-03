---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/android-kotlin/track/
---
## Track Views

To track screen views, pass an instance of `TealiumView(viewName:mutableMapOf)` to the [`track()`](/platforms/android-kotlin/api/tealium/#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

The following is an example:

```java
val screenView = TealiumView(
  &#34;purchase&#34;, 
  mutableMapOf(
    &#34;customer_id&#34; to &#34;abc123&#34;, 
    &#34;order_total&#34; to 10.00, 
    &#34;product_id&#34; to listOf(&#34;PROD123&#34;, &#34;PROD456&#34;),
    &#34;order_id&#34; to &#34;0123456789&#34;
  )
)
tealium.track(screenView);
```

## Track Events

To track non-view events, pass an instance of `TealiumEvent(eventName:mutableMapOf)` to the [`track()`](/platforms/android-kotlin/api/tealium/#track) method.  `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

The following is an example:

```java
val tealEvent = TealiumEvent(
  &#34;cart_add&#34;, 
  mutableMapOf(
    &#34;customer_id&#34; to &#34;abc123&#34;, 
    &#34;product_id&#34; to listOf(&#34;PROD123&#34;, &#34;PROD456&#34;), 
    &#34;product_price&#34; to listOf(4.00, 6.00)
  )
)
tealium.track(tealEvent);
```

## Timed Events

[Timed events](/platforms/getting-started-mobile/timed-events/) measure the duration of an event or the duration between two events. Timed events are triggered automatically or manually.

### Automatic Triggers

Automatically track the duration between events by setting [`timedEventTriggers`](/platforms/android-kotlin/api/tealium-config/#timedeventtriggers) to a list of `EventTrigger` objects, specifying the names of the start and stop events.

The following is an example of tracking a timed event with an automatic trigger:

```java
timedEventTriggers = mutableListOf(EventTrigger.forEventName(
    &#34;cart_add&#34;,
    &#34;purchase&#34;))
```

### Manual Triggers

Manually track the duration of an event by starting and stopping the timed event based on your custom logic.

Start tracking the duration of an event with [`startTimedEvent()`](/platforms/android-kotlin/api/tealium/#starttimedevent).  
```java
tealium.startTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

Stop a timed event with [`stopTimedEvent()`](/platforms/android-kotlin/api/tealium/#stoptimedevent):  
```java
tealium.stopTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

Cancel a previously started timed event with [`cancelTimedEvent()`](/platforms/android-kotlin/api/tealium/#canceltimedevent):  
```java
tealium.cancelTimedEvent(name: &#34;TimeSpentViewingProduct&#34;)
```

## Trace

### Join Trace

Join a trace with the specified ID by calling [`joinTrace()`](/platforms/android-kotlin/api/tealium/#jointrace). Learn more about the [Trace]() feature in the Tealium Customer Data Hub.

```java
Tealium[&#34;INSTANCE_NAME&#34;]?.joinTrace(&#34;TRACE_ID&#34;)
```
Replace the following:
* `INSTANCE_NAME`: the instance name you used when initializing the Tealium Kotlin library.
* `TRACE_ID`: the ID of the trace you want to join.

### Leave trace

A trace remains active for the duration of the app session until you call [`leaveTrace()`](/platforms/android-kotlin/api/tealium/#leavetrace), which leaves a previously joined trace and ends the visitor session.

```java
Tealium[&#34;INSTANCE_NAME&#34;]?.leaveTrace()
```

End the visitor session remotely with [`endTraceVisitorSession()`](/platforms/android-kotlin/api/tealium/#endtracevisitorsession), which does not terminate the SDK session or reset the session ID.


```java
Tealium[&#34;INSTANCE_NAME&#34;]?.endTraceVisitorSession()
```
