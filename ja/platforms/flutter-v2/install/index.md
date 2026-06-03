---
title: インストール
description: Flutter用Tealiumのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v2/install/
---これはFlutter用Tealiumの以前のバージョン（2.x）です。最新バージョンについては、[Flutter用Tealium](/ja/platforms/flutter/)をご覧ください。

Flutter用Tealiumを使用すると、Flutterアプリケーションで[Android](/ja/platforms/android-kotlin/)または[iOS](/ja/platforms/ios-swift/)のTealiumネイティブモバイルライブラリを使用できます。

## 要件

* [Flutter](https://flutter.dev/) アプリケーション開発フレームワーク
* [Android Studio](https://developer.android.com/studio) や [VS Code](https://code.visualstudio.com/) などのIDE
* IDEにインストールされたFlutterプラグイン

 Flutter用TealiumはFlutter Webアプリケーションと互換性がありません。Flutter Webアプリケーションを追跡するには、[JavaScript用Tealium](/ja/platforms/javascript/)を使用してください。

## サンプルアプリ

ライブラリ、追跡方法、およびベストプラクティスの実装に慣れるために、Flutter用Tealiumの[サンプルアプリ](https://github.com/Tealium/tealium-flutter/tree/master/tealium/example)を探索してください。

## インストール

Flutter用Tealiumライブラリをインストールするには：

1. Flutterアプリプロジェクトで、`pubspec.yaml`ファイルを更新して、次のようにTealium Flutterプラグインの依存関係を追加します：
      ```yaml
      dependencies:
        flutter:
          sdk: flutter
        tealium: &#39;2.6.3&#39;
      ```

1. プロジェクトでTealium Flutterプラグインの依存関係を取り込むには、次のコマンドを実行します：
      ```bash
      flutter pub get
      ```

1. Dartコードをプロジェクトにインポートします：
      ```dart
      import &#39;package:tealium/common.dart&#39;;
      import &#39;package:tealium/tealium.dart&#39;;
      ```

FlutterプロジェクトでTealium APIを使用します。

## 初期化

次の例に示すように、[`initialize()`](/ja/platforms/flutter-v2/api/tealium/#initialize)メソッドでTealiumインスタンスを初期化します：

```dart
final config = TealiumConfig(
    &#39;ACCOUNT&#39;,
    &#39;PROFILE&#39;,
    TealiumEnvironment.dev,
    [Collectors.AppData, Collectors.Lifecycle],
    [Dispatchers.RemoteCommands, Dispatchers.TagManagement],
    consentPolicy: ConsentPolicy.GDPR,
    useRemoteLibrarySettings: true,
    batchingEnabled: false,
    visitorServiceEnabled: true,
    consentExpiry: ConsentExpiry(5, TimeUnit.MINUTES)
);

Tealium.initialize(config).then((value) {
    print(&#39;Tealium initialized&#39;);
});
```

初期化オプションについて詳しくは、[Flutter API](/ja/platforms/flutter-v2/api/)をご覧ください。