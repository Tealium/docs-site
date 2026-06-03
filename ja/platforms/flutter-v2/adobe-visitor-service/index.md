---
title: Adobe訪問サービスモジュール
description: このドキュメントでは、Flutter用Tealium Adobe訪問サービスモジュールのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/flutter-v2/adobe-visitor-service/
---これはTealium for Flutterの以前のバージョン（2.x）です。最新バージョンについては、[Tealium for Flutter](/ja/platforms/flutter/)を参照してください。

Tealium for Flutterを使用すると、Tealiumモバイルライブラリ（iOS、Android）を使用してTealium FlutterプラグインのAdobe訪問サービスモジュールをインストールできます。

## 動作原理

Tealiumモバイルライブラリは、以下の方法のいずれかを使用してFlutterアプリケーションに統合されます：

*   Dartパッケージ（推奨）
*   [GitHub](https://github.com/Tealium/tealium-flutter)を使用した手動

## 要件

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
      import &#39;package:tealium_adobevisitor/common.dart&#39;;
      ```

## 初期化

Tealium Flutter統合の初期化前に、Adobe訪問サービスモジュールを構成します。

```dart
final adobeVisitorConfig = AdobeVisitorConfig(
    &#34;ADOBE-ORG-ID&#34;,
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: &#34;EXISTING-ECID&#34;,  // オプション
);

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

`adobeVisitorCustomVisitorId`、`adobeVisitorDataProviderId`、`adobeVisitorAuthState`のプロパティは、アプリセッションの開始時にすべての値がわかっている場合にのみ構成します。`adobeVisitorAuthState`は、`adobeVisitorCustomVisitorId`を構成するときにのみ構成します。初期化時に訪問のIDが不明な場合（例えば、ログイン前など）、これらのプロパティを省略し、IDが利用可能になったら[`linkEcidToKnownIdentifier`](#linkecidtoknownidentifierknownid-adobedataproviderid-authstate)を呼び出します。

```dart
final adobeVisitorConfig = AdobeVisitorConfig(
    &#34;ADOBE-ORG-ID&#34;,
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: &#34;EXISTING-ECID&#34;,
    adobeVisitorDataProviderId: &#34;DATA-PROVIDER-ID&#34;,
    adobeVisitorCustomVisitorId: &#34;CUSTOM-VISITOR-ID&#34;,
    adobeVisitorAuthState: AuthState.authenticated,
);

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

## APIリファレンス

Adobe訪問サービスモジュールとTealium Flutter統合の両方が初期化された後、既存のAdobe訪問をリンクできます。

### `linkEcidToKnownIdentifier(knownId, adobeDataProviderId, authState)`

既存のExperience Cloud ID（ECID）を既知の識別子にリンクします。

```dart
final visitor = await TealiumAdobeVisitor.linkEcidToKnownIdentifier(&#34;myidentifier&#34;, &#34;123456&#34;, AuthState.unknown);
```

### `getAdobeVisitor()`

現在のAdobe訪問情報を取得します。

```dart
TealiumAdobeVisitor.getAdobeVisitor()
        .then((visitor) =&gt; print(visitor));
```

### `decorateUrl(url)`

URLをECID訪問データで装飾します。

```dart
String? decoratedUrl = await TealiumAdobeVisitor.decorateUrl(&#34;https://example.com&#34;);
```

### `getUrlParameters()`

Adobe訪問IDを含むURLパラメータを取得し、手動でURLに追加します。

```dart
TealiumAdobeVisitor.getUrlParameters().then(
                            (value) =&gt;
                            value?.forEach((key, value) {
                                print(&#34;Retrieved URL Parameters: $key = $value&#34;);
                            })
                    );
```

### `resetVisitor()`

現在の訪問をリセットします。

```dart
TealiumAdobeVisitor.resetVisitor();
```