---
title: Lifecycle
description: Reference guide for LifeCycle class and methods provided by Tealium for Android.
url: https://docs.tealium.com/platforms/android-java/api/life-cycle/
---
## Class: `LifeCycle`

The following summarizes the commonly used methods of the `Lifecycle` class.

| Method | Description |
| ----- | ------ |
|`setupInstance()` | Sets up the applications's lifecycle instance |


### `setupInstance()`

Sets up the applications's lifecycle instance. This method needs to be called prior to calling `Tealium.createInstance(config)` in order for the data to track correctly

```java
setupInstance(instanceId, config, isAutoTracking);
```

| Parameters  | Type | Description | Example |
| --- | --- | --- | --- |
| `instanceId` | `String` | Tealium instance name |  `"abc123"`  |
| `config` | `Tealium.Config` | Tealium configuration object |  `"configObject"`  |     
| `isAutoTracking` | `boolean` | Is auto-tracking enabled? |  [`"true"`, `"false"`]  |                      
