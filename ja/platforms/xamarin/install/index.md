---
title: インストール
description: Tealium for Xamarinのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/xamarin/install/
---Tealium Xamarin統合は、Tealium for iOSおよびTealium for Androidとインターフェースを持つクロスプラットフォームインターフェースと構成クラスを提供します。


<blockquote>
前のバージョンについては、[Tealium for Xamarin 1.x](https://docs.tealium.com/ja/platforms/xamarin-v1)を参照してください。
</blockquote>


## サンプルアプリ

サンプルアプリを使用して、ライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れてください。

[Xamarinサンプルアプリをダウンロード](https://github.com/Tealium/tealium-xamarin/tree/master/TealiumXamarinExample)

## コードの取得

### インストール

Visual Studioの組み込みNuGetパッケージマネージャーを使用して、TealiumライブラリをXamarinに直接インストールします。

[NuGetパッケージ: Tealium.Xamarin](https://www.nuget.org/packages/Tealium.Xamarin/)

### 利用可能なDLL

Xamarin統合のためのいくつかの[dynamic-link libraries](https://github.com/Tealium/tealium-xamarin) (DLLs)が利用可能です：

*   **Common DLL**  
このDLLには、クロスプラットフォームコード、インターフェース、およびXamarinアプリケーション内のすべてのプロジェクトで使用される共通コードが含まれています。このDLLを共有プロジェクトとプラットフォーム固有のプロジェクトの両方で参照として追加します。
    * `Tealium.Common.dll`
*   **Abstraction DLL**  
抽象化DLLは、プラットフォーム固有のプロジェクトでネイティブのTealium SDKをC# APIラッパーとして作成するために含まれています。これらのライブラリには、Tealium共通ライブラリによって提供されるインターフェースと抽象クラスの具体的なクラス実装が含まれています。すべてのクロスプラットフォームロジックを共通ライブラリに対してコード化します。
    *   `Tealium.Droid.dll` – Androidモバイルプラットフォーム用
    *   `Tealium.iOS.dll` – Appleモバイルプラットフォーム用
*  **Platform DLL**  
各モバイルプラットフォームに固有のDLLがあり、抽象化DLLによって参照されます。プラットフォームDLLはバインディングライブラリであり、ネイティブのTealium SDKに組み込まれています。これらは、ネイティブSDKと直接対話するための自動生成されたラッパーコードを提供します。
    *   `Tealium.Platform.Droid.dll`
    *   `Tealium.Platform.iOS.dll`


<blockquote>
バインディングライブラリはそれ自体で使用することができます。それらが自動的に生成されるため、各プラットフォームの名前空間が大幅に異なり、構成が複雑になる可能性があります。代わりに`Common`とプラットフォーム固有の抽象化ライブラリの使用をお勧めします。
</blockquote>



<blockquote>
ライフサイクルモジュールはデフォルトで含まれています。追加のDLLは必要ありません。
</blockquote>


### Androidの例

次の例は、典型的なXamarinベースのアプリからの共有プロジェクトとAndroidプラットフォーム固有のプロジェクトを示しています：

![](https://docs.tealium.com/images/platforms/xamarin/consent-manager-model.png)

例に示されているように、共有プロジェクトは`Tealium.Common.dll`ライブラリのみを参照し、Android固有のプロジェクトは以下のすべてを参照します：

*   `Tealium.Common.dll`
*   `Tealium.Droid.dll`
*   `Tealium.Platform.Droid.dll`

## 初期化

### インスタンスマネージャー

クラスインスタンスをインスタンス化するには、まずプロジェクトが適切なライブラリを参照していることを確認します。スレッドセーフなTealiumインスタンス管理を提供する`TealiumInstanceManager`クラスの使用をお勧めします。



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

`TealiumInstanceManager`を作成した後、アカウント詳細と構成を含む`TealiumConfig`オブジェクトを作成します：  

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

[TealiumConfig](https://docs.tealium.com/ja/platforms/xamarin/api/#object-tealiumconfig)の構成パラメータの完全なリストを参照してください。

### インスタンス

`TealiumConfig`オブジェクトを作成した後、`TealiumInstanceManager`を使用してTealiumインスタンスを作成します：

```csharp
ITealium tealium = instanceManager.CreateInstance(tealConfig, (tealium) => 
{
  // インスタンスが準備完了したときのコールバック。
  // 例えば： 
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

ベンダーSDK内のネイティブコードをトリガーするために[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/)を使用します。リモートコマンドは、[`IRemoteCommand`](https://docs.tealium.com/ja/platforms/xamarin/api/#iremotecommand)インターフェースと`DelegateRemoteCommand`という名前の組み込み実装を使用してXamarinでサポートされています。

Tealium iQのカスタムコマンドタグと連携するリモートコマンドを作成するには、コマンドIDと説明を追加パラメータなしで渡し、レスポンスハンドラを定義します。`resp.Payload`のコマンドのデータペイロードにアクセスします。

ローカルファイルまたはリモートURLオプションを使用してリモートコマンドを作成するには、それぞれ`path`または`url`パラメータを追加します：

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

より高度なソリューションとして、独自のクラスで`IRemoteCommand`インターフェースを実装します。

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

リモートコマンドを使用するには、`TealiumConfig`オブジェクトに[`Dispatcher.RemoteCommands`](https://docs.tealium.com/ja/platforms/xamarin/api/#dispatchers)を含める必要があります。その後、リモートコマンドを`TealiumConfig`オブジェクトに追加するか、Tealiumインスタンスで[`AddRemoteCommand()`](https://docs.tealium.com/ja/platforms/xamarin/api/#addremotecommand)を呼び出します。

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
| 委任メソッド | 説明 |
|:----------------|:-----------|
| `DelegateDispatchValidator()`              | [`ShouldDropDispatchDelegate()`,  `ShouldQueueDispatchDelegate()`]という2つの委任メソッドを提供し、そのブール値の戻り値が既存のディスパッチがドロップされるかキューに入れられるかを決定します。ユーザーがオフラインになる可能性があるアプリ内のステップがある場合や、独自のバッチ処理ロジックを書きたい場合に使用します。 |
| `DispatchSentDelegateEventListener()`      | ディスパッチが送信されたときに呼び出されます。|
| `DispatchQueuedDelegateEventListener()`    | ディスパッチがキューに入れられたときに呼び出されます。|
| `WebViewReadyDelegateEventListener()`      | タグ管理モジュールを使用している場合、非表示のウェブビューが完全にロードされて準備ができたときに呼び出されます。|
| `SettingsPublishedDelegateEventListener()` | 公開構成の更新セットが取得されたときに呼び出されます。|

委任メソッドの使用例：

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

## リソース

以下のリソースは、TealiumのAndroidとiOSライブラリを追加するためのXamarinの詳細なドキュメンテーションへのリンクを提供します：

*   [Xamarin: Kotlinライブラリのバインディング](https://docs.microsoft.com/ja-jp/xamarin/android/platform/binding-kotlin-library/)
*   [Xamarin: iOS Swiftライブラリのバインディング](https://docs.microsoft.com/ja-jp/xamarin/ios/platform/binding-swift/)