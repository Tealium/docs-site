---
title: リクエスト形式
description: この記事では、Tealium APIのリクエスト形式について説明します。
url: https://docs.tealium.com/ja/api-v1/getting-started/request-format/
---

これは、[現行のTealium API]()の古いバージョンです。


## ルートURL

各APIは独自のエンドポイントとサポートされるパラメータを持ちます。すべてのAPIリクエストのルートURLは次のとおりです：

```
https://api.tealiumiq.com/v1
```

APIエンドポイントは、特定のHTTPメソッドとパスで文書化されます。例えば：

```
GET /revisions
```

プレースホルダー値を使用するエンドポイントは、このように中括弧を使用します：`{value}`。これらは、API呼び出しに特有の値に置き換えられます。ほとんどのエンドポイントでは、パス内で呼び出しを行うiQアカウントとプロファイルの名前が必要です。

完全なAPIエンドポイントは次のようになります：

```
https://api.tealiumiq.com/v1/accounts/{account}/{profile}/revisions
```


## リクエストとレスポンスの形式

APIはJSONをサポートしているため、ほとんどの呼び出しは適切なヘッダーを構成する必要があります：`Content-Type: application/json`。ほとんどのレスポンスもJSON形式になります。各エンドポイントのドキュメンテーションには、例のcurl呼び出しとレスポンスがあります。
