---
title: Tealium
description: Reference guide for Tealium class and methods provided by Tealium for Android.
url: https://docs.tealium.com/platforms/android-java/api/tealium/
---

## Class: `Tealium`

The following summarizes the commonly used methods of the `Tealium` class.

| Method | Description |
| ----- | ------ |
| `createInstance()`| Create a new Tealium Multiton |
| `disableConsentManager()`| Disables consent manager |
| `getConsentManager()`| Returns the instance of consent manager if enabled |
| `requestFlush()` | Request to dispatch a batch queue of events |
| `trackEvent()` | Track an event |
| `trackView()` | Track a presented view |


### `createInstance()`

Create a new Tealium Multiton, and returns the newly created instance. Instances are accessible by `getInstance()` and destroyable by `destroyInstance()`. Multiple instances are supported.

```java
Tealium.createInstance(key, config);
```
| Parameters  | Type | Description | Example |
| --- | --- | --- | --- |
| `key` | `String` |New Tealium instance name |  `"abc123"` |
| `config` | `Tealium.Config` | The configuration for the new instance | `tealConfigObj` |

| Returns | Return Type |
| --- | --- |
| Tealium Multiton | `Tealium` |

### `disableConsentManager()`

Disables consent manager. Call this method after Tealium is fully initialized to disable consent manager.

```java
final Tealium tealiumInstance = Tealium.createInstance(TEALIUM_MAIN, config);

tealiumInstance.disableConsentManager();
```

### `getConsentManager()`

Returns the instance of consent manager if enabled.

```java
final Tealium tealiumInstance = Tealium.createInstance(TEALIUM_MAIN, config);

ConsentManager consentManager = tealiumInstance.getConsentManager();
```

| Returns | Return Type |
| --- | --- |
| Consent Manager | `ConsentManager` |

### `requestFlush()`

Request to dispatch a batch queue of events when the batch limit has not been reached. If all other dispatching checks are okay (online, consent management, dispatch validators), the queue is dispatched.

```java
Tealium instance = Tealium.getInstance("my_instance_name");
instance.requestFlush();
```


### `trackEvent()`

Track a non-view event.

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackEvent(eventName, data);
```

| Parameter | Type | Description  | Example |
|-----------|-------------| ---- | ------- |
| `eventName`| `String` |Non-view event name | `"Button Click"` |
| `data`    |`[Map<String, dynamic>]` | (Optional) Event data as key-value pairs (Use `null` if none)| `{"key1": "value1"}` |


### `trackView()`

Track a presented view.

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackView(screenName, data);
```
| Parameter | Type | Description | Example |
|-----------|------| ---- | ------- |
| `screenName`| `String` | View screen name | `"Home screen"` |
| `data`    | `[Map<String, dynamic>]` | (Optional) Event data as key-value pairs (Use `null` if none)| `{"key1": "value1"}` |
