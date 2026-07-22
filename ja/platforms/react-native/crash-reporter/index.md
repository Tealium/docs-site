---
title: クラッシュレポーターモジュール
description: このドキュメントでは、React Native用のTealiumクラッシュレポーターモジュールのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/react-native/crash-reporter/
---
クラッシュレポーターモジュールは、アプリケーションのクラッシュ追跡イベントを提供します。

## 仕組み

以下の2つの方法のいずれかを使用して、TealiumのモバイルライブラリをReact Nativeアプリケーションに統合します：

* NPMパッケージ（推奨）
* 手動で[GitHub](https://github.com/Tealium/tealium-react-native)経由

クラッシュレポーターモジュールについての詳細は、[Android用クラッシュレポーターモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/crash-reporter/)または[iOS用クラッシュレポーターモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/crash-reporter/)を参照してください。

## 必要条件

* ネイティブビルド環境へのアクセス
* [Tealium for React Native v2.2.0+](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63+](https://github.com/Tealium/tealium-react-native)とツールがインストールされていること。
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## インストール (NPM/YARN)

React Native用のTealiumクラッシュレポーターモジュールをNPMでインストールするには：

1. [メインの`tealium-react-native`ライブラリのインストール手順](https://docs.tealium.com/ja/platforms/react-native/install/)に従います。少なくともバージョン2.2.0以上をインストールしていることを確認してください。

2. React Nativeプロジェクトのルートに移動します。

3. 次のコマンドで`tealium-react-native-crash-reporter`パッケージをダウンロードしてインストールします：  
    ```bash
    yarn install tealium-react-native-crash-reporter
    ```

## JavaScript

アプリに関連するクラスをインポートするには、次のようにします：

```javascript
import TealiumCrashReporter from 'tealium-react-native-crash-reporter';
```

## 初期化

メインのTealium React Native統合を初期化する前に、クラッシュレポーターモジュールを構成します：

Android:
```javascript
let truncateStack: boolean = true; // Androidのみ。スタックトレースを切り捨てるかどうかを指定するオプションのパラメータ、デフォルトはfalseです

TealiumCrashReporter.initialize(truncateStack);
```

iOS:
```javascript
TealiumCrashReporter.initialize();
```


