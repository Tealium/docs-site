---
title: Adobe Visitor Serviceモジュール
description: React Native向けTealium Adobe Visitor Serviceモジュールのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/react-native/adobe-visitor-service/
---
Tealium for React Nativeを使用すると、React NativeアプリケーションでTealiumモバイルライブラリ（iOS、Android）を利用できます。

## 仕組み

Tealiumモバイルライブラリは、次のいずれかの方法でReact Nativeアプリケーションに統合できます。

*   NPMパッケージ（推奨）
*   [GitHub](https://github.com/Tealium/tealium-react-native)を使用した手動インストール

## 要件

* ネイティブビルド環境へのアクセス
* [Tealium for React Native 2.2.0以降](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63以降](https://github.com/Tealium/tealium-react-native)および必要なツールのインストール
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/)または[Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/)または[Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)


## インストール（NPM/YARN）

NPMを使用してReact Native向けTealium Adobe Visitorモジュールをインストールするには、次の手順を実行します。

1. メインの`tealium-react-native`ライブラリについて、[こちら](https://docs.tealium.com/ja/platforms/react-native/install/)のインストール手順に従います。バージョン2.2.0以降がインストールされていることを確認してください。

2. React Nativeプロジェクトのルートディレクトリに移動します。

3. 次のコマンドを使用して、`tealium-react-native-adobe-visitor`パッケージをダウンロードしてインストールします。  
    ```bash
    yarn install tealium-react-native-adobe-visitor
    ```


## JavaScript

関連するクラスをアプリにインポートするには、次のようにします。

```javascript
import TealiumAdobeVisitor from 'tealium-react-native-adobe-visitor';
import { TealiumAdobeVisitorConfig } from 'tealium-react-native-adobe-visitor/common';
```

## 初期化

メインのTealium React Native統合を初期化する前に、Adobe Visitorモジュールを構成します。

```javascript
let adobeVisitorConfig: TealiumAdobeVisitorConfig = {
    adobeVisitorOrgId: "ADOBE-ORG-ID",
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: "",  // optional
}

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

`adobeVisitorCustomVisitorId`、`adobeVisitorDataProviderId`、`adobeVisitorAuthState`プロパティは、アプリセッションの開始時に3つすべての値が判明している場合にのみ構成してください。`adobeVisitorAuthState`は、`adobeVisitorCustomVisitorId`も構成する場合にのみ構成します。初期化時に訪問IDが不明な場合（ログイン前など）は、これらのプロパティを省略し、IDが利用可能になった時点で[`linkEcidToKnownIdentifier`](#linkecidtoknownidentifierid-providerid-authstate-callback)を呼び出します。

```javascript
let adobeVisitorConfig: TealiumAdobeVisitorConfig = {
    adobeVisitorOrgId: "ADOBE-ORG-ID",
    adobeVisitorRetries: 1,
    adobeVisitorExistingEcid: "",
    adobeVisitorDataProviderId: "DATA-PROVIDER-ID",
    adobeVisitorCustomVisitorId: "CUSTOM-VISITOR-ID",
    adobeVisitorAuthState: AuthState.authenticated
}

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

## APIリファレンス

Adobe VisitorモジュールとメインのTealium React Native統合の両方を初期化した後、既存のAdobe訪問をリンクできます。

### `linkEcidToKnownIdentifier(id, providerId, authState, callback)`

既存のECIDを既知の識別子にリンクします。

```javascript
TealiumAdobeVisitor.linkEcidToKnownIdentifier(id, providerId, authState, value => {
    console.log("AdobeVisitor Data: " + JSON.stringify(value))
});
```

### `getAdobeVisitor(callback)`

現在のAdobe訪問情報を取得します。

```javascript
TealiumAdobeVisitor.getAdobeVisitor(value => {
    console.log("Current Adobe Visitor: " + JSON.stringify(value))
});
```

### `decorateUrl(url, callback)`

ECID訪問データをURLにエンリッチメントします。

```javascript
TealiumAdobeVisitor.decorateUrl(("https://tealium.com", value => {
    console.log("Decorated URL: " + value);
});
```

### `getUrlParameters(callback)`

URLに追加するAdobe VisitorのURLパラメータを取得します。

```javascript
TealiumAdobeVisitor.getUrlParameters(value => {
    if (value === null || value === undefined) {
        console.log("Adobe Visitor was null");
        return;
    } else {
        for (var key of Object.keys(value)) {
            // Result: key = adobe_mc
            //         value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
            // Only for demonstration purposes; call some method in your app that decorates the URL and then launches your webview
            console.log("Retrieved URL Parameters: ", key + "=" + value[key]);
            break;
        }
    }
});
```

### `resetVisitor()`

現在の訪問をリセットします。

```javascript
TealiumAdobeVisitor.resetVisitor();
```