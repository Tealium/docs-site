---
title: インストール
description: Xamarin向けTealiumのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/xamarin/install/
---TealiumのXamarin統合では、Tealium for iOSおよびTealium for Androidと連携するクロスプラットフォームのインターフェイスと構成クラスが提供されます。


<blockquote>
以前のバージョンについては、[Tealium for Xamarin 1.x](https://docs.tealium.com/ja/platforms/xamarin-v1)を参照してください。
</blockquote>


## サンプルアプリ

サンプルアプリを使用して、ライブラリ、トラッキングメソッド、および実装のベストプラクティスについて理解を深めてください。

[Xamarinサンプルアプリをダウンロード](https://github.com/Tealium/tealium-xamarin/tree/master/TealiumXamarinExample)

## コードの入手

### インストール

組み込みのNuGetパッケージマネージャーを使用して、Visual StudioからXamarin向けTealiumライブラリを直接インストールします。

[NuGetパッケージ：Tealium.Xamarin](https://www.nuget.org/packages/Tealium.Xamarin/)

### 利用可能なDLL

Xamarin統合では、複数の[ダイナミックリンクライブラリ](https://github.com/Tealium/tealium-xamarin)（DLL）を利用できます。

*   **共通DLL**  
このDLLには、Xamarinアプリケーション内のすべてのプロジェクトで使用するクロスプラットフォームコード、インターフェイス、および共通コードが含まれています。このDLLを共有プロジェクトとプラットフォーム固有のプロジェクトの両方に参照として追加します。
    * `Tealium.Common.dll`
*   **抽象化DLL**  
抽象化DLLは、プラットフォーム固有のプロジェクトでネイティブTealium SDK用のC# APIラッパーを作成するために含まれています。これらのライブラリには、Tealium共通ライブラリが提供するインターフェイスおよび抽象クラスに対する、プラットフォーム固有の具象クラス実装が含まれています。すべてのクロスプラットフォームロジックは、共通ライブラリを対象として記述してください。
    *   `Tealium.Droid.dll` – Androidモバイルプラットフォーム用
    *   `Tealium.iOS.dll` – Appleモバイルプラットフォーム用
*  **プラットフォームDLL**  
抽象化DLLから参照される、各モバイルプラットフォーム固有のDLLがあります。プラットフォームDLLはバインディングライブラリであり、ネイティブTealium SDKが組み込まれています。ネイティブSDKを直接操作するための自動生成されたラッパーコードを提供します。
    *   `Tealium.Platform.Droid.dll`
    *   `Tealium.Platform.iOS.dll`


<blockquote>
バインディングライブラリは単独でも使用できます。ただし、自動生成されるため、プラットフォームごとに名前空間が大きく異なり、セットアップが複雑になる場合があります。代わりに、`Common`ライブラリとプラットフォーム固有の抽象化ライブラリを使用することをお勧めします。
</blockquote>



<blockquote>
ライフサイクルモジュールはデフォルトで含まれています。追加のDLLは必要ありません。
</blockquote>


### Androidの例

次の例は、一般的なXamarinベースのアプリに含まれる共有プロジェクトとAndroidプラットフォーム固有のプロジェクトを示しています。

![](https://docs.tealium.com/images/platforms/xamarin/consent-manager-model.png)

例に示すように、共有プロジェクトは`Tealium.Common.dll`ライブラリのみを参照しますが、Android固有のプロジェクトは次のすべてを参照します。

*   `Tealium.Common.dll`
*   `Tealium.Droid.dll`
*   `Tealium.Platform.Droid.dll`

## 初期化

### インスタンスマネージャー

クラスのインスタンスを生成する前に、各プロジェクトが適切なライブラリを参照していることを確認します。スレッドセーフなTealiumインスタンス管理を提供する`TealiumInstanceManager`クラスの使用をお勧めします。



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

`TealiumInstanceManager`を作成した後、アカウントの詳細と構成構成を指定して`TealiumConfig`オブジェクトを作成します。  

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

構成パラメータの完全な一覧については、[TealiumConfig](https://docs.tealium.com/ja/platforms/xamarin/api/#object-tealiumconfig)を参照してください。

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

[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/)を使用して、ベンダーSDK内のネイティブコードを実行します。Xamarinでは、[`IRemoteCommand`](https://docs.tealium.com/ja/platforms/xamarin/api/#iremotecommand)インターフェイスと、`DelegateRemoteCommand`という組み込み実装によってリモートコマンドがサポートされています。

タグ管理のカスタムコマンドタグと連携するリモートコマンドを作成するには、追加のパラメータを指定せずにコマンドIDと説明を渡し、レスポンスハンドラーを定義します。コマンドのデータペイロードには`resp.Payload`でアクセスします。

ローカルファイルまたはリモートURLオプションを使用するリモートコマンドを作成するには、それぞれ`path`または`url`パラメータを追加します。

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

リモートコマンドを使用するには、`TealiumConfig`オブジェクトに[`Dispatcher.RemoteCommands`](https://docs.tealium.com/ja/platforms/xamarin/api/#dispatchers)を含める必要があります。次に、リモートコマンドを`TealiumConfig`オブジェクトに追加するか、Tealiumインスタンスで[`AddRemoteCommand()`](https://docs.tealium.com/ja/platforms/xamarin/api/#addremotecommand)を呼び出して追加します。

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

Tealium SDK 内の処理ロジックにコードを挿入する、5 つのデリゲートメソッドがあります。

| デリゲートメソッド | 説明 |
|:----------------|:-----------|
| `DelegateDispatchValidator()` | 2 つのデリゲートメソッド [`ShouldDropDispatchDelegate()`、`ShouldQueueDispatchDelegate()`] を提供します。これらのブール型の戻り値により、既存のディスパッチを破棄するか、キューに追加するかが決まります。ユーザーがオフラインになる可能性があることが分かっているアプリ内の処理や、独自のバッチ処理ロジックを実装する場合に使用します。 |
| `DispatchSentDelegateEventListener()` | ディスパッチが送信されたときに呼び出されます。 |
| `DispatchQueuedDelegateEventListener()` | ディスパッチがキューに追加されたときに呼び出されます。 |
| `WebViewReadyDelegateEventListener()` | Tag Management モジュールを使用している場合、非表示の Web ビューが完全に読み込まれ、使用可能になったときに呼び出されます。 |
| `SettingsPublishedDelegateEventListener()` | 更新されたパブリッシュ構成一式が取得されたときに呼び出されます。 |

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

## リソース

以下のリソースには、Tealium の Android および iOS ライブラリを追加するための Xamarin の詳細なドキュメントへのリンクがあります。

*   [Xamarin：Kotlin ライブラリのバインド](https://docs.microsoft.com/en-us/xamarin/android/platform/binding-kotlin-library/)
*   [Xamarin：iOS Swift ライブラリのバインド](https://docs.microsoft.com/en-us/xamarin/ios/platform/binding-swift/)