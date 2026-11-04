---
title: インストール
description: .NET MAUI向けTealiumのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/dotnet-maui/install/
---
Tealium .NET MAUI統合では、Tealium for iOSおよびTealium for Androidと連携するクロスプラットフォームのインターフェイスと構成クラスが提供されます。


<blockquote>
この統合はTealium Xamarinから移行されたものです。詳細については、[Tealium for Xamarin](https://docs.tealium.com/ja/platforms/xamarin/)を参照してください。
</blockquote>


## サンプルアプリ

サンプルアプリを使用して、ライブラリ、トラッキングメソッド、実装のベストプラクティスについて理解を深めてください。

[.NET MAUIサンプルアプリをダウンロード](https://github.com/Tealium/tealium-dotnet-maui/tree/master/TealiumMauiExample)

## コードの取得

### インストール

組み込みのNuGetパッケージマネージャーを使用して、Visual Studioから.NET MAUI向けTealiumライブラリを直接インストールします。

[NuGetパッケージ：Tealium.Maui](https://www.nuget.org/packages/Tealium.Maui/)

## 初期化

### インスタンスマネージャー

クラスのインスタンスを作成する前に、プロジェクトが適切なライブラリを参照していることを確認します。スレッドセーフなTealiumインスタンス管理を提供する`TealiumInstanceManager`クラスの使用を推奨します。



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



### 構成

`TealiumInstanceManager`を作成した後、アカウントの詳細と構成構成を使用して`TealiumConfig`オブジェクトを作成します。  

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

構成パラメーターの完全な一覧については、[API：TealiumConfig](https://docs.tealium.com/ja/platforms/dotnet-maui/api/#object-tealiumconfig)を参照してください。

### インスタンス

`TealiumConfig`オブジェクトを作成した後、`TealiumInstanceManager`を使用してTealiumインスタンスを作成します。

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

## リモートコマンド

[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/)を使用して、ベンダーSDK内のネイティブコードをトリガーします。.NET MAUIでは、[`IRemoteCommand`](https://docs.tealium.com/ja/platforms/dotnet-maui/api/#iremotecommand)インターフェイスと、`DelegateRemoteCommand`という組み込み実装によってリモートコマンドがサポートされています。

タグ管理のカスタムコマンドタグで動作するリモートコマンドを作成するには、追加のパラメーターを指定せずにコマンドIDと説明を渡し、レスポンスハンドラーを定義します。コマンドのデータペイロードには`resp.Payload`でアクセスします。

ローカルファイルまたはリモートURLオプションを使用してリモートコマンドを作成するには、それぞれ`path`または`url`パラメーターを追加します。

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

より高度なソリューションを実装するには、独自のクラスで`IRemoteCommand`インターフェイスを実装します。

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

// Tag Management mapped Remote Command
var iqCommand = new MyRemoteCommand(null, null);

// Locally mapped Remote Command
var localCommand = new MyRemoteCommand("FILENAME.json", null);

// Remotely mapped Remote Command
var remoteCommand = new MyRemoteCommand(null, "https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json");
```

リモートコマンドを使用するには、`TealiumConfig`オブジェクトに[`Dispatcher.RemoteCommands`](https://docs.tealium.com/ja/platforms/dotnet-maui/api/#dispatchers)を含める必要があります。その後、リモートコマンドを`TealiumConfig`オブジェクトに追加するか、Tealiumインスタンスで[`AddRemoteCommand()`](https://docs.tealium.com/ja/platforms/dotnet-maui/api/#addremotecommand)を呼び出します。

`TealiumConfig`を使用する場合：

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

Tealiumインスタンスを使用する場合：

```csharp
InstanceManager.CreateInstance(config, (tealium) =>
{
    if (tealium != null)
    {
        tealium.AddRemoteCommand(myCommand);
    }
});
```
## デリゲートメソッド

Tealium SDK 内の処理ロジックにコードを挿入するデリゲートメソッドは、次の 5 つです。

| デリゲートメソッド | 説明 |
|:----------------|:-----------|
| `DelegateDispatchValidator()`              | 2 つのデリゲートメソッド [`ShouldDropDispatchDelegate()`, `ShouldQueueDispatchDelegate()`] を提供します。これらの Boolean 戻り値によって、既存のディスパッチを破棄するか、キューに追加するかが決まります。アプリ内にユーザーがオフラインになる可能性がある処理が含まれる場合や、独自のバッチ処理ロジックを実装する場合に使用します。 |
| `DispatchSentDelegateEventListener()`      | ディスパッチが送信されたときに呼び出されます。|
| `DispatchQueuedDelegateEventListener()`    | ディスパッチがキューに追加されたときに呼び出されます。|
| `WebViewReadyDelegateEventListener()`      | Tag Management モジュールを使用している場合に、非表示の Web ビューが完全に読み込まれ、準備が整ったときに呼び出されます。|
| `SettingsPublishedDelegateEventListener()` | 更新されたパブリッシュ構成一式が取得されたときに呼び出されます。|

デリゲートメソッドの使用例：

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