---
title: Install
description: Learn to install Tealium for Xamarin 1.x.
url: https://docs.tealium.com/platforms/xamarin-v1/install/
---
<blockquote>
For the current version, see [Tealium for Xamarin 2.x](https://docs.tealium.com/platforms/xamarin/).
</blockquote>


The Tealium Xamarin integration provides a set of cross-platform interfaces and configuration classes that interface with the native Tealium iOS and Android SDKs.

## Sample App

To help to familiarize yourself with our library, the tracking methods, and best practice implementation, download the Xamarin [sample app](https://github.com/Tealium/tealium-xamarin/tree/master/Samples/ExampleApp).

## Get the Code

#### Available DLLs

Several [dynamic-link libraries](https://github.com/Tealium/tealium-xamarin) (DLLs) are available for the Xamarin integration:

*   **`Tealium.Common.dll`**  
This DLL contains cross-platform code, interfaces, and common code to be used in all projects within your Xamarin application. Add this DLL as a reference in both shared project and platform specific projects.
*   **Abstraction DLLs**  
Abstraction DLLS are included to create a C# API wrapper for the native Tealium SDKs in platform specific projects. These libraries contain platform specific, concrete class implementations for the interfaces and abstract classes provided by the Tealium common library. Code all of your cross-platform logic against the common library.
    *   `Tealium.Droid.dll` – for Android mobile platforms
    *   `Tealium.iOS.dll` – for Apple mobile platforms

There are DLLs specific to each mobile platform which are referenced by the abstraction DLLs. The platform DLLs are binding libraries and therefore embedded in Tealium's native SDKs. They provide auto-generated wrapper code that lets you interact with our native SDKs directly and as a result they may be used standalone.

*   `Tealium.Platform.Droid.dll`
*   `Tealium.Platform.iOS.dll`


<blockquote>
Binding libraries may be used by themselves. The fact that they are automatically generated results in vastly different namespaces for each platform, which adds an extra complication to development efforts. It is advised to make use of the `Common` and platform-specific abstraction libraries instead.
</blockquote>


#### Lifecycle Modules

An optional lifecycle module is available by referencing the relevant DLL for the platform. These are binding libraries for the native equivalent SDKs:

*   `Tealium.Platform.Lifecycle.Droid.dll`
*   `Tealium.Platform.Lifecycle.iOS.dll`

#### Android Example

The following example illustrates the Shared project and Android platform-specific project from a typical Xamarin based app:

![](https://docs.tealium.com/images/platforms/xamarin/consent-manager-model.png)

As shown in the example, the Shared Project references only the `Tealium.Common.dll` library, whereas the Android-specific project references all of the following:

*   `Tealium.Common.dll`
*   `Tealium.Droid.dll`
*   `Tealium.Platform.Droid.dll`
*   `Tealium.Platform.Lifecycle.Droid.dll`

## Install

To install Tealium library for Xamarin, first verify that your projects reference the appropriate libraries. We recommend using the `TealiumInstanceManager` classes provided as they provide out-of-the-box, thread-safe Tealium instance management.



```csharp
using Tealium.Droid;
//...

ITealiumInstanceManager instanceManager = new TealiumInstanceManager(new TealiumInstanceFactoryDroid(<myAndroidApplication>));
//Optional Lifecycle Module enablement - must reference Tealium.Platform.Lifecycle.Droid.dll
TealiumLifecycleManager.SetLifecycleAutoTracking = TealiumDroid.Lifecycle.TealiumLifecycleControlDelegation.SetLifecycleAutoTracking;
```


```csharp
using Tealium.iOS;
//...

ITealiumInstanceManager instanceManager = new TealiumInstanceManager(new TealiumInstanceFactoryIOS());
//Optional Lifecycle Module enablement - must reference Tealium.Platform.Lifecycle.iOS.dll
TealiumLifecycleManager.SetLifecycleAutoTracking =TealiumIOS.Lifecycle.TealiumLifecycleControlDelegation.SetLifecycleAutoTracking;
```



### NuGet

To install the Tealium library for Xamarin as a NuGet package, install it directly from Visual Studio using the built-in NuGet package manager. [Learn more](https://www.nuget.org/packages/Tealium.Xamarin/) about the Tealium NuGet listing.

## Initialize

Once the `TealiumInstanceManager` is created, begin creating `Tealium` instances as with the native SDKs. The `TealiumInstanceManager` is a multiton pattern that provides access to multiple named instances if you need to track data on more than one Tealium profile.

To create a new instance, first create a `TealiumConfig` object with your account details:  

```csharp
TealiumConfig tealConfig
     = new TealiumConfig(instance, account, profile, environment, lifecycleAutoTracking);

```
| Parameter               | Type      | Description                                          | Example                     |
|:------------------------|:----------|:-----------------------------------------------------|:----------------------------|
| `instance`              | `String`  | Tealium Instance ID                                  | `"tealium_main"`            |
| `account`               | `String`  | Tealium account name                                 | `"companyXYZ"`              |
| `profile`               | `String`  | Tealium profile name                                 | `"main"`                    |
| `environment`           | `String`  | Tealium environment name                             | [`"dev"`, `"qa"`, `"prod"`] |
| `lifecycleAutoTracking` | `Boolean` | (Optional) Lifecycle auto-tracking (default: `true`) | ``true`, `false``           |


Then use the `TealiumInstanceManager` to create a Tealium instance, which is used to track your events:  

```csharp
ITealium tealium = instanceManager.CreateInstance(tealConfig);
```

## Advanced Configuration

The `TealiumConfig` class has overloaded constructors for the option of specifying optional parameters to enable or disable the more advanced aspects of the Tealium Mobile SDKs. These parameters are optional as not all customers require these features.

### Remote Commands

While the majority of the events within mobile are either sent to our data collection servers to be actioned through connectors, or processed in the tag management web view to trigger vendor tags, remote commands provide additional flexibility to trigger native code through the `IRemoteCommand` interface.

The following sample code prints out the command ID (set to `TealiumConsts.REMOTE_COMMAND_ID`). This example also provides access to a full payload of data, as configured in the associated TagBridge Custom Command tag required to set this up:

```csharp
static List<IRemoteCommand> SetupRemoteCommands()
{
    var command = new DelegateRemoteCommand(TealiumConsts.REMOTE_COMMAND_ID, "Test command " + TealiumConsts.REMOTE_COMMAND_ID) {
        HandleResponseDelegate = (DelegateRemoteCommand cmd,
            IRemoteCommandResponse resp) => {
                System.Diagnostics.Debug.WriteLine($"Handling command {cmd.CommandId}...");
            }
        };
    return new List<IRemoteCommand>() { command };
}
```

[Learn more](https://docs.tealium.com/platforms/remote-commands/how-it-works/) about remote commands.

### Delegate Methods

There are five delegated methods that allow you to inject code into the processing logic within the Tealium SDK:

| Delegated Method                           | Description                                                                                                                                                                                                                                                                                                                                           |
|:-------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `DelegateDispatchValidator()`              | Provides two delegate methods [`ShouldDropDispatchDelegate()`,  `ShouldQueueDispatchDelegate()`] where the boolean return value determines whether or not an existing dispatch is dropped or queued -- Useful if you have steps within your app where you know that the user may be offline or you specifically want to write your own batching logic |
| `DispatchSentDelegateEventListener()`      | Called whenever a dispatch has been sent                                                                                                                                                                                                                                                                                                              |
| `DispatchQueuedDelegateEventListener()`    | Called whenever a dispatch has been queued                                                                                                                                                                                                                                                                                                            |
| `WebViewReadyDelegateEventListener()`      | Called when the WebView is fully loaded and ready, if you are using the Tag Management module                                                                                                                                                                                                                                                         |
| `SettingsPublishedDelegateEventListener()` | Called when there has been an updated set of publish settings retrieved                                                                                                                                                                                                                                                                               |

The following example illustrates the usage of the delegate method:

```csharp
static TealiumAdvancedConfig SetupAdvancedConfig() {

    DelegateDispatchValidator validator = new DelegateDispatchValidator() {
        ShouldDropDispatchDelegate = (ITealium arg1, IDispatch arg2) => {
            System.Diagnostics.Debug.WriteLine("Inside ShouldDropDispatchDelegate!");
            return false;
        },
        ShouldQueueDispatchDelegate = (ITealium arg1, IDispatch arg2, bool shouldQueue) => {
            System.Diagnostics.Debug.WriteLine("Inside ShouldQueueDispatchDelegate!");
            return shouldQueue;
        }
    };
    DispatchSentDelegateEventListener sendingListener = new DispatchSentDelegateEventListener() {
        DispatchSent = (tealium, dispatch) => {
            System.Diagnostics.Debug.WriteLine("Inside DispatchSent!");
            dispatch.PutString("KeyAddedBySendListener", "Value added by sending listener.");
        }
    };
    DispatchQueuedDelegateEventListener queuingListener = new DispatchQueuedDelegateEventListener() {
        DispatchQueued = (tealium, dispatch) => {
            System.Diagnostics.Debug.WriteLine("Inside DispatchQueued!");
            dispatch.PutString("KeyAddedByQueuedListener", "Value added by queuing listener.");
        }
    };
    WebViewReadyDelegateEventListener webViewListener = new WebViewReadyDelegateEventListener() {
        WebViewReady = (tealium, webView) =>  {
            System.Diagnostics.Debug.WriteLine("Inside WebViewReady!");
        }
    };
    SettingsPublishedDelegateEventListener settingsListener = new SettingsPublishedDelegateEventListener() {
        SettingsPublished = (tealium) => {
            System.Diagnostics.Debug.WriteLine("Inside SettingsPublished!");
        }
    };
    TealiumAdvancedConfig advConfig = new TealiumAdvancedConfig(validator,
        sendingListener, queuingListener, webViewListener, settingsListener);

    return advConfig;
}
```

## Resources

The following resources provide links to Xamarin's extensive documentation for adding Tealium's Android and iOS libraries:

*   [Xamarin](https://www.xamarin.com/platform)
*   [Binding a Java Library](https://developer.xamarin.com/guides/android/advanced_topics/binding-a-java-library "Xamarin How to Bind a Java Library")
*   [Xamarin - Binding an iOS Objective-C Library](https://developer.xamarin.com/guides/ios/advanced_topics/binding_objective-c/)
*   [Walkthrough: Binding an iOS Objective-C Library](https://developer.xamarin.com/guides/ios/advanced_topics/binding_objective-c/walkthrough/ "Xamarin how to bind an Objective-C library")
