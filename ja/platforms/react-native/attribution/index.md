---
title: アトリビューションモジュール
description: React Native向けTealiumアトリビューションモジュールのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/react-native/attribution/
---
Tealium for React Nativeを使用すると、React NativeアプリケーションでTealiumモバイルライブラリ（iOS、Android）を利用できます。

## 仕組み

Tealiumモバイルライブラリは、次のいずれかの方法でReact Nativeアプリケーションに統合します。

* NPMパッケージ（推奨）
* [GitHub](https://github.com/Tealium/tealium-react-native)を使用して手動で統合

## 要件

* ネイティブビルド環境へのアクセス
* [Tealium for React Native 2.2.0以降](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63以降](https://github.com/Tealium/tealium-react-native)および必要なツールがインストールされていること
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## インストール（NPM/YARN）

NPMを使用してReact Native向けTealiumアトリビューションモジュールをインストールするには、次の手順を実行します。

1. メインの`tealium-react-native`ライブラリについて、[インストール手順](https://docs.tealium.com/ja/platforms/react-native/install/)に従います。バージョン2.2.0以降がインストールされていることを確認してください。
1. React Nativeプロジェクトのルートディレクトリに移動します。
1. 次のコマンドを使用して、`tealium-react-native-attribution`パッケージをダウンロードしてインストールします。  
    ```bash
    yarn install tealium-react-native-attribution
    ```

## JavaScript

関連するクラスをアプリにインポートするには、次のコードを追加します。

```javascript
import TealiumAttribution from 'tealium-react-native-attribution';
import { TealiumAttributionConfig } from 'tealium-react-native-attribution/common';
```

## 初期化

メインのTealium React Native統合を初期化する前に、`Attribution`モジュールを構成します。この統合では、Tealium Swift Attribution Moduleに加えて、Tealium Kotlin Install ReferrerおよびAd Identifierを必要に応じて有効化できます。必要に応じて構成を有効にするには、`TealiumAttributionConfig`パラメータを使用します。

```javascript
let attributionConfig: TealiumAttributionConfig = {
    androidInstallReferrerEnabled: true,
    androidAdIdentifierEnabled: true,
    iosSearchAdsEnabled: true,
    iosSkAdAttributionEnabled: true,
    iosSkAdConversionKeys: {"event": "conversion_value"}
}

TealiumAttribution.configure(attributionConfig);
```

## APIリファレンス

アトリビューションモジュールとメインのTealium React Native統合の両方を初期化した後、必要に応じて広告データを消去できます。

### `removeAdInfo()`

Tealium Android Ad Identifierモジュールに関連する値を消去し、データレイヤーから広告情報を削除します（Androidのみ）。

```javascript
TealiumAttribution.removeAdInfo();
```

### `removeAppSetIdInfo()`

Tealium Android AdIdentifierモジュールに関連する値を消去し、データレイヤーからアプリセットIDを削除します（Androidのみ）。

```javascript
TealiumAttribution.removeAppSetIdInfo();
```