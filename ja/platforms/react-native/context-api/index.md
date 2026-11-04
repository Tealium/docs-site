---
title: Context APIモジュール（現Context API）
description: React Native用Tealium Context APIモジュールのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/react-native/context-api/
---

<blockquote>
Moments APIはContext APIに名称変更されました。製品ドキュメントの全文については、[Context APIについて](https://docs.tealium.com/about-context-api/)を参照してください。
</blockquote>


## 仕組み

Tealiumモバイルライブラリは、次のいずれかの方法を使用してReact Nativeアプリケーションに統合します。

* NPMパッケージ（推奨）
* [GitHub](https://github.com/Tealium/tealium-react-native)を使用して手動で統合

Context APIモジュールをインストールした後、必要なクラスをアプリにインポートし、Context APIモジュールを初期化します。

## 要件

Tealium Context APIモジュールには、以下が必要です。

* ネイティブビルド環境へのアクセス
* [Tealium for React Native 2.2.0以降](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63以降](https://github.com/Tealium/tealium-react-native)および関連ツール
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## インストール（NPM/YARN）

NPMを使用してReact Native用Tealium Context APIモジュールをインストールするには、次の手順を実行します。

1. メインの`tealium-react-native`ライブラリをインストールするための[インストール手順](https://docs.tealium.com/ja/platforms/react-native/install/)に従います。バージョン2.2.0以降がインストールされていることを確認してください。
1. React Nativeプロジェクトのルートディレクトリに移動します。
1. 次のコマンドを使用して、`tealium-react-native-moments-api`パッケージをダウンロードしてインストールします。  
    ```bash
    yarn install tealium-react-native-moments-api
    ```

## JavaScript

関連するクラスをアプリにインポートするには、次のコードを追加します。

```javascript
import TealiumMomentsApi from 'tealium-react-native-moments-api';
import { TealiumMomentsApiConfig, MomentsApiRegion} from 'tealium-react-native-moments-api/common';
```

## 初期化

メインのTealium React Native統合を初期化する前に、Context APIモジュールを構成します。必要に応じて、`TealiumMomentsApiConfig`パラメータを使用して各構成を有効にします。

```javascript
let momentsApiConfig: TealiumMomentsApiConfig = {
    region: MomentsApiRegion.UsEast,   // Setting a region is mandatory. The Context API module will not initialize if it is missing.
    referrer: "https://tealium.com"    // Optional - specify a referrer URL. This URL must match the "Domain Allow List" in the Tealium UI, or the Context API will not return any data.
}

TealiumMomentsApi.configure(momentsApiConfig);
```

## APIリファレンス

Context APIモジュールとメインのTealium React Native統合の両方を初期化した後、IDを使用してエンジンデータを取得できます。

### `fetchEngineResponse(engineId, callback)`

指定されたエンジンIDに対応するエンジンレスポンスを取得します。

```javascript
TealiumMomentsApi.fetchEngineResponse(
    id,
    value => {
        console.log("Engine Response data: " + JSON.stringify(value))
    }
);
```