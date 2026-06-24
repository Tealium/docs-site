---
title: Lifecycle module
description: Tracks app lifecycle events such as launch, wake, and sleep.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/lifecycle/
---
## How it works

The Lifecycle module tracks app lifecycle events and adds lifecycle metrics to tracked events. The Lifecycle module automatically detects when the app is launched, moved to the foreground (wake), or moved to the background (sleep).

### Event names

The module tracks the following lifecycle events:

| Event | Description |
| :--- | :--- |
| `launch` | Tracked on first app start in a session. |
| `wake` | Tracked when the app returns to the foreground from being in the background for 5 or more seconds. |
| `sleep` | Tracked when the app moves to the background and does not return to the foreground within 5 seconds. |

### Crash detection

The Lifecycle module infers a crash when a launch event occurs without a preceding sleep event. On the subsequent launch, `lifecycle_diddetectcrash` is set to `true` and `lifecycle_totalcrashcount` is incremented.

### Data layer

The following variables are added to each tracking call while the module is enabled:

| Variable | Description | Example |
| :--- | :--- | :--- |
| `lifecycle_dayofweek_local` | Local day of week when the call was made (1 = Sunday, 7 = Saturday) | `2` |
| `lifecycle_dayssincelaunch` | Days since the first app launch, in integer increments | `23` |
| `lifecycle_dayssinceupdate` | Days since the last detected app version update, in integer increments | `46` |
| `lifecycle_dayssincelastwake` | Days since the last detected wake, in integer increments | `1` |
| `lifecycle_diddetectcrash` | Present only if a crash was inferred from a missing prior sleep event | `&#34;true&#34;` |
| `lifecycle_firstlaunchdate` | GMT timestamp of the first detected launch, in ISO 8601 format | `&#34;2013-07-11T17:55:04Z&#34;` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | GMT timestamp of the first detected launch, formatted as MM/DD/YYYY | `&#34;01/17/2012&#34;` |
| `lifecycle_hourofday_local` | Local hour of day when the call was made (24-hour format) | `&#34;12&#34;` |
| `lifecycle_isfirstlaunch` | Present only on the first ever launch call | `&#34;true&#34;` |
| `lifecycle_isfirstlaunchupdate` | Present only on the first launch after a detected app version update | `&#34;true&#34;` |
| `lifecycle_isfirstwakemonth` | Present only on the first launch or wake of the month | `&#34;true&#34;` |
| `lifecycle_isfirstwaketoday` | Present only on the first launch or wake of the day | `&#34;true&#34;` |
| `lifecycle_launchcount` | Number of launches for the current app version (resets on update) | `3` |
| `lifecycle_secondsawake` | Whole seconds the app was awake since the last wake or launch. Sent with `sleep` events. | `30` |
| `lifecycle_priorsecondsawake` | Whole seconds the app was awake before the current launch, aggregated across prior wakes. Sent with `launch` events. | `126` |
| `lifecycle_sleepcount` | Number of times the app has gone to sleep for the current app version (resets on update) | `5` |
| `lifecycle_totalcrashcount` | Total number of inferred crashes since install | `21` |
| `lifecycle_totallaunchcount` | Total number of launches since install | `3` |
| `lifecycle_totalsecondsawake` | Total seconds the app has been in the foreground since install | `36` |
| `lifecycle_totalsleepcount` | Total number of times the app has gone to the background since install | `400` |
| `lifecycle_totalwakecount` | Total number of launches and wakes since install | `563` |
| `lifecycle_type` | Type of lifecycle event | `&#34;launch&#34;`, `&#34;wake&#34;`, `&#34;sleep&#34;` |
| `lifecycle_updatelaunchdate` | GMT timestamp of the first launch or wake after a version update, in ISO 8601 format | `&#34;2014-09-08T18:10:01Z&#34;` |
| `lifecycle_wakecount` | Total number of launches and wakes for the current app version (resets on update) | `29` |

## Install



Add the `prism-lifecycle` dependency to your `build.gradle` file:

```kotlin
implementation(platform(&#34;com.tealium.prism:prism-bom:0.4.0&#34;))
implementation(&#34;com.tealium.prism:prism-lifecycle&#34;)
```


Add `TealiumPrismLifecycle` as a Swift Package Manager dependency using the repository URL `https://github.com/Tealium/tealium-prism-swift`.



## Initialize

To initialize the module, add it to the `modules` list in your `TealiumConfig`.



```kotlin
val config = TealiumConfig.Builder(
    accountName = &#34;my_account&#34;,
    profileName = &#34;my_profile&#34;,
    environment = Environment.PROD,
    modules = listOf(
        Modules.lifecycle(),
        // other modules...
    )
).build()
```


```swift
let config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
                           modules: [
                               Modules.lifecycle(),
                               // other modules...
                           ])
```



## Manual tracking

To track lifecycle events yourself, disable automatic lifecycle tracking and use the following methods.



```kotlin
Modules.lifecycle { settings -&gt;
    settings.setAutoTrackingEnabled(false)
}
```


```swift
Modules.lifecycle { settings in
    settings.setAutoTrackingEnabled(false)
}
```



Call the lifecycle event methods with an optional data object.

Calling these methods while automatic lifecycle tracking is enabled results in an error.



```kotlin
tealium.lifecycle.launch(dataObject)
tealium.lifecycle.wake(dataObject)
tealium.lifecycle.sleep(dataObject)
```


```swift
tealium.lifecycle.launch(dataObject)
tealium.lifecycle.wake(dataObject)
tealium.lifecycle.sleep(dataObject)
```

