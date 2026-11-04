---
title: クラッシュレポーターモジュール
description: このドキュメントでは、React Native用Tealiumクラッシュレポーターモジュールのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/react-native/crash-reporter/
---
クラッシュレポーターモジュールは、アプリケーションのクラッシュを追跡するイベントを提供します。

## 仕組み

次のいずれかの方法を使用して、TealiumモバイルライブラリをReact Nativeアプリケーションに統合します。

* NPMパッケージ（推奨）
* [GitHub](https://github.com/Tealium/tealium-react-native)を使用して手動で統合

クラッシュレポーターモジュールの詳細については、[Android用クラッシュレポーターモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/crash-reporter/)または[iOS用クラッシュレポーターモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/crash-reporter/)を参照してください。

## 要件

* ネイティブビルド環境へのアクセス
* [Tealium for React Native v2.2.0以降](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63以降](https://github.com/Tealium/tealium-react-native)およびインストール済みのツール
* [モバイル用タグ管理プロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## インストール（NPM/YARN）

NPMを使用してReact Native用Tealiumクラッシュレポーターモジュールをインストールするには、次の手順を実行します。

1. [メインの`tealium-react-native`ライブラリのインストール手順](https://docs.tealium.com/ja/platforms/react-native/install/)に従います。バージョン2.2.0以降がインストールされていることを確認してください。

2. React Nativeプロジェクトのルートに移動します。

3. 次のコマンドを使用して、`tealium-react-native-crash-reporter`パッケージをダウンロードしてインストールします。  
    ```bash
    yarn install tealium-react-native-crash-reporter
    ```

## JavaScript

関連するクラスをアプリにインポートするには、次のようにします。

```javascript
import TealiumCrashReporter from 'tealium-react-native-crash-reporter';
```

## 初期化

メインのTealium React Native統合を初期化する前に、クラッシュレポーターモジュールを構成します。

Android：
```javascript
let truncateStack: boolean = true; // Android only. Optional param to specify whether or not to truncate stack trace, default is false

TealiumCrashReporter.initialize(truncateStack);
```

iOS：
```javascript
TealiumCrashReporter.initialize();
```