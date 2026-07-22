---
title: Tealium V3 APIリクエスト形式
description: この記事では、Tealium v3 APIのリクエスト形式について説明します。
url: https://docs.tealium.com/ja/api/v3/getting-started/request-format/
---## ルートURL

各APIには独自のエンドポイントとサポートされるパラメータがあります。すべてのAPIリクエストのルートURLは次のとおりです：

```none
https://platform.tealiumapis.com/v3
```

APIエンドポイントは、特定のHTTPメソッドとパスで文書化されています。例えば：

```none
GET /visitor
```

一部のエンドポイントでは、プレースホルダ変数（`{variable}`）を表示して、供給する値を示します。ほとんどのエンドポイントでは、呼び出しのパスにTealiumアカウントとプロファイルの名前が必要です。

Visitor Profile APIの例APIエンドポイントパス：

```none
https://platform.tealiumapis.com/v3/customer/visitor/accounts/{account}/profiles/{profile}
```

## リクエストとレスポンス形式

APIはJavaScript Object Notation（JSON）をサポートしています。JSONを使用するAPIリクエストは、次のヘッダ構成が必要です：

```none
Content-Type: application/json
```

ほとんどのレスポンスはJSON形式です。各エンドポイントのドキュメンテーションには、cURLの呼び出しとレスポンスの例が含まれています。

## レート制限

Tealium APIエンドポイントはさまざまな目的を果たし、レート制限は異なる場合があります。レート制限情報については、特定のAPIエンドポイントのドキュメンテーションを確認してください。任意のAPIエンドポイントの指定されたレート制限を超えると、HTTP `429 Too Many Requests`レスポンスコードが返されることがあります。


<blockquote>
ビジネスのニーズが高い制限を必要とする場合は、Tealiumのアカウントマネージャーに連絡してください。
</blockquote>
