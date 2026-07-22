---
title: インストール
description: Xamarin 1.x用Tealiumのインストール方法を学ぶ。
url: https://docs.tealium.com/ja/platforms/xamarin-v1/install/
---
<blockquote>
現在のバージョンについては、[Tealium for Xamarin 2.x](https://docs.tealium.com/ja/platforms/xamarin/)を参照してください。
</blockquote>


Tealium Xamarin統合は、ネイティブTealium iOSおよびAndroid SDKとインターフェースするクロスプラットフォームインターフェースと構成クラスのセットを提供します。

## サンプルアプリ

ライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、Xamarin [サンプルアプリ](https://github.com/Tealium/tealium-xamarin/tree/master/Samples/ExampleApp)をダウンロードしてください。

## コードの取得

#### 利用可能なDLL

Xamarin統合用にいくつかの[ダイナミックリンクライブラリ](https://github.com/Tealium/tealium-xamarin)（DLL）が利用可能です：

*   **`Tealium.Common.dll`**  
このDLLには、Xamarinアプリケーション内のすべてのプロジェクトで使用されるクロスプラットフォームコード、インターフェース、および共通コードが含まれています。このDLLを共有プロジェクトとプラットフォーム固有のプロジェクトの両方に参照として追加します。
*   **抽象化DLL**  
ネイティブTealium SDKのC# APIラッパーを作成するために含まれる抽象化DLL。これらのライブラリには、Tealium共通ライブラリによって提供されるインターフェースと抽象クラスのプラットフォーム固有の具体的なクラス実装が含まれています。共通ライブラリに対してクロスプラットフォームロジックをすべてコーディングします。
    *   `Tealium.Droid.dll` – Androidモバイルプラットフォーム用
    *   `Tealium.iOS.dll` – Appleモバイルプラットフォーム用

各モバイルプラットフォームに固有のDLLがあり、抽象化DLLによって参照されます。プラットフォームDLLはバインディングライブラリであり、そのためTealiumのネイティブSDKに組み込まれています。これらは、ネイティブSDKと直接やり取りするための自動生成されたラッパーコードを提供し、その結果、単独で使用することができます。

*   `Tealium.Platform.Droid.dll`
*   `Tealium.Platform.iOS.dll`


<blockquote>
バインディングライブラリは単独で使用することができます。自動生成されるため、各プラットフォームの名前空間が大きく異なり、開発努力に追加の複雑さをもたらします。代わりに`Common`およびプラットフォーム固有の抽象化ライブラリの使用をお勧めします。
</blockquote>


#### ライフサイクルモジュール

プラットフォームに関連するDLLを参照することで、オプションのライフサイクルモジュールが利用可能です。これらはネイティブ同等のSDKのバインディングライブラリです：

*   `Tealium.Platform.Lifecycle.Droid.dll`
*   `Tealium.Platform.Lifecycle.iOS.dll`

#### Androidの例

次の例は、典型的なXamarinベースのアプリからの共有プロジェクトとAndroidプラットフォーム固有のプロジェクトを示しています：

![](https://docs.tealium.com/images/platforms/xamarin/consent-manager-model.png)

例に示されているように、共有プロジェクトは`Tealium.Common.dll`ライブラリのみを参照していますが、Android固有のプロジェクトは次のすべてを参照しています：

*   `Tealium.Common.dll`
*   `Tealium.Droid.dll`
*   `Tealium.Platform.Droid.dll`
*   `Tealium.Platform.Lifecycle.Droid.dll`

## インストール

Xamarin用Tealiumライブラリをインストールするには、まずプロジェクトが適切なライブラリを参照していることを確認してください。スレッドセーフなTealiumインスタンス管理を提供する`TealiumInstanceManager`クラスの使用をお勧めします。



```csharp
using Tealium.Droid;
//...

ITealiumInstanceManager instanceManager = new TealiumInstanceManager(new TealiumInstanceFactoryDroid(<myAndroidApplication>));
//オプションのライフサイクルモジュールの有効化 - Tealium.Platform.Lifecycle.Droid.dllを参照する必要があります
TealiumLifecycleManager.SetLifecycleAutoTracking = TealiumDroid.Lifecycle.TealiumLifecycleControlDelegation.SetLifecycleAutoTracking;
```


```csharp
using Tealium.iOS;
//...

ITealiumInstanceManager instanceManager = new TealiumInstanceManager(new TealiumInstanceFactoryIOS());
//オプションのライフサイクルモジュールの有効化 - Tealium.Platform.Lifecycle.iOS.dllを参照する必要があります
TealiumLifecycleManager.SetLifecycleAutoTracking =TealiumIOS.Lifecycle.TealiumLifecycleControlDelegation.SetLifecycleAutoTracking;
```



### NuGet

Xamarin用TealiumライブラリをNuGetパッケージとしてインストールするには、Visual Studioの組み込みNuGetパッケージマネージャーを使用して直接インストールします。[Tealium NuGetリスティングについてもっと学ぶ](https://www.nuget.org/packages/Tealium.Xamarin/)。

## 初期化

`TealiumInstanceManager`が作成されたら、ネイティブSDKと同様に`Tealium`インスタンスを作成して開始します。`TealiumInstanceManager`はマルチトンパターンであり、複数の名前付きインスタンスへのアクセスを提供します。複数のTealiumプロファイルでデータを追跡する必要がある場合に便利です。

新しいインスタンスを作成するには、まずアカウントの詳細を含む`TealiumConfig`オブジェクトを作成します：

```csharp
TealiumConfig tealConfig
     = new TealiumConfig(instance, account, profile, environment, lifecycleAutoTracking);

```
| パラメータ               | タイプ      | 説明                                          | 例                     |
|:------------------------|:----------|:-----------------------------------------------------|:----------------------------|
| `instance`              | `String`  | TealiumインスタンスID                                  | `"tealium_main"`            |
| `account`               | `String`  | Tealiumアカウント名                                 | `"companyXYZ"`              |
| `profile`               | `String`  | Tealiumプロファイル名                                 | `"main"`                    |
| `environment`           | `String`  | Tealium環境名                             | [`"dev"`, `"qa"`, `"prod"`] |
| `lifecycleAutoTracking` | `Boolean` | (オプション) ライフサイクル自動追跡 (デフォルト: `true`) | ``true`, `false``           |

その後、`TealiumInstanceManager`を使用してTealiumインスタンスを作成し、イベントを追跡します：

```csharp
ITealium tealium = instanceManager.CreateInstance(tealConfig);
```

## 高度な構成

`TealiumConfig`クラスには、TealiumモバイルSDKのより高度な側面を有効または無効にするオプションのパラメータを指定するためのオーバーロードされたコンストラクタがあります。これらのパラメータはオプションであり、すべての顧客がこれらの機能を必要とするわけではありません。

### リモートコマンド

モバイル内のイベントの大部分は、コネクタを通じてアクションを実行するためにデータ収集サーバーに送信されるか、タグ管理ウェブビューでベンダータグをトリガーするために処理されますが、リモートコマンドはネイティブコードをトリガーするための追加の柔軟性を提供します。

次のサンプルコードは、コマンドID（`TealiumConsts.REMOTE_COMMAND_ID`に構成）を出力します。この例では、これを構成するために必要な関連するTagBridgeカスタムコマンドタグで構成された完全なペイロードデータへのアクセスも提供します：

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

[リモートコマンドについてもっと学ぶ](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/)。
### デリゲートメソッド

Tealium SDK内の処理ロジックにコードを挿入するための5つのデリゲートメソッドがあります：

| デリゲートメソッド                           | 説明                                                                                                                                                                                                                                                                                                                                           |
|:-------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `DelegateDispatchValidator()`              | 2つのデリゲートメソッド [`ShouldDropDispatchDelegate()`,  `ShouldQueueDispatchDelegate()`] を提供し、ブール値の戻り値が既存のディスパッチがドロップされるかキューに入れられるかを決定します。アプリ内でユーザーがオフラインである可能性があるステップがある場合や、独自のバッチ処理ロジックを書きたい場合に便利です |
| `DispatchSentDelegateEventListener()`      | ディスパッチが送信されたときに呼び出されます                                                                                                                                                                                                                                                                                                              |
| `DispatchQueuedDelegateEventListener()`    | ディスパッチがキューに入れられたときに呼び出されます                                                                                                                                                                                                                                                                                                            |
| `WebViewReadyDelegateEventListener()`      | WebViewが完全にロードされて準備ができたときに呼び出されます。タグ管理モジュールを使用している場合                                                                                                                                                                                                                                                         |
| `SettingsPublishedDelegateEventListener()` | 更新された公開構成のセットが取得されたときに呼び出されます                                                                                                                                                                                                                                                                               |

以下の例は、デリゲートメソッドの使用方法を示しています：

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

以下のリソースは、TealiumのAndroidおよびiOSライブラリをXamarinに追加するための広範なドキュメントへのリンクを提供します：

*   [Xamarin](https://www.xamarin.com/platform)
*   [Javaライブラリのバインディング](https://developer.xamarin.com/guides/android/advanced_topics/binding-a-java-library "Xamarin Javaライブラリのバインド方法")
*   [Xamarin - iOS Objective-Cライブラリのバインディング](https://developer.xamarin.com/guides/ios/advanced_topics/binding_objective-c/)
*   [ウォークスルー：iOS Objective-Cライブラリのバインディング](https://developer.xamarin.com/guides/ios/advanced_topics/binding_objective-c/walkthrough/ "Xamarin Objective-Cライブラリのバインド方法")