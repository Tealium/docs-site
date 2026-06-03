---
title: インストール
description: Tealium for Node.jsのインストールについて説明します。
url: https://docs.tealium.com/ja/platforms/node/install/
---Node.js用の`tealium-collect`モジュールでは、イベントデータが[Tealium HTTP API](/ja/platforms/http-api/)経由でTealium Customer Data Hubに送信されます。このモジュールは、[サーバーサイド](/ja/server-side/)アプリケーションやブラウザで使用します。

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
var Tealium = require(&#39;tealium&#39;);
var tealiumCollect = require(&#39;tealium-collect&#39;);
```

2. `Tealium`インスタンスを[`Tealium()`](/ja/platforms/node/api/#tealium)コンストラクタメソッドで初期化します。
```javascript
var config = {
      &#34;account&#34;    : &#34;ACCOUNT&#34;,
      &#34;profile&#34;    : &#34;PROFILE&#34;,
      &#34;datasource&#34; : &#34;DATASOURCE&#34;
};
var tealium = Tealium(config);
```

3. [`addModule()`](/ja/platforms/node/api/#addmodule)メソッドを呼び出してTealium Collectモジュールを追加します。
```javascript
tealium.addModule(tealiumCollect);
```

