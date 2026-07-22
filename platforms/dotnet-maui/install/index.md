---
title: Install
description: Learn to install Tealium for .NET MAUI.
url: https://docs.tealium.com/platforms/dotnet-maui/install/
---
The Tealium .NET MAUI integration provides cross-platform interfaces and configuration classes that interface with Tealium for iOS and Tealium for Android.


<blockquote>
This integration is a migration from Tealium Xamarin. For more information, see [Tealium for Xamarin](https://docs.tealium.com/platforms/xamarin/).
</blockquote>


## Sample App

Use the sample app to familiarize yourself with our library, the tracking methods, and best practice implementation.

[Download the .NET MAUI sample app](https://github.com/Tealium/tealium-dotnet-maui/tree/master/TealiumMauiExample)

## Get the Code

### Install

Install the Tealium library for .NET MAUI directly from Visual Studio using the built-in NuGet package manager.

[NuGet Package: Tealium.Maui](https://www.nuget.org/packages/Tealium.Maui/)

## Initialize

### Instance Manager

To instantiate a class instance, first verify that your projects reference the appropriate libraries. We recommend using the `TealiumInstanceManager` classes, which provide thread-safe Tealium instance management.



```csharp
using Tealium.Droid;
//...

ITealiumInstanceManager instanceManager = new TealiumInstanceManager(new TealiumInstanceFactoryDroid(<myAndroidApplication>));
```


```csharp
using Tealium.iOS;
//...

ITealiumInstanceManager instanceManager = new TealiumInstanceManager(new TealiumInstanceFactoryIOS());
```



### Config

After you create the `TealiumInstanceManager`, create a `TealiumConfig` object with your account details and configuration settings:  

```csharp
TealiumConfig tealConfig = new TealiumConfig(
    "ACCOUNT",                                          
    "PROFILE",
    Tealium.Environment.Dev,
    new List<Dispatchers> {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    },
    new List<Collectors> {
        Collectors.LifeCycle, Collectors.AppData
    }
);
```

For the full list of configuration parameters, see [API: TealiumConfig](https://docs.tealium.com/platforms/dotnet-maui/api/#object-tealiumconfig).

### Instance

After you create the `TealiumConfig` object, use the `TealiumInstanceManager` to create a Tealium instance:

```csharp
ITealium tealium = instanceManager.CreateInstance(tealConfig, (tealium) => 
{
  // Callback for once the instance is ready.
  // For example: 
  if (tealium != null) 
  {
    // success
  } 
  else 
  {
    // failure
  }
});
```

## Remote Commands

Use [remote commands](https://docs.tealium.com/platforms/remote-commands/how-it-works/) to trigger native code within a vendor SDK. Remote commands is supported in .NET MAUI with the [`IRemoteCommand`](https://docs.tealium.com/platforms/dotnet-maui/api/#iremotecommand) interface and a built-in implementation called `DelegateRemoteCommand`.

To create a remote command that works with the Custom Command tag in Tealium iQ, pass a command ID and description with no additional parameters, then define the response handler. Access the data payload of the command in `resp.Payload`.

To create a remote command using the local file or remote URL option, add the `path` or `url` parameter respectively:

```csharp
var myCommand = new DelegateRemoteCommand("logger", "Logger command.", path: "FILENAME.json")
{
    HandleResponseDelegate = (DelegateRemoteCommand cmd, IRemoteCommandResponse resp) =>
    {
        var payload = resp.Payload;
        System.Diagnostics.Debug.WriteLine($"Command Payload: {payload}");
        
        if (payload.GetValueForKey<Boolean>("frequent_visitor"))
        {
            // take action
        }
    }
};
```

For a more advanced solution, implement the `IRemoteCommand` interface in your own class.

```csharp
public class MyRemoteCommand : IRemoteCommand
{
    private readonly string path;
    private readonly string url;

    public MyRemoteCommand(string path, string url)
    {
        this.path = path;
        this.url = url;
    }

    public string CommandId => "logger";

    public string Description => "Logger command";

    // Sets the path to a local JSON mappings file
    public string Path => path;

    // Sets the url to a remote JSON mappings file
    public string Url => url;

    public void Dispose()
    {
        // tidy up resources
    }

    public void HandleResponse(IRemoteCommandResponse response)
    {
        var payload = response.Payload;
        System.Diagnostics.Debug.WriteLine($"Command Payload: {payload}");

        if (payload.GetValueForKey<Boolean>("frequent_visitor"))
        {
            // take action
        }
    }
}

// Tealium iQ mapped Remote Command
var iqCommand = new MyRemoteCommand(null, null);

// Locally mapped Remote Command
var localCommand = new MyRemoteCommand("FILENAME.json", null);

// Remotely mapped Remote Command
var remoteCommand = new MyRemoteCommand(null, "https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json");
```

To use remote commands, you must include [`Dispatcher.RemoteCommands`](https://docs.tealium.com/platforms/dotnet-maui/api/#dispatchers) in the `TealiumConfig` object. Then add your remote command to the `TealiumConfig` object or call [`AddRemoteCommand()`](https://docs.tealium.com/platforms/dotnet-maui/api/#addremotecommand) on the Tealium instance.

Using `TealiumConfig`:

```csharp
TealiumConfig config = new TealiumConfig(
    "ACCOUNT",                                          
    "PROFILE",
    Tealium.Environment.Dev,
    new List<Dispatchers> {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    },
    remoteCommands: new List<IRemoteCommand>
    {
        myCommand
    }
);  
```

Using the Tealium instance:

```csharp
InstanceManager.CreateInstance(config, (tealium) =>
{
    if (tealium != null)
    {
        tealium.AddRemoteCommand(myCommand);
    }
});
```

## Delegate Methods

There are five delegated methods that inject code into the processing logic within the Tealium SDK:

| Delegated Method| Description|
|:----------------|:-----------|
| `DelegateDispatchValidator()`              | Provides two delegate methods [`ShouldDropDispatchDelegate()`,  `ShouldQueueDispatchDelegate()`] where the boolean return value determines whether or not an existing dispatch is dropped or queued. Use this if you have steps within your app where you know that the user may be offline or if you want to write your own batching logic. |
| `DispatchSentDelegateEventListener()`      | Called when a dispatch has been sent.|
| `DispatchQueuedDelegateEventListener()`    | Called when a dispatch has been queued.|
| `WebViewReadyDelegateEventListener()`      | Called when the hidden web view is fully loaded and ready, if you are using the Tag Management module.|
| `SettingsPublishedDelegateEventListener()` | Called when there has been an updated set of publish settings retrieved|

Example use of the delegate method:

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
