---
title: Trace
description: Use trace sessions to debug and validate your Tealium Prism SDK implementation.
url: https://docs.tealium.com/platforms/prism-mobile/trace/
---
The Trace module provides debugging and testing capabilities for the Tealium Prism SDK. Use trace sessions for real-time event monitoring to verify that events are tracked and dispatched correctly. When a trace is active, the trace ID is automatically added to all tracking events for server-side filtering and analysis.

For more information about the trace tool, see [Debug with trace](https://docs.tealium.com/platforms/getting-started-mobile/debug-with-trace/).

## Collected data points

When a trace session is active, the Trace module collects the following data:

| Data point | Key | Description |
|:-----------|:----|:------------|
| Trace ID | `cp.trace_id` | The unique identifier for the active trace session (legacy compatibility) |
| Trace ID | `tealium_trace_id` | The unique identifier for the active trace session |

## Installation

The Trace module can be configured using programmatic, remote JSON, or local JSON settings.


<blockquote>
In React Native, the Trace module is enabled via your Tealium settings JSON. No programmatic setup is required.
</blockquote>




Add the Trace module to your Tealium configuration:

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev"
)
.addModule(Modules.trace())
.build()
```

To configure with enforced settings:

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev"
)
.addModule(Modules.trace {
    setEnabled(true)
    setTrackErrors(true)
})
.build()
```


Add the Trace module to your Tealium configuration:

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.trace(),
                              // other modules...
                          ])
```

To configure with enforced settings:

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
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
    "modules": {
        "Trace": {
            "module_type": "Trace",
            "enabled": true,
            "configuration": {
                "track_errors": true
            }
        }
    }
}
```

## Join a trace session

To start a trace session, call `trace.join()` with a trace ID. The trace ID is added to all future events until you call `leave()` or the session expires.



```kotlin
tealium.trace.join("your-trace-id")
    .subscribe { result ->
        // Optionally handle result here
    }
```


```swift
tealium.trace.join(id: "your-trace-id").subscribe { result in
    // Optionally handle result here
}
```


```javascript
await tealium.trace.join("your-trace-id");
```



## Leave a trace session

To stop a trace session, call `trace.leave()`. This removes the trace ID from future events.



```kotlin
tealium.trace.leave()
    .subscribe { result ->
        // Optionally handle result here
    }
```


```swift
tealium.trace.leave().subscribe { result in
    // Optionally handle result here
}
```


```javascript
await tealium.trace.leave();
```



## Force end of visit

To test "End of Visit" actions in AudienceStream, force the session to end immediately instead of waiting for the session to expire:



```kotlin
tealium.trace.forceEndOfVisit()
    .subscribe { result ->
        // Handle the track result
    }
```


```swift
tealium.trace.forceEndOfVisit().subscribe { result in
    // Handle the track result
}
```


```javascript
await tealium.trace.forceEndOfVisit();
```



The trace remains active until `leave()` is called. The `forceEndOfVisit()` method dispatches a track call that signals the session to end, following standard dequeueing flows.

## Error tracking

When error tracking is enabled (`track_errors: true`), the Trace module automatically tracks SDK errors that occur during an active trace session. To prevent duplicate error reports, the module deduplicates errors by category:

* Only the first error from each category is tracked per trace session
* Subsequent errors from the same category are ignored until a new trace session begins
* Joining a new trace session or leaving the current session resets the deduplication cache

## QR trace

You can also start a trace directly from a deep link. If the opened URL contains the right query parameter, the trace starts automatically. This is typically done with the QR trace tool on the Tealium platform. For more information, see [Debug with trace](https://docs.tealium.com/platforms/getting-started-mobile/debug-with-trace/).

## API reference

For detailed class and method signatures, see the API reference documentation:

* [Trace (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/Trace.html)
* [TraceSettingsBuilder (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/TraceSettingsBuilder.html)
* [Trace (Kotlin)](https://docs.tealium.com/tealium-prism-kotlin/)
* [Trace (React Native)](https://docs.tealium.com/tealium-prism-react-native/interfaces/Trace.html)
