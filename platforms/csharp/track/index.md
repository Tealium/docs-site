---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/csharp/track/
---
## Track Events

Once the Tealium object has been defined, begin tracking events with the [`Track()`](/platforms/csharp/api/#track) method.

The following example tracks a call with only an event name:  
```csharp
tealium.Track(&#34;EVENT_NAME&#34;);
```  

The following example tracks a call with event name and optional data dictionary:  
```csharp
Dictionary&lt;string, object&gt; customData = new Dictionary() {
    {&#34;KEY1&#34;, new string[]{&#34;STRING1&#34;,&#34;STRING2&#34;}},
    {&#34;KEY2&#34;, &#34;VALUE2&#34;},
    {&#34;KEY3&#34;, &#34;VALUE3&#34;}};
tealium.Track(&#34;EVENT_NAME&#34;, customData);
```

The following example tracks a call with event name, optional data dictionary, and track completion:  
```csharp
Dictionary&lt;string, object&gt; customData = new Dictionary() {
    {&#34;KEY1&#34;, new string[]{&#34;STRING1&#34;,&#34;STRING2&#34;}},
    {&#34;KEY2&#34;, &#34;VALUE2&#34;},
    {&#34;KEY3&#34;, &#34;VALUE3&#34;}};
tealium.Track(&#34;EVENT_NAME,
    customData,
    (success, info, error)=&gt;) {
        Debug.WriteLine(&#34;eventTrackComplete: was successful: &#34; &#43; success);
});
```

## Trace

This library uses the [HTTP API](/platforms/http-api/) and therefore supports sending a Trace ID for debugging purposes.

### Join Trace

The [`JoinTrace()`](/platforms/csharp/api/#jointrace) method joins a trace, as shown in the following example:

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace(&#34;TRACE_ID&#34;);
```

### Leave Trace

The [`LeaveTrace()`](/platforms/csharp/api/#leavetrace) method leaves a trace, as shown in the following example:

```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace(&#34;TRACE_ID&#34;);
//...
instance.LeaveTrace();
```

The `tealium_trace_id` is no longer populated automatically on future events.


### Kill Trace


The [`KillTraceSession()`](/platforms/csharp/api/#killtracesession) method kils a trace, as shown in the following example:


```csharp
Tealium instance = new Tealium(testConfig);
instance.JoinTrace(&#34;TRACE_ID&#34;);
//...
instance.KillTraceSession();
```

The `KillTraceSession()` method triggers an event to kill/end the visitor trace session at the server. This is useful for testing end-of-visit behavior in your Tealium Customer Data Hub configuration.

The method also calls the [`LeaveTrace()`](/platforms/csharp/api/#leavetrace) method to remove the expired `tealium_trace_id` and stop any more events being sent with the previous trace ID.
