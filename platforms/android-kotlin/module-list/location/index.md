---
title: Location Manager Module
description: Provides device location data for your events and the ability to add geofences around points of interest.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/location/
---
The Location Manager module enables your Android app to receive location information and the ability to configure and monitor geofences. Learn more about [location tracking and geofencing](/platforms/getting-started-mobile/location/).

## Supported Platforms

The following platforms are supported:

* [Android](/platforms/android-kotlin/)

## Requirements

* Google Play Services [Location](https://developer.android.com/training/location) (11.0.0&#43;)

This module supports Firebase Cloud Messaging.

&lt;!-- ## Sample App

Explore the [Android Location module sample app](https://github.com/Tealium/tealium-android/tree/master/Modules/Location) to familiarize yourself with our library, tracking methods, and best practice implementation. --&gt;

## Install

Install the module with Maven (Recommended) or manually. After you install, add the following import statement:  
```groovy
&lt;!-- import com.tealium.location.TealiumLocation; --&gt;
```

### Maven

To install the module using Maven:

1. In your project&#39;s top-level `build.gradle` file, add the following Maven repository:  
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```
2. In your project module&#39;s `build.gradle` file, add the Maven dependencies for the Tealium library, Location module, and Google Play Services Location API:  
      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-location:1.1.2&#39;
            runtimeOnly &#39;com.google.android.gms:play-services-location:17.0.0&#39;
      }
      ```

### Manual

To install the Location module manually:

1. Download the [Location module](https://github.com/Tealium/tealium-kotlin/tree/master/location).

2. In your top-level `build.gradle` file, verify the following:  
      ```groovy
      allprojects {
            repositories {
            ...
            google()
            flatDir {
                  dirs &#39;libs&#39;
            }
            ...
            }
      }
      ```
3. Copy the file `tealium-kotlin.location-1.1.2.aar` into your project&#39;s `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` directory.

4. Add the Tealium library dependency to your project module’s `build.gradle` file:  
      ```groovy
      dependencies {
            // only required if you do not already have this reference
            implementation(name:&#39;tealium-1.5.3&#39;, ext:&#39;aar&#39;)
            // location module reference
            implementation(name:&#39;tealium-kotlin.location-1.1.2&#39;, ext:&#39;aar&#39;)
            // Google&#39;s Location Services API reference
            runtimeOnly &#39;com.google.android.gms:play-services-location:17.0.0&#39;
      }
      ```

## Initialize

Initialize the Location module, as shown in the following example:

```kotlin
val config = TealiumConfig(application,
              &#34;ACCOUNT&#34;,
              &#34;PROFILE&#34;,
              ENVIRONMENT,
              collectors = mutableSetOf(Collectors.Location) // Location module
)

```

## Location Tracking

The Location module performs continuous location tracking automatically when it is enabled and location permissions are granted. Location updates are based on two settings: accuracy and time interval.

Set accuracy to either high or low. High accuracy corresponds to the Android setting `PRIORITY_HIGH_ACCURACY` and low accuracy corresponds to the Android setting `PRIORITY_BALANCED_POWER_ACCURACY`.

Learn more about [Android location accuracy settings](https://developer.android.com/guide/topics/location/battery#accuracy).

The time interval between location updates is set with a value in milliseconds. Use the highest possible value that is still useful to your app. The interval value is passed to the Android methods `setInterval()` and `setFastestInterval()`.

Learn more about [Android location interval settings](https://developer.android.com/guide/topics/location/battery#frequency).

Start location tracking by calling [`startLocationTracking()`](/platforms/android-kotlin/api/#startlocationtracking). Set the first parameter to `true` for high accuracy and `false` for lower accuracy tracking.

The following example uses high accuracy and a time interval of 60000 milliseconds (60 seconds):  
```kotlin
tealium.location?.startLocationTracking(true, 60000)

```

Disable continuous tracking by calling the method [`stopLocationTracking()`](/platforms/android-kotlin/api/#stoplocationtracking).

### Last Known Location

When continuous tracking is disabled, request the last known location with the method [`lastLocation()`](/platforms/android-kotlin/api/#lastLocation). This method relies on the location client being used by other apps on the device for accuracy. If no other apps are receiving location updates, then the method returns the last known location (or `null` if the location is not available).  
```kotlin
tealium.location?.lastLocation();
```

## Geofencing

To enable geofencing, use one of the following methods to provide your [geofence JSON file](/platforms/getting-started-mobile/location/#json-file):

* **Hosted URL**  
Use your own hosted geofences file provided as a URL to the config option [tealiumConfig.options[GEOFENCE_URL]](/platforms/android-kotlin/api/#overridegeofenceurl).  
This option is recommended if you have overridden the publish settings URL or want to use [Hosted data layer]().  
    ```kotlin
    tealiumConfig.options[GEOFENCE_URL] = &#34;https://example.com/geofences.json&#34;
    ```

* **Local File**  
Use a geofences file stored in the Assets directory of your app with [`tealiumConfig.options[GEOFENCE_FILENAME]`](/platforms/android-kotlin/api/#geofenceFilename).

      ```kotlin
      tealiumConfig.options[GEOFENCE_FILENAME] = &#34;geofences.json&#34;
      ```

## Additional Considerations

**Number of Active Geofences**  
Geofences are added and removed dynamically, using as few resources as possible. There is no limit to the number of geofences defined, but the number of active geofences is limited to 100 per device user across _all_ running applications.

**Initializing Geofences**  
If a user is within a geofence at the time of creation, the `&#34;enter&#34;` transition event does not fire. This is because `&#34;exit&#34;` and `&#34;enter&#34;` transition events are fired when crossing the perimeter and not when materializing inside.

**Battery Optimization Features**  
Android devices that implement battery optimization features may interfere with geofence monitoring, leading to events not firing.

**BroadcastReceiver**  
A `GEOFENCE_EVENT` broadcast is sent when a geofence transition type is triggered. Android only calls the _first_ `BroadcastReceiver` for this particular broadcast, even if multiple are defined. For third party SDKs that handle the `GEOFENCE_EVENT` broadcast, implement a &#34;proxy&#34; `BroadcastReceiver` that calls the `onReceive()` method of each individual receiver for the `GEOFENCE_EVENT` broadcast.

**Latency:**   
When using the geofencing capabilities, take the following into account:  

* The geofence service does not continuously query for location, so latency is expected when receiving alerts. The latency is typically less than 2 minutes, but if background location limits are set or if the device has been stationary for a while, the latency increases.
* The geofence service depends on the network location provider and a data connection. If there is no reliable network connectivity inside the geofence, alerts may not be triggered.
* If Wi-Fi is turned off on the device, your application might never receive geofence alerts depending on several settings including the radius of the geofence, the device model, or the Android version. In Android 4.3&#43; provides the capability of &#34;Wi-Fi scan only mode&#34; which allows users to disable Wi-Fi and still receive a reliable network location. It is recommended to prompt the user to enable this setting.


## Data Layer

The following variables are populated by the Location module as part of the mobile data layer. These variables are included automatically in each tracking call from the library.

| Variable Name | Type | Description | Example             |
|---------------|-----|-------------|----------------------|
| `latitude`     | `String` | The latitude of the user&#39;s most recently recorded location | `32.906119` |
| `longitude`    | `String` |The longitude of the user&#39;s most recently recorded location | `-117.2367` |
| `location_accuracy` | `String` | The accuracy setting for the location module, such as `high` or `low` | `high`|

During geofencing, a tracking call containing location data is sent when the transition state of the user changes. Transition state changes include a user entering, exiting, or dwelling within a geofence for a specified duration of time. You must set the duration of loitering before the dwelling alert is sent using the Android method [setLoiteringDelay()](https://developers.google.com/android/reference/com/google/android/gms/location/Geofence.Builder#setLoiteringDelay(int)).

The following variables are sent to the data layer:

| Variable Name | Type | Description | Example             |
|---------------|-----|-------------|----------------------|
| `tealium_event`            | `String` | The Tealium tracked geofence event | `geofence_entered`, `geofence_exited`, or `geofence_dwell` |
| `geofence_name`            | `String` | The name of the geofence region | `Tealium_San_Diego` |
| `geofence_transition_type` | `String` | The type of geofence transition event | `geofence_entered`, `geofence_exited`, or `geofence_dwell` |

## API Reference

For the reference of methods used by the Lifecycle Tracking module, see the [`LocationManager`](/platforms/android-kotlin/api/location-manager/) class in the Tealium SDK for Android API.
