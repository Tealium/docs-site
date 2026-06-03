---
title: Crash Reporter Module
description: Provides application crash tracking events.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/crash-reporter/
---
## Install

Install the Crash Reporter module using Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project&#39;s top-level `build.gradle` file, add the following Maven repository:  
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```
2. In your project module&#39;s `build.gradle` file, add the Maven dependencies for the Tealium library and Crash Reporter:  
      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-crash-reporter:1.1.1&#39;
      }
      ```

### Manual

To install the Crash Reporter manually:

1. Download the Tealium [Crash Reporter](https://github.com/Tealium/tealium-kotlin/tree/master/crashreporter) module.

2. Copy the file `tealium-kotlin.crashreporter-1.1.1.aar` into your project&#39;s `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kotlin.crashreporter-1.1.1&#39;, ext:&#39;aar&#39;)
      }
      ```

## Initialize

Initialize the Crash Reporter module, as shown in the following example:

```kotlin
val config = TealiumConfig(application,
              &#34;ACCOUNT&#34;,
              &#34;PROFILE&#34;,
              ENVIRONMENT,
              modules = mutableSetOf(Modules.CrashReporter), // Crash Reporter module
              dispatchers = mutableSetOf(Dispatchers.Collect,
              Dispatchers.TagManagement,
              Dispatchers.RemoteCommands)
)
```

To truncate the Crash Reporter&#39;s stack trace, set the configuration option `truncateCrashReporterStackTraces` to `true` (default: `false`).

```java
config.truncateCrashReporterStackTraces = true
```

## Tracked Events

Once initialized, the Crash Reporter module automatically captures crash data. If a thread abruptly terminates, `.uncaughtExceptionHandler()` is invoked and the crash information is saved to disk. Upon the next launch, the saved crash information will be dispatched along with your other events.

Crash events are tracked as `tealium_event=&#34;crash&#34;`.

Crash Reporter is a singleton instance call. Chaining handlers is not currently supported.

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
  &#34;tealium_event&#34; : &#34;crash&#34;,
  &#34;crash_cause&#34;   : &#34;java.lang.RuntimeException&#34;,
  &#34;crash_count&#34;   : &#34;1&#34;,
  &#34;crash_name&#34;    : &#34;Connection refused by server&#34;,
  &#34;crash_threads&#34; : [
    &#34;{ \&#34;crashed\&#34;: \&#34;true\&#34;, \&#34;state\&#34;: \&#34;RUNNABLE\&#34;, \&#34;threadNumber\&#34;: \&#34;1\&#34;, \&#34;threadId\&#34;: \&#34;main\&#34;, \&#34;priority\&#34;: \&#34;5\&#34;, \&#34;stack\&#34;:  [ { \&#34;fileName\&#34;: \&#34;MainActivity.java\&#34;, \&#34;className\&#34;: \&#34;com.tealium.libraryproject.MainActivity$1\&#34;, \&#34;methodName\&#34;: \&#34;onClick\&#34;, \&#34;lineNumber\&#34;: \&#34;38\&#34; }] }&#34;
  ],
  &#34;crash_uuid&#34;    : &#34;3c91d707-949e-445f-8ad1-4d6e200bfd6f&#34;
}
```
