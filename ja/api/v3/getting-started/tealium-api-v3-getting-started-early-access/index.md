---
title: Tealium API v3 - 認証とリクエスト形式（早期アクセス）
description: この記事では、Tealium v3 APIの使用を開始するために必要な情報を提供します。
url: https://docs.tealium.com/ja/api/v3/getting-started/tealium-api-v3-getting-started-early-access/
---

<blockquote>
[以前のTealium v2 API](https://docs.tealium.com/api-authentication/)はまだ利用可能ですが、最終的には廃止されます。
</blockquote>


## ルートURL

各APIには独自のエンドポイントとサポートされるパラメータがあります。すべてのAPIリクエストのルートURLは次のとおりです：

`https://platform.tealiumapis.com/v3`

APIエンドポイントは、特定のHTTPメソッドとパスで文書化されています。例えば：

`GET /visitor`

一部のエンドポイントでは、プレースホルダ変数（`{variable}`）が表示され、ユーザーが提供する値を示します。ほとんどのエンドポイントでは、Tealiumアカウントとプロファイルの名前が呼び出しのパスに必要です。

iQプロファイルのAPIエンドポイントパスの例：

`https://platform.tealiumapis.com/v3/tiq/accounts/{account}/{profile}`

## リクエストとレスポンスの形式

APIはJavaScript Object Notation（JSON）をサポートしています。JSONを使用するAPIリクエストでは、次のヘッダ構成が必要です：

`Content-Type: application/json`

ほとんどのレスポンスはJSON形式です。各エンドポイントのドキュメンテーションには、cURLの呼び出しとレスポンスの例が含まれています。

## レート制限

Tealium APIのエンドポイントはそれぞれ異なる目的を果たし、レート制限も異なる場合があります。レート制限の情報については、特定のAPIエンドポイントのドキュメンテーションを確認してください。任意のAPIエンドポイントの指定されたレート制限を超えると、TealiumはHTTP 429レスポンスを送信し、リクエストが多すぎることを示します。


<blockquote>
ビジネスのニーズが高い制限を必要とする場合は、Tealiumのアカウントマネージャーに連絡してください。
</blockquote>


## 認証

認証（ログイン）には、Tealium iQタグ管理からのAPIキーが必要です。Tealium APIキーについて詳しくは、[APIキーの管理と生成](https://docs.tealium.com/api-keys/)を参照してください。

認証呼び出しには2つのパラメータがあります：ユーザ名とAPIキー。APIキーは、APIにログインするためのパスワードの代わりに使用されます。APIへの成功したログイン後、認証呼び出しはJWTを返し、これをベアラートークンと呼びます。ベアラートークンは30分間有効で、その後のAPI呼び出しを認証するために使用する必要がある値です。


<blockquote>
すべての呼び出しで新しいベアラートークンを生成しないでください。トークンが期限切れになるまで使用してください。各トークンは30分以内に期限切れになります。この方法でトークンを使用しないと、Tealiumの裁量により認証呼び出しがスロットリングされる可能性があります。
</blockquote>


### リージョン固有のホスト

認証レスポンスにはトークンとホスト値が含まれています。

```bash
{
  "token":"eyJ0[...]kqkpj8vE"
  "host": "us-east-1-platform.tealiumapis.com"
}
```

ホスト値は、リージョン固有の後続のAPI呼び出しで使用する必要があります。例えば、訪問APIエンドポイントは次のようになります：

`https://us-east-1-platform.tealiumapis.com/v3/visitor/accounts/{account}/{profile}`

### cURLリクエスト

次のcURLリクエストは、JWTトークンとのAPIキー交換に必要な変数を示しています。URL、ユーザ名、APIキーがエンコードされています。

```bash
curl -X POST \
https://platform.tealiumapis.com/v3/auth/accounts/{account}/profiles/{profile} \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'username={email}' \
--data-urlencode 'key={api_key}'
```

#### 例リクエスト

```bash
curl -X POST \
https://platform.tealiumapis.com/v3/auth/accounts/{account}/profiles/{profile} \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'username=tealium.user@yourdomain.com' \
--data-urlencode 'key=7O4Pjn8tuc0%5B3Nc2)%7DyXJW8EaCuDRA1U8Jn%23p)qc*O94(*ubIeEUz%25%5D%242~)WKlLB'
```

#### 例レスポンス

```bash
* Trying 10.220.2.176...
* Connected to platform.tealiumapis.com (10.220.2.176) port 443 (#0)
* TLS 1.2 connection using TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
* Server certificate: *.tealiumiq.com
* Server certificate: DigiCert SHA2 Secure Server CA
* Server certificate: DigiCert Global Root CA
> POST /v3/auth/accounts/{account}/profiles/{profile} HTTP/1.1
> Host: platform.tealiumapis.com
> User-Agent: curl/7.43.0
> Accept: */*
> cache-control: no-cache
> content-type: application/x-www-form-urlencoded
> Content-Length: 127
>
* upload completely sent off: 127 out of 127 bytes
< HTTP/1.1 200 OK
< Date: Wed, 14 Feb 2018 19:04:22 GMT
< Content-Type: application/json
< Content-Length: 893
< Connection: keep-alive
< Cache-Control: no-cache,no-store,must-revalidate
< Pragma: no-cache
< Expires: 0
< X-XSS-Protection: 1;mode=block
< X-NodeId: i-0afb3e9b53ba15930
< X-Version: 1.0.130-SNAPSHOT
< Set-Cookie: rememberMe=deleteMe; Path=/urest_service; Max-Age=0; Expires=Tue, 13-Feb-2018 19:10:41 GMT
<
* Connection #0 to host platform.tealiumapis.com left intact
{
  "token":"eyJ0[...]kqkpj8vE"
  "host": "us-east-1-platform.tealiumapis.com"<br>
}

```
## ステータスコード

Tealium v3 APIは、リクエストのステータスを示すために標準的なHTTPレスポンスステータスコードを使用します。

| ステータスコード | 説明 |
| --- | --- |
| 200 | OK |
| 400 | バッドリクエスト |
| 401 | 認証が必要 |
| 404 | 見つかりません |
| 429 | リクエストが多すぎます |
| 50X | サーバーエラー |
