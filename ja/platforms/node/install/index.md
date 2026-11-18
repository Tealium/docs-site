---
title: インストール
description: Node.js向けTealiumのインストール方法
url: https://docs.tealium.com/ja/platforms/node/install/
---Node.js向けの`tealium-collect`モジュールは、[Tealium HTTP API](https://docs.tealium.com/ja/platforms/http-api/)を通じてイベントデータをTealium Customer Data Hubに送信します。このモジュールは、サーバーサイドアプリケーションまたはブラウザーで使用できます。

## 要件

* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## インストール

NPMを使用してNode.js向けTealium Collectモジュールをインストールするには、次のコマンドを実行します。  
```bash
npm install tealium-collect
```
インストール時に、依存モジュール`tealium`も自動的に含まれます。

## 初期化

1. モジュールをインポートします。  
      ```javascript
      var Tealium = require('tealium');
      var tealiumCollect = require('tealium-collect');
      ```

2. [`Tealium()`](https://docs.tealium.com/ja/platforms/node/api/#tealium)コンストラクターメソッドを使用して、`Tealium`インスタンスを初期化します。
      ```javascript
      var config = {
            "account"    : "ACCOUNT",
            "profile"    : "PROFILE",
            "datasource" : "DATASOURCE"
      };
      var tealium = Tealium(config);
      ```

3. [`addModule()`](https://docs.tealium.com/ja/platforms/node/api/#addmodule)メソッドを呼び出して、Tealium Collectモジュールを追加します。  
      ```javascript
      tealium.addModule(tealiumCollect);
      ```