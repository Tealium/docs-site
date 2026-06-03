---
title: インストール
description: Flutter用Tealiumのインストール方法を学ぶ。
url: https://docs.tealium.com/ja/platforms/flutter-v1/install/
---これはFlutter用Tealiumの以前のバージョン（1.x）です。最新バージョンについては、[Flutter用Tealium](/ja/platforms/flutter/)を参照してください。

Flutter用Tealiumを使用すると、Flutterアプリケーションで[Android](/ja/platforms/android-java/)または[iOS](/ja/platforms/ios-swift/)のTealiumネイティブモバイルライブラリを使用できます。

## 要件

* [Flutter](https://flutter.dev/) アプリケーション開発フレームワーク
* [Android Studio](https://developer.android.com/studio) や [VS Code](https://code.visualstudio.com/) などのIDE
* IDEにインストールされたFlutterプラグイン

 Flutter用TealiumはFlutter Webアプリケーションと互換性がありません。Flutter Webアプリケーションを追跡するには、[JavaScript用Tealium](/ja/platforms/javascript/)を使用してください。

## インストール

Flutter用Tealiumライブラリをインストールするには：

1. Flutterアプリプロジェクトで、`pubspec.yaml`ファイルを更新して、以下のようにTealium Flutterプラグインの依存関係を追加します：
      ```yaml
      dependencies:
        flutter:
          sdk: flutter
        tealium: &#39;1.0.0&#39;
      ```

1. プロジェクトでTealium Flutterプラグインの依存関係を取り込むには、次のコマンドを実行します：
      ```bash
      flutter pub get
      ```

1. Dartコードをプロジェクトにインポートします：
      ```dart
      import &#39;package:tealium/tealium.dart&#39;;
      ```

FlutterプロジェクトでTealium APIを使用します。

## 初期化

次の例に示すように、[`initialize()`](/ja/platforms/flutter-v1/api/#initialize)メソッドでTealiumインスタンスを初期化します：

```dart
final teal = Tealium.initialize(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;, null, null);
```

次の例に示すように、[`initializeCustom()`](/ja/platforms/flutter-v1/api/#initializecustom)メソッドはすべての初期化オプションでTealiumインスタンスを初期化します：

```dart
final teal = Tealium.initializeCustom(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;, null, null,
      &#34;INSTANCE&#34;, true, null, null, null, true);
```

初期化オプションについて詳しくは、[Flutter API](/ja/platforms/flutter-v1/api/)を参照してください。