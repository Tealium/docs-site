---
title: Install
description: Install the Tealium plugin in your Unity application.
url: https://docs.tealium.com/platforms/unity/install/
---

<blockquote>
We have discontinued active development of the Tealium for Unity plugin. If you use this plugin and need assistance with it, contact Tealium Support.
</blockquote>


Tealium for Unity provides the Tealium native mobile libraries in your Unity application for iOS and Android.

## Requirements

* [Unity 2020.3+](https://docs.unity3d.com/Manual/UnityOverview.html)
* [Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/) or [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/)

## Sample app

Explore the iOS or Android [sample apps](https://github.com/Tealium/unity-plugin) to familiarize yourself with the Tealium library, tracking methods, and best practice implementation.

For the iOS app, open the `Examples/TealiumUnity-iOS/Unity-iPhone.xcodeproj` file in XCode. For the Android app, open the `Examples/TealiumUnity-Android/TealiumUnity-Android.apk` file in Android Studio

Alternatively, drag the contents of `Assets/Scenes` and `Assets/Scripts` into your project, then import `Tealium.unitypackage`.

## Install


<blockquote>
Tealium only supports Android and iOS platforms within Unity.
</blockquote>


### Package Import

The recommended installation method is to use the `TealiumUnityPlugin` as a `.unitypackage`.

1. Visit the [GitHub releases page](https://github.com/Tealium/unity-plugin/tree/release/2.0.0) and download `Tealium.unitypackage` from the latest release.
2. Create a new Unity project or open an existing project.
3. Import the `Tealium.unitypackage` to your project by selecting **Assets > Import Package > Custom Package**.
4. Add the following import statement to your project:   
      ```bash
      using TealiumCommon;
      ```

### Manual

To manually install Tealium for Unity, for iOS or Android, into your Unity application:

1. Clone the [GitHub repo](https://github.com/Tealium/unity-plugin).
2. Copy the `Assets/Plugins` and `Assets/Tealium` folders into your project.
3. Add the following import statement to your project:   
      ```bash
      using TealiumCommon;
      ```

### iOS

After you build and run your project for the first time, manually link the Tealium frameworks within XCode:

1. Click on the **Unity-iPhone** project.
2. Click on the **Build Phases** tab.
3. Expand the **Embedded Frameworks** section.
4. Copy all the frameworks located in the `Frameworks/Plugins/iOS` folder into the **Embedded Frameworks** section.


<blockquote>
`TealiumUnityPlugin` has a dependency on the Unity plugin `JSON.net` to serialize and deserialize objects. If `JSON.net` is already included in your project, you may need to remove it to avoid conflicts.
</blockquote>



## Initialize

Initialize the Tealium instance with the [`Initialize()`](https://docs.tealium.com/platforms/unity/api/#initialize) method, as shown in the following example:

```javascript
private TealiumConfig config = new TealiumConfig("tealiummobile",
                     "demo",
                     TealiumEnvironment.DEV,
                     new List<Dispatchers> {
                        Dispatchers.TagManagement,
                        Dispatchers.Collect,
                        Dispatchers.RemoteCommands },
                     new List<Collectors> {
                        Collectors.AppData,
                        Collectors.DeviceData,
                        Collectors.Lifecycle,
                        Collectors.Connectivity },
                     logLevel: LogLevel.Dev,
                     batchingEnabled: false,
                     visitorServiceEnabled: true);

TealiumUnityPlugin.Initialize(config);
```
