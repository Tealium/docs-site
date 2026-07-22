---
title: Install
description: Learn to install the Tealium SDK for Android (Java).
url: https://docs.tealium.com/platforms/android-java/install/
---
## Requirements

* [Android Studio](https://developer.android.com/studio)
* Android (KitKat/4.4+ / API Level 19+)
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## Sample Apps

To help to familiarize yourself with our library, tracking methods, and best practice implementation, explore the Tealium for Android [sample apps](https://github.com/Tealium/tealium-android/tree/master/Samples).

## Get the Code

Clone the [Tealium Android library](https://github.com/Tealium/tealium-android). Cloning the library, rather than downloading, makes it easier to update to future releases.


<blockquote>
See the [Tealium API](https://tealium.github.io/tealium-android/) for a complete listing of Tealium classes and methods for Android.
</blockquote>


## Install

Install the Tealium SDK for Android with Maven, or manually.

### Maven

To install Tealium for Android library with Maven (Recommended):

1. Add the Tealium Maven URL to your project's top-level `build.gradle` file:

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
            implementation 'com.tealium:library:5.8.0'
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
                  dirs 'libs'
            }
            }
      }
      ```  

2. Add `tealium-5.x.x.aar` to `<PROJECT_ROOT>/<MODULE>/libs`.  

3. Add the Tealium library dependency to your `build.gradle` file:      
      ```groovy
      dependencies {
            implementation(name:'tealium-5.6.1', ext:'aar')
      }
      ```

## Initialize

To initialize, make the following changes in app's `onCreate()` method:

1. Create instance of the [`Tealium.Config`](https://docs.tealium.com/platforms/android-java/api/tealium-config/#class-tealium-config) object:  
      ```java
      Tealium.Config tealConfig = Tealium.Config.create(
            this,
            "ACCOUNT",
            "PROFILE",
            "ENVIRONMENT");
      ```

2. Call any additional needed methods to set the configuration data such as [`setDatasourceId()`](https://docs.tealium.com/platforms/android-java/api/tealium-config/#setdatasourceid):
      ```java
      tealConfig.setDatasourceId("DATASOURCE_ID");
      ```

3. Call the [`setupInstance()`](https://docs.tealium.com/platforms/android-java/api/life-cycle/#setupinstance) method to setup the app's lifecycle instance:
      ```java
      LifeCycle.setupInstance("INSTANCE_NAME", config, true);
      ```

4. Call the [`createInstance()`](https://docs.tealium.com/platforms/android-java/api/tealium/#createinstance) method to create the Tealium instance, passing the configuration instance as a constructor argument:    
      ```java
      tealium = Tealium.createInstance("INSTANCE_NAME", tealConfig);
      ```


<blockquote>
When Collect is enabled in versions 5.5.1+, data is sent to the profile provided in `Tealium.Config` object. In previous versions, data is sent to the default profile (`"main"`)
</blockquote>


## Log Level

The log level is controlled by the remote publish settings and is inferred from the environment set in the initialization.

In versions 5.3.1+, it is possible to override the log level locally with the [`setForceOverrideLogLevel()`](https://docs.tealium.com/platforms/android-java/api/tealium-config/#setforceoverrideloglevel) method as shown in the following example:

```java
tealConfig.setForceOverrideLogLevel("LOG_LEVEL");
```

## Cookies

Enabling cookies is required if you have enabled Tag Management in your mobile profile.

Add the following code, after the initialization statement, to activate cookie management.

```java
config.getEventListeners().add(createCookieEnablerListener());
private static WebViewCreatedListener createCookieEnablerListener() {
    return new WebViewCreatedListener() {
        @Override
        public void onWebViewCreated(WebView webView) {
            final CookieManager mgr = CookieManager.getInstance();
            // Accept all cookies
            mgr.setAcceptCookie(true);
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
                mgr.setAcceptThirdPartyCookies(webView, true);
            }
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB_MR1) {
                CookieManager.setAcceptFileSchemeCookies(true);
            }
            Log.d(TAG, "WebView " + webView + " created and cookies enabled.");
        }
    };
}
```

This code allows the tag management `Webview` to [accept](https://developer.android.com/reference/android/webkit/CookieManager.html#acceptCookie()) first-party, third-party, and file scheme cookies.


<blockquote>
In versions 5.1.0+, `CookieManager` is **enabled** by default. In versions 5.0.4 and below, `CookieManager` is **disabled** by default.
</blockquote>


## Event Batching

To enable event batching, go to the [Mobile Publish Settings](https://docs.tealium.com/creating-a-mobile-profile/) and set the batch size to a value greater than 1. Events are dispatched when the number of events in the queue equals the batch size.

The dispatch of events can also be triggered based on the _batch timeout_ setting. This setting ensures that, when the batch size is not reached, the queue is still dispatched after an elapsed period of time.  Set the batch timeout by calling the method [`setSecondsBeforeBatchTimeout()`](https://docs.tealium.com/platforms/android-java/api/tealium-config/#setsecondsbeforebatchtimeout).

To override the batch size and batch timeout checks, flush the queue immediately by calling the method [`requestFlush()`](https://docs.tealium.com/platforms/android-java/api/tealium/#requestflush).


<blockquote>
If the device is offline or has the consent manager enabled, the flush override has no effect.
</blockquote>



## Multiprocess Apps

#### Android 9+ Multiprocess Applications

Android 9 introduced a behavior change around `WebView` data directories in multiprocess applications. In this change, a `WebView` no longer shares a single data directory across multiple processes. Typically, you'll want to have all your Activities that use a `WebView` in the same process.  

If you use the Tag Management module and implement additional instances of `WebView`, we recommend calling `WebView.setDataDirectorySuffix()` before creating the Tealium instance to prevent the app from crashing.

If you need to access cookies and web data from the Tag Management module, copy it between processes using the `CookieManager.getCookie()` and `CookieManager.setCookie()` methods.

To learn more, see [Web-based data directories separated by process](https://developer.android.com/about/versions/pie/android-9.0-changes-28#web-data-dirs).
