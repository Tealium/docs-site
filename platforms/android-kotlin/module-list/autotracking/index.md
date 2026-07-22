---
title: AutoTracking Module
description: Track screen views automatically.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/autotracking/
---
The AutoTracking module adds automatic tracking of common events to your app, without writing additional code in your app.

## How It Works

Add automatic tracking to your app by including the AutoTracking module in your build and initialization. The module has several options to control which screens are tracked and how they are named.

The Autotracking module has two modes of tracking:

* **Full Tracking**  
Tracks all screen views automatically, with the option to omit screens or override the screen names.
* **Partial Tracking**  
Tracks only the activities that are annotated, with the option to override the screen names.

### Annotations

Use the following annotations to adjust the behavior of the module:

* **Override event name**  
Use this annotation to override the default screen name.

      ```kotlin
      @Autotracked(name = "MyCustomName")
      private class AnnotatedActivityWithOverride : Activity()
      ```
* **Include in tracking**  
In partial tracking mode, use this annotation to track specific activities.

      ```kotlin
      @Autotracked()
      private class AnnotatedActivity : Activity()
      ```
* **Omit from tracking**  
In full tracking mode, use this annotation to omit activities from being tracked automatically.

      ```kotlin
      @Autotracked(track = false)
      private class AnnotatedActivityWithoutTracking : Activity()
      ```

### Full Tracking

The full tracking mode uses `Application.ActivityLifecycleCallbacks` to determine when a new activity comes into focus and then triggers a `TealiumView` event. In the event, `tealium_event` is set to the class name, but with "Activity" trimmed from the name.

Use annotations to override the screen name or to prevent activities from being tracked.

Learn more from [Android Developers: The Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle).

### Partial Tracking

The partial tracking mode relies on Annotations to determine which activities to track. Use annotations to specify which activities to track or to override the screen name.

### Block List

The block list is a JSON file that contains a single array of strings. The strings represent activities to omit from automatic tracking. If a string in the block list appears anywhere in the activity name, it will not be tracked. The string comparisons are case-insensitive.

For example, if you don't want to track activities that contain the strings "Settings" or "Profile", then the block list could contain:

```json
[
  "settings", "profile"
]
```

The block list file can be stored locally in the `assets` directory of your app or hosted remotely as a URL.

Use the one of the following `TealiumConfig` properties to use a block list:

* [`autoTrackingBlocklistFilename`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#autotrackingblocklistfilename)
* [`autoTrackingBlocklistUrl`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#autotrackingblocklisturl)

## Install

Install the module with Maven (Recommended) or manually.

### Maven

To install the AutoTracking Tracking module using Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      allprojects {
          repositories {
            mavenCentral()
            maven {
                url "https://maven.tealiumiq.com/android/releases/"
            }
          }
      }
      ```

2. In your project module's `build.gradle` file, add the following Maven dependency:
      ```groovy
      dependencies {
          implementation 'com.tealium:kotlin-core:1.6.0'
          implementation 'com.tealium:kotlin-autotracking:1.0.1'
      }
      ```

### Manual

To install the AutoTracking module manually, following these steps:

1. Download the Tealium [AutoTracking Module](https://github.com/Tealium/tealium-kotlin/tree/master/autotracking/) module.

2. Copy the file `tealium-kotlin.autotracking-1.0.1.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.autotracking-1.0.1', ext:'aar')
      }
      ```

## Initialize

To initialize the AutoTracking module, add it to the list of modules in `TealiumConfig` and set the tracking mode.

Example of initializing the AutoTracking module:

```kotlin
val config = TealiumConfig(application,
              "ACCOUNT",
              "PROFILE",
              ENVIRONMENT,
              modules = mutableSetOf(Modules.AutoTracking)
              ).apply {
                autoTrackingMode = AutoTrackingMode.ANNOTATED
              }
```

See [`TealiumConfig.autoTrackingMode`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/#autotrackingmode) for more options.

## Data Layer

The following variables are included with each tracking call that is triggered by this module:

| Variable Name | Type     | Description                                            | Example |
|:--------------|:---------|:-------------------------------------------------------|:--------|
| `autotracked` | `String` | Set for all events tracked by the Autotracking module. | `true`  |

### Custom Data

By default, the automatically tracked events do not include any context variables. To add context data to an event from the AutoTracking module, use the global delegate set in the `TealiumConfig` to return a map of the custom data object for each tracked activity. This executes for every event tracked by the module.

To set the delegate:

```kotlin
config.autoTrackingCollectorDelegate = object: ActivityDataCollector {
    override fun onCollectActivityData(activityName: String): Map<String, Any>? {
        when (activityName) {
            "some_activity" -> return mapOf("some_key" to "some_value")
            else -> return null
        }
    }
}
```

Alternatively, to add context data to a specific activity, make your `Activity` implement the same `ActivityDataCollector` interface.

```kotlin
class ActivityWithDataCollector : Activity(), ActivityDataCollector {
    override fun onCollectActivityData(activityName: String): Map<String, Any>? {
        return mapOf("some_key" to "some_value")
    }
}
```

Both delegates are executed for each tracked activity, so add common data at the global level, and add specific data using the `onCollectActivityData` method.

## API Reference

* [`TealiumConfig`](https://docs.tealium.com/platforms/android-kotlin/api/tealium-config/)
