---
title: Adobe Visitor Serviceモジュール
description: React Native用Tealium Adobe Visitor Serviceモジュールのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/react-native/adobe-visitor-service/
---
Tealium for React Nativeは、React NativeアプリケーションでTealiumのモバイルライブラリ（iOS、Android）を使用できます。

## 動作原理

Tealiumのモバイルライブラリは、以下の2つの方法のいずれかを使用してReact Nativeアプリケーションに統合されます：

*   NPMパッケージ（推奨）
*   [GitHub](https://github.com/Tealium/tealium-react-native)を使用して手動で

## 要件

* ネイティブビルド環境へのアクセス
* [Tealium for React Native 2.2.0+](https://docs.tealium.com/ja/platforms/react-native/)
* [React Native 0.63+](https://github.com/Tealium/tealium-react-native) およびツールがインストールされていること
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Android Studio](https://developer.android.com/studio/) または [Xcode](https://developer.apple.com/xcode/)
* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-kotlin/) または [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## インストール（NPM/YARN）

React Native用Tealium Adobe VisitorモジュールをNPMでインストールするには：

1. こちらの[メイン `tealium-react-native` ライブラリのインストール手順](https://docs.tealium.com/ja/platforms/react-native/install/)に従ってください。少なくともバージョン2.2.0以上をインストールしていることを確認してください。

2. React Nativeプロジェクトのルートに移動します。

3. 次のコマンドで `tealium-react-native-adobe-visitor` パッケージをダウンロードしてインストールします：
    ```bash
    yarn install tealium-react-native-adobe-visitor
    ```

## JavaScript

アプリに関連するクラスをインポートするには、次のようにします：

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
    adobeVisitorExistingEcid: "",  // オプション
}

TealiumAdobeVisitor.configure(adobeVisitorConfig);
```

アプリセッションの開始時にすべての値がわかっている場合のみ、`adobeVisitorCustomVisitorId`、`adobeVisitorDataProviderId`、`adobeVisitorAuthState`プロパティを構成します。`adobeVisitorAuthState`は、`adobeVisitorCustomVisitorId`を構成するときにのみ構成します。初期化時に訪問のIDが不明な場合（例えば、ログイン前など）、これらのプロパティを省略し、IDが利用可能になったら[`linkEcidToKnownIdentifier`](#linkecidtoknownidentifierid-providerid-authstate-callback)を呼び出します。

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

Adobe VisitorモジュールとメインのTealium React Native統合が両方初期化された後、既存のAdobe訪問をリンクできます。

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

URLをECID訪問データで装飾します。

```javascript
TealiumAdobeVisitor.decorateUrl(("https://tealium.com", value => {
    console.log("Decorated URL: " + value);
});
```

### `getUrlParameters(callback)`

URLに追加するためのAdobe訪問URLパラメータを取得します。

```javascript
TealiumAdobeVisitor.getUrlParameters(value => {
    if (value === null || value === undefined) {
        console.log("Adobe Visitor was null");
        return;
    } else {
        for (var key of Object.keys(value)) {
            // 結果: key = adobe_mc
            //         value = MCMID=1234|MCORGID=12345@AdobeOrg|TS=1655826247
            // デモンストレーション目的のみ; アプリでURLを装飾してからウェブビューを起動するメソッドを呼び出します
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