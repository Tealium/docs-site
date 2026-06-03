---
title: Tealium
description: The Tealium class serves as the main API entry point for all modules.
url: https://docs.tealium.com/platforms/ios-swift/api/tealium/
---
## Class: `Tealium`

The following summarizes the commonly used methods of the iOS (Swift) `Tealium` class.

| Method/Property                                           | Description                |
|:----------------------------------------------------------|:---------------------------|
| [`cancelTimedEvent()`](#canceltimedevent)                 | Cancels the timer for a timed event. |
| [`clearStoredVisitorIds()`](#clearstoredvisitorids)       | Deletes the stored cache of visitorIds and calls `resetVisitorId`. |
| [`clearAllTimedEvents()`](#clearalltimedevents)           | Clears all previously started timed events. |
| [`decorateUrl()`](#decorateurl)                           | Decorates the URL with the Adobe ECID parameters. |
| [`disable()`](#disable)                                   | Disables the Tealium library. |
| [`flushQueue()`](#flushqueue)                             | Sends any queued dispatches immediately. |
| [`gatherTrackData()`](#gathertrackdata)                   | Returns all custom data layer values and collector module data layer values. |
| [`getTagManagementWebView()`](#gettagmanagementwebview)   | Returns the TagManagement WebView. |
| [`joinTrace()`](#jointrace)                               | Joins a trace with the specified ID. |
| [`leaveTrace()`](#leavetrace)                             | Leave a previously joined trace and end the visitor session. |
| [`linkECIDToKnownIdentifier`](#linkecidtoknownidentifier) | Links the current ECID to a known secondary ID. |
| [`onVisitorId`](#onvisitorid)                             | Allows subscription to changes on `visitorId`. |
| [`resetVisitor()`](#resetvisitor)                         | Resets the visitor ECID by retrieving a new one on the next tracking call. |
| [`resetVisitorId()`](#resetvisitorid)                     | Generates a new visitor ID for the user. |
| [`startTimedEvent()`](#starttimedevent)                   | Starts a timed event with the given name. |
| [`stopTimedEvent()`](#stoptimedevent)                     | Stops the timer for a timed event which triggers the `timed_event` tracking call. |
| [`Tealium()`](#tealium)                                   | Constructor for a new `Tealium` object. |
| [`track()`](#track)                                       | Tracks an event with associated data and, optionally, triggers a callback function. |
| [`visitor`](#visitor)                                     | Returns the full `AdobeVisitor` instance. |
| [`visitorId`](#visitorid)                                 | Returns a randomly generated and unique persistent visitor ID. |

### `cancelTimedEvent()`

Cancels the timer for a timed event. The timed event is not tracked.

```swift
tealium?.cancelTimedEvent(name: &#34;TIMED_EVENT_NAME&#34;)
```

| Parameters | Type     | Description                 |
|:-----------|:---------|:----------------------------|
| `name`     | `String` | The name of the timed event |

### `clearAllTimedEvents()`

Clears all previously started timed events. The timed events are not tracked.

```swift
tealium?.clearAllTimedEvents()
```

### `clearStoredVisitorIds()`

Clears all previously stored visitor IDs and hashed customer identifiers.

```swift
tealium?.clearStoredVisitorIds()
```

### `decorateUrl()`

Decorates the input URL with the Adobe ECID query parameters.

```swift
decorateUrl(_ url: URL, completion: ((URL) → Void)
```

| Parameters            | Type                          | Description                    |
|:----------------------|:------------------------------|:-------------------------------|
| `url`                 | `URL`                         | The URL to decorate            |
| `completion`          | `URL` -&gt; Void                 | The block called with the decorated URL. |

Example:

```swift
var tealium: Tealium?
...
let url = URL(string: &#34;https://www.tealium.com&#34;)!
tealium?.adobeVisitorApi?.decorateUrl(url) { newUrl in
    // use the new URL
}
```

### `disable()`

Disables the Tealium library and removes all module references. Re-enable by creating a new Tealium instance if required.

```swift
tealium?.disable()
```

### `flushQueue()`

Sends all queued dispatches immediately. Requests may still be blocked by `DispatchValidator`s such as consent manager

```swift
tealium?.disable()
```

### `gatherTrackData()`

Retrieves all the current custom data layer values and collector module data layer values. The results are cached for subsequent calls and returned asynchronously. Set `retrieveCachedData` to `false` to get the most recent values. Use the completion handler to process the returned values. Reference custom data layer values directly using their custom keys and reference collector module values using `TealiumDataKey.`.  

```swift
 tealium?.gatherTrackData(retreiveCachedData: false, completion: { allData in
    let lifecycleTotalWakeCount = allData[TealiumDataKey.totalWakeCount]
    let visitorId = allData[TealiumDataKey.visitorId]
    let userLanguage = allData[&#34;user_language&#34;]
})
```

See also [`Tealium.dataLayer.all`](/platforms/ios-swift/data-layer/#retrieve-all-data).

### `getTagManagementWebView()`
(New in [v2.10.0](/platforms/ios-swift/release-notes/#2100-may-2023))

Returns the TagManagement WebView so clients can set the `isInspectable` flag and debug on XCode 14.3&#43;.

Any other use of the private Webview object, such as loading another web page, may lead to unpredictable behavior and is strongly discouraged.

```swift
 tealium?.getTagManagementWebView { webView in
    if #available(iOS 16.4, *) {
        webView.isInspectable = true // To inspect tagManagement webviews on XCode 14.3&#43; and iOS 16.4&#43;
    }
  }
```

### `joinTrace()`

Joins a trace with the specified ID. The trace remains active for the duration of the app session until `leaveTrace()` is called. Learn more about the [trace feature]() in the Tealium Customer Data Hub.

```swift
joinTrace(traceId: String)
```

| Parameters | Type     | Description                               | Example   |
|:-----------|:---------|:------------------------------------------|:----------|
| `traceId`  | `String` | The trace ID acquired from the Trace tool | `&#34;12345&#34;` |


### `leaveTrace()`

Leave a previously joined trace and end the visitor session. Optional parameter to preserve the trace visitor session when leaving the trace.

```swift
tealium?.leaveTrace(killVisitorSession: false)
```

| Parameters           | Type   | Description                                                                                                               | Example |
|:---------------------|:-------|:--------------------------------------------------------------------------------------------------------------------------|:--|
| `killVisitorSession` | `Bool` | (Optional) Set to `true` if no params are passed. Set to `false` if you don&#39;t want to terminate the visitor session. The default is `true`. | `false` |

### `linkECIDToKnownIdentifier()`

Links the current ECID to a known secondary identifier, such as an email address or other internal ID.

```swift
linkECIDToKnownIdentifier(
  _ knownID: String,
  adobeDataProviderId: String,
  authState: AdobeVisitorAuthState?,
  completion: ((Result&lt;AdobeVisitor, Error&gt;) → Void)
```

| Parameters            | Type                          | Description                    |
|:----------------------|:------------------------------|:-------------------------------|
| `knownId`             | `String`                      | The known identifier.          |
| `adobeDataProviderId` | `String`                      | The Adobe data provider identifier. |
| `authState`           | `AdobeVisitorAuthState`       | The authenticated state.       |
| `completion`          | `Result&lt;AdobeVisitor, Error&gt;` | The Adobe response listener.   |


Example:

```swift
var tealium: Tealium?
...

tealium?.adobeVisitorApi?.linkECIDToKnownIdentifier(
  &#34;myidentifier&#34;, adobeDataProviderId: &#34;123456&#34;, .unknown
  )
```

### `onVisitorId`

Notifies of visitor ID changes.

```swift
let subscription = tealium?.onVisitorId.subscribe { newVisitor in
    // handle visitor change here
}
```

### `resetVisitor()`

Resets the visitor ECID by retrieving a new one on the next tracking call.

```swift
resetVisitor()
```

Example:

```swift
var tealium: Tealium?
//...
tealium?.adobeVisitorApi?.resetVisitor()
```


### `resetVisitorId()`

Generates a new visitor ID for the user.

```swift
tealium?.resetVisitorId()
```

### `startTimedEvent()`

Starts a timed event with the given name. If this method is called again with the same event name, it is ignored if the event has not been ended or canceled. The event start time is not persisted.  

If optional data is passed along with the event name, it is added to the track call when the timer is stopped with the [`stopTimedEvent()`](#stoptimedevent) call.

```swift
tealium.startTimedEvent(name: &#34;TIMED_EVENT_NAME&#34;, with: [&#34;custom_key&#34;: &#34;custom_value&#34;])
```

| Parameters                                  | Type     | Description                   |
|:--------------------------------------------|:---------|:------------------------------|
| `name`                                      | `String` | The name of the timed event   |
| `[&#34;custom_key&#34;: &#34;custom_value&#34;]` (Optional) | `Map`    | An object of key-value pair data to be tracked in the data layer |

### `stopTimedEvent()`

Stops the timer for a timed event which triggers the `timed_event` tracking call.

```swift
tealium?.stopTimedEvent(name: &#34;TIMED_EVENT_NAME&#34;)
```

| Parameters | Type     | Description                 |
|:-----------|:---------|:----------------------------|
| `name`     | `String` | The name of the timed event |


### `Tealium()`
Constructor for a new `Tealium` object.

```swift
Tealium(config: TealiumConfig, completion: Closure)
```

| Parameters   | Type            | Description                                           |
|:-------------|:----------------|:------------------------------------------------------|
| `config`     | `TealiumConfig` | Initialize the Tealium object with a `TealiumConfig` object containing your account details. |
| `completion` | `Closure`       | (Optional) Completion closure to be called on init completion`()-&gt; Void )?` |

### `track()`

Tracks a screen view or event with optional event data.

```swift
tealium?.track(tealiumEvent)
```

| Parameters | Type  | Description | 
|:-----------|:------|:------------|
| `tealiumEvent` | `TealiumView` or `TealiumEvent` | A dispatch object with the event name and optional event data. |

To track events, pass a [`TealiumView`](#class-tealiumview) or [`TealiumEvent`](#class-tealiumevent) object to the `track()` method:

```swift
let tealiumEvent = TealiumView(
  &#34;purchase&#34;,
  dataLayer: [
    &#34;customer_id&#34;: &#34;abc123&#34;, 
    &#34;order_total&#34;: 10.00,
    &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
    &#34;order_id&#34;: &#34;0123456789&#34;
  ]
)
tealium?.track(tealiumEvent)
```

### `visitor`

Returns the full AdobeVisitor instance.

```swift
var tealium: Tealium?
//...
let visitor = tealium?.adobeVisitorApi?.visitor
let id: String? = visitor?.experienceCloudId
let nextRefresh: Date? = visitor?.nextRefresh
let blob: String? = visitor?.blob
let region: String? = visitor?.dcsRegion
let ttl: String? = visitor?.idSyncTTL
```

### `visitorId`

Returns a randomly generated and unique persistent visitor ID.

```swift
let visitorId: String? = tealium.visitorId
```

## Interface: `TealiumDispatch`

An interface that defines the type of dispatch to be tracked. The following classes implement `TealiumDispatch`:

### Class: `TealiumEvent`

To track a user&#39;s interaction with a screen or a screen view, pass an instance of `TealiumEvent(tealiumEvent:dataLayer:)` to the [`Track()`](#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```swift
let tealEvent = TealiumEvent(tealiumEvent, dataLayer: eventData)
tealium?.track(tealEvent)
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| The event name passed as `tealium_event`.| 
| `eventData` | `Dictionary&lt;string, object&gt;` | (Optional) Data to be sent with the event in key-value format. | 

Example:

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

### Class: `TealiumView`

To track screen views, pass an instance of `TealiumView(tealiumEvent:dataLayer:)` to the [`Track()`](#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```swift
let screenView = TealiumView(tealiumEvent, dataLayer: eventData)
tealium?.track(screenView)
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| The event name passed as `tealium_event`.| 
| `eventData` | `Dictionary&lt;string, object&gt;` | (Optional) Data to be sent with the event in key-value format. | 

Example:

```swift
let screenView = TealiumView(
  &#34;purchase&#34;, 
  dataLayer: [
    &#34;customer_id&#34;, &#34;abc123&#34;, 
    &#34;order_total&#34;: 10.00, 
    &#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;],     
    &#34;order_id&#34;: &#34;0123456789&#34;
  ]
)
tealium?.track(screenView)
```