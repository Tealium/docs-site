---
title: Attribution Module
description: Learn to install Tealium Attribution Module for React Native.
url: https://docs.tealium.com/platforms/react-native/attribution/
---
Tealium for React Native lets you use the Tealium mobile libraries (iOS, Android) in your React Native application.

## How it works

Tealium mobile libraries are integrated into your React Native application using one of the following two methods:

* NPM package (Recommended)
* Manually with [GitHub](https://github.com/Tealium/tealium-react-native)

## Requirements

* Access to your native build environments
* [Tealium for React Native 2.2.0 or later](https://docs.tealium.com/platforms/react-native/)
* [React Native 0.63 or later](https://github.com/Tealium/tealium-react-native) and tools installed 
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/) or [Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/) or [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/)

## Install (NPM/YARN)

To install the Tealium Attribution module for React Native with NPM:

1. Follow the [installation instructions](https://docs.tealium.com/platforms/react-native/install/) for the main `tealium-react-native` library installation. Ensure that you have installed at least version 2.2.0 or later.
1. Navigate to the root directory of your React Native project.
1. Download and install the `tealium-react-native-attribution` package with the following command:  
    ```bash
    yarn install tealium-react-native-attribution
    ```

## JavaScript

To import the relevant classes into your app, add the following code:

```javascript
import TealiumAttribution from 'tealium-react-native-attribution';
import { TealiumAttributionConfig } from 'tealium-react-native-attribution/common';
```

## Initialize

Configure the `Attribution` module prior to initializing the main Tealium React Native integration. This integration optionally enables Tealium Swift Attribution Module, as well as the Tealium Kotlin Install Referrer and Ad Identifier. Use `TealiumAttributionConfig` parameters to enable settings as needed. 

```javascript
let attributionConfig: TealiumAttributionConfig = {
    androidInstallReferrerEnabled: true,
    androidAdIdentifierEnabled: true,
    iosSearchAdsEnabled: true,
    iosSkAdAttributionEnabled: true,
    iosSkAdConversionKeys: {"event": "conversion_value"}
}

TealiumAttribution.configure(attributionConfig);
```

## API Reference

After the Attribution Module and the main Tealium React Native integration have both been initialized, you can optionally clear ad data.

### `removeAdInfo()`

Clears values and removes ad information from the data layer related to the Tealium Android Ad Identifier module (Android only).

```javascript
TealiumAttribution.removeAdInfo();
```

### `removeAppSetIdInfo()`

Clears values and removes app set Id form the data layer related to the Tealium Android AdIdentifier module (Android only).

```javascript
TealiumAttribution.removeAppSetIdInfo();
```
