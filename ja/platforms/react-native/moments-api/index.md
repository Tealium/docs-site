---
title: Moments APIモジュール
description: React Native用のTealium Moments APIモジュールのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/react-native/moments-api/
---
## 仕組み

Tealiumのモバイルライブラリは、以下の方法のいずれかでReact Nativeアプリケーションに統合されます：

* NPMパッケージ（推奨）
* 手動で[GitHub](https://github.com/Tealium/tealium-react-native)経由

Moments APIモジュールをインストールした後、必要なクラスをアプリにインポートし、Moments APIモジュールを初期化します。

## 必要条件

Tealium Moments APIモジュールには以下が必要です：

* ネイティブビルド環境へのアクセス
* [Tealium for React Native 2.2.0以降](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63以降](https://github.com/Tealium/tealium-react-native)とツール
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## インストール（NPM/YARN）

React Native用のTealium Moments APIモジュールをNPMでインストールするには：

1. メインの`tealium-react-native`ライブラリのインストールについて[インストール手順](https://docs.tealium.com/ja/platforms/react-native/install/)を参照してください。バージョン2.2.0以降をインストールしていることを確認してください。
1. React Nativeプロジェクトのルートディレクトリに移動します。
1. 以下のコマンドで`tealium-react-native-moments-api`パッケージをダウンロードしてインストールします：  
    ```bash
    yarn install tealium-react-native-moments-api
    ```

## JavaScript

アプリに関連するクラスをインポートするには、以下のコードを追加します：

```javascript
import TealiumMomentsApi from 'tealium-react-native-moments-api';
import { TealiumMomentsApiConfig, MomentsApiRegion} from 'tealium-react-native-moments-api/common';
```

## 初期化

`Moments API`モジュールを、メインのTealium React Native統合を初期化する前に構成します。必要に応じて`TealiumMomentsApiConfig`パラメータを使用して構成を有効にします。

```javascript
let momentsApiConfig: TealiumMomentsApiConfig = {
    region: MomentsApiRegion.UsEast,   // 地域の構成は必須です。これがないとMoments APIモジュールは初期化されません。
    referrer: "https://tealium.com"    // 任意 - リファラーURLを指定します。このURLはTealium UIの“Domain Allow List”と一致しなければならず、一致しない場合、Moments APIはデータを返しません。
}

TealiumMomentsApi.configure(momentsApiConfig);
```

## APIリファレンス

Moments APIモジュールとメインのTealium React Native統合が両方とも初期化された後、IDによってエンジンデータを取得できます。

### `fetchEngineResponse(engineId, callback)`

指定されたエンジンIDのエンジンレスポンスを取得します。

```javascript
TealiumMomentsApi.fetchEngineResponse(
    id,
    value => {
        console.log("Engine Response data: " + JSON.stringify(value))
    }
);
```

