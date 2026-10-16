---
title: モジュール
description: Tealium Prism SDKのKotlin、Swift、React Native用の利用可能なモジュールのリストです。
url: https://docs.tealium.com/ja/platforms/prism-mobile/modules/
---
Tealium Prismライブラリはモジュラー構造を採用しています。リソースフットプリントを小さく保つために必要なモジュールのみをインストールしてください。すべてのモジュールはCoreモジュールに依存しています。

## 利用可能なモジュール



| モジュール | パッケージ | 説明 |
| :--- | :--- | :--- |
| Core | `prism-core` | 必須。Tealiumインスタンス、構成、トラッキング、データレイヤーを提供します。 |
| [Lifecycle](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/lifecycle/) | `prism-lifecycle` | アプリのライフサイクルイベント（起動、起床、休止など）を追跡します。 |
| [Moments API](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/moments-api/) | `prism-moments-api` | Tealium AudienceStreamからリアルタイム訪問プロファイルへのアクセスを提供します。 |
| [Moments iQ](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/moments-iq/) | — | Tealium iQモバイルプロファイルからのアプリ内調査および体験ウィジェットを構成します。 |
| [AppData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/appdata/) | `prism-appdata` | アプリレベルのデータ（アプリ名、バージョン、ビルド番号など）を収集します。 |
| [Collect](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/collect/) | `prism-collect` | Tealium Collectエンドポイントへのイベントを送信します。 |
| [ConnectivityData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/connectivitydata/) | `prism-connectivity-data` | デバイスの接続情報（ネットワークタイプなど）を収集します。 |
| [DeepLink](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/deep-link/) | `prism-deeplink` | ディープリンクURLを処理し、ディープリンクデータをデータレイヤーに渡します。 |
| [DeviceData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/devicedata/) | `prism-device-data` | デバイス情報（モデル、OSバージョン、画面解像度など）を収集します。 |
| [TimeData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/timedata/) | `prism-time-data` | トラッキングコールにタイムスタンプデータを追加します。 |
| Trace | `prism-trace` | デバッグおよび検証のためのトレースセッションを有効にします。 |


| モジュール | パッケージ | 説明 |
| :--- | :--- | :--- |
| Core | `TealiumPrismCore` | 必須。Tealiumインスタンス、構成、トラッキング、データレイヤーを提供します。 |
| [Lifecycle](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/lifecycle/) | `TealiumPrismLifecycle` | アプリのライフサイクルイベント（起動、起床、休止など）を追跡します。 |
| [Moments API](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/moments-api/) | `TealiumPrismMomentsAPI` | Tealium AudienceStreamからリアルタイム訪問プロファイルへのアクセスを提供します。 |
| [Moments iQ](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/moments-iq/) | — | Tealium iQモバイルプロファイルからのアプリ内調査および体験ウィジェットを構成します。 |
| [AppData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/appdata/) | `TealiumPrismAppData` | アプリレベルのデータ（アプリ名、バージョン、ビルド番号など）を収集します。 |
| [Collect](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/collect/) | `TealiumPrismCollect` | Tealium Collectエンドポイントへのイベントを送信します。 |
| [ConnectivityData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/connectivitydata/) | `TealiumPrismConnectivityData` | デバイスの接続情報（ネットワークタイプなど）を収集します。 |
| [DeepLink](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/deep-link/) | `TealiumPrismDeepLink` | ディープリンクURLを処理し、ディープリンクデータをデータレイヤーに渡します。 |
| [DeviceData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/devicedata/) | `TealiumPrismDeviceData` | デバイス情報（モデル、OSバージョン、画面解像度など）を収集します。 |
| DataLayer | `TealiumPrismDataLayer` | データレイヤーの操作と永続性を拡張します。 |
| [TimeData](https://docs.tealium.com/ja/platforms/prism-mobile/module-list/timedata/) | `TealiumPrismTimeData` | トラッキングコールにタイムスタンプデータを追加します。 |
| Trace | `TealiumPrismTrace` | デバッグおよび検証のためのトレースセッションを有効にします。 |


React Nativeモジュールはnpmパッケージです。アプリに必要なパッケージのみをインストールしてください。

| モジュール | パッケージ | 説明 |
| :--- | :--- | :--- |
| Core | `@tealium/prism-react-native` | 必須。ネイティブのiOSおよびAndroid Prism SDKをラップします。Tealiumインスタンス、トラッキング、データレイヤーを提供します。 |
| Lifecycle | `@tealium/prism-react-native-lifecycle` | アプリのライフサイクルイベント（起動、起床、休止など）を追跡します。 |

モジュールの有効化は、個々のパッケージではなく、Tealium構成JSONによって制御されます。



## モジュールのインストール



`build.gradle`ファイルにPrism BOMと必要なモジュールを追加します：

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-core")
implementation("com.tealium.prism:prism-lifecycle")
implementation("com.tealium.prism:prism-collect")
```


Swiftパッケージ依存関係を追加する際に必要なモジュールを選択するか、CocoaPodsのPodfileで指定します。


npmでコアパッケージをインストールします：

```bash
npm install @tealium/prism-react-native
```

Lifecycleモジュールを追加するには：

```bash
npm install @tealium/prism-react-native-lifecycle
```

ネイティブのiOS依存関係をインストールします：

```bash
cd ios && pod install
```



## UIでのモジュール構成

SDKモジュールは、タグに似たマーケットプレイスとしてTealiumモバイルプロファイルで利用可能です。アプリコードを変更することなく、UIからモジュールを追加、構成、管理できます。

UIでモジュールを追加するには：

1. Tealiumモバイルプロファイルにアクセスします。
1. **モジュール**に移動します。
1. **モジュールを追加**を選択し、マーケットプレイスからモジュールを選びます。
1. モジュール構成を構成します。
1. 変更を保存して公開します。

SDKは次のリモート構成のリフレッシュまたはアプリの起動時に更新されたモジュール構成を取得します。

## 高度な構成：プログラムによるモジュールの有効化

SDKの初期化中に`TealiumConfig`でモジュールを指定することにより、プログラムによってモジュールを有効化できます：


<blockquote>
React Nativeはプログラムによるモジュールの有効化をサポートしていません。モジュールを有効にし、Tealiumモバイルプロファイルまたは構成JSONで構成してください。
</blockquote>




```kotlin
val config = TealiumConfig.Builder(
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
import TealiumPrismCollect
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

