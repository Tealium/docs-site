---
title: インストール
description: Tealium for .NET MAUIのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/dotnet-maui/install/
---
Tealium .NET MAUI統合は、Tealium for iOSとTealium for Androidとのインターフェースと構成クラスを提供するクロスプラットフォームインターフェースを提供します。


<blockquote>
この統合はTealium Xamarinからの移行です。詳細は[Tealium for Xamarin](https://docs.tealium.com/ja/platforms/xamarin/)を参照してください。
</blockquote>


## サンプルアプリ

ライブラリ、トラッキング方法、ベストプラクティスの実装について理解するために、サンプルアプリを使用します。

[.NET MAUIサンプルアプリをダウンロード](https://github.com/Tealium/tealium-dotnet-maui/tree/master/TealiumMauiExample)

## コードの取得

### インストール

Visual Studioの組み込みNuGetパッケージマネージャを使用して、.NET MAUI用のTealiumライブラリを直接インストールします。

[NuGetパッケージ: Tealium.Maui](https://www.nuget.org/packages/Tealium.Maui/)

## 初期化

### インスタンスマネージャ

クラスインスタンスをインスタンス化する前に、プロジェクトが適切なライブラリを参照していることを確認します。スレッドセーフなTealiumインスタンス管理を提供する`TealiumInstanceManager`クラスの使用を推奨します。



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

`TealiumInstanceManager`を作成した後、アカウント詳細と構成を含む`TealiumConfig`オブジェクトを作成します。

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

構成パラメータの完全なリストについては、[API: TealiumConfig](https://docs.tealium.com/ja/platforms/dotnet-maui/api/#object-tealiumconfig)を参照してください。

### インスタンス

`TealiumConfig`オブジェクトを作成した後、`TealiumInstanceManager`を使用してTealiumインスタンスを作成します。

```csharp
ITealium tealium = instanceManager.CreateInstance(tealConfig, (tealium) => 
{
  // インスタンスが準備完了したときのコールバック。
  // 例えば: 
  if (tealium != null) 
  {
    // 成功
  } 
  else 
  {
    // 失敗
  }
});
```

## リモートコマンド

ベンダーSDK内のネイティブコードをトリガーするために[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/)を使用します。.NET MAUIでは、[`IRemoteCommand`](https://docs.tealium.com/ja/platforms/dotnet-maui/api/#iremotecommand)インターフェースと`DelegateRemoteCommand`という組み込みの実装を使用してリモートコマンドがサポートされています。

Tealium iQのカスタムコマンドタグと連携するリモートコマンドを作成するには、コマンドIDと説明を追加パラメータなしで渡し、レスポンスハンドラを定義します。`resp.Payload`のコマンドのデータペイロードにアクセスします。

ローカルファイルまたはリモートURLオプションを使用してリモートコマンドを作成するには、それぞれ`path`または`url`パラメータを追加します。

```csharp
var myCommand = new DelegateRemoteCommand("logger", "Logger command.", path: "FILENAME.json")
{
    HandleResponseDelegate = (DelegateRemoteCommand cmd, IRemoteCommandResponse resp) =>
    {
        var payload = resp.Payload;
        System.Diagnostics.Debug.WriteLine($"Command Payload: {payload}");
        
        if (payload.GetValueForKey<Boolean>("frequent_visitor"))
        {
            // アクションを実行
        }
    }
};
```

より高度なソリューションについては、独自のクラスで`IRemoteCommand`インターフェースを実装します。

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

    // ローカルのJSONマッピングファイルへのパスを構成します
    public string Path => path;

    // リモートのJSONマッピングファイルへのURLを構成します
    public string Url => url;

    public void Dispose()
    {
        // リソースを整理します
    }

    public void HandleResponse(IRemoteCommandResponse response)
    {
        var payload = response.Payload;
        System.Diagnostics.Debug.WriteLine($"Command Payload: {payload}");

        if (payload.GetValueForKey<Boolean>("frequent_visitor"))
        {
            // アクションを実行
        }
    }
}

// Tealium iQマップ済みリモートコマンド
var iqCommand = new MyRemoteCommand(null, null);

// ローカルにマップされたリモートコマンド
var localCommand = new MyRemoteCommand("FILENAME.json", null);

// リモートにマップされたリモートコマンド
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

Tealium SDK内の処理ロジックにコードを注入する5つのデリゲートメソッドがあります：

| デリゲートメソッド | 説明 |
|:----------------|:-----------|
| `DelegateDispatchValidator()`              | 既存のディスパッチがドロップされるかキューに入れられるかを決定するブール値を返す2つのデリゲートメソッド[`ShouldDropDispatchDelegate()`,  `ShouldQueueDispatchDelegate()`]を提供します。ユーザーがオフラインになる可能性があるアプリ内のステップがある場合や、独自のバッチ処理ロジックを書きたい場合に使用します。 |
| `DispatchSentDelegateEventListener()`      | ディスパッチが送信されたときに呼び出されます。|
| `DispatchQueuedDelegateEventListener()`    | ディスパッチがキューに入れられたときに呼び出されます。|
| `WebViewReadyDelegateEventListener()`      | タグ管理モジュールを使用している場合、非表示のウェブビューが完全にロードされて準備ができたときに呼び出されます。|
| `SettingsPublishedDelegateEventListener()` | 更新されたパブリッシュ構成のセットが取得されたときに呼び出されます|

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
dispatch.PutString("KeyAddedByQueuedListener", "キューによって追加された値");
        }
    };
    WebViewReadyDelegateEventListener webViewListener = new WebViewReadyDelegateEventListener() {
        WebViewReady = (tealium, webView) =>  {
            System.Diagnostics.Debug.WriteLine("WebViewReadyの中にいます！");
        }
    };
    SettingsPublishedDelegateEventListener settingsListener = new SettingsPublishedDelegateEventListener() {
        SettingsPublished = (tealium) => {
            System.Diagnostics.Debug.WriteLine("SettingsPublishedの中にいます！");
        }
    };
    TealiumAdvancedConfig advConfig = new TealiumAdvancedConfig(validator,
        sendingListener, queuingListener, webViewListener, settingsListener);

    return advConfig;
}
```