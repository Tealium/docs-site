---
title: Lifecycle
description: Reference guide for Lifecycle class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/lifecycle/
---
## Class: `Lifecycle`

The following summarizes the methods of the `Lifecycle` class for manually tracking application lifecycle. To allow the Lifecycle module to manually track lifecycle events, disable lifecycle autotracking by setting the `TealiumConfig` option `isAutotrackingEnabled` to `false`. Usage of manual lifecycle tracking is only recommended for unconventional lifecycle paradigms.

| Method | Description |
| ----- | ------ |
|[`trackLaunchEvent()`](#tracklaunchevent) | Manually tracks launch event |
|[`trackSleepEvent()`](#tracksleepevent) | Manually tracks sleep event |
|[`trackWakeEvent()`](#trackwakeevent) | Manually tracks wake event |

### `trackLaunchEvent()`

Manually tracks launch event with optional data map.

```java
tealiumInstance.lifecycle?.trackLaunchEvent(mapOf("key" to "launch-value"))
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | `Map<String, Any>` | Map of custom data to send with launch event | mapOf("key" to "launch-value") |

### `trackSleepEvent()`

Manually tracks sleep event with optional data map.

```java
tealiumInstance.lifecycle?.trackSleepEvent(mapOf("key" to "sleep-value"))
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | `Map<String, Any>` | Map of custom data to send with sleep event | mapOf("key" to "sleep-value") |

### `trackWakeEvent()`

Manually tracks wake event with optional data map.

```java
tealiumInstance.lifecycle?.trackWakeEvent(mapOf("key" to "wake-value"))
```

| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | `Map<String, Any>` | Map of custom data to send with wake event | mapOf("key" to "wake-value") |
