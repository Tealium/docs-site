---
title: Install
description: Learn to install Tealium for React Native.
url: https://docs.tealium.com/platforms/react-native-v1/install/
---

<blockquote>
This is the previous version (1.x) of Tealium for React Native.  
For the current version, see [Tealium for React Native 2.x](https://docs.tealium.com/platforms/react-native/).
</blockquote>


Tealium for React Native lets you use the Tealium native mobile libraries (iOS, Android) in your React Native application.



## How It Works

Tealium mobile libraries are integrated into your React Native application using one of the following two methods:

*   NPM package (Recommended)
*   Manually with [GitHub](https://github.com/Tealium/tealium-react-native)

## Requirements

* Access to your native build environments
* [React Native](https://github.com/Tealium/tealium-react-native) and tools installed
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/) or [Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/platforms/android-java/) or [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/)

## Sample App

To help familiarize yourself with our library, the tracking methods, and best practice implementation, it is recommended to download the [React Native sample app](https://github.com/Tealium/tealium-react-native/tree/master/TealiumSampleApp).


## Install (NPM/YARN)

To install the Tealium library for React Native with NPM:

1. Navigate to the root of your React Native project.

2. Download and install the `tealium-react-native` package with the following command:  
      ```bash
      yarn install tealium-react-native
      ```
3. React Native Autolinking is enabled in version 1.0.7 of the NPM package and is no longer needed to run `react-native link` if using version 0.60+ of React Native.

### Android

Add a reference to Tealium's Maven repository in your Android project's root `build.gradle` file as described in the [Android Maven Install](https://docs.tealium.com/platforms/android/install/#maven-install) documentation. The project dependencies are automatically handled by the Autolinking process.

### iOS

The Autolinking feature of React Native 0.60+ automatically adds the required CocoaPods dependencies into your iOS application workspace.

To install the pods, run the following commands:

```bash
// From your React Native application folder:
cd ios && pod install
```

In some cases, it's necessary to enable the clang parameter to allow non-modular includes in the framework modules. To enable the clang parameter:

1. In Xcode, open the app's `.xcworkspace` file and selecting your `Pods` from the navigator.

2. Under **Targets** select the **tealium-react-native** target, and click the **Build Settings** tab.

3. Find and update the following setting under **Apple Clang - Language - Modules** > **Allow Non-modular Includes In Framework Modules**:  
      ```groovy
      CLANG_ALLOW_NON_MODULAR_INCLUDES_IN_FRAMEWORK_MODULES = YES;
      ```



## Install (Manual)

### Android

For Android apps, follow these manual installation steps:

1. To integrate Tealium into your Android application, add this to your Tealium Maven repository:

2. In your project root `build.gradle`, add the Tealium Maven URL:
      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              maven {
                  url "http://maven.tealiumiq.com/android/releases/"
              }
            }
      }
      ```

3. Add the Tealium core library dependency to your project module `build.gradle` file. Also, add the Tealium lifecycle dependency (if needed):

      ```groovy
      dependencies {
          compile 'com.tealium:library:5.5.2'
              compile 'com.tealium:lifecycle:1.1'
      }
      ```

To copy Bridging logic:

1. From the Android folder, add `TealiumModule.java` and `TealiumPackage.java` into your project files.

2. Include `TealiumPackage` into the `getPackages()` method of your `MainApplication.java` file.
      ```java
      @Override
      protected List getPackages() {
            return Arrays.asList(
                new MainReactPackage(),
                new TealiumPackage()    // <--- Add TealiumPackage
            );
      }
      ```

### iOS

Adding Tealium for iOS to a React Native project requires the same steps for a non-React Native application (with the exception of the bridging files), so reference [Adding Tealium to Your iOS App](https://docs.tealium.com/platforms/ios/) for complete details.

The Core library is required and optional modules are added as needed. These are available from [our GitHub repository for iOS](https://github.com/Tealium/tealium-ios).

The sample app is for developer experimentation and not meant for publishing on the App Store, so it uses the modules `TealiumIOS.framework` and `TealiumIOSLifecycle.framework` (suitable for a simulator but not for publishing). When working on your own app with intent to publish to the App Store, make sure to use the frameworks in the [devices only folder](https://github.com/Tealium/tealium-ios/tree/master/DevicesOnly).

## Install (CocoaPods)

CocoaPods is another way to perform the Installation. Our pod is named "TealiumIOS". See the [Tealium for iOS guide](https://docs.tealium.com/platforms/ios/) for full details. The command `create-react-native-app` does not create a Podfile so the sample app was built using manual installation. For complex production apps with many dependencies, CocoaPods is the recommended method.

#### Copy Bridging Logic

In the [GitHub repository](https://github.com/Tealium/tealium-react-native/tree/master/ios), there are two files that provide the bridging between the Tealium native iOS SDK and the Javascript in your React Native app: `TealiumModule.m` and `TealiumModule.h`.

Copy these two files into your app's main project.

## JavaScript

The method for importing the module into your app depends on how you installed.

If you installed with NPM, add the following line to your code:

```javascript
import Tealium from 'tealium-react-native';
```

If you installed manually, then in the  `npm-package` folder of the [GitHub repository](https://github.com/Tealium/tealium-react-native), find the file `index.js`, rename it to `TealiumModule.js` and copy it into your React Native JavaScript Project.

Next, add this line to your code to import the Tealium JavaScript module:

```javascript
import Tealium from './TealiumModule';
```

## Initialize

Once your app has been installed, initialize the `Tealium` instance with the [`initialize()`](https://docs.tealium.com/platforms/react-native-v1/api/#initialize) method, as shown in the following examples:

```javascript
Tealium.initialize("ACCOUNT",
                   "PROFILE",
                   "ENVIRONMENT",
                   "IOS_DATA_SOURCE_KEY",
                   "ANDROID_DATA_SOURCE_KEY")
```

**Consent Management**  
To use consent management, initialize with the method [`initializeWithConsentManager()`](https://docs.tealium.com/platforms/react-native-v1/api/#initializewithconsentmanager) using the same parameters.

Learn more:

* [Consent manager for Android](https://docs.tealium.com/platforms/android-java/consent-management/)
* [Consent manager for iOS](https://docs.tealium.com/platforms/ios-swift/consent-management/)


**Custom Initialization**  
All initialization options are available with the method [`initializeCustom()`](https://docs.tealium.com/platforms/react-native-v1/api/#initializecustom).

```javascript
Tealium.initializeCustom('ACCOUNT',
                         'PROFILE',
                         'ENVIRONMENT',
                         'IOS_DATA_SOURCE_KEY',
                         'ANDROID_DATA_SOURCE_KEY',
                         'INSTANCE',
                         ENABLE_LIFECYCLE,        // enable lifecycle tracking
                         'PUBLISH_SETTINGS_URL',  // custom publish settings URL
                         'TAG_MANAGEMENT_URL',    // custom tag management URL
                         USE_COLLECT_ENDPOINT,    // toggle between data endpoints, true: Tealium Collect, false: Visitor Data
                         ENABLE_CONSENT_MANAGER); // enable consent management
```

See the [API Reference](https://docs.tealium.com/platforms/react-native-v1/api/) for more information.
