---
title: Install
description: Learn to install Tealium for React Native.
url: https://docs.tealium.com/platforms/react-native-v1/install/
---
This is the previous version (1.x) of Tealium for React Native.  
For the current version, see [Tealium for React Native 2.x](/platforms/react-native/).

Tealium for React Native lets you use the Tealium native mobile libraries (iOS, Android) in your React Native application.



## How It Works

Tealium mobile libraries are integrated into your React Native application using one of the following two methods:

*   NPM package (Recommended)
*   Manually with [GitHub](https://github.com/Tealium/tealium-react-native)

## Requirements

* Access to your native build environments
* [React Native](https://github.com/Tealium/tealium-react-native) and tools installed
* [Tealium iQ Mobile Profile]()
* [Android Studio](https://developer.android.com/studio/) or [Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](/platforms/android-java/) or [Tealium for iOS](/platforms/ios-swift/)

## Sample App

To help familiarize yourself with our library, the tracking methods, and best practice implementation, it is recommended to download the [React Native sample app](https://github.com/Tealium/tealium-react-native/tree/master/TealiumSampleApp).


## Install (NPM/YARN)

To install the Tealium library for React Native with NPM:

1. Navigate to the root of your React Native project.

2. Download and install the `tealium-react-native` package with the following command:  
      ```bash
      yarn install tealium-react-native
      ```
3. React Native Autolinking is enabled in version 1.0.7 of the NPM package and is no longer needed to run `react-native link` if using version 0.60&#43; of React Native.

### Android

Add a reference to Tealium&#39;s Maven repository in your Android project&#39;s root `build.gradle` file as described in the [Android Maven Install](/platforms/android/install/#maven-install) documentation. The project dependencies are automatically handled by the Autolinking process.

### iOS

The Autolinking feature of React Native 0.60&#43; automatically adds the required CocoaPods dependencies into your iOS application workspace.

To install the pods, run the following commands:

```bash
// From your React Native application folder:
cd ios &amp;&amp; pod install
```

In some cases, it&#39;s necessary to enable the clang parameter to allow non-modular includes in the framework modules. To enable the clang parameter:

1. In Xcode, open the app&#39;s `.xcworkspace` file and selecting your `Pods` from the navigator.

2. Under **Targets** select the **tealium-react-native** target, and click the **Build Settings** tab.

3. Find and update the following setting under **Apple Clang - Language - Modules** &gt; **Allow Non-modular Includes In Framework Modules**:  
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
                  url &#34;http://maven.tealiumiq.com/android/releases/&#34;
              }
            }
      }
      ```

3. Add the Tealium core library dependency to your project module `build.gradle` file. Also, add the Tealium lifecycle dependency (if needed):

      ```groovy
      dependencies {
          compile &#39;com.tealium:library:5.5.2&#39;
              compile &#39;com.tealium:lifecycle:1.1&#39;
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
                new TealiumPackage()    // &lt;--- Add TealiumPackage
            );
      }
      ```

### iOS

Adding Tealium for iOS to a React Native project requires the same steps for a non-React Native application (with the exception of the bridging files), so reference [Adding Tealium to Your iOS App](/platforms/ios/) for complete details.

The Core library is required and optional modules are added as needed. These are available from [our GitHub repository for iOS](https://github.com/Tealium/tealium-ios).

The sample app is for developer experimentation and not meant for publishing on the App Store, so it uses the modules `TealiumIOS.framework` and `TealiumIOSLifecycle.framework` (suitable for a simulator but not for publishing). When working on your own app with intent to publish to the App Store, make sure to use the frameworks in the [devices only folder](https://github.com/Tealium/tealium-ios/tree/master/DevicesOnly).

## Install (CocoaPods)

CocoaPods is another way to perform the Installation. Our pod is named &#34;TealiumIOS&#34;. See the [Tealium for iOS guide](/platforms/ios/) for full details. The command `create-react-native-app` does not create a Podfile so the sample app was built using manual installation. For complex production apps with many dependencies, CocoaPods is the recommended method.

#### Copy Bridging Logic

In the [GitHub repository](https://github.com/Tealium/tealium-react-native/tree/master/ios), there are two files that provide the bridging between the Tealium native iOS SDK and the Javascript in your React Native app: `TealiumModule.m` and `TealiumModule.h`.

Copy these two files into your app&#39;s main project.

## JavaScript

The method for importing the module into your app depends on how you installed.

If you installed with NPM, add the following line to your code:

```javascript
import Tealium from &#39;tealium-react-native&#39;;
```

If you installed manually, then in the  `npm-package` folder of the [GitHub repository](https://github.com/Tealium/tealium-react-native), find the file `index.js`, rename it to `TealiumModule.js` and copy it into your React Native JavaScript Project.

Next, add this line to your code to import the Tealium JavaScript module:

```javascript
import Tealium from &#39;./TealiumModule&#39;;
```

## Initialize

Once your app has been installed, initialize the `Tealium` instance with the [`initialize()`](/platforms/react-native-v1/api/#initialize) method, as shown in the following examples:

```javascript
Tealium.initialize(&#34;ACCOUNT&#34;,
                   &#34;PROFILE&#34;,
                   &#34;ENVIRONMENT&#34;,
                   &#34;IOS_DATA_SOURCE_KEY&#34;,
                   &#34;ANDROID_DATA_SOURCE_KEY&#34;)
```

**Consent Management**  
To use consent management, initialize with the method [`initializeWithConsentManager()`](/platforms/react-native-v1/api/#initializewithconsentmanager) using the same parameters.

Learn more:

* [Consent manager for Android](/platforms/android-java/consent-management/)
* [Consent manager for iOS](/platforms/ios-swift/consent-management/)


**Custom Initialization**  
All initialization options are available with the method [`initializeCustom()`](/platforms/react-native-v1/api/#initializecustom).

```javascript
Tealium.initializeCustom(&#39;ACCOUNT&#39;,
                         &#39;PROFILE&#39;,
                         &#39;ENVIRONMENT&#39;,
                         &#39;IOS_DATA_SOURCE_KEY&#39;,
                         &#39;ANDROID_DATA_SOURCE_KEY&#39;,
                         &#39;INSTANCE&#39;,
                         ENABLE_LIFECYCLE,        // enable lifecycle tracking
                         &#39;PUBLISH_SETTINGS_URL&#39;,  // custom publish settings URL
                         &#39;TAG_MANAGEMENT_URL&#39;,    // custom tag management URL
                         USE_COLLECT_ENDPOINT,    // toggle between data endpoints, true: Tealium Collect, false: Visitor Data
                         ENABLE_CONSENT_MANAGER); // enable consent management
```

See the [API Reference](/platforms/react-native-v1/api/) for more information.
