---
title: Crash Reporter Module
description: Provides application crash tracking events.
url: https://docs.tealium.com/platforms/android-java/module-list/crash-reporter/
---
## Requirements

* [Tealium for Android](/platforms/android-java/) (5.0.0&#43;)

## Install

Install the Crash Reporter module with Maven or manually.

### Maven

To install the Crash Reporter module with Maven:

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
            // add crash reporter to list of dependencies
            implementation &#39;com.tealium:crashreporter:1.1.0&#39;
      }
      ```

### Manual

To install the Crash Reporter module manually:

1. Download the Tealium [Crash Reporter](https://github.com/Tealium/tealium-android/tree/master/Modules/CrashReporter) module.  

2. Copy the file `tealium.crashreporter-1.1.0.aar` into your project&#39;s `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation (name:&#39;tealium.crashreporter-1.1.0&#39;, ext:&#39;aar&#39;)
      }
      ```


## Initialize

Initialize the Crash Reporter module, as shown in the following example::

      ```java
      Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);

      //Enable Crash Reporter
      CrashReporter.initialize(BuildConfig.TEALIUM_MAIN, config, true);

      //Standard Tealium instance
      Tealium.createInstance(&#34;INSTANCE_NAME&#34;, config);
      ```

## Tracked Events

Once initialized, the Crash Reporter module automatically captures crash data. If a thread abruptly terminates, `.uncaughtExceptionHandler()` is invoked and the crash information is saved to disk. Upon the next launch, the saved crash information will be dispatched along with your other events.

Crash events are tracked as `tealium_event=&#34;crash&#34;`.

Crash Reporter is a singleton instance call. Chaining handlers is not currently supported.

## Data Layer

The Crash Reporter module sends the following crash attributes in the event:

| Variable | Type | Description | Example |
| --- | --- | --- | --- |
| `crash_cause` | `String` | The exception type | `java.lang.RuntimeException` |
| `crash_count` | `Number` | An incremented counter for each crash since install | `1` |
| `crash_name` | `String` | The exception message |`&#34;Connection refused by server&#34;` |
| `crash_threads` | `[String]` | Array of JSON strings  containing data of the crashed thread, including the thread ID and stack trace| ` [&#39;{ &#34;crashed&#34;: &#34;true&#34;, &#34;state&#34;: &#34;RUNNABLE&#34;, &#34;threadNumber&#34;: &#34;1&#34;, &#34;threadId&#34;: &#34;main&#34;, &#34;priority&#34;: &#34;5&#34;, &#34;stack&#34;:  [ { &#34;fileName&#34;: &#34;MainActivity.java&#34;, &#34;className&#34;: &#34;com.tealium.libraryproject.MainActivity$1&#34;, &#34;methodName&#34;: &#34;onClick&#34;, &#34;lineNumber&#34;: &#34;38&#34; }] }&#39;]` |
| `crash_uuid` | `String` | 16-character unique ID for each crash event | `3c91d707-949e-445f-8ad1-4d6e200bfd6f` |

## Integrations

*  [New Relic Mobile Crash Tracking Connector]()

## API Reference

For the complete reference of methods for the Crash Reporter module, see the [`CrashReporter`](https://tealium.github.io/tealium-android/com/tealium/crashreporter/CrashReporter.html) class in the Tealium SDK for Android API.
