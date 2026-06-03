---
title: Install
description: Install the Tealium 1.x plugin in your Unity application.
url: https://docs.tealium.com/platforms/unity-v1/install/
---
This is the previous version (1.x) of Tealium for Unity. For the current version, see [Tealium for Unity 2.x](/platforms/unity/).

Tealium for Unity lets you use the Tealium native mobile libraries (iOS, Android) in your Unity application.

This is the previous version (1.x) of Tealium for Unity. For the current version, see [Tealium for Unity 2.x](/platforms/unity/).

## Requirements

*   [Unity](https://unity.com/) 4.5&#43;
*   iOS or Android target

## Sample app

Explore the [sample app](https://github.com/Tealium/unity-plugin/tree/master/Sample) to familiarize yourself with the Tealium library, tracking methods, and best practice implementation.


## Install

To integrate Tealium mobile libraries (iOS/Android) into your Unity application, copy all the contents of the Unity [plugin code](https://github.com/Tealium/unity-plugin) into the `Assets/Plugins/` directory within your Unity project.

When the Unity plugin is deployed to an Android or iOS device, Tealium events are logged in the respective device logs.

Tealium only supports Android and iOS platforms within Unity.

## Initialize

To initialize the Tealium instance, configure the following parameters:




Update the following [meta-data](https://developer.android.com/guide/topics/manifest/meta-data-element) keys in the Android manifest file `~/Assets/Plugins/Android/AndroidManifest.xml` to point to your Tealium instance.

```xml
&lt;meta-data android:name=&#34;com.tealium.library.ACCOUNT&#34; android:value=&#34;ACCOUNT&#34; /&gt;
&lt;meta-data android:name=&#34;com.tealium.library.PROFILE&#34; android:value=&#34;PROFILE&#34; /&gt;
&lt;meta-data android:name=&#34;com.tealium.library.ENVIRONMENT&#34; android:value=&#34;ENVIRONMENT&#34; /&gt;
&lt;meta-data android:name=&#34;com.tealium.library.DATA_SOURCE&#34; android:value=&#34;DATASOURCE&#34; /&gt;
&lt;!--TODO: remove for release builds--&gt;
&lt;meta-data android:name=&#34;com.tealium.library.DEBUG&#34; android:value=&#34;true&#34; /&gt;
```





Update the Tealium account information in the bridging code file `Assets/Plugins/iOS/TealiumBridge.mm` to point to your Tealium instance.

```swift
#define TEALIUM_INSTANCE_NAME    @&#34;TEALIUM_INSTANCE&#34;
#define TEALIUM_ACCOUNT_NAME     @&#34;ACCOUNT&#34;
#define TEALIUM_PROFILE_NAME     @&#34;PROFILE&#34;
#define TEALIUM_ENVIRONMENT_NAME @&#34;ENVIRONMENT&#34;
#define TEALIUM_DATA_SOURCE      @&#34;DATASOURCE&#34;
```




## Verify

The following steps verify that Tealium is properly installed on your Unity application.

* In Unity, create a new empty `GameObject` by selecting from the menu **GameObject &gt; Create Empty**. The `GameObject` displays in the **Inspector** window.

* Select `TealiumInitializer.cs` from the Unity **Project** window and drag/drop it into the **Inspector** window

* Select from the menu **Edit &gt; Project Settings &gt; Script Execution Order** and click the **&#43;** sign to add the `TealiumInitializer` script.

* Drag the `TealiumInitializer` script to the top of the list of existing scripts to initialize the plugin, and then apply the changes.

* Click the **Play** button (or **Edit &gt; Play**) to launch the Unity Editor and verify that you see a similar initialization message logged into to the Unity Console:
      ```
      view: {
        custom_alpha : alpha
        custom_beta : beta
        screen_title : SCREEN_NAME
      }
      ```

To open the Console from Unity’s main menu, select **Window &gt; General &gt; Console**. Click the speech balloon icon to see full details.
