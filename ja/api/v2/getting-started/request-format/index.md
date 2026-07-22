---
title: Tealium APIのリクエスト形式
description: この記事では、Tealium APIのリクエスト形式について説明します。
url: https://docs.tealium.com/ja/api/v2/getting-started/request-format/
---

<blockquote>
[以前のv1 API](https://docs.tealium.com/request-format-v1/)はまだ利用可能ですが、最終的には廃止される予定です。
</blockquote>


## ルートURL

各APIには独自のエンドポイントとサポートされるパラメータがあります。すべてのAPIリクエストのルートURLは次のとおりです：

```
https://api.tealiumiq.com/v2
```

APIエンドポイントは、特定のHTTPメソッドとパスで文書化されています。例えば：

```
GET /revisions
```

一部のエンドポイントでは、プレースホルダ変数（`{variable}`）を表示して、供給する値を示します。ほとんどのエンドポイントでは、呼び出しのパスにiQタグ管理（TiQ）アカウントとプロファイルの名前が必要です。

TiQリビジョンのAPIエンドポイントパスの例：

```
https://api.tealiumiq.com/v2/accounts/{account}/{profile}/revisions
```

## リクエストとレスポンスの形式

APIはJavaScript Object Notation（JSON）をサポートしています。JSONを使用するAPIリクエストは、次のヘッダ構成が必要です：

```
Content-Type: application/json
```

ほとんどのレスポンスはJSON形式です。各エンドポイントのドキュメンテーションには、cURLの呼び出しとレスポンスの例が含まれています。