---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/csharp/track/
---
## Track Events

Once the Tealium object has been defined, begin tracking events with the [`Track()`](https://docs.tealium.com/platforms/csharp/api/#track) method.

The following example tracks a call with only an event name:  
```csharp
tealium.Track("EVENT_NAME");
```  

The following example tracks a call with event name and optional data dictionary:  
```csharp
Dictionary<string, object> customData = new Dictionary() {
    {"KEY1", new string[]{"STRING1","STRING2"}},
    {"KEY2", "VALUE2"},
    {"KEY3", "VALUE3"}};
tealium.Track("EVENT_NAME", customData);
```

The following example tracks a call with event name, optional data dictionary, and track completion:  
```csharp
Dictionary<string, object> customData = new Dictionary() {
    {"KEY1", new string[]{"STRING1","STRING2"}},
    {"KEY2", "VALUE2"},
    {"KEY3", "VALUE3"}};
tealium.Track("EVENT_NAME,
    customData,
    (success, info, error)=>) {
        Debug.WriteLine("eventTrackComplete: was successful: " + success);
});
```

## Trace

This library uses the [HTTP API](https://docs.tealium.com/platforms/http-api/) and therefore supports sending a Trace ID for debugging purposes.

### Join Trace

The [`JoinTrace()`](https://docs.tealium.com/platforms/csharp/api/#jointrace) method joins a trace, as shown in the following example:

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace("TRACE_ID");
```

### Leave Trace

The [`LeaveTrace()`](https://docs.tealium.com/platforms/csharp/api/#leavetrace) method leaves a trace, as shown in the following example:

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace("TRACE_ID");
//...
instance.LeaveTrace();
```

The `tealium_trace_id` is no longer populated automatically on future events.


### Kill Trace


The [`KillTraceSession()`](https://docs.tealium.com/platforms/csharp/api/#killtracesession) method kils a trace, as shown in the following example:


```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace("TRACE_ID");
//...
instance.KillTraceSession();
```

The `KillTraceSession()` method triggers an event to kill/end the visitor trace session at the server. This is useful for testing end-of-visit behavior in your Tealium Customer Data Hub configuration.

The method also calls the [`LeaveTrace()`](https://docs.tealium.com/platforms/csharp/api/#leavetrace) method to remove the expired `tealium_trace_id` and stop any more events being sent with the previous trace ID.
