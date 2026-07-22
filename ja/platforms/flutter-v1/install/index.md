---
title: インストール
description: Flutter用Tealiumのインストール方法を学ぶ。
url: https://docs.tealium.com/ja/platforms/flutter-v1/install/
---
<blockquote>
これはFlutter用Tealiumの以前のバージョン（1.x）です。最新バージョンについては、[Flutter用Tealium](https://docs.tealium.com/ja/platforms/flutter/)を参照してください。
</blockquote>


Flutter用Tealiumを使用すると、Flutterアプリケーションで[Android](https://docs.tealium.com/ja/platforms/android-java/)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/)のTealiumネイティブモバイルライブラリを使用できます。

## 要件

* [Flutter](https://flutter.dev/) アプリケーション開発フレームワーク
* [Android Studio](https://developer.android.com/studio) や [VS Code](https://code.visualstudio.com/) などのIDE
* IDEにインストールされたFlutterプラグイン


<blockquote>
Flutter用TealiumはFlutter Webアプリケーションと互換性がありません。Flutter Webアプリケーションを追跡するには、[JavaScript用Tealium](https://docs.tealium.com/ja/platforms/javascript/)を使用してください。
</blockquote>


## インストール

Flutter用Tealiumライブラリをインストールするには：

1. Flutterアプリプロジェクトで、`pubspec.yaml`ファイルを更新して、以下のようにTealium Flutterプラグインの依存関係を追加します：
      ```yaml
      dependencies:
        flutter:
          sdk: flutter
        tealium: '1.0.0'
      ```

1. プロジェクトでTealium Flutterプラグインの依存関係を取り込むには、次のコマンドを実行します：
      ```bash
      flutter pub get
      ```

1. Dartコードをプロジェクトにインポートします：
      ```dart
      import 'package:tealium/tealium.dart';
      ```

FlutterプロジェクトでTealium APIを使用します。

## 初期化

次の例に示すように、[`initialize()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#initialize)メソッドでTealiumインスタンスを初期化します：

```dart
final teal = Tealium.initialize("ACCOUNT", "PROFILE", "ENVIRONMENT", null, null);
```

次の例に示すように、[`initializeCustom()`](https://docs.tealium.com/ja/platforms/flutter-v1/api/#initializecustom)メソッドはすべての初期化オプションでTealiumインスタンスを初期化します：

```dart
final teal = Tealium.initializeCustom("ACCOUNT", "PROFILE", "ENVIRONMENT", null, null,
      "INSTANCE", true, null, null, null, true);
```

初期化オプションについて詳しくは、[Flutter API](https://docs.tealium.com/ja/platforms/flutter-v1/api/)を参照してください。