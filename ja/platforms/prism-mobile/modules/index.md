---
title: モジュール
description: Kotlin、Swift、React Native向けTealium Prism SDKで利用可能なモジュールの一覧です。
url: https://docs.tealium.com/ja/platforms/prism-mobile/modules/
---
Tealium Prismライブラリはモジュール式アーキテクチャを採用しています。リソース使用量を抑えるため、必要なモジュールのみをインストールしてください。すべてのモジュールはCoreモジュールに依存します。

## 利用可能なモジュール



| モジュール | パッケージ | 説明 |
| :--- | :--- | :--- |
| Core | `prism-core` | 必須。Tealiumインスタンス、構成、トラッキング、データレイヤーを提供します。 |
| [Lifecycle](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/lifecycle/) | `prism-lifecycle` | 起動、ウェイク、スリープなど、アプリのライフサイクルイベントを追跡します。 |
| [Context API](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/context-api/) | `prism-context-api` | 顧客データプラットフォーム（CDP）からリアルタイムの訪問プロファイルにアクセスできるようにします。 |
| [AppData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/appdata/) | `prism-core` | アプリ名、バージョン、ビルド番号など、アプリレベルのデータを収集します。 |
| [Collect](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/collect/) | `prism-core` | イベントをTealium Collectエンドポイントに送信します。 |
| [ConnectivityData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/connectivitydata/) | `prism-core` | ネットワークタイプなど、デバイスの接続情報を収集します。 |
| [DeepLink](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/deep-link/) | `prism-core` | ディープリンクURLを処理し、ディープリンクデータをデータレイヤーに渡します。 |
| [DeviceData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/devicedata/) | `prism-core` | モデル、OSバージョン、画面解像度などのデバイス情報を収集します。 |
| [TimeData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/timedata/) | `prism-core` | トラッキング呼び出しにタイムスタンプデータを追加します。 |
| Trace | `prism-core` | デバッグと検証に使用するトレースセッションを有効にします。 |


| モジュール | パッケージ | 説明 |
| :--- | :--- | :--- |
| Core | `TealiumPrismCore` | 必須。Tealiumインスタンス、構成、トラッキング、データレイヤーを提供します。 |
| [Lifecycle](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/lifecycle/) | `TealiumPrismLifecycle` | 起動、ウェイク、スリープなど、アプリのライフサイクルイベントを追跡します。 |
| [Context API](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/context-api/) | `TealiumPrismContextAPI` | CDPからリアルタイムの訪問プロファイルにアクセスできるようにします。 |
| [AppData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/appdata/) | `TealiumPrismCore` | アプリ名、バージョン、ビルド番号など、アプリレベルのデータを収集します。 |
| [Collect](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/collect/) | `TealiumPrismCore` | イベントをTealium Collectエンドポイントに送信します。 |
| [ConnectivityData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/connectivitydata/) | `TealiumPrismCore` | ネットワークタイプなど、デバイスの接続情報を収集します。 |
| [DeepLink](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/deep-link/) | `TealiumPrismCore` | ディープリンクURLを処理し、ディープリンクデータをデータレイヤーに渡します。 |
| [DeviceData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/devicedata/) | `TealiumPrismCore` | モデル、OSバージョン、画面解像度などのデバイス情報を収集します。 |
| DataLayer | `TealiumPrismCore` | 拡張データレイヤー操作と永続化を提供します。 |
| [TimeData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/timedata/) | `TealiumPrismCore` | トラッキング呼び出しにタイムスタンプデータを追加します。 |
| Trace | `TealiumPrismCore` | デバッグと検証に使用するトレースセッションを有効にします。 |


React Nativeモジュールはnpmパッケージです。アプリに必要なパッケージのみをインストールしてください。

| モジュール | パッケージ | 説明 |
| :--- | :--- | :--- |
| Core | `@tealium/prism-react-native` | 必須。ネイティブのiOSおよびAndroid Prism SDKをラップし、Tealiumインスタンス、トラッキング、データレイヤーを提供します。 |
| Lifecycle | `@tealium/prism-react-native-lifecycle` | 起動、ウェイク、スリープなど、アプリのライフサイクルイベントを追跡します。 |

モジュールの有効化は個々のパッケージではなく、Tealium構成JSONによって制御されます。



## モジュールのインストール



Prism BOMと必要なモジュールを`build.gradle`ファイルに追加します。

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-core")
implementation("com.tealium.prism:prism-lifecycle")
```


Swiftパッケージの依存関係を追加するときに必要なモジュールを選択するか、CocoaPodsのPodfileで指定します。


npmを使用してCoreパッケージをインストールします。

```bash
npm install @tealium/prism-react-native
```

Lifecycleモジュールを追加するには、次のコマンドを実行します。

```bash
npm install @tealium/prism-react-native-lifecycle
```

ネイティブiOSの依存関係をインストールします。

```bash
cd ios && pod install
```



## UIでのモジュールの構成

SDKモジュールは、タグと同様に、Tealiumモバイルプロファイル内でマーケットプレイスとして利用できます。アプリのコードを変更せずに、UIからモジュールを追加、構成、管理できます。

UIでモジュールを追加するには、次の手順を実行します。

1. Tealiumモバイルプロファイルに移動します。
1. **モジュール**に移動します。
1. **モジュールを追加**を選択し、マーケットプレイスからモジュールを選択します。
1. モジュール構成を構成します。
1. 変更を保存してパブリッシュします。

SDKは、次回のリモート構成の更新時またはアプリの起動時に、更新されたモジュール構成を取得します。

## 高度な構成：プログラムによるモジュールの有効化

プログラムによってモジュールを有効化するには、SDKの初期化時に`TealiumConfig`でモジュールを指定します。


<blockquote>
React Nativeは、プログラムによるモジュールの有効化をサポートしていません。Tealiumモバイルプロファイルまたは構成JSONでモジュールを有効化し、構成してください。
</blockquote>




```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "my_account",
    profileName = "my_profile",
    environment = Environment.PROD,
    modules = listOf(
        Modules.appData(),
        Modules.collect(),
        Modules.lifecycle(),
    )
).build()
```


```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
import TealiumPrismLifecycle
#endif

let config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [
                            Modules.appData(),
                            Modules.collect(),
                            Modules.lifecycle(),
                           ],
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json")
```

