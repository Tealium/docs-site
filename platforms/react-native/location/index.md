---
title: Location Module
description: Learn to install Tealium Location Module for React Native.
url: https://docs.tealium.com/platforms/react-native/location/
---
Tealium for React Native lets you use the Tealium native mobile libraries (iOS, Android) in your React Native application.

## How It Works

Tealium mobile libraries are integrated into your React Native application using one of the following two methods:

*   NPM package (Recommended)
*   Manually with [GitHub](https://github.com/Tealium/tealium-react-native)

## Requirements

* Access to your native build environments
* [Tealium for React Native v2.2.0+](https://docs.tealium.com/platforms/react-native/)
* [React Native 0.63+](https://github.com/Tealium/tealium-react-native) and tools installed. 
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/) or [Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/) or [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/)


## Install (NPM/YARN)

To install the Tealium Location module for React Native with NPM:

1. Follow the installation instructions for the main `tealium-react-native` library installation [here](https://docs.tealium.com/platforms/react-native/install/). Ensure you have installed at least verion 2.2.0 or above.

2. Navigate to the root of your React Native project.

3. Download and install the `tealium-react-native-location` package with the following command:  
    ```bash
    yarn install tealium-react-native-location
    ```


## JavaScript

To import the relevant classes into your app, do the following:

```javascript
import TealiumLocation from 'tealium-react-native-location';
import { TealiumLocationConfig, Accuracy, DesiredAccuracy, LocationData } from 'tealium-react-native-location/common';
```

## Initialize

Configure the Location module prior to initializing the main Tealium React Native integration.

You can configure all your required options in one single method, or by calling the helper methods individually:

```javascript
let locationConfig: TealiumLocationConfig = {
    accuracy: Accuracy.high,
    geofenceUrl: "...",
    geofenceFile: "...",
    interval: 6000,                         // android only
    geofenceEnabled: false,                 // iOS only
    desiredAccuracy: DesiredAccuracy.best,  // iOS only
    updateDistance: 150                    // iOS only    
}

TealiumLocation.configure(locationConfig);

// or call them individually:
TealiumLocation.setAccuracy(Accuracy.high);
TealiumLocation.setGeofenceUrl(".../...");
// etc
```

## API Reference

After the Location Module and the main Tealium React Native integration have both been initialized, you can request that location tracking be started or stopped, and request the latest known location point data.

### `startLocationTracking()`

Starts location data tracking - you should ensure that the relevant permissions have been granted prior to starting location tracking.

```javascript
TealiumLocation.startLocationTracking();
```

### `stopLocationTracking()`

Stops location data tracking - only relevant if you are currently tracking location data.

```javascript
TealiumLocation.stopLocationTracking();
```


### `lastLocation(callback)`

Requests the last known location, and returns an object containing the latitude and longitude coordinates as `lat` and `lng` keys - only relevant if you are currently tracking location data.

```javascript
TealiumLocation.lastLocation((loc) => {
    if (loc) {
        Alert.alert(`Lat: ${loc.lat} | Lng: ${loc.lng}`)
    }
})
```