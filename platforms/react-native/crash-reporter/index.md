---
title: Crash Reporter Module
description: This document explains how to install the Tealium Crash Reporter Module for React Native.
url: https://docs.tealium.com/platforms/react-native/crash-reporter/
---
The Crash Reporter Module provides application crash tracking events.

## How it works

Integrate Tealium mobile libraries into your React Native application using one of the following two methods:

* NPM package (Recommended)
* Manually with [GitHub](https://github.com/Tealium/tealium-react-native)

For more information about the Crash Reporter Module, see [Crash Reporter Module for Android](/platforms/android-kotlin/module-list/crash-reporter/) or [Crash Reporter Module for iOS](/platforms/ios-swift/module-list/crash-reporter/).

## Requirements

* Access to your native build environments
* [Tealium for React Native v2.2.0&#43;](/platforms/react-native/)
* [React Native 0.63&#43;](https://github.com/Tealium/tealium-react-native) and tools installed. 
* [Tealium iQ Mobile Profile]()
* [Android Studio](https://developer.android.com/studio/) or [Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](/platforms/android-kotlin/) or [Tealium for iOS](/platforms/ios-swift/)

## Install (NPM/YARN)

To install the Tealium Crash Reporter module for React Native with NPM:

1. Follow the [installation instructions for the main `tealium-react-native` library installation](/platforms/react-native/install/). Ensure you have installed at least verion 2.2.0 or above.

2. Navigate to the root of your React Native project.

3. Download and install the `tealium-react-native-crash-reporter` package with the following command:  
    ```bash
    yarn install tealium-react-native-crash-reporter
    ```

## JavaScript

To import the relevant classes into your app, do the following:

```javascript
import TealiumCrashReporter from &#39;tealium-react-native-crash-reporter&#39;;
```

## Initialize

Configure the Crash Reporter module prior to initializing the main Tealium React Native integration:

Android:
```javascript
let truncateStack: boolean = true; // Android only. Optional param to specify whether or not to truncate stack trace, default is false

TealiumCrashReporter.initialize(truncateStack);
```

iOS:
```javascript
TealiumCrashReporter.initialize();
```
