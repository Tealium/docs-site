---
title: アトリビューションモジュール
description: React Native用のTealiumアトリビューションモジュールのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/react-native/attribution/
---
Tealium for React Nativeは、React NativeアプリケーションでTealiumのモバイルライブラリ（iOS、Android）を使用することを可能にします。

## 仕組み

Tealiumのモバイルライブラリは、以下の2つの方法のいずれかを使用してReact Nativeアプリケーションに統合されます：

* NPMパッケージ（推奨）
* 手動で[GitHub](https://github.com/Tealium/tealium-react-native)経由

## 必要条件

* ネイティブビルド環境へのアクセス
* [Tealium for React Native 2.2.0以降](/ja/platforms/react-native/)
* [React Native 0.63以降](https://github.com/Tealium/tealium-react-native)とツールのインストール
* [Tealium iQ Mobile Profile]()
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](/ja/platforms/android-kotlin/)または[Tealium for iOS](/ja/platforms/ios-swift/)

## インストール（NPM/YARN）

React Native用のTealiumアトリビューションモジュールをNPMでインストールするには：

1. メインの`tealium-react-native`ライブラリの[インストール手順](/ja/platforms/react-native/install/)に従います。バージョン2.2.0以降をインストールしたことを確認してください。
1. React Nativeプロジェクトのルートディレクトリに移動します。
1. 次のコマンドで`tealium-react-native-attribution`パッケージをダウンロードしてインストールします：  
    ```bash
    yarn install tealium-react-native-attribution
    ```

## JavaScript

アプリに関連するクラスをインポートするには、次のコードを追加します：

```javascript
import TealiumAttribution from &#39;tealium-react-native-attribution&#39;;
import { TealiumAttributionConfig } from &#39;tealium-react-native-attribution/common&#39;;
```

## 初期化

メインのTealium React Native統合を初期化する前に、`Attribution`モジュールを構成します。この統合では、Tealium Swift Attribution Module、Tealium Kotlin Install Referrer、Ad Identifierをオプションで有効にすることができます。`TealiumAttributionConfig`パラメータを使用して、必要に応じて構成を有効にします。

```javascript
let attributionConfig: TealiumAttributionConfig = {
    androidInstallReferrerEnabled: true,
    androidAdIdentifierEnabled: true,
    iosSearchAdsEnabled: true,
    iosSkAdAttributionEnabled: true,
    iosSkAdConversionKeys: {&#34;event&#34;: &#34;conversion_value&#34;}
}

TealiumAttribution.configure(attributionConfig);
```

## APIリファレンス

Attribution ModuleとメインのTealium React Native統合が両方とも初期化された後、広告データをオプションでクリアすることができます。

### `removeAdInfo()`

Tealium Android Ad Identifierモジュールに関連するデータレイヤーから広告情報を削除し、値をクリアします（Androidのみ）。

```javascript
TealiumAttribution.removeAdInfo();
```

### `removeAppSetIdInfo()`

Tealium Android AdIdentifierモジュールに関連するデータレイヤーからアプリセットIDを削除し、値をクリアします（Androidのみ）。

```javascript
TealiumAttribution.removeAppSetIdInfo();
```


