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
| `key` | `String` |New Tealium instance name |  `&#34;abc123&#34;` |
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
Tealium instance = Tealium.getInstance(&#34;my_instance_name&#34;);
instance.requestFlush();
```


### `trackEvent()`

Track a non-view event.

```java
Map&lt;String, Object&gt; data = new HashMap&lt;&gt;(1);
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);
Tealium.getInstance(&#34;INSTANCE KEY&#34;).trackEvent(eventName, data);
```

| Parameter | Type | Description  | Example |
|-----------|-------------| ---- | ------- |
| `eventName`| `String` |Non-view event name | `&#34;Button Click&#34;` |
| `data`    |`[Map&lt;String, dynamic&gt;]` | (Optional) Event data as key-value pairs (Use `null` if none)| `{&#34;key1&#34;: &#34;value1&#34;}` |


### `trackView()`

Track a presented view.

```java
Map&lt;String, Object&gt; data = new HashMap&lt;&gt;(1);
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);
Tealium.getInstance(&#34;INSTANCE KEY&#34;).trackView(screenName, data);
```
| Parameter | Type | Description | Example |
|-----------|------| ---- | ------- |
| `screenName`| `String` | View screen name | `&#34;Home screen&#34;` |
| `data`    | `[Map&lt;String, dynamic&gt;]` | (Optional) Event data as key-value pairs (Use `null` if none)| `{&#34;key1&#34;: &#34;value1&#34;}` |
