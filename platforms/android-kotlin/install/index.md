---
title: Install
description: Learn to install the Tealium SDK for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/install/
---
## Requirements

* [Android Studio](https://developer.android.com/studio)
* Android SDK (Lollipop/5.0&#43; / API Level 21&#43;)
* [Tealium iQ Mobile Profile]()
* [Tealium Customer Data Hub account]()

## Sample Apps

Explore the Android (Kotlin) [sample apps](https://github.com/Tealium/tealium-kotlin/tree/master/mobile) to further your knowledge of the Tealium library, tracking events, and best practice implementations.

Additionally, we recommend abstracting all the Tealium functionality in a central helper class. Explore our [sample helper class](https://github.com/Tealium/tealium-kotlin/blob/master/mobile/src/main/java/com/tealium/mobile/TealiumHelper.kt).

## Get the Code

Clone the [Tealium Android library](https://github.com/Tealium/tealium-kotlin). Cloning the library, rather than downloading, makes it easier to update to future releases.

See the [Tealium API](/platforms/android-kotlin/api/) for a complete listing of Tealium classes and methods for Android.

## Install

The Tealium Kotlin library is divided into modules. To maintain the smallest installation size possible, we recommended that you only install the modules necessary to achieve the functionality you want.

Install the Tealium Kotlin library with Maven or manually.

### Maven

To install Tealium for Android library with Maven (Recommended):

1. Add the Tealium Maven URL to your project&#39;s top-level `build.gradle` file:

      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              maven {
                url &#34;https://maven.tealiumiq.com/android/releases/&#34;
              }
            }
      }
      ```

2. In your project module&#39;s `build.gradle` file, add the following Maven dependency:

      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
      }
      ```

### Manual

To install Tealium for Android library manually:

1. Add `flatDir` to your project root `build.gradle` file:  
      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              flatDir {
                  dirs &#39;libs&#39;
              }
            }
      }
      ```  

2. Add `tealium-kotlin-1.5.x.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.  

3. Add the Tealium library dependency to your `build.gradle` file:      
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kotlin-1.6.0&#39;, ext:&#39;aar&#39;)
      }
      ```

## Initialize

To initialize Tealium, configure a [`TealiumConfig`](/platforms/android-kotlin/api/tealium-config/) instance and pass it into a [`Tealium`](/platforms/android-kotlin/api/tealium/) instance. It&#39;s recommended to initialize the Tealium Kotlin library in the app&#39;s global application class within the `onCreate()` method.

Manage your [`Tealium`](/platforms/android-kotlin/api/tealium/#class-tealium) instance by using a tracking helper class, which provides a single point of entry for the Tealium Kotlin library and simplifies future upgrades. 

```kotlin
object TealiumHelper {

  lateinit var tealium: Tealium

  fun init(application: Application) {
    val tealiumConfig = TealiumConfig(
                      application,
                      &#34;ACCOUNT&#34;,
                      &#34;PROFILE&#34;,
                      Environment.DEV,
                      dataSourceId = &#34;DATASOURCE_ID&#34;,  //optional
                      modules = mutableSetOf(VisitorService),
                      dispatchers = mutableSetOf(Dispatchers.Collect)
                    )
    tealium = Tealium.create(&#34;tealium_instance&#34;, tealiumConfig)
  }
}
```
Replace the following:
* `ACCOUNT`: your Tealium account name you want to use to initialize the library in lowercase.
* `PROFILE`: your Tealium profile name you want to use to initialize the library in lowercase.
* `DATASOURCE_ID`: your Tealium data source ID.


## Dispatcher

To send your data to the Tealium ecosystem, select from the following dispatchers:

* **Tag Management**    
Add the [TagManagement Dispatcher](/platforms/android-kotlin/module-list/tag-management/) to use Tealium iQ Tag Management and make use of its tag management configuration logic.
* **Collect**  
Add the [Collect Dispatcher](/platforms/android-kotlin/module-list/collect/) to use the server-side solutions of the Tealium Customer Data Hub.


## Log Level

Log level is set to the environment from the `TealiumConfig` instance.

To use a different log level, set the [`logLevel`](/platforms/android-kotlin/api/tealium-config/#loglevel) property:

```kotlin
config.logLevel = LogLevel.DEV // or LogLevel.QA, LogLevel.PROD
```

## Cookies

Cookies are enabled by default in the webview.

## Event Batching

Event Batching can be configured locally on the `TealiumConfig` instance, or remotely using the [Mobile Publish Settings](). Setting the batch size to a value greater than 1 will enable it. Events are dispatched when the number of events in the queue equals the batch size.

The following shows the possible options when configuring batching locally:

```kotlin
object TealiumHelper {
      private lateinit var tealium: Tealium

      fun init(app: Application) {
            config.overrideDefaultLibrarySettings = LibrarySettings(
                batching = Batching(
                    batchSize = 10,             // send in batches of 10 (default: 1)
                    maxQueueSize = 1000,        // maximum of 1000 queued events (default: 100)
                    expiration = TimeUnit.DAYS  // queue for a maxumum of 5 days (default: 86400)
                        .toSeconds(5).toInt()     
                )
            )
      }
}
```

## Migrate from Java

When migrating to the Kotlin library from the [Java library](https://github.com/Tealium/tealium-android), saved data is automatically migrated including:

* Consent Preferences
* Lifecycle data
* Persistent data
      * Custom persistent data added through the [Persistent Data](/platforms/android-java/data-management/#persistent-data) API
	    * Tealium persistent data: `app_uuid`, `tealium_visitor_id`

After transfer to the Kotlin library is complete, legacy data from the Java library is deleted. Subsequently switching back to the Java library results in a new `tealium_visitor_id` and `app_uuid` generated, and loss of any custom persistent data.

## Android Wear

For Android Wear apps, use the Collect module for data collection, as the Tag Management module is not supported since Android Wear OS does not provide webview support.

If you are developing an Android Wear app using Tealium for Android, [Google recommends](https://developer.android.com/training/wearables/apps/creating) creating a standalone app.

## Multiprocess Apps

#### Android 9&#43; Multiprocess Applications

Android 9 introduced a behavior change around `WebView` data directories in multiprocess applications. In this change, a `WebView` no longer shares a single data directory across multiple processes. Typically, you&#39;ll want to have all your Activities that use a `WebView` in the same process.  

If you use the Tag Management module and implement additional instances of `WebView`, we recommend calling `WebView.setDataDirectorySuffix()` before creating the Tealium instance to prevent the app from crashing.

If you need to access cookies and web data from the Tag Management module, copy it between processes using the `CookieManager.getCookie()` and `CookieManager.setCookie()` methods.

To learn more, see [Web-based data directories separated by process](https://developer.android.com/about/versions/pie/android-9.0-changes-28#web-data-dirs).
