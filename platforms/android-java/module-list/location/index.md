---
title: Location Module
description: Provides device location data for your events and the ability to add geofences around points of interest.
url: https://docs.tealium.com/platforms/android-java/module-list/location/
---
The Location module enables your Android app to receive location information and the ability to configure and monitor geofences. Learn more about [location tracking and geofencing](https://docs.tealium.com/platforms/getting-started-mobile/location/).

## Supported Platforms

The following platforms are supported:

* [Android](https://docs.tealium.com/platforms/android-java/)
* [Android TV](https://docs.tealium.com/platforms/android-java/tv/)
* [Android Wear](https://docs.tealium.com/platforms/android-java/wear/)

## Requirements

* [Tealium for Android](https://docs.tealium.com/platforms/android-java/) (5.6.0+)
* Google Play Services [Location](https://developer.android.com/training/location) (11.0.0+)

This module supports Firebase Cloud Messaging.

## Sample App

Explore the [Android Location module sample app](https://github.com/Tealium/tealium-android/tree/master/Modules/Location) to familiarize yourself with our library, tracking methods, and best practice implementation.

## Install

Install the module with Maven (Recommended) or manually. After you install, add the following import statement:  
```groovy
import com.tealium.location.TealiumLocation;
```

### Maven

To install the module using Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:  
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```
2. In your project module's `build.gradle` file, add the Maven dependencies for the Tealium library, Location module, and Google Play Services Location API:  
      ```groovy
      dependencies {
            implementation 'com.tealium:library:5.8.0'
            implementation 'com.tealium:location:1.0.0'
            runtimeOnly 'com.google.android.gms:play-services-location:17.0.0'
      }
      ```

### Manual

To install the Location module manually:

1. Download the [Location module](https://github.com/Tealium/tealium-android/tree/master/Modules/Location)


2. In your top-level `build.gradle` file, verify the following:  
      ```groovy
      allprojects {
            repositories {
            ...
            google()
            flatDir {
                  dirs 'libs'
            }
            ...
            }
      }
      ```
3. Copy the file `tealium.location-1.0.0.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

4. Add the Tealium library dependency to your project module’s `build.gradle` file:  
      ```groovy
      dependencies {
            // only required if you do not already have this reference
            implementation(name:'tealium-5.6.0', ext:'aar')
            // location module reference
            implementation(name:'tealium.location-1.0.0', ext:'aar')
            // Google's Location Services API reference
            runtimeOnly 'com.google.android.gms:play-services-location:17.0.0'
      }
      ```

## Initialize

Initialize the Location module by passing a Tealium instance name to [`TealiumLocation.setupInstance()`](https://docs.tealium.com/platforms/android-java/api/tealium-location/#setupinstance).

```java
Set<String> tealiumInstances = new HashSet<>();
tealiumInstances.add(TealiumHelper.TEALIUM_MAIN);

mInstance = TealiumLocation.setupInstance(this, tealiumInstances);
```

## Location Tracking

The Location module performs continuous location tracking automatically when it is enabled and [location permissions](#location-permissions) are granted. Location updates are based on two settings: accuracy and time interval.

Accuracy may be set to high or low. High accuracy corresponds to the Android setting `PRIORITY_HIGH_ACCURACY` and low accuracy corresponds to the Android setting `PRIORITY_BALANCED_POWER_ACCURACY`.

Learn more about [Android location accuracy settings](https://developer.android.com/guide/topics/location/battery#accuracy).

The time interval between location updates is set with a value in milliseconds. Use the highest possible value that is still useful to your app. The interval value is passed to the Android methods `setInterval()` and `setFastestInterval()`.

Learn more about [Android location interval settings](https://developer.android.com/guide/topics/location/battery#frequency).

Start location tracking by calling [`TealiumLocation.startLocationUpdates()`](https://docs.tealium.com/platforms/android-java/api/tealium-location/#startlocationupdates). Set the first parameter to `true` for high accuracy and `false` for lower accuracy tracking.

The following example uses high accuracy and a time interval of 60000 milliseconds (60 seconds):  
```java
TealiumLocation.getInstance().startLocationUpdates(true, 60000);

```

Disable continuous tracking by calling the methods `TealiumLocation.destroyInstance()` or [`TealiumLocation.stopLocationUpdates()`](https://docs.tealium.com/platforms/android-java/api/tealium-location/#stoplocationupdates).

### Location Permissions

To grant location permissions in your app:

1. Set the constant variable for the location request code:   
      ```java
      public static final int LOCATION_REQUEST_CODE = 101;
      ```

2. Add the following method in your app's `MainActivity` class:  
      ```java
      public void requestLocationPermission() {
            if (ContextCompat.checkSelfPermission(getApplicationContext(),
            Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
                  ActivityCompat.requestPermissions(this,
                  new String[]{
                        Manifest.permission.ACCESS_FINE_LOCATION,
                        Manifest.permission.ACCESS_COARSE_LOCATION
                  }, LOCATION_REQUEST_CODE);
            }
      }
      ```

3. Call the `requestLocationPermission()` method within the `onCreate()` method of the `MainActivity` class:  
      ```java
      if ((ContextCompat.checkSelfPermission(getApplicationContext(),
            Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
            && ContextCompat.checkSelfPermission(getApplicationContext(),
            Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            requestLocationPermission();
      }
      ```

4. Optionally, to verify that location permissions are granted, override the `onRequestPermissionsResult`() method:  
      ```java
      @Override
      public void onRequestPermissionsResult(int requestCode,
            String[] permissions,
            int[] grantResults) {
            String message;
            if (requestCode == LOCATION_REQUEST_CODE) {
                  // If request is cancelled, the result arrays are empty.
                  if ((grantResults.length > 0) && (grantResults[0]
                  == PackageManager.PERMISSION_GRANTED)) {
                  message = "Location Permission Granted";
                  } else {
                  message = "Location Permission Not Granted";
                  }
            } else {
                  message = "Location Permission Not Granted";
            }
            showToast(message);
      }

      private void showToast(String message) {
            Toast.makeText(getApplicationContext(),
            message,
            Toast.LENGTH_LONG).show();
      }
      ```

### Last Known Location

When continuous tracking is disabled, request the last known location with the method [`TealiumLocation.requestDeviceLastLocation()`](https://docs.tealium.com/platforms/android-java/api/tealium-location/#requestdevicelastlocation). This method relies on the location client being used by other apps on the device for accuracy. If no other apps are receiving location updates, then the method returns the last known location (or `null` if the location is not available).  
```java
TealiumLocation.getInstance().requestDeviceLastLocation();
```

## Geofencing

To initialize with geofencing enabled, use one of the following methods to provide your [geofence JSON file](https://docs.tealium.com/platforms/getting-started-mobile/location/#json-file) to the setup method:

* **Hosted URL**  
Use your own hosted geofences file provided as a URL to the method [`TealiumLocation.setupInstanceWithUrl()`](https://docs.tealium.com/platforms/android-java/api/tealium-location/#setupinstancewithurl).  
This option is recommended if you have overridden the publish settings URL or want to use [Hosted Data Layer](https://docs.tealium.com/use-case-supplementing-product-data/).  
```java
TealiumLocation.setupInstanceWithUrl(this, tealiumInstances, "https://example.com/geofences.json");
```
* **Local File**  
Use a geofences file stored in the Assets directory of your app with [`TealiumLocation.setupInstanceWithFile()`](https://docs.tealium.com/platforms/android-java/api/tealium-location/#setupinstancewithfile).  
```java
TealiumLocation.setupInstanceWithFile(this, tealiumInstances, "geofences.json");
```

## Additional Considerations

**Battery Optimization Features**  
Android devices that implement battery optimization features may interfere with geofence monitoring, leading to events not firing.

**BroadcastReceiver**  
A `GEOFENCE_EVENT` broadcast is sent when a geofence transition type is triggered. Android only calls the _first_ `BroadcastReceiver` for this particular broadcast, even if multiple are defined. For third party SDKs that handle the `GEOFENCE_EVENT` broadcast, implement a "proxy" `BroadcastReceiver` that calls the `onReceive()` method of each individual receiver for the `GEOFENCE_EVENT` broadcast.

**Initializing Geofences**  
If a user is within a geofence at the time of creation, the `"enter"` transition event does not fire. This is because `"exit"` and `"enter"` transition events are fired when crossing the perimeter and not when materializing inside.

**Latency:**   
When using the geofencing capabilities, take the following into account:  

* The geofence service does not continuously query for location, so latency is expected when receiving alerts. The latency is typically less than 2 minutes, but if background location limits are set or if the device has been stationary for a while, the latency increases.
* The geofence service depends on the network location provider and a data connection. If there is no reliable network connectivity inside the geofence, alerts may not be triggered.
* If Wi-Fi is turned off on the device, your application might never receive geofence alerts depending on several settings including the radius of the geofence, the device model, or the Android version. In Android 4.3+ provides the capability of "Wi-Fi scan only mode" which allows users to disable Wi-Fi and still receive a reliable network location. It is recommended to prompt the user to enable this setting.

**Number of Active Geofences**  
Geofences are added and removed dynamically, using as few resources as possible. There is no limit to the number of geofences defined, but the number of active geofences is limited to 100 per device user across _all_ running applications.

## Data Layer

The following variables are populated by the Location module as part of the mobile data layer. These variables are included automatically in each tracking call from the library.

| Variable Name       | Type     | Description                                                               | Example       |
|:--------------------|:---------|:--------------------------------------------------------------------------|:--------------|
| `latitude`          | `String` | The latitude of the user's most recently recorded location                | `"32.906119"` |
| `longitude`         | `String` | The longitude of the user's most recently recorded location               | `"-117.2367"` |
| `location_accuracy` | `String` | The accuracy setting for the location module, such as `"high"` or `"low"` | `"high"`      |

During geofencing, a tracking call containing location data is sent when the transition state of the user changes. Transition state changes include a user entering, exiting, or dwelling within a geofence for a specified duration of time. You must set the duration of loitering before the dwelling alert is sent using the Android method [setLoiteringDelay()](https://developers.google.com/android/reference/com/google/android/gms/location/Geofence.Builder#setLoiteringDelay(int)).

The following variables are sent to the data layer:

| Variable Name              | Type     | Description                           | Example                                                          |
|:---------------------------|:---------|:--------------------------------------|:-----------------------------------------------------------------|
| `tealium_event`            | `String` | The Tealium tracked geofence event    | `"geofence_entered"`, `"geofence_exited"`, or `"geofence_dwell"` |
| `geofence_name`            | `String` | The name of the geofence region       | `"Tealium_San_Diego"`                                            |
| `geofence_transition_type` | `String` | The type of geofence transition event | `"geofence_entered"`, `"geofence_exited"`, or `"geofence_dwell"` |

## API Reference

For the reference of methods used in the Location module, see the [`TealiumLocation`](https://docs.tealium.com/platforms/android-java/api/tealium-location/#class-tealiumlocation) class in the Tealium SDK for Android API.
