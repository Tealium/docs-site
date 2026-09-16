---
title: Moments APIモジュール（現在はContext API）
description: React Native用Tealium Context APIモジュールのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/react-native/context-api/
---

<blockquote>
Moments APIはContext APIに名称が変更されました。製品の完全なドキュメントについては、[About Context API](https://docs.tealium.com/about-context-api/)をご覧ください。
</blockquote>


## 動作原理

Tealiumのモバイルライブラリは、以下の方法のいずれかを使用してReact Nativeアプリケーションに統合されます：

* NPMパッケージ（推奨）
* [GitHub](https://github.com/Tealium/tealium-react-native)を使用した手動インストール

Context APIモジュールをインストールした後、必要なクラスをアプリにインポートし、Context APIモジュールを初期化します。

## 要件

Tealium Context APIモジュールには以下が必要です：

* ネイティブビルド環境へのアクセス
* [Tealium for React Native 2.2.0以降](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63以降](https://github.com/Tealium/tealium-react-native)およびツール
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## インストール（NPM/YARN）

React Native用Tealium Context APIモジュールをNPMでインストールするには：

1. メインの`tealium-react-native`ライブラリの[インストール手順](https://docs.tealium.com/ja/platforms/react-native/install/)に従ってください。少なくともバージョン2.2.0以降をインストールしていることを確認してください。
1. React Nativeプロジェクトのルートディレクトリに移動します。
1. 次のコマンドで`tealium-react-native-moments-api`パッケージをダウンロードしてインストールします：
    ```bash
    yarn install tealium-react-native-moments-api
    ```

## JavaScript

アプリに関連するクラスをインポートするには、次のコードを追加します：

```javascript
import TealiumMomentsApi from 'tealium-react-native-moments-api';
import { TealiumMomentsApiConfig, MomentsApiRegion} from 'tealium-react-native-moments-api/common';
```

## 初期化

メインのTealium React Native統合を初期化する前に、Context APIモジュールを構成します。`TealiumMomentsApiConfig`パラメータを使用して必要に応じて構成を有効にします。

```javascript
let momentsApiConfig: TealiumMomentsApiConfig = {
    region: MomentsApiRegion.UsEast,   // 地域の構成は必須です。この構成がない場合、Context APIモジュールは初期化されません。
    referrer: "https://tealium.com"    // 任意 - リファラーURLを指定します。このURLはTealium UIの「ドメイン許可リスト」と一致する必要があります。そうでない場合、Context APIはデータを返しません。
}

TealiumMomentsApi.configure(momentsApiConfig);
```

## APIリファレンス

Context APIモジュールとメインのTealium React Native統合が両方とも初期化された後、IDによってエンジンデータを取得できます。

### `fetchEngineResponse(engineId, callback)`

指定されたエンジンIDのエンジン応答を取得します。

```javascript
TealiumMomentsApi.fetchEngineResponse(
    id,
    value => {
        console.log("Engine Response data: " + JSON.stringify(value))
    }
);
```