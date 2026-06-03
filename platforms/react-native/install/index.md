---
title: Install
description: Learn to install Tealium for React Native.
url: https://docs.tealium.com/platforms/react-native/install/
---
Tealium for React Native lets you use the Tealium native mobile libraries (iOS, Android) in your React Native application.

This is the current version (2.x) of Tealium for React Native.  
For the previous version, see [Tealium for React Native 1.x](/platforms/react-native-v1/).

## How It Works

Tealium mobile libraries are integrated into your React Native application using one of the following two methods:

*   NPM package (Recommended)
*   Manually with [GitHub](https://github.com/Tealium/tealium-react-native)

## Requirements

* Access to your native build environments
* [React Native 0.63&#43;](https://github.com/Tealium/tealium-react-native) and tools installed. 
* [Tealium iQ Mobile Profile]()
* [Android Studio](https://developer.android.com/studio/) or [Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](/platforms/android-kotlin/) or [Tealium for iOS](/platforms/ios-swift/)

## Sample App

To help familiarize yourself with our library, the tracking methods, and best practice implementation, we recommend that you download the [React Native sample app](https://github.com/Tealium/tealium-react-native/tree/master/example).


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

From version 2.2.0 to version 2.5.1, add the following reference to your Podfile: `pod &#34;tealium-react-native-swift&#34;, :path =&gt; &#39;../node_modules/tealium-react-native/tealium-react-native-swift.podspec&#39;`.
In version 2.6.0 and later, this extra dependency is not required anymore and must be removed.

In some cases, it&#39;s necessary to enable the `clang` parameter to allow non-modular includes in the framework modules. To enable the clang parameter:

1. In Xcode, open the app&#39;s `.xcworkspace` file and select your `Pods` from the navigator.

2. Under **Targets** select the **tealium-react-native** target, and click the **Build Settings** tab.

3. Find and update the following setting under **Apple Clang - Language - Modules** &gt; **Allow Non-modular Includes In Framework Modules**:  
      ```groovy
      CLANG_ALLOW_NON_MODULAR_INCLUDES_IN_FRAMEWORK_MODULES = YES;
      ```

#### Bridging Header

The `TealiumReactNative` module uses the [`Tealium iOS (Swift)`](/platforms/ios-swift) library. To expose the Objective-C files from React Native to Swift, use Xcode to create a bridging header file to your iOS project.

1. In Xcode, select **File &gt; New &gt; File...** from the menu.
2. Select **Swift File** as the template and click **Next**.
3. In the **Group** drop-down, select the top-level folder of your app (not the project).
4. When the prompt &#34;Would you like to configure an Objective-D bridging header?&#34; appears, select **Create Bridging Header** to generate the bridging header file.

The bridging header filename is in the format: `YourProject-Bridging-Header.h`. Do not rename the file, as Xcode configures the project with the generated filename.

You are only prompted once per project for adding a bridging header.

## JavaScript

The method for importing the module into your app depends on how you installed.

If you installed with NPM, add the following line to your code:

```javascript
import Tealium from &#39;tealium-react-native&#39;;
```

If you installed manually, then in the  `npm-package` folder of the [GitHub repository](https://github.com/Tealium/tealium-react-native), find the file `index.js`, rename it to `TealiumModule.js` and copy it into your React Native JavaScript Project.

After installation, import the Tealium module into your app&#39;s JavaScript code as follows:

```javascript
import Tealium from &#39;tealium-react-native&#39;;
import { TealiumConfig, TealiumView, TealiumEvent, ConsentCategories, Dispatchers, Collectors, ConsentPolicy, Expiry, ConsentExpiry, TimeUnit, ConsentStatus, TealiumEnvironment } from &#39;tealium-react-native/common&#39;;
```

## Initialize

Once your app has been installed, initialize the `Tealium` instance with the [`initialize()`](/platforms/react-native/api/#initialize) method, as shown in the following example:

```javascript
let config: TealiumConfig = {
      // Replace &#39;ACCOUNT&#39; with your Tealium account name
      account: &#39;ACCOUNT&#39;,
      // Replace &#39;PROFILE&#39; with your Tealium profile name
      profile: &#39;PROFILE&#39;,
      environment: TealiumEnvironment.dev,
      dispatchers: [Dispatchers.Collect, Dispatchers.RemoteCommands, Dispatchers.TagManagement],
      collectors: [Collectors.AppData, Collectors.DeviceData, Collectors.Lifecycle, Collectors.Connectivity],
      consentPolicy: ConsentPolicy.gdpr,
      visitorServiceEnabled: true
};
Tealium.initialize(config);
```
See the [API Reference](/platforms/react-native/api/) for more information and additional configuration options.