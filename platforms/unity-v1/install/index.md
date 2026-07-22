---
title: Install
description: Install the Tealium 1.x plugin in your Unity application.
url: https://docs.tealium.com/platforms/unity-v1/install/
---

<blockquote>
This is the previous version (1.x) of Tealium for Unity. For the current version, see [Tealium for Unity 2.x](https://docs.tealium.com/platforms/unity/).
</blockquote>


Tealium for Unity lets you use the Tealium native mobile libraries (iOS, Android) in your Unity application.


<blockquote>
This is the previous version (1.x) of Tealium for Unity. For the current version, see [Tealium for Unity 2.x](https://docs.tealium.com/platforms/unity/).
</blockquote>


## Requirements

*   [Unity](https://unity.com/) 4.5+
*   iOS or Android target

## Sample app

Explore the [sample app](https://github.com/Tealium/unity-plugin/tree/master/Sample) to familiarize yourself with the Tealium library, tracking methods, and best practice implementation.


## Install

To integrate Tealium mobile libraries (iOS/Android) into your Unity application, copy all the contents of the Unity [plugin code](https://github.com/Tealium/unity-plugin) into the `Assets/Plugins/` directory within your Unity project.

When the Unity plugin is deployed to an Android or iOS device, Tealium events are logged in the respective device logs.


<blockquote>
Tealium only supports Android and iOS platforms within Unity.
</blockquote>


## Initialize

To initialize the Tealium instance, configure the following parameters:




Update the following [meta-data](https://developer.android.com/guide/topics/manifest/meta-data-element) keys in the Android manifest file `~/Assets/Plugins/Android/AndroidManifest.xml` to point to your Tealium instance.

```xml
<meta-data android:name="com.tealium.library.ACCOUNT" android:value="ACCOUNT" />
<meta-data android:name="com.tealium.library.PROFILE" android:value="PROFILE" />
<meta-data android:name="com.tealium.library.ENVIRONMENT" android:value="ENVIRONMENT" />
<meta-data android:name="com.tealium.library.DATA_SOURCE" android:value="DATASOURCE" />
<!--TODO: remove for release builds-->
<meta-data android:name="com.tealium.library.DEBUG" android:value="true" />
```





Update the Tealium account information in the bridging code file `Assets/Plugins/iOS/TealiumBridge.mm` to point to your Tealium instance.

```swift
#define TEALIUM_INSTANCE_NAME    @"TEALIUM_INSTANCE"
#define TEALIUM_ACCOUNT_NAME     @"ACCOUNT"
#define TEALIUM_PROFILE_NAME     @"PROFILE"
#define TEALIUM_ENVIRONMENT_NAME @"ENVIRONMENT"
#define TEALIUM_DATA_SOURCE      @"DATASOURCE"
```




## Verify

The following steps verify that Tealium is properly installed on your Unity application.

* In Unity, create a new empty `GameObject` by selecting from the menu **GameObject > Create Empty**. The `GameObject` displays in the **Inspector** window.

* Select `TealiumInitializer.cs` from the Unity **Project** window and drag/drop it into the **Inspector** window

* Select from the menu **Edit > Project Settings > Script Execution Order** and click the **+** sign to add the `TealiumInitializer` script.

* Drag the `TealiumInitializer` script to the top of the list of existing scripts to initialize the plugin, and then apply the changes.

* Click the **Play** button (or **Edit > Play**) to launch the Unity Editor and verify that you see a similar initialization message logged into to the Unity Console:
      ```
      view: {
        custom_alpha : alpha
        custom_beta : beta
        screen_title : SCREEN_NAME
      }
      ```


<blockquote>
To open the Console from Unity’s main menu, select **Window > General > Console**. Click the speech balloon icon to see full details.
</blockquote>

