---
title: インストール
description: Tealium for Node.jsのインストールについて説明します。
url: https://docs.tealium.com/ja/platforms/node/install/
---Node.js用の`tealium-collect`モジュールでは、イベントデータが[Tealium HTTP API](https://docs.tealium.com/ja/platforms/http-api/)経由でTealium Customer Data Hubに送信されます。このモジュールは、[サーバーサイド](https://docs.tealium.com/ja/server-side/)アプリケーションやブラウザで使用します。

## 要件

* [ealium Customer Data Hubアカウント

## インストール

Node.js向けTealium CollectモジュールをNPMによってインストールするには、次のコマンドを実行します。
```bash
npm install tealium-collect
```
インストールの際には、依存関係モジュールの`tealium`が自動的にインクルードされます。

## 初期化

1. モジュールをインポートします。
```javascript
var Tealium = require('tealium');
var tealiumCollect = require('tealium-collect');
```

2. `Tealium`インスタンスを[`Tealium()`](https://docs.tealium.com/ja/platforms/node/api/#tealium)コンストラクタメソッドで初期化します。
```javascript
var config = {
      "account"    : "ACCOUNT",
      "profile"    : "PROFILE",
      "datasource" : "DATASOURCE"
};
var tealium = Tealium(config);
```

3. [`addModule()`](https://docs.tealium.com/ja/platforms/node/api/#addmodule)メソッドを呼び出してTealium Collectモジュールを追加します。
```javascript
tealium.addModule(tealiumCollect);
```

