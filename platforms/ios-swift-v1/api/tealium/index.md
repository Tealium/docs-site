---
title: Tealium
description: The Tealium class serves as the main API entry point for all modules.
url: https://docs.tealium.com/platforms/ios-swift-v1/api/tealium/
---
## Class: `Tealium`

The following summarizes the commonly used methods of the iOS (Swift) `Tealium` class.

| Method/Property | Description |
| ----- | ------ |
| `joinTrace()`  | Joins a trace with the specified ID|
| `leaveTrace()`  |Leave a previously joined trace and end the visitor session |
| `Tealium()`  |Constructor for a new `Tealium` object|
| `track()`  | Tracks an event with associated data and, optionally, triggers a callback function |
| `trackView()`  | Tracks a screen view with associated data and, optionally, triggers a callback function|
| `visitorId` | Returns a randomly generated and unique persistent visitor ID |

### `joinTrace()`

Joins a trace with the specified ID. The trace remains active for the duration of the app session until `leaveTrace()` is called. [Learn more]() about the Trace feature in the Tealium Customer Data Hub.

```swift
joinTrace(traceId: String)
```

| Parameters | Type                 | Description              | Example |
|------------|----------------------|-----------------| ---- |
| `traceId`  | `String` | The trace ID acquired from the Trace tool | `&#34;12345&#34;` |


### `leaveTrace()`

Leave a previously joined trace and end the visitor session. Optional parameter to preserve the trace visitor session when leaving the trace.

```swift
tealium?.leaveTrace(killVisitorSession: false)
```

| Parameters | Type                 | Description     | Example |
|------------|----------------------|-----------------| ---- |
| `killVisitorSession`     | `Bool` | (Optional) Defaults to `true` if no parameters are passed or pass `false` if you do not want to terminate the visitor session | [`true`, `false`] |

### `Tealium()`
Constructor for a new `Tealium` object.

```swift
Tealium(config: TealiumConfig, completion: Closure)
```

| Parameters | Type                 | Description                                                                                |
|------------|----------------------|--------------------------------------------------------------------------------------------|
| `config`| `TealiumConfig` | Initialize the Tealium object with a `TealiumConfig` object containing your account details. |
| `completion`  | `Closure` | (Optional) Completion closure to be called on init completion`()-&gt; Void )?` |


### `track()`

Tracks an event with associated data and, optionally, triggers a callback function.

```swift
track(title:String, data:[String:Any], completion:ClosureType)
```

| Parameters    | Type          | Description      | Example |
|---------------|---------------|------------------| --- |
| `title`| `String`             | The name of the event to be tracked     | `title: &#34;Buy Now&#34;` |
| `data`| `Dictionary`          | An object of key-value pairs with data associated with the event to be tracked | `data: data: [&#34;product_id&#34; : [&#34;widget123&#34;]]` |
| `completion`| `ClosureType`   | A function to execute upon completion of the tracking call (use `nil` if none) | `nil` |


### `trackView()`
Tracks a screen view with associated data and, optionally, triggers a callback function.

```swift
trackView(title:String, data:[String:Any], completion:ClosureType)
```

| Parameters    | Type          | Description      | Example |
|---------------|---------------|------------------| --- |
| `title`| `String`             | The name of the screen view to be tracked     | `title: &#34;Homescreen&#34;` |
| `data`| `Dictionary`          | An object of key-value pairs with data associated with the event to be tracked | `data: [&#34;customer_id&#34;: &#34;1234567890-a&#34;]` |
| `completion`| `ClosureType`   | A function to execute upon completion of the tracking call (use `nil` if none) | `nil` |


### `visitorId`

Returns a randomly generated and unique persistent visitor ID.

```swift
let visitorId: String = tealium.visitorId
```
