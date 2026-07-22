---
title: Lifecycle Module
description: Automatically tracks app lifecycle events and associated data.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/lifecycle/
---## Usage

The Lifecycle module automatically tracks app lifecycle events and associated data. The launch event is triggered when the library is loaded for the first time, sleep event on `UIApplicationWillResignActive` notification and wake event on `UIApplicationDidBecomeActive`.

Usage of this module is recommended if you are using Adobe Analytics. Otherwise, it is optional, but the additional events captured (launch/wake/sleep) may be useful to you for other vendor implementations.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Requirements

If the `UIKit` dependency is added to the target app, no further configuration or implementation is necessary. For other platform builds (watchOS, macOS), the Lifecycle module functions may be triggered manually (see [API Reference](https://docs.tealium.com/platforms/ios-swift-v1/module-list/lifecycle/#api-reference)).

## Install

Install the Lifecycle module with CocoaPods or Carthage.

### CocoaPods

To install the Lifecycle module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod 'tealium-swift/TealiumLifecycle'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.


### Carthage

To install the Lifecycle module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```ruby
      TealiumLifecycle.framework
      ```
3. To import the Lifecycle library, add the following import statement to your project:   
      ```swift
      import TealiumLifecycle
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable  Name                     | Type | Description                                                                        | Example              |
|------------------------------------|-----------------------------------------------------------------------------------|---------|----------------------|
| `lifecycle_diddetect_crash`        | `Boolean` | Was a crash detected during this launch/wake event. Populated only if true.       | [`"true"`, `"false"`]                 |
| `lifecycle_dayofweek_local`        | `Number`  |Local day of week that call was made, such as 1=Sunday, 2=Monday.                   | `13`                   |
| `lifecycle_dayssincelaunch`        | `Number`  |Days since first launch in integer increments.                                      | `23`                   |
| `lifecycle_dayssinceupdate`        | `Number`  |Days since the last detected app version update in integer increments.              | `46`                   |
| `lifecycle_dayssincelastwake`      | `Number`  | Days since last detected wake in integer increments.                               | `1`                    |
| `lifecycle_firstlaunchdate`        | `String` | GMT timestamp of the first detected launch/wake in ISO 8601 format from UTC.   | `"2013-07-11T17:55:04Z"` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | `String` |GMT Timestamp formatted as MM/DD/YYYY.                                             | `"01/18/2012" `          |
| `lifecycle_hourofday_local`        | `String` |Local hour of day that call was made (24 hour format).                               | [`"true"`, `"false"`]                 |
| `lifecycle_isfirstlaunch`          | `String` |Only present if call is the first launch/wake call.                                  | [`"true"`, `"false"`]                 |
| `lifecycle_isfirstlaunchupdate` | `Boolean` |Only present if call is first launch/wake after a detected updated.                 | [`"true"`, `"false"`] |
| `lifecycle_isfirstwakemonth`    | `Boolean` |Only present if call is first launch/wake of the month.                                 | [`"true"`, `"false"`] |
| `lifecycle_isfirstwaketoday`    | `Boolean` | Only present if call is first launch/wake of the day.                       | [`"true"`, `"false"`] |
| `lifecycle_launchcount`         | `Number`  |Total number of launches this version of your app (since the last update).                                       | `3`    |
| `lifecycle_priorsecondsawake`   | `Number`  |Whole seconds app was awake since last launch only. Aggregates total from all wakes prior. Sent only with `lifecycle_type:launch` calls.  | `126`  |
| `lifecycle_secondsawake`        | `Number`  |Whole seconds app was awake since most recent wake/launch.                                                                             | `30`   |
| `lifecycle_sleepcount`          | `Number`  |Total number of times your app has gone to sleep (resets if updated).                                                                    | `5`    |
| `lifecycle_totalcrashcount`     | `Number`  |Total number of crashes counted since install (only reset if app deleted).                                                             | `21`   |
| `lifecycle_totallaunchcount`    | `Number`  |Total number of launches since install (only reset if app deleted)                                             | `3`     |
| `lifecycle_totalsecondsawake`   | `Number`  |Total number of seconds your app has been in a woken/active state since app install (only reset if app deleted). | `36`    |
| `lifecycle_totalsleepcount`     | `Number`  |Total number of times your app has gone into the background since app install (only reset if app deleted).    | `400` |
| `lifecycle_totalwakecount`      | `Number`  |Total number of launches + wakes since install (only reset if app deleted). |  `"563"` |
| `lifecycle_updatelaunchdate`    | `String`  |GMT timestamp of first wake/launch after a version update has been detected .     |  `"2014-09-08T18:10:01Z"` |
| `lifecycle_type`                | `String`  |Type of lifecycle call. | [`"launch"`, `"wake"`, `"sleep"` ]                |
| `lifecycle_wakecount`           | `Number`  |Total number of launches + wakes in this version of your app (resets if updated).  | `"29"`                 |

## Crash Detection

The Lifecycle module performs basic crash detection, but does not collect any details about the cause of the crash. It records a crash whenever a lifecycle launch event is seen, without a preceding sleep event.

Normally, when an app is closed by the user, a notification from the OS triggers a lifecycle sleep event, but if the app crashes, there is no time for this to happen, and thus, no sleep event takes place. On the subsequent launch after the crash, the `lifecycle_diddetectcrash` variable is set to `true`, and the `lifecycle_totalcrashcount` variable is incremented by 1.

If you require more advanced crash detection, our Crash Reporter module provides full details of each crash, and the reasons for the crash. This is currently supported on iOS only.

## API Reference
You only need to use these API methods if you are targeting a platform that doesn't support `UIKit`.

### `launchDetected()`
Updates lifecycle records with a launch event and trigger a lifecycle event dispatch.

```
func someMethodCalledAtLaunchTime {
    tealium?.lifecycle()?.launchDetected()

}
```

### `wakeDetected()`
Updates lifecycle records with a wake event and trigger a lifecycle event dispatch.

```
func someMethodCalledWhenAppStarts {
    tealium?.lifecycle()?.wakeDetected()

}
```

<blockquote>
`wakeDetected()` calls are safely added after a `launchDetected()` in the same function. The module only accepts a single launch event per instantiated instance.
</blockquote>



### `sleepDetected()`
Update lifecycle records with a sleep event and trigger a lifecycle event dispatch.

```
func someMethodCalledBeforeAppTerminated {
    tealium?.lifecycle()?.sleepDetected()
}
```

### `dictionary`

Property that provides read-only access to the lifecycle data as a `[String: Any]` dictionary.

```
// retrieves the total wake count from the lifecycle data dictionary
let wakeCount = tealium?.lifecycle()?.dictionary?["lifecycle_totalwakecount"]
```
