---
title: インストール
description: TealiumをNativeScriptにインストールする方法を学びます。
url: https://docs.tealium.com/ja/platforms/nativescript/install/
---
TealiumのNativeScript統合は、ネイティブのTealium iOSおよびAndroid SDKとインターフェースを持つクロスプラットフォームインターフェースと構成クラスのセットを提供します。

## 要件

* ネイティブビルド環境へのアクセス
* [NativeScriptプラグイン](https://github.com/Tealium/tealium-nativescript-plugin)とツールがインストールされていること
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)

## サンプルアプリ

私たちのライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、[NativeScriptサンプルアプリ](https://github.com/Tealium/tealium-nativescript-plugin/tree/main/apps/demo)をダウンロードしてください。

サンプルアプリを実行するには、`npm i`コマンドを実行してすべての依存関係をインストールし、その後、ルートディレクトリ(`tealium-nativescript-plugin`)で`npm start`を実行します。プラットフォームに応じて、`apps.demo.android`または`apps.demo.ios`を選択します。


<blockquote>
現在、NativeScript on iOSでは初期アプリビルドが失敗するという既知の問題があります。成功するためには、`.xcworkspace`ファイルを開き、**Project** > **Build Settings** > **Validate Workspace**に移動し、プロパティを`Yes`に構成します。
</blockquote>



## インストール (NPM)

NPMを使用してNativeScript用のTealiumライブラリをインストールするには：

1. NativeScriptプロジェクトのルートに移動します。

2. 次のコマンドで`@tealium/nativescript-plugin`パッケージをダウンロードしてインストールします：  
      ```bash
      npm i @tealium/nativescript-plugin
      ```

## TypeScript

インストール後、TealiumモジュールをアプリのTypeScriptコードにインポートします：  
```javascript
import { Tealium } from '@tealium-nativescript/tealium';
import {
   TealiumConfig, TealiumView, TealiumEvent, ConsentCategories, Dispatchers, Collectors,ConsentPolicy,
   Expiry, ConsentStatus, TealiumEnvironment } from '@tealium-nativescript/tealium/common';
```

## 初期化

アプリがインストールされた後、[TealiumConfig](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/#tealiumconfig)初期化オプションを使用して`initialize()`メソッドで`Tealium`インスタンスを初期化します：  

```javascript
let config: TealiumConfig = {
    account: 'ACCOUNT',
    profile: 'PROFILE',
    environment: TealiumEnvironment.dev,
    dispatchers: [
        Dispatchers.Collect,
        Dispatchers.RemoteCommands,
        Dispatchers.TagManagement
    ],
    collectors: [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity
    ],
    consentPolicy: ConsentPolicy.gdpr,
    visitorServiceEnabled: true
};

Tealium.initialize(config);
```

詳細な情報と追加の構成オプションについては、[APIリファレンス](https://docs.tealium.com/ja/platforms/nativescript/api/)を参照してください。

## サポートされているモジュール

### コレクター

コレクターは、デバイスから補足情報を収集し、それをデータレイヤーに追加してからTealium Customer Data Hubに送信するモジュールです。一部のコレクターはコアライブラリに含まれていますが、他のコレクターはオプションであり、別のモジュールとしてインストールされます。

以下の表は、利用可能なコレクターを一覧表示しています。デフォルトのコレクターはコレクター名の隣に`*`が付いています。

| コレクター名 | TealiumConfig参照 |
| --- | --- |
| `AppData`* | `Collectors.AppData`|
| `Connectivity`* | `Collectors.Connectivity`|
| `Device` | `Collectors.Device`|
| `Lifecycle` | `Collectors.Lifecycle`|

これらのモジュールは、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/)の`collectors`プロパティを使用して有効または無効にします。

### ディスパッチャー

ディスパッチャーは、データレイヤーからのデータをTealiumエンドポイントに送信するモジュールです。現在利用可能なディスパッチャーは次のとおりです：

| ディスパッチャー名 | TealiumConfig参照 |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|


<blockquote>
少なくとも1つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、トラッキングは行われません。
</blockquote>

