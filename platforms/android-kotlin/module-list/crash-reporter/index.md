---
title: Crash Reporter Module
description: Provides application crash tracking events.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/crash-reporter/
---
## Install

Install the Crash Reporter module using Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:  
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```
2. In your project module's `build.gradle` file, add the Maven dependencies for the Tealium library and Crash Reporter:  
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-crash-reporter:1.1.1'
      }
      ```

### Manual

To install the Crash Reporter manually:

1. Download the Tealium [Crash Reporter](https://github.com/Tealium/tealium-kotlin/tree/master/crashreporter) module.

2. Copy the file `tealium-kotlin.crashreporter-1.1.1.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.crashreporter-1.1.1', ext:'aar')
      }
      ```

## Initialize

Initialize the Crash Reporter module, as shown in the following example:

```kotlin
val config = TealiumConfig(application,
              "ACCOUNT",
              "PROFILE",
              ENVIRONMENT,
              modules = mutableSetOf(Modules.CrashReporter), // Crash Reporter module
              dispatchers = mutableSetOf(Dispatchers.Collect,
              Dispatchers.TagManagement,
              Dispatchers.RemoteCommands)
)
```

To truncate the Crash Reporter's stack trace, set the configuration option `truncateCrashReporterStackTraces` to `true` (default: `false`).

```java
config.truncateCrashReporterStackTraces = true
```

## Tracked Events

Once initialized, the Crash Reporter module automatically captures crash data. If a thread abruptly terminates, `.uncaughtExceptionHandler()` is invoked and the crash information is saved to disk. Upon the next launch, the saved crash information will be dispatched along with your other events.

Crash events are tracked as `tealium_event="crash"`.


<blockquote>
Crash Reporter is a singleton instance call. Chaining handlers is not currently supported.
</blockquote>


## Data Layer

The Crash Reporter module sends the following crash attributes in the event:

| Variable        | Type             | Description                                                                                          |
|:----------------|:-----------------|:-----------------------------------------------------------------------------------------------------|
| `crash_cause`   | String           | The exception type                                                                                   |
| `crash_count`   | Number           | An incremented counter for each crash since install                                                  |
| `crash_name`    | String           | The exception message                                                                                |
| `crash_threads` | Array of Strings | Array of JSON strings containing data of the crashed thread, including the thread ID and stack trace |
| `crash_uuid`    | String           | 16-character unique ID for each crash event                                                          |

Example:

```json
{
  "tealium_event" : "crash",
  "crash_cause"   : "java.lang.RuntimeException",
  "crash_count"   : "1",
  "crash_name"    : "Connection refused by server",
  "crash_threads" : [
    "{ \"crashed\": \"true\", \"state\": \"RUNNABLE\", \"threadNumber\": \"1\", \"threadId\": \"main\", \"priority\": \"5\", \"stack\":  [ { \"fileName\": \"MainActivity.java\", \"className\": \"com.tealium.libraryproject.MainActivity$1\", \"methodName\": \"onClick\", \"lineNumber\": \"38\" }] }"
  ],
  "crash_uuid"    : "3c91d707-949e-445f-8ad1-4d6e200bfd6f"
}
```
