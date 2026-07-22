---
title: Crash Reporter Module
description: Provides application crash tracking events.
url: https://docs.tealium.com/platforms/android-java/module-list/crash-reporter/
---
## Requirements

* [Tealium for Android](https://docs.tealium.com/platforms/android-java/) (5.0.0+)

## Install

Install the Crash Reporter module with Maven or manually.

### Maven

To install the Crash Reporter module with Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      // Top-level build file where you add configuration options common to all sub-projects/modules.
      allprojects {
            repositories {
              mavenCentral()
              // Tealium Maven repo directive
              maven {
                  url "https://maven.tealiumiq.com/android/releases/"
              }
            }
        }
      ```

2. In your project module's `build.gradle` file, add the following Maven dependency:
      ```groovy
      dependencies {
            // only add if not already present
            implementation 'com.tealium:library:5.8.0'
            // add crash reporter to list of dependencies
            implementation 'com.tealium:crashreporter:1.1.0'
      }
      ```

### Manual

To install the Crash Reporter module manually:

1. Download the Tealium [Crash Reporter](https://github.com/Tealium/tealium-android/tree/master/Modules/CrashReporter) module.  

2. Copy the file `tealium.crashreporter-1.1.0.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation (name:'tealium.crashreporter-1.1.0', ext:'aar')
      }
      ```


## Initialize

Initialize the Crash Reporter module, as shown in the following example::

      ```java
      Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");

      //Enable Crash Reporter
      CrashReporter.initialize(BuildConfig.TEALIUM_MAIN, config, true);

      //Standard Tealium instance
      Tealium.createInstance("INSTANCE_NAME", config);
      ```

## Tracked Events

Once initialized, the Crash Reporter module automatically captures crash data. If a thread abruptly terminates, `.uncaughtExceptionHandler()` is invoked and the crash information is saved to disk. Upon the next launch, the saved crash information will be dispatched along with your other events.

Crash events are tracked as `tealium_event="crash"`.


<blockquote>
Crash Reporter is a singleton instance call. Chaining handlers is not currently supported.
</blockquote>


## Data Layer

The Crash Reporter module sends the following crash attributes in the event:

| Variable | Type | Description | Example |
| --- | --- | --- | --- |
| `crash_cause` | `String` | The exception type | `java.lang.RuntimeException` |
| `crash_count` | `Number` | An incremented counter for each crash since install | `1` |
| `crash_name` | `String` | The exception message |`"Connection refused by server"` |
| `crash_threads` | `[String]` | Array of JSON strings  containing data of the crashed thread, including the thread ID and stack trace| ` ['{ "crashed": "true", "state": "RUNNABLE", "threadNumber": "1", "threadId": "main", "priority": "5", "stack":  [ { "fileName": "MainActivity.java", "className": "com.tealium.libraryproject.MainActivity$1", "methodName": "onClick", "lineNumber": "38" }] }']` |
| `crash_uuid` | `String` | 16-character unique ID for each crash event | `3c91d707-949e-445f-8ad1-4d6e200bfd6f` |

## Integrations

*  [New Relic Mobile Crash Tracking Connector](https://docs.tealium.com/new-relic-mobile-crash-tracking-connector/)

## API Reference

For the complete reference of methods for the Crash Reporter module, see the [`CrashReporter`](https://tealium.github.io/tealium-android/com/tealium/crashreporter/CrashReporter.html) class in the Tealium SDK for Android API.
