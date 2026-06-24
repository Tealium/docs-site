---
title: Trace
description: Use trace sessions to debug and validate your Tealium Prism SDK implementation.
url: https://docs.tealium.com/platforms/prism-mobile/trace/
---
The Trace module provides debugging and testing capabilities for the Tealium Prism SDK. Use trace sessions for real-time event monitoring to verify that events are tracked and dispatched correctly. When a trace is active, the trace ID is automatically added to all tracking events for server-side filtering and analysis.

For more information about the trace tool, see [Debug with trace]().

## Collected data points

When a trace session is active, the Trace module collects the following data:

| Data point | Key | Description |
|:-----------|:----|:------------|
| Trace ID | `cp.trace_id` | The unique identifier for the active trace session (legacy compatibility) |
| Trace ID | `tealium_trace_id` | The unique identifier for the active trace session |

## Installation

The Trace module can be configured using programmatic, remote JSON, or local JSON settings.



Add the Trace module to your Tealium configuration:

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = &#34;tealiummobile&#34;,
    profileName = &#34;your-profile&#34;,
    environment = &#34;dev&#34;
)
.addModule(Modules.trace())
.build()
```

To configure with enforced settings:

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = &#34;tealiummobile&#34;,
    profileName = &#34;your-profile&#34;,
    environment = &#34;dev&#34;
)
.addModule(Modules.trace {
    setEnabled(true)
    setTrackErrors(true)
})
.build()
```


Add the Trace module to your Tealium configuration:

```swift
let config = TealiumConfig(account: &#34;tealiummobile&#34;,
                          profile: &#34;your-profile&#34;,
                          environment: &#34;dev&#34;,
                          modules: [
                              Modules.trace(),
                              // other modules...
                          ])
```

To configure with enforced settings:

```swift
let config = TealiumConfig(account: &#34;tealiummobile&#34;,
                          profile: &#34;your-profile&#34;,
                          environment: &#34;dev&#34;,
                          modules: [
                              Modules.trace(forcingSettings: { builder in
                                  builder.setEnabled(true)
                                         .setTrackErrors(true)
                              }),
                              // other modules...
                          ])
```



### JSON configuration

Configure the Trace module in your local or remote settings JSON file:

```json
{
    &#34;modules&#34;: {
        &#34;Trace&#34;: {
            &#34;module_type&#34;: &#34;Trace&#34;,
            &#34;enabled&#34;: true,
            &#34;configuration&#34;: {
                &#34;track_errors&#34;: true
            }
        }
    }
}
```

## Join a trace session

To start a trace session, call `trace.join()` with a trace ID. The trace ID is added to all future events until you call `leave()` or the session expires.



```kotlin
tealium.trace.join(&#34;your-trace-id&#34;)
    .subscribe { result -&gt;
        // Optionally handle result here
    }
```


```swift
tealium.trace.join(id: &#34;your-trace-id&#34;).subscribe { result in
    // Optionally handle result here
}
```



## Leave a trace session

To stop a trace session, call `trace.leave()`. This removes the trace ID from future events.



```kotlin
tealium.trace.leave()
    .subscribe { result -&gt;
        // Optionally handle result here
    }
```


```swift
tealium.trace.leave().subscribe { result in
    // Optionally handle result here
}
```



## Force end of visit

To test &#34;End of Visit&#34; actions in AudienceStream, force the session to end immediately instead of waiting for the session to expire:



```kotlin
tealium.trace.forceEndOfVisit()
    .subscribe { result -&gt;
        // Handle the track result
    }
```


```swift
tealium.trace.forceEndOfVisit().subscribe { result in
    // Handle the track result
}
```



The trace remains active until `leave()` is called. The `forceEndOfVisit()` method dispatches a track call that signals the session to end, following standard dequeueing flows.

## Error tracking

When error tracking is enabled (`track_errors: true`), the Trace module automatically tracks SDK errors that occur during an active trace session. To prevent duplicate error reports, the module deduplicates errors by category:

* Only the first error from each category is tracked per trace session
* Subsequent errors from the same category are ignored until a new trace session begins
* Joining a new trace session or leaving the current session resets the deduplication cache

## QR trace

You can also start a trace directly from a deep link. If the opened URL contains the right query parameter, the trace starts automatically. This is typically done with the QR trace tool on the Tealium platform. For more information, see [Debug with trace]().

## API reference

For detailed class and method signatures, see the API reference documentation:

* [Trace (Swift)](/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html)
* [TraceSettingsBuilder (Swift)](/tealium-prism-swift/TealiumPrismCore/Classes/TraceSettingsBuilder.html)
* [Trace (Kotlin)](/tealium-prism-kotlin/)
