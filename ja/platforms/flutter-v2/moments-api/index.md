---
title: Moments APIモジュール
description: Flutter用Tealium Moments APIモジュールのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/flutter-v2/moments-api/
---
<blockquote>
これはTealium for Flutterの以前のバージョン（2.x）です。最新バージョンについては、[Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


Tealium for Flutterを使用すると、Tealiumモバイルライブラリ（iOS、Android）を利用してTealium FlutterプラグインのMoments APIモジュールをインストールできます。

## 動作原理

以下の方法のいずれかを使用して、TealiumモバイルライブラリをFlutterアプリケーションに統合できます：

* Dartパッケージ（推奨）
* [GitHub](https://github.com/Tealium/tealium-flutter)を使用して手動で

## 必要条件

* [Flutter](https://flutter.dev/) アプリケーション開発フレームワーク
* [Android Studio](https://developer.android.com/studio) や [VS Code](https://code.visualstudio.com/) などのIDE
* IDEにインストールされたFlutter [プラグイン](https://github.com/flutter/plugins)

## インストール

Flutter用Tealiumライブラリをインストールするには：

1. Flutterアプリプロジェクトで、以下のコマンドを実行します：
    ```bash
    dart pub add tealium_moments_api
    ```
1. 次のDartコードをプロジェクトにインポートします：
    ```dart
    import 'package:tealium_moments_api/common.dart';
    import 'package:tealium_moments_api/tealium_moments_api.dart';
    ```

## 初期化

メインのTealium Flutter統合を初期化する前に、Moments APIモジュールを構成します。

Moments APIインターフェースで指定されたMoments APIリージョンを構成します。利用可能なリージョンは以下の通りです：

* `GERMANY`
* `US_EAST`
* `SYDNEY`
* `OREGON`
* `TOKYO`
* `HONG_KONG`

[ドメイン許可リスト](https://docs.tealium.com/about-moments-api/#domain-allow-list)を使用している場合、リファラーを許可されたドメインに構成します。

次の例のコードは、`US_EAST`リージョンと`example.com`をリファラーとして使用し、許可されたドメインと一致させます：

```dart
final config = MomentsApiConfig(
    MomentsApiRegion.US_EAST,   // 必須
    "https://example.com");     // オプション

// モジュールを構成
TealiumMomentsApi.configure(config);

// ... メインTealiumプラグインを初期化
```

## クラス: TealiumMomentsApi

Moments APIモジュールとメインのTealium Flutter統合が初期化された後、IDによってエンジンデータを取得できます。

### `fetchEngineResponse`

指定されたエンジンIDのエンジンレスポンスを取得します。

```dart
TealiumMomentsApi.fetchEngineResponse(
    engineId: "ENGINEID",
    callback: (response) {
        if (response is EngineResponse) {
            // 成功を処理
            final audiences = response.audiences;
            // 何かをする
        } else if (response is String) {
            // エラーを処理
        }
    }
);
```

#### パラメータ

| パラメータ | タイプ | 説明 |
| ---- | ---- | ---- |
| `engineId` | `String` | チェックするエンジンのID |
| `callback` | `Function(dynamic)` | 成功時に`EngineResponse`を受け取るコールバック、または失敗時に`String`エラーメッセージを受け取るコールバック |

### `EngineResponse`

`EngineResponse`クラスは、Moments APIエンジンから返された訪問データを含みます。

| プロパティ | タイプ | 説明 |
| ---- | ---- | ---- |
| `audiences` | `List<String>?` | 訪問が属するオーディエンスID |
| `badges` | `List<String>?` | 訪問に割り当てられたバッジ |
| `strings` | `Map<String, String>?` | 文字列属性 |
| `booleans` | `Map<String, bool>?` | ブール属性 |
| `dates` | `Map<String, int>?` | 日付属性（タイムスタンプとして） |
| `numbers` | `Map<String, double>?` | 数値属性 |