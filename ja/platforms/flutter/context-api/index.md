---
title: Context APIモジュール（現Context API）
description: Flutter向けTealium Context APIモジュールのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/flutter/context-api/
---

<blockquote>
Moments APIはContext APIに名称変更されました。製品ドキュメント全体については、[Context APIについて](https://docs.tealium.com/about-context-api/)を参照してください。
</blockquote>


Tealium for Flutterでは、Tealiumモバイルライブラリ（iOS、Android）を使用して、Tealium Flutterプラグイン用のContext APIモジュールをインストールできます。

## 仕組み

Tealiumモバイルライブラリは、次のいずれかの方法でFlutterアプリケーションに統合できます。

* Dartパッケージ（推奨）
* [GitHub](https://github.com/Tealium/tealium-flutter)を使用して手動で統合

## 要件

* [Flutter](https://flutter.dev/)アプリケーション開発フレームワーク
* [Android Studio](https://developer.android.com/studio)や[VS Code](https://code.visualstudio.com/)などのIDE
* IDEにインストールされたFlutter[プラグイン](https://github.com/flutter/plugins)

## インストール

Flutter用Tealiumライブラリをインストールするには、次の手順を実行します。

1. Flutterアプリプロジェクトで、次のコマンドを実行します。
    ```bash
    dart pub add tealium_moments_api
    ```
1. 次のDartコードをプロジェクトにインポートします。
    ```dart
    import 'package:tealium_moments_api/common.dart';
    import 'package:tealium_moments_api/tealium_moments_api.dart';
    ```

## 初期化

メインのTealium Flutter統合を初期化する前に、Context APIモジュールを構成します。

Context APIインターフェイスで指定されているContext APIリージョンを構成します。次のリージョンを使用できます。

* `GERMANY`
* `US_EAST`
* `SYDNEY`
* `OREGON`
* `TOKYO`
* `HONG_KONG`

[ドメイン許可リスト](https://docs.tealium.com/about-context-api/#domain-allow-list)を使用している場合は、リファラーを許可済みドメインに構成します。

次のサンプルコードでは、許可済みドメインと一致するように、`US_EAST`リージョンと`example.com`をリファラーとして使用しています。

```dart
MomentsApiConfig config = MomentsApiConfig(
    MomentsApiRegion.US_EAST,   // required
    "https://example.com");     // optional

// Configure the module
TealiumMomentsApi.configure(config);

// ... Initialize main Tealium plugin
```

## クラス：TealiumMomentsApi

Context APIモジュールとメインのTealium Flutter統合の両方を初期化した後、IDを指定してエンジンデータを取得できます。

### `fetchEngineResponse`

指定したエンジンIDのエンジンレスポンスを取得します。

```dart
TealiumMomentsApi.fetchEngineResponse(
    engineId: "ENGINEID",
    callback: (response) {
        if (response is EngineResponse) {
            // handle success
            final audiences = response.audiences;
            // do something
        } else if (response is String) {
            // handle error
        } 
    }
);
```

#### パラメータ

| パラメータ | 型 | 説明 |
| ---- | ---- | ---- |
| `engineId` | `String` | 確認するエンジンのID |
| `callback` | `Function(dynamic)` | 成功時に`EngineResponse`を、失敗時に`String`型のエラーメッセージを受け取るコールバック |

### `EngineResponse`

`EngineResponse`クラスには、Context APIエンジンから返された訪問データが含まれます。

| プロパティ | 型 | 説明 |
| ---- | ---- | ---- |
| `audiences` | `List<String>?` | 訪問が属するオーディエンスのID |
| `badges` | `List<String>?` | 訪問に割り当てられたバッジ |
| `strings` | `Map<String, String>?` | 文字列属性 |
| `booleans` | `Map<String, bool>?` | ブール属性 |
| `dates` | `Map<String, int>?` | 日付属性（タイムスタンプ形式） |
| `numbers` | `Map<String, double>?` | 数値属性 |