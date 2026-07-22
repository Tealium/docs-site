---
title: インストール
description: Flutter用Tealiumのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v2/install/
---
<blockquote>
これはFlutter用Tealiumの以前のバージョン（2.x）です。最新バージョンについては、[Flutter用Tealium](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


Flutter用Tealiumを使用すると、Flutterアプリケーションで[Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[iOS](https://docs.tealium.com/ja/platforms/ios-swift/)のTealiumネイティブモバイルライブラリを使用できます。

## 要件

* [Flutter](https://flutter.dev/) アプリケーション開発フレームワーク
* [Android Studio](https://developer.android.com/studio) や [VS Code](https://code.visualstudio.com/) などのIDE
* IDEにインストールされたFlutterプラグイン


<blockquote>
Flutter用TealiumはFlutter Webアプリケーションと互換性がありません。Flutter Webアプリケーションを追跡するには、[JavaScript用Tealium](https://docs.tealium.com/ja/platforms/javascript/)を使用してください。
</blockquote>


## サンプルアプリ

ライブラリ、追跡方法、およびベストプラクティスの実装に慣れるために、Flutter用Tealiumの[サンプルアプリ](https://github.com/Tealium/tealium-flutter/tree/master/tealium/example)を探索してください。

## インストール

Flutter用Tealiumライブラリをインストールするには：

1. Flutterアプリプロジェクトで、`pubspec.yaml`ファイルを更新して、次のようにTealium Flutterプラグインの依存関係を追加します：
      ```yaml
      dependencies:
        flutter:
          sdk: flutter
        tealium: '2.6.3'
      ```

1. プロジェクトでTealium Flutterプラグインの依存関係を取り込むには、次のコマンドを実行します：
      ```bash
      flutter pub get
      ```

1. Dartコードをプロジェクトにインポートします：
      ```dart
      import 'package:tealium/common.dart';
      import 'package:tealium/tealium.dart';
      ```

FlutterプロジェクトでTealium APIを使用します。

## 初期化

次の例に示すように、[`initialize()`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/#initialize)メソッドでTealiumインスタンスを初期化します：

```dart
final config = TealiumConfig(
    'ACCOUNT',
    'PROFILE',
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
    print('Tealium initialized');
});
```

初期化オプションについて詳しくは、[Flutter API](https://docs.tealium.com/ja/platforms/flutter-v2/api/)をご覧ください。