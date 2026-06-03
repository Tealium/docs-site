---
title: Install
description: Learn to install Tealium for .NET MAUI.
url: https://docs.tealium.com/platforms/dotnet-maui/install/
---
The Tealium .NET MAUI integration provides cross-platform interfaces and configuration classes that interface with Tealium for iOS and Tealium for Android.

This integration is a migration from Tealium Xamarin. For more information, see [Tealium for Xamarin](/platforms/xamarin/).

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

ITealiumInstanceManager instanceManager = new TealiumInstanceManager(new TealiumInstanceFactoryDroid(&lt;myAndroidApplication&gt;));
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
    &#34;ACCOUNT&#34;,                                          
    &#34;PROFILE&#34;,
    Tealium.Environment.Dev,
    new List&lt;Dispatchers&gt; {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    },
    new List&lt;Collectors&gt; {
        Collectors.LifeCycle, Collectors.AppData
    }
);
```

For the full list of configuration parameters, see [API: TealiumConfig](/platforms/dotnet-maui/api/#object-tealiumconfig).

### Instance

After you create the `TealiumConfig` object, use the `TealiumInstanceManager` to create a Tealium instance:

```csharp
ITealium tealium = instanceManager.CreateInstance(tealConfig, (tealium) =&gt; 
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

Use [remote commands](/platforms/remote-commands/how-it-works/) to trigger native code within a vendor SDK. Remote commands is supported in .NET MAUI with the [`IRemoteCommand`](/platforms/dotnet-maui/api/#iremotecommand) interface and a built-in implementation called `DelegateRemoteCommand`.

To create a remote command that works with the Custom Command tag in Tealium iQ, pass a command ID and description with no additional parameters, then define the response handler. Access the data payload of the command in `resp.Payload`.

To create a remote command using the local file or remote URL option, add the `path` or `url` parameter respectively:

```csharp
var myCommand = new DelegateRemoteCommand(&#34;logger&#34;, &#34;Logger command.&#34;, path: &#34;FILENAME.json&#34;)
{
    HandleResponseDelegate = (DelegateRemoteCommand cmd, IRemoteCommandResponse resp) =&gt;
    {
        var payload = resp.Payload;
        System.Diagnostics.Debug.WriteLine($&#34;Command Payload: {payload}&#34;);
        
        if (payload.GetValueForKey&lt;Boolean&gt;(&#34;frequent_visitor&#34;))
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

    public string CommandId =&gt; &#34;logger&#34;;

    public string Description =&gt; &#34;Logger command&#34;;

    // Sets the path to a local JSON mappings file
    public string Path =&gt; path;

    // Sets the url to a remote JSON mappings file
    public string Url =&gt; url;

    public void Dispose()
    {
        // tidy up resources
    }

    public void HandleResponse(IRemoteCommandResponse response)
    {
        var payload = response.Payload;
        System.Diagnostics.Debug.WriteLine($&#34;Command Payload: {payload}&#34;);

        if (payload.GetValueForKey&lt;Boolean&gt;(&#34;frequent_visitor&#34;))
        {
            // take action
        }
    }
}

// Tealium iQ mapped Remote Command
var iqCommand = new MyRemoteCommand(null, null);

// Locally mapped Remote Command
var localCommand = new MyRemoteCommand(&#34;FILENAME.json&#34;, null);

// Remotely mapped Remote Command
var remoteCommand = new MyRemoteCommand(null, &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json&#34;);
```

To use remote commands, you must include [`Dispatcher.RemoteCommands`](/platforms/dotnet-maui/api/#dispatchers) in the `TealiumConfig` object. Then add your remote command to the `TealiumConfig` object or call [`AddRemoteCommand()`](/platforms/dotnet-maui/api/#addremotecommand) on the Tealium instance.

Using `TealiumConfig`:

```csharp
TealiumConfig config = new TealiumConfig(
    &#34;ACCOUNT&#34;,                                          
    &#34;PROFILE&#34;,
    Tealium.Environment.Dev,
    new List&lt;Dispatchers&gt; {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    },
    remoteCommands: new List&lt;IRemoteCommand&gt;
    {
        myCommand
    }
);  
```

Using the Tealium instance:

```csharp
InstanceManager.CreateInstance(config, (tealium) =&gt;
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
        ShouldDropDispatchDelegate = (ITealium arg1, IDispatch arg2) =&gt; {
            System.Diagnostics.Debug.WriteLine(&#34;Inside ShouldDropDispatchDelegate!&#34;);
            return false;
        },
        ShouldQueueDispatchDelegate = (ITealium arg1, IDispatch arg2, bool shouldQueue) =&gt; {
            System.Diagnostics.Debug.WriteLine(&#34;Inside ShouldQueueDispatchDelegate!&#34;);
            return shouldQueue;
        }
    };
    DispatchSentDelegateEventListener sendingListener = new DispatchSentDelegateEventListener() {
        DispatchSent = (tealium, dispatch) =&gt; {
            System.Diagnostics.Debug.WriteLine(&#34;Inside DispatchSent!&#34;);
            dispatch.PutString(&#34;KeyAddedBySendListener&#34;, &#34;Value added by sending listener.&#34;);
        }
    };
    DispatchQueuedDelegateEventListener queuingListener = new DispatchQueuedDelegateEventListener() {
        DispatchQueued = (tealium, dispatch) =&gt; {
            System.Diagnostics.Debug.WriteLine(&#34;Inside DispatchQueued!&#34;);
            dispatch.PutString(&#34;KeyAddedByQueuedListener&#34;, &#34;Value added by queuing listener.&#34;);
        }
    };
    WebViewReadyDelegateEventListener webViewListener = new WebViewReadyDelegateEventListener() {
        WebViewReady = (tealium, webView) =&gt;  {
            System.Diagnostics.Debug.WriteLine(&#34;Inside WebViewReady!&#34;);
        }
    };
    SettingsPublishedDelegateEventListener settingsListener = new SettingsPublishedDelegateEventListener() {
        SettingsPublished = (tealium) =&gt; {
            System.Diagnostics.Debug.WriteLine(&#34;Inside SettingsPublished!&#34;);
        }
    };
    TealiumAdvancedConfig advConfig = new TealiumAdvancedConfig(validator,
        sendingListener, queuingListener, webViewListener, settingsListener);

    return advConfig;
}
```
