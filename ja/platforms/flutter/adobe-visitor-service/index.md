---
title: Adobe訪問サービスモジュール
description: このドキュメントでは、Flutter用Tealium Adobe訪問サービスモジュールのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/flutter/adobe-visitor-service/
---
Tealium for Flutterは、Tealiumモバイルライブラリ（iOS、Android）を使用して、Tealium Flutterプラグイン用のAdobe訪問サービスモジュールをインストールすることができます。

## 動作原理

Tealiumモバイルライブラリは、以下の方法のいずれかを使用してFlutterアプリケーションに統合されます：

*   Dartパッケージ（推奨）
*   [GitHub](https://github.com/Tealium/tealium-flutter)を使用して手動で

## 必要条件

* [Flutter](https://flutter.dev/) アプリケーション開発フレームワーク
* [Android Studio](https://developer.android.com/studio) や [VS Code](https://code.visualstudio.com/) などのIDE
* IDEにインストールされたFlutter [プラグイン](https://github.com/flutter/plugins)

## インストール

Flutter用Tealiumライブラリをインストールするには：

1. Flutterアプリプロジェクトで、以下を実行します
    ```bash
    dart pub add tealium_adobevisitor
    ```
2. Dartコードをプロジェクトにインポートします：
      ```dart
      import 'package:tealium_adobevisitor/common.dart';
      ```

## 初期化

メインのTealium Flutter統合を初期化する前に、Adobe訪問サービスモジュールを構成します。

```dart
final adobeVisitorConfig = AdobeVisitorConfig(
    "ADOBE-ORG-ID",
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: "EXISTING-ECID",  // オプション
);

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

`adobeVisitorCustomVisitorId`、`adobeVisitorDataProviderId`、`adobeVisitorAuthState`のプロパティは、アプリセッションの開始時にすべての値がわかっている場合にのみ構成します。`adobeVisitorAuthState`は、`adobeVisitorCustomVisitorId`を構成するときにのみ構成します。初期化時に訪問のIDが不明な場合（例えば、ログイン前など）、これらのプロパティを省略し、IDが利用可能になったら[`linkEcidToKnownIdentifier`](#linkecidtoknownidentifierknownid-adobedataproviderid-authstate)を呼び出します。

```dart
final adobeVisitorConfig = AdobeVisitorConfig(
    "ADOBE-ORG-ID",
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: "EXISTING-ECID",
    adobeVisitorDataProviderId: "DATA-PROVIDER-ID",
    adobeVisitorCustomVisitorId: "CUSTOM-VISITOR-ID",
    adobeVisitorAuthState: AuthState.authenticated,
);

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

## APIリファレンス

Adobe訪問サービスモジュールとメインのTealium Flutter統合が両方初期化された後、既存のAdobe訪問をリンクすることができます。

### `linkEcidToKnownIdentifier(knownId, adobeDataProviderId, authState)`

既存のExperience Cloud ID（ECID）を既知の識別子にリンクします。

```dart
final visitor = await TealiumAdobeVisitor.linkEcidToKnownIdentifier("myidentifier", "123456", AuthState.unknown);
```

### `getAdobeVisitor()`

現在のAdobe訪問情報を取得します。

```dart
TealiumAdobeVisitor.getAdobeVisitor()
        .then((visitor) => print(visitor));
```

### `decorateUrl(url)`

URLをECID訪問データで装飾します。

```dart
String? decoratedUrl = await TealiumAdobeVisitor.decorateUrl("https://example.com");
```

### `getUrlParameters()`

Adobe訪問IDを含むURLパラメータを取得し、手動でURLに追加します。

```dart
TealiumAdobeVisitor.getUrlParameters().then(
                            (value) =>
                            value?.forEach((key, value) {
                                print("Retrieved URL Parameters: $key = $value");
                            })
                    );
```

### `resetVisitor()`

現在の訪問をリセットします。

```dart
TealiumAdobeVisitor.resetVisitor();
```