---
title: Lifecycle Tracking Module
description: Provides app lifecycle tracking events to an existing 5.x implementation of Tealium for iOS.
url: https://docs.tealium.com/platforms/ios-objective-c/module-list/lifecycle-tracking/
---

## Install

The Lifecycle Tracking module must be added to your app. Install the module with CocoaPods or manually similar to the Tealium for iOS library.  

In any abstraction class (like `TealiumHelper.h`) replace any `@import TealiumIOS` with `@import TealiumIOSLifecycle`.

### CocoaPods

To install the Lifecycle Tracking module with CocoaPods, add the following to your Podfile:

```perl
pod &#39;TealiumIOSLifecycle&#39;
```

### Manual

To install the Lifecycle Tracking module manually, following these steps:

1. Download the [Lifecycle Tracking module](https://github.com/Tealium/tealium-ios/tree/master/TealiumIOSLifecycle.framework).

2. Add the `TealiumIOSLifecycle.framework` file to your project (in the Embedded Binaries section).

## Track

The module tracks the following lifecycle events:

| Lifecycle Event | Description |
| --- | --- |
| `launch` | App is launched |
| `sleep` | App sent to background |
| `wake` | App sent to foreground |
| `none` | For data added to events but not associated with a lifecycle event |

These values are indicated in the `lifecycle_type` variable.

### Automatic Tracking

Configure the Lifecycle Tracking module to automatically listen for the standard `UIApplication` notifications to automatically trigger `launch`, `wake` and `sleep` events.

Unlink or remove the `TealiumIOSLifecycle.framework` from your project to remove lifecycle tracking.

**Launch Event**  
Generated on detection of `UIApplicationDidFinishLaunchingNotification`.

**Sleep Event**   
Generated on detection of `UIApplicationWillResignActiveNotification`.

**Wake Event**  
Generated on detection of `UIApplicationWillEnterForegroundNotification`.

### Manual Tracking

Available for specific lifecycle paradigms and non-conventional lifecycle tracking. To manually track lifecycle events, disable lifecycle auto-tracking by setting `setLifecycleAutotrackingIsEnabled` to `NO`.

**Launch Event**  
To manually track a `launch` event, call:

```objc
[[Tealium instanceForKey:@&#34;(uniqueInstanceId)&#34;] launch];
```

**Sleep Event**  
To manually track a `sleep` event, call:

```objc
[[Tealium instanceForKey:@&#34;(uniqueInstanceId)&#34;] sleep];
```

**Wake Event**  
To manually track a `wake` event, call:

```objc
[[Tealium instanceForKey:@&#34;(uniqueInstanceId)&#34;] wake];
```

## Data Layer

The Lifecycle Tracking module adds the following data layer variables:

| Variable | Type | Description | Example | Event |
| --- | --- | --- | --- | --- |
| `lifecycle_ dayofweek_local` | `Number` | Local day of week that call was made, such as 1=Sunday, 2=Monday | `2` | all |
| `lifecycle_ dayssincelaunch` | `Number` | Days since first launch in integer increments| `23` | all |
| `lifecycle_ dayssinceupdate` | `Number` | Days since the last detected app version update in integer increments| `46` | all |
| `lifecycle_ dayssincelastwake` | `Number` | Days since last detected wake in integer increments | `1` | all |
| `lifecycle_ diddetectcrash` | `Boolean` | Crash inferred from missing prior sleep event (only present if a launch event follows a wake event) | [`true`, `false`] | launch |
| `lifecycle_ firstlaunchdate` | `String` | GMT timestamp of the first detected launch/wake in ISO 8601 format from UTC | `&#34;2013-07-11T17:55:04Z&#34;`  | all  |
| `lifecycle_ firstlaunchdate_ MMDDYYYY ` | `String` | GMT Timestamp formatted as MM/DD/YYYY  | `&#34;01/17/2012&#34;` |  all |
| `lifecycle_ hourofday_local` | `String` | Local hour of day that call was made (24 hour format)  | `&#34;12&#34;` |  all |
| `lifecycle_ isfirstlaunch` | `Boolean` |Only present if call is the first launch call | [`true`, `false`] | launch |
| `lifecycle_ isfirstlaunchupdate` | `Boolean` |Only present if call is first launch after a detected updated  | [`true`, `false`] | launch |
| `lifecycle_ isfirstwakemonth` | `Boolean` |Only present if call is first launch/wake of the month | [`true`, `false`] | launch, wake  |
| `lifecycle_ isfirstwaketoday` | `Boolean` |Only present if call is first launch/wake of the day   | [`true`, `false`] | launch, wake |
| `lifecycle_ launchcount` | `Number` |Total number of launches this version of your app (since the last update) |  `3` |  all |
| `lifecycle_ secondsawake` | `Number` |Whole seconds app was awake since last wake/launch (sent only with `lifecycle_type:sleep` or `lifecycle_type:terminate` calls) |  `30` | all  |
| `lifecycle_ priorsecondsawake ` | `Number` |Whole seconds app was awake since last launch only - aggregates total from all wakes prior (sent only with `lifecycle_type:launch` calls)  | `126` |  all |
| `lifecycle_ sleepcount` | `Number` |Total number of times your app has gone to sleep (resets if updated) |  `5`  |  all |
| `lifecycle_ totalcrashcount` | `Number` |Total number of crashes counted since install (only reset if app deleted)  |`21 ` |  all |
| `lifecycle_ totallaunchcount` | `Number` |Total number of launches since install (only reset if app deleted)  | `3`  |  all |
| `lifecycle_ totalsecondsawake` | `Number` |Total number of seconds your app has been in a woken/active state since app install (only reset if app deleted) | `36` |  all |
| `lifecycle_ totalsleepcount` |`Number` | Total number of times your app has gone into the background since app install (only reset if app deleted) |  `&#34;400&#34;` |  all |
| `lifecycle_ totalwakecount` | `Number` |Total number of launches &#43; wakes since install (only reset if app deleted)  |`563` |  all |
| `lifecycle_type` | `String` | Type of lifecycle call |  [`&#34;launch&#34;`, `&#34;wake&#34;`, `&#34;sleep&#34;`] |  all |
| `lifecycle_ updatelaunchdate` | `String` |GMT timestamp of first wake/launch after a version update has been detected | `&#34;2014-09-08T18:10:01Z&#34;` |  all |
| `lifecycle_ wakecount` | `Number` | Total number of launches &#43; wakes in this version of your app (resets if updated) | ` 29` |  all |
