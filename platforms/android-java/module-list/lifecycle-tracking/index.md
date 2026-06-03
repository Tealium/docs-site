---
title: Lifecycle Tracking Module
description: Provides app lifecycle tracking events.
url: https://docs.tealium.com/platforms/android-java/module-list/lifecycle-tracking/
---
## Install

Install the Lifecycle Tracking module with Maven or manually.

### Maven

To install the Lifecycle Tracking module using Maven:

1. In your project&#39;s top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      // Top-level build file where you add configuration options common to all sub-projects/modules.
      allprojects {
      repositories {
            mavenCentral()
            // Tealium Maven repo directive
            maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
            }
      }
      }
      ```

2. In your project module&#39;s `build.gradle` file, add the following Maven dependency:
      ```groovy
      dependencies {
      // only add if not already present
      implementation &#39;com.tealium:library:5.8.0&#39;
      // add lifecycle to list of dependencies
      implementation &#39;com.tealium:lifecycle:1.1.4&#39;
      }
      ```

### Manual

To install the Lifecycle Tracking module manually, following these steps:

1. Download the Tealium [Lifecycle Tracking Module](https://github.com/Tealium/tealium-android/tree/master/Modules/LifeCycle) module.

2. Copy the file `tealium.lifecycle-1.1.4.aar` into your project&#39;s `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation(name:&#39;tealium.lifecycle-1.1.4&#39;, ext:&#39;aar&#39;)
      }
      ```

## Auto-Tracked Events

The module tracks the following lifecycle events, set by the `lifecycle_type` variable:

| Lifecycle Event | Description |
| --- | --- |
| `launch` | Generated on the first `onActivityResumed` to occur. If `onActivityPaused` is called before `onActivityResumed` (when the library is initialized in the middle of the `Activity` lifecycle), then the module creation time is used to generate a `launch` event. |
| `sleep` | Generated 5 seconds after `onActivityPaused` is called and `onActivityResumed` was not called. This indicates that the application has been backgrounded because a new view has not been presented. |
| `wake` |  Generated during `onActivityResumed` when more than 5 seconds has elapsed since the last `onActivityPaused`. This indicates that `onActivityResumed` is called because the app is foregrounding and not because of a view change. |

Tealium lifecycle tracking solely associates usage with the activity lifecycle.

The library leverages the [Application.ActivityLifecycleCallbacks](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html) API and evaluates its conditions on [onActivityResumed](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html#onActivityResumed%28android.app.Activity%29) and [onActivityPaused](http://developer.android.com/reference/android/app/Application.ActivityLifecycleCallbacks.html#onActivityPaused%28android.app.Activity%29).

It is enabled with the following code:

```java
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
boolean isAutoTracking = true;

// Additional instance for Lifecycle Tracking
LifeCycle.setupInstance(&#34;INSTANCE_NAME&#34;, config, isAutoTracking);
// Standard Tealium instance
Tealium.createInstance(&#34;INSTANCE_NAME&#34;, config);
```

## Manually Tracked Events

Available for specific lifecycle paradigms and unconventional lifecycle tracking. This approach is not recommended for most implementations. To allow manual lifecycle tracking update your lifecycle initiation code to set `isAutoTracking` to `false`.

To manually track a `launch` event, call the `trackLaunchEvent()` method:

```java
LifeCycle lifeCycle = LifeCycle.getInstance(TEALIUM_INSTANCE_ID);

if(lifeCycle != null) {

    // OPTIONAL
    Map&lt;String, String&gt; data = new HashMap&lt;&gt;();
    data.put(&#34;boot_time&#34;, &#34;5ms&#34;);

    lifeCycle.trackLaunchEvent(data);
}
```

To manually track a `sleep` event, call the `trackSleepEvent()` method:

```java
LifeCycle lifeCycle = LifeCycle.getInstance(TEALIUM_INSTANCE_ID);

if(lifeCycle != null) {

    // OPTIONAL
    Map&lt;String, String&gt; data = new HashMap&lt;&gt;();
    data.put(&#34;foreground_time&#34;, &#34;4000ms&#34;);

    lifeCycle.trackSleepEvent(data);
}
```

To manually track a `wake` event, call the `trackWakeEvent()` method:

```java
LifeCycle lifeCycle = LifeCycle.getInstance(TEALIUM_INSTANCE_ID);

if(lifeCycle != null) {

    // OPTIONAL
    Map&lt;String, String&gt; data = new HashMap&lt;&gt;();
    data.put(&#34;background_time&#34;, &#34;600000ms&#34;);

    lifeCycle.trackWakeEvent(data);
}
```

Tealium and the attached LifeCycle multitons are remote-killable by publish settings in Tealium iQ. Perform Null checks when getting the instances to call their methods.

## Crash Detection

When a `launch` event follows a `wake` event or vice-versa, this indicates a crash has occurred since the app did not successfully `sleep`. If the aforementioned sequence occurs because of a Tealium library shutdown, this is not considered to be a crash event.

When a crash event is detected, the `launch` or `wake` event data has the `lifecycle_diddetectcrash` variable added.

```javascript
{
    &#34;lifecycle_type&#34; : &#34;launch&#34;,
    &#34;lifecycle_diddetectcrash&#34; : &#34;true&#34;,
    //...
}
```

## Data Layer

The Lifecycle Tracking module adds the following additional variables for the listed lifecycle event types (`launch`, `wake`, `sleep`):

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
| `lifecycle_ totalsleepcount` |`Number` | Total number of times your app has gone into the background since app install (only reset if app deleted) |  `400` |  all |
| `lifecycle_ totalwakecount` | `Number` |Total number of launches &#43; wakes since install (only reset if app deleted)  |`563` |  all |
| `lifecycle_type` | `String` | Type of lifecycle call |  [`&#34;initial&#34;`, `&#34;launch&#34;`, `&#34;wake&#34;`, `&#34;sleep&#34;`, `&#34;terminate&#34;`] |  all |
| `lifecycle_ updatelaunchdate` | `String` |GMT timestamp of first wake/launch after a version update has been detected | `&#34;2014-09-08T18:10:01Z&#34;` |  all |
| `lifecycle_ wakecount` | `Number` | Total number of launches &#43; wakes in this version of your app (resets if updated) | ` 29` |  all |


## API Reference

For the complete reference of methods for the Lifecycle Tracking module, see the [`LifeCycle`](https://tealium.github.io/tealium-android/com/tealium/lifecycle/LifeCycle.html) class in the Tealium SDK for Android API.
