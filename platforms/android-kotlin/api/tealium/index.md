---
title: Tealium
description: Reference guide for Tealium class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/tealium/
---
## Class: `Tealium`

The `Tealium` class provides methods for tracking screen views and events. The following document summarizes the commonly used methods and properties of the `Tealium` class for Kotlin. Individual modules may also provide their own extensions for the `Tealium` class if they are enabled.

| Method/Property                                           | Description                                                                                       |
|:----------------------------------------------------------|:--------------------------------------------------------------------------------------------------|
| [`cancelTimedEvent()`](#canceltimedevent)                 | Cancels the timer for a timed event.                                                              |
| [`consentManager`](#consentmanager)                       | Access to the consent manager to set the user consent preferences.                       |
| [`dataLayer`](#datalayer)                                 | Access to persistent storage on the device - items within the data layer are added to each event. |
| [`endTraceVisitorSession()`](#endtracevisitorsession)     | Ends the visitor session remotely to test end of session events.                                  |
| [`events`](#events)                                       | Lets you provide listener classes to a numerous events throughout the Tealium SDK.           |
| [`gatherTrackData()`](#gathertrackdata)                   | Exposes all track data for data layer and Collectors.                                             |
| [`joinTrace()`](#jointrace)                               | Adds the supplied trace ID to the data layer for the current session.                             |
| [`leaveTrace()`](#leavetrace)                             | Leaves the trace by removing the trace ID.                                                        |
| [`linkEcidToKnownIdentifier`](#linkecidtoknownidentifier) | Links the current ECID to a known secondary ID.                                                   |
| [`modules`](#modules)                                     | Provides access to the modules within the system.                                                 |
| [`resetVisitor()`](#resetvisitor)                         | Resets the visitor ECID by retrieving a new one on the next tracking call.                        |
| [`sendQueuedDispatches()`](#sendqueueddispatches)         | Requests that any DispatchValidators be re-evaluated.                                             |
| [`session`](#session)                                     | Provides information relating to the current session.                                             |
| [`startTimedEvent()`](#starttimedevent)                   | Starts a timed event with the given name.                                                         |
| [`stopTimedEvent()`](#stoptimedevent)                     | Stops the timer for a timed event which triggers the `timed_event` tracking call.                 |
| [`Tealium`](#tealium)                                     | Constructor method that creates a `Tealium` instance.                                             |
| [`track()`](#track)                                       | Method for tracking your Screen views or events.                                                  |
| [`visitor`](#visitor)                                     | Returns the full `AdobeVisitor` instance.                                                         |
| [`visitorId`](#visitorid)                                 | The current Visitor ID that is stored in the data layer.                                          |


### `cancelTimedEvent()`

Cancels a previously started timed event. The timed event is not tracked.

```java
tealium.cancelTimedEvent(name: "TIMED_EVENT_NAME")
```

| Parameters | Type     | Description                 |
|:-----------|:---------|:----------------------------|
| `name`     | `String` | The name of the timed event |

### `consentManager`

Lets you set your current consent status and categories, and see the current policy enforced. Learn more in the [consent management](https://docs.tealium.com/platforms/android-kotlin/consent-management/) guide.

```java
tealium.consentManager.userConsentStatus = ConsentStatus.CONSENTED
```

### `dataLayer`

Provides persistent storage on the device for key-value pairs, while also allowing you to set expiry times. Each entry is also added to every dispatch that you send through the [`track()`](#track) method. Learn more in the [Data Management](https://docs.tealium.com/platforms/android-kotlin/data-layer/) guide.

```java
tealium.dataLayer.putString("key", "value", Expiry.FOREVER)
```

### `endTraceVisitorSession()`

Ends the visitor session remotely. Does not terminate the SDK session or reset the session ID.

```java
Tealium["INSTANCE_NAME"]?.endTraceVisitorSession()
```

### `events`

Provides listener classes to your `Tealium` instance to receive useful information from the SDK.

The following example registers a listener for any consent preference changes. This listener is provided with the new consent preferences and the current policy enforced.
Additional listeners available at `com.tealium.core.messaging`.

```java
tealium.events.subscribe(object: UserConsentPreferencesUpdatedListener {
    override fun onUserConsentPreferencesUpdated(userConsentPreferences: UserConsentPreferences, policy: ConsentManagementPolicy) {
        // take action on consent changes
    }
})
```

### `gatherTrackData()`

Retrieves track data from data layer and Collectors.

```java
Tealium["INSTANCE_NAME"]?.gatherTrackData()
```

### `joinTrace()`

Adds the supplied trace ID to the data layer for the current session.

```java
Tealium["INSTANCE_NAME"]?.joinTrace(traceId)
```

| Parameters | Type     | Description |
|:-----------|:---------|:------------|
| `traceId`  | `String` | Trace ID    |


### `leaveTrace()`

Leaves the trace by removing the trace ID.

```java
Tealium["INSTANCE_NAME"]?.leaveTrace()
```

### `linkEcidToKnownIdentifier()`

Links the current ECID to a known secondary identifier, such as an email address or other internal ID.

```java
linkEcidToKnownIdentifier(
  knownId: String,
  adobeDataProviderId: String,
  authState: Int?,
  adobeResponseListener: ResponseListener<AdobeVisitor>?
  )
```

| Parameters              | Type                             | Description                         |
|:------------------------|:---------------------------------|:------------------------------------|
| `knownId`               | `String`                         | The known identifier.               |
| `adobeDataProviderId`   | `String`                         | The Adobe data provider identifier. |
| `authState`             | `Int`                            | The authenticated state.            |
| `adobeResponseListener` | `ResponseListener<AdobeVisitor>` | The Adobe response listener.        |


Example:

```java
var tealium: Tealium?
...

tealium.adobeVisitorApi?.linkEcidToKnownIdentifier(
  "myidentifier",
  "123456",
  AdobeAuthState.AUTH_STATE_AUTHENTICATED,
  null
  )
```

### `modules`

Provides access to the Module Manager for the SDK, and used to provide access to specific modules.

```java
tealium.modules.getModule(VisitorService::class.java)?.delegate = myDelegate
```

### `resetVisitor()`

Resets the visitor ECID by retrieving a new one on the next tracking call.

```java
resetVisitor()
```

Example:

```java
var tealium: Tealium?
//...
tealium?.adobeVisitorApi?.resetVisitor()
```


### `sendQueuedDispatches()`

Dispatches are queued for a number of reasons by any DispatchValidator. You may request that they be re-evaluated using this method which ignores the event batching restrictions, but adheres to other DispatchValidators. For example, if there was no connectivity and there is still no connectivity then queued dispatches remain queued.

```java
tealium.sendQueuedDispatches()
```

### `session`

Contains all data relating to the current Session.

```java
val sessionId = tealium.session.id
```

### `startTimedEvent()`

Starts a timed event with the given name. If this method is called again with the same event name, it is ignored if the event has not been ended or canceled. The event start time is not persisted.   

If optional data is passed along with the event name, it is added to the track call when the timer is stopped with the [`stopTimedEvent()`](#stoptimedevent) call.

```java
tealium.startTimedEvent(name: "TIMED_EVENT_NAME", mapOf("custom_value" to "custom_key"))
```

| Parameters                              | Type     | Description                                                                 |
|:----------------------------------------|:---------|:----------------------------------------------------------------------------|
| `name`                                  | `String` | The name of the timed event                                                 |
| `mapOf("custom_key" to "custom_value")` | `Map`    | (Optional) An object of key-value pair data to be tracked in the data layer |

### `stopTimedEvent()`

Stops the timer for a timed event which triggers the `timed_event` tracking call.

```java
tealium.stopTimedEvent(name: "TIMED_EVENT_NAME")
```

| Parameters | Type     | Description                 |
|:-----------|:---------|:----------------------------|
| `name`     | `String` | The name of the timed event |


### `Tealium`

Constructor method that creates a `Tealium` instance.

```java
val config = TealiumConfig(key, config);
```

| Parameters | Type             | Description                            | Example         |
|:-----------|:-----------------|:---------------------------------------|:----------------|
| `key`      | `String`         | New Tealium instance name              | `"abc123"`      |
| `config`   | `Tealium.Config` | The configuration for the new instance | `tealConfigObj` |


```java
// Assuming execution is within Application.onCreate()
val config = TealiumConfig(this, "ACCOUNT_NAME", "PROFILE_NAME", Environment.PROD)
val tealium = Tealium.create("main", config)
```

Modules are initialized on a background Thread and therefore may not be ready directly after creation of the Tealium object. Add a completion block to add any subsequent required configuration as soon as the instance is ready:

```java
val tealium = Tealium.create("main", config) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev("--", "VisitorProfile updated: $visitorProfile")
        }
    })
}
```

### `track()`

Tracks a screen view or event with optional event data.

```java
tealium.track(tealiumlEvent)
```

| Parameters  | Type         | Description       | 
|:------------|:-------------|:------------------|
| `tealiumlEvent`  | `TealiumView` or `TealiumEvent`     | A dispatch object with the event name and optional event data.   |

To track events, pass a [`TealiumView`](#class-tealiumview) or [`TealiumEvent`](#class-tealiumevent) object to the `track()` method:

```java
val tealiumlEvent = TealiumView(
  "purchase", 
  mutableMapOf(
    "customer_id" to "abc123", 
    "order_total" to 10.00, 
    "product_id" to listOf("PROD123", "PROD456"),
    "order_id" to "0123456789"
  )
)
tealium.track(tealiumlEvent);
```

### `visitor`

Returns the full AdobeVisitor instance.

```java
var tealium: Tealium?
//...
val visitor = tealium.adobeVisitorApi?.visitor?.let { visitor ->
    val ecid = visitor.experienceCloudId
    val nextRefresh = visitor.nextRefresh
    val blob = visitor.blob
    val region = visitor.region
    val idSyncTTL = visitor.idSyncTTL
}
```

### `visitorId`

The current String for the Visitor ID. It is stored within the data layer, and may be overridden if required.

```java
val visitorId = tealium.visitorId
```

## Interface: `TealiumDispatch`

An interface that defines the type of dispatch to be tracked. The following classes implement `TealiumDispatch`:

### Class: `TealiumEvent`

To track a user's interaction with a screen, pass an instance of `TealiumEvent(tealiumEvent, eventData)` to the [`Track()`](#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional mutable map.

```java
val tealiumEvent = TealiumEvent(tealiumEvent, eventData)
tealium.track(tealiumEvent);
```

| Parameters  | Type    | Description      |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | The event name, passed as the `tealium_event` attribute.  |
| `eventData` | `MutableMap<String, Any>` | (Optional) Data to be sent with the event in key-value format. | 

Example:

```java
val tealiumEvent = TealiumEvent(
  "cart_add", 
  mutableMapOf(
    "customer_id" to "abc123", 
    "product_id" to listOf("PROD123", "PROD456"),
    "product_price" to listOf(4.00, 6.00)
  )
)
tealium.track(tealiumEvent);
```

### Class: `TealiumView`

To track screen views, pass an instance of `TealiumView(tealiumEvent, eventData)` to the [`Track()`](#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional mutable map.

```java
val tealiumView = TealiumView(tealiumEvent, eventData)
tealium.track(tealiumView);
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| `tealium_event` name of view event or screen.          | 
| `eventData` | `MutableMap<String, Any>` | (Optional) Data to be sent with the event in key-value format. |

Example:

```java
val tealiumView = TealiumView(
  "purchase", 
  mutableMapOf(
    "customer_id" to "abc123", 
    "order_total" to 10.00, 
    "product_id" to listOf("PROD123", "PROD456"),
    "order_id" to "0123456789"
  )
)
tealium.track(tealiumView);
```