---
title: Lifecycle Module
description: Automatically tracks app lifecycle events and associated data.
url: https://docs.tealium.com/platforms/ios-swift/module-list/lifecycle/
---## Usage

The Lifecycle module automatically tracks app lifecycle events and associated data. The launch event is triggered when the library is loaded for the first time, sleep event on `UIApplicationWillResignActive` notification and wake event on `UIApplicationDidBecomeActive`.

Usage of this module is recommended if you are using Adobe Analytics. Otherwise, it is optional, but the additional events captured (launch/wake/sleep) may be useful to you for other vendor implementations.

The following platforms are supported:

* iOS
* tvOS
* watchOS
* macOS

## Requirements

If the `UIKit` dependency is added to the target app, no further configuration or implementation is necessary.  For other platform builds (watchOS, macOS), the Lifecycle module functions may be triggered manually (see [API Reference](/platforms/ios-swift/module-list/lifecycle/#api-reference)).

## Install

Install the Lifecycle module with Swift Package Manager, CocoaPods or Carthage.

### Swift Package Manager (Recommended)

Supported in version 1.9.0&#43;, the Swift Package Manager is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File &gt; Add Package Dependencies**.
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `&#34;Up to next major&#34;` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
1. Select the `Lifecycle` module from the list of modules to install and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**.

Learn more about the [Swift Package Manager installation for iOS](/platforms/ios-swift/install/#swift-package-manager-recommended).

### CocoaPods

To install the Lifecycle module with CocoaPods, add the following pod to your Podfile:  
```perl
pod &#39;tealium-swift/Lifecycle&#39;
```

Learn more about the [CocoaPods installation for iOS](/platforms/ios-swift/install/#cocoapods).


### Carthage

To install the Lifecycle module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```perl
      TealiumLifecycle.framework
      ```
3. To import the Lifecycle library, add the following import statement to your project:   
      ```swift
      import TealiumLifecycle
      ```

Learn more about the [Carthage installation for iOS](/platforms/ios-swift/install/#carthage).

## Configure

To instantiate the Lifecycle module, you must specify it in your `TealiumConfig` object when initializing the SDK:

```swift
import TealiumCore
import TealiumInAppPurchase

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           datasource: &#34;DATASOURCE&#34;)

config.collectors = [Collectors.Lifecycle]
tealium = Tealium(config: config) { _ in }
```

Review the [Collectors](/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.

## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable  Name                     | Type | Description                                                                        | Example              |
|------------------------------------|-----------------------------------------------------------------------------------|---------|----------------------|
| `lifecycle_diddetect_crash`        | `Boolean` | Was a crash detected during this launch/wake event.  Populated only if true.       | [`&#34;true&#34;`, `&#34;false&#34;`]                 |
| `lifecycle_dayofweek_local`        | `Number`  |Local day of week that call was made, such as 1=Sunday, 2=Monday.                   | `13`                   |
| `lifecycle_dayssincelaunch`        | `Number`  |Days since first launch in integer increments.                                      | `23`                   |
| `lifecycle_dayssinceupdate`        | `Number`  |Days since the last detected app version update in integer increments.              | `46`                   |
| `lifecycle_dayssincelastwake`      | `Number`  | Days since last detected wake in integer increments.                               | `1`                    |
| `lifecycle_firstlaunchdate`        | `String` | GMT timestamp of the first detected launch/wake in ISO 8601 format from UTC.   | `&#34;2013-07-11T17:55:04Z&#34;` |
| `lifecycle_firstlaunchdate_MMDDYYYY` | `String` |GMT Timestamp formatted as MM/DD/YYYY.                                             | `&#34;01/18/2012&#34; `          |
| `lifecycle_hourofday_local`        | `String` |Local hour of day that call was made (24 hour format).                               | [`&#34;true&#34;`, `&#34;false&#34;`]                 |
| `lifecycle_isfirstlaunch`          | `String` |Only present if call is the first launch/wake call.                                  | [`&#34;true&#34;`, `&#34;false&#34;`]                 |
| `lifecycle_isfirstlaunchupdate` | `Boolean` |Only present if call is first launch/wake after a detected updated.                 | [`&#34;true&#34;`, `&#34;false&#34;`] |
| `lifecycle_isfirstwakemonth`    | `Boolean` |Only present if call is first launch/wake of the month.                                 | [`&#34;true&#34;`, `&#34;false&#34;`] |
| `lifecycle_isfirstwaketoday`    | `Boolean` | Only present if call is first launch/wake of the day.                       | [`&#34;true&#34;`, `&#34;false&#34;`] |
| `lifecycle_launchcount`         | `Number`  |Total number of launches this version of your app (since the last update).                                       | `3`    |
| `lifecycle_priorsecondsawake`   | `Number`  |Whole seconds app was awake since last launch only. Aggregates total from all wakes prior. Sent only with `lifecycle_type:launch` calls.  | `126`  |
| `lifecycle_secondsawake`        | `Number`  |Whole seconds app was awake since most recent wake/launch.                                                                             | `30`   |
| `lifecycle_sleepcount`          | `Number`  |Total number of times your app has gone to sleep (resets if updated).                                                                    | `5`    |
| `lifecycle_totalcrashcount`     | `Number`  |Total number of crashes counted since install (only reset if app deleted).                                                             | `21`   |
| `lifecycle_totallaunchcount`    | `Number`  |Total number of launches since install (only reset if app deleted)                                             | `3`     |
| `lifecycle_totalsecondsawake`   | `Number`  |Total number of seconds your app has been in a woken/active state since app install (only reset if app deleted). | `36`    |
| `lifecycle_totalsleepcount`     | `Number`  |Total number of times your app has gone into the background since app install (only reset if app deleted).    | `400` |
| `lifecycle_totalwakecount`      | `Number`  |Total number of launches &#43; wakes since install (only reset if app deleted). |  `&#34;563&#34;` |
| `lifecycle_updatelaunchdate`    | `String`  |GMT timestamp of first wake/launch after a version update has been detected .     |  `&#34;2014-09-08T18:10:01Z&#34;` |
| `lifecycle_type`                | `String`  |Type of lifecycle call. | [`&#34;launch&#34;`, `&#34;wake&#34;`, `&#34;sleep&#34;` ]                |
| `lifecycle_wakecount`           | `Number`  |Total number of launches &#43; wakes in this version of your app (resets if updated).  | `&#34;29&#34;`                 |

## Crash Detection

The Lifecycle module performs basic crash detection, but does not collect any details about the cause of the crash. It records a crash whenever a lifecycle launch event is seen, without a preceding sleep event.

Normally, when an app is closed by the user, a notification from the OS triggers a lifecycle sleep event, but if the app crashes, there is no time for this to happen, and thus, no sleep event takes place. On the subsequent launch after the crash, the `lifecycle_diddetectcrash` variable is set to `true`, and the `lifecycle_totalcrashcount` variable is incremented by 1.

If you require more advanced crash detection, our Crash Reporter module provides full details of each crash, and the reasons for the crash. This is currently supported on iOS only.

## API Reference

You only need to use the following API methods if you are targeting a platform that doesn&#39;t support `UIKit`.

### `launchDetected()`
Updates lifecycle records with a launch event and trigger a lifecycle event dispatch.

```
func someMethodCalledAtLaunchTime {
    tealium?.lifecycle?.launchDetected()

}
```

### `wakeDetected()`
Updates lifecycle records with a wake event and trigger a lifecycle event dispatch.

```
func someMethodCalledWhenAppStarts {
    tealium?.lifecycle?.wakeDetected()

}
```
 `wakeDetected()` calls are safely added after a `launchDetected()` in the same function. The module only accepts a single launch event per instantiated instance. 


### `sleepDetected()`
Update lifecycle records with a sleep event and trigger a lifecycle event dispatch.

```
func someMethodCalledBeforeAppTerminated {
    tealium?.lifecycle?.sleepDetected()
}
```

### `dictionary`

Property that provides read-only access to the lifecycle data as a `[String: Any]` dictionary.

```
// retrieves the total wake count from the lifecycle data dictionary
let wakeCount = tealium?.lifecycle?.dictionary?[&#34;lifecycle_totalwakecount&#34;]
```
