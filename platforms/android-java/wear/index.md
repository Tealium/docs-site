---
title: Android Wear
description: Learn to install the Tealium SDK for Android Wear.
url: https://docs.tealium.com/platforms/android-java/wear/
---
## Requirements

* AndroidWear app with [Tealium for Android](https://docs.tealium.com/platforms/android-java/)
* Android (KitKat/4.4+ / API Level 20+ for Android Wear)
* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)


## API Reference

For the complete reference of classes and methods for Android Wear, see the [`com.tealium.wear`](http://tealium.github.io/tealium-android/com/tealium/wear/package-frame.html) package in the Tealium SDK for Android API.


## Sample App

To help familiarize yourself with the Tealium library, tracking methods, and best practice implementation, it is recommended to download the Tealium for AndroidWear [sample app](https://github.com/Tealium/tealium-android/tree/master/Modules/AndroidWear/WearSample).

To abstract the Tealium implementation from the rest of your app, we recommend the use of the [sample helper class](https://github.com/Tealium/tealium-android/blob/master/Samples/BlankApp%2BTealium/app/src/main/java/com/tealium/blankapp/helper/TealiumHelper.java). This gives you a single entry point from which to initialize and make tracking calls. It also lets you update the code in your helper file and not in every single Java file.

## Install

Install the Tealium library for your Android Wear app:

1. Download and install [Tealium for Android Wear](https://github.com/Tealium/tealium-android/tree/master/Modules/AndroidWear).

2. Add `tealium.mobile-5.x.x.aar` to your application's dependencies.

      
<blockquote>
For non-wearable Android applications, no additional code is necessary.
</blockquote>


3. Create a subclass of the `Application` class, and add the `TealiumWear`'s initialization code in the app's `onCreate()` method, as shown in the following example:

      ```java
      public class WearApp extends Application {

            // Instance name from main app
            public static final String TEALIUM_MAIN = "INSTANCE_NAME";

            @Override
            public void onCreate() {
              super.onCreate();
              TealiumWear.createInstance(TEALIUM_MAIN,
                  TealiumWear.Config.create(this)
                  .setLogLevel(Log.VERBOSE));
            }
      //...
      }
      ```

4. The value of `TEALIUM_MAIN` must match the instance name used in the initialization of the main application, as shown in the following example:

      ```java  
      // Main application initialization
      Tealium.createInstance("INSTANCE_NAME", config);

      // WearApp initialization
      public static final String TEALIUM_MAIN = "INSTANCE_NAME";
      ```

## Tracking

### Track Views

Tracking on the wearable is similar to the handheld side. The only difference is in how to pass custom data to the tracking calls. The wearable side uses a [`DataMap`](https://developers.google.com/android/reference/com/google/android/gms/wearable/DataMap) object, rather than a `Map`:

The [`trackView()`](https://docs.tealium.com/platforms/android-java/api/tealium/#trackview) method tracks screen views, as shown in the following example:

```java
final DataMap data = new DataMap();
// ...
TealiumWear.getInstance(WearApp.TEALIUM_MAIN)
    .trackView("SCREEN_NAME", data);
```


### Track Events

The [`trackEvent()`](https://docs.tealium.com/platforms/android-java/api/tealium/#trackevent) method tracks non-view events, as shown in the following example:

```java
final DataMap data = new DataMap();
// ...
TealiumWear.getInstance(WearApp.TEALIUM_MAIN)
    .trackEvent("EVENT_NAME", data);
```
