---
title: Install
description: Learn to install the Tealium SDK for Android (Java).
url: https://docs.tealium.com/platforms/android-java/install/
---
## Requirements

* [Android Studio](https://developer.android.com/studio)
* Android (KitKat/4.4&#43; / API Level 19&#43;)
* [Tealium iQ Mobile Profile]()
* [Tealium Customer Data Hub account]()

## Sample Apps

To help to familiarize yourself with our library, tracking methods, and best practice implementation, explore the Tealium for Android [sample apps](https://github.com/Tealium/tealium-android/tree/master/Samples).

## Get the Code

Clone the [Tealium Android library](https://github.com/Tealium/tealium-android). Cloning the library, rather than downloading, makes it easier to update to future releases.

See the [Tealium API](https://tealium.github.io/tealium-android/) for a complete listing of Tealium classes and methods for Android.

## Install

Install the Tealium SDK for Android with Maven, or manually.

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
            implementation &#39;com.tealium:library:5.8.0&#39;
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

2. Add `tealium-5.x.x.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.  

3. Add the Tealium library dependency to your `build.gradle` file:      
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-5.6.1&#39;, ext:&#39;aar&#39;)
      }
      ```

## Initialize

To initialize, make the following changes in app&#39;s `onCreate()` method:

1. Create instance of the [`Tealium.Config`](/platforms/android-java/api/tealium-config/#class-tealium-config) object:  
      ```java
      Tealium.Config tealConfig = Tealium.Config.create(
            this,
            &#34;ACCOUNT&#34;,
            &#34;PROFILE&#34;,
            &#34;ENVIRONMENT&#34;);
      ```

2. Call any additional needed methods to set the configuration data such as [`setDatasourceId()`](/platforms/android-java/api/tealium-config/#setdatasourceid):
      ```java
      tealConfig.setDatasourceId(&#34;DATASOURCE_ID&#34;);
      ```

3. Call the [`setupInstance()`](/platforms/android-java/api/life-cycle/#setupinstance) method to setup the app&#39;s lifecycle instance:
      ```java
      LifeCycle.setupInstance(&#34;INSTANCE_NAME&#34;, config, true);
      ```

4. Call the [`createInstance()`](/platforms/android-java/api/tealium/#createinstance) method to create the Tealium instance, passing the configuration instance as a constructor argument:    
      ```java
      tealium = Tealium.createInstance(&#34;INSTANCE_NAME&#34;, tealConfig);
      ```

When Collect is enabled in versions 5.5.1&#43;, data is sent to the profile provided in `Tealium.Config` object. In previous versions, data is sent to the default profile (`&#34;main&#34;`)

## Log Level

The log level is controlled by the remote publish settings and is inferred from the environment set in the initialization.

In versions 5.3.1&#43;, it is possible to override the log level locally with the [`setForceOverrideLogLevel()`](/platforms/android-java/api/tealium-config/#setforceoverrideloglevel) method as shown in the following example:

```java
tealConfig.setForceOverrideLogLevel(&#34;LOG_LEVEL&#34;);
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
            if (Build.VERSION.SDK_INT &gt;= Build.VERSION_CODES.LOLLIPOP) {
                mgr.setAcceptThirdPartyCookies(webView, true);
            }
            if (Build.VERSION.SDK_INT &gt;= Build.VERSION_CODES.HONEYCOMB_MR1) {
                CookieManager.setAcceptFileSchemeCookies(true);
            }
            Log.d(TAG, &#34;WebView &#34; &#43; webView &#43; &#34; created and cookies enabled.&#34;);
        }
    };
}
```

This code allows the tag management `Webview` to [accept](https://developer.android.com/reference/android/webkit/CookieManager.html#acceptCookie()) first-party, third-party, and file scheme cookies.

In versions 5.1.0&#43;, `CookieManager` is **enabled** by default. In versions 5.0.4 and below, `CookieManager` is **disabled** by default.  

## Event Batching

To enable event batching, go to the [Mobile Publish Settings]() and set the batch size to a value greater than 1. Events are dispatched when the number of events in the queue equals the batch size.

The dispatch of events can also be triggered based on the _batch timeout_ setting. This setting ensures that, when the batch size is not reached, the queue is still dispatched after an elapsed period of time.  Set the batch timeout by calling the method [`setSecondsBeforeBatchTimeout()`](/platforms/android-java/api/tealium-config/#setsecondsbeforebatchtimeout).

To override the batch size and batch timeout checks, flush the queue immediately by calling the method [`requestFlush()`](/platforms/android-java/api/tealium/#requestflush).

If the device is offline or has the consent manager enabled, the flush override has no effect.


## Multiprocess Apps

#### Android 9&#43; Multiprocess Applications

Android 9 introduced a behavior change around `WebView` data directories in multiprocess applications. In this change, a `WebView` no longer shares a single data directory across multiple processes. Typically, you&#39;ll want to have all your Activities that use a `WebView` in the same process.  

If you use the Tag Management module and implement additional instances of `WebView`, we recommend calling `WebView.setDataDirectorySuffix()` before creating the Tealium instance to prevent the app from crashing.

If you need to access cookies and web data from the Tag Management module, copy it between processes using the `CookieManager.getCookie()` and `CookieManager.setCookie()` methods.

To learn more, see [Web-based data directories separated by process](https://developer.android.com/about/versions/pie/android-9.0-changes-28#web-data-dirs).
