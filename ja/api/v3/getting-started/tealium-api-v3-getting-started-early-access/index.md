---
title: Tealium API v3 - 認証とリクエスト形式（早期アクセス）
description: この記事では、Tealium v3 APIの使用を開始するために必要な情報を提供します。
url: https://docs.tealium.com/ja/api/v3/getting-started/tealium-api-v3-getting-started-early-access/
---
[以前のTealium v2 API]()はまだ利用可能ですが、最終的には廃止されます。

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

ビジネスのニーズが高い制限を必要とする場合は、Tealiumのアカウントマネージャーに連絡してください。

## 認証

認証（ログイン）には、Tealium iQタグ管理からのAPIキーが必要です。Tealium APIキーについて詳しくは、[APIキーの管理と生成]()を参照してください。

認証呼び出しには2つのパラメータがあります：ユーザ名とAPIキー。APIキーは、APIにログインするためのパスワードの代わりに使用されます。APIへの成功したログイン後、認証呼び出しはJWTを返し、これをベアラートークンと呼びます。ベアラートークンは30分間有効で、その後のAPI呼び出しを認証するために使用する必要がある値です。

すべての呼び出しで新しいベアラートークンを生成しないでください。トークンが期限切れになるまで使用してください。各トークンは30分以内に期限切れになります。この方法でトークンを使用しないと、Tealiumの裁量により認証呼び出しがスロットリングされる可能性があります。

### リージョン固有のホスト

認証レスポンスにはトークンとホスト値が含まれています。

```bash
{
  &#34;token&#34;:&#34;eyJ0[...]kqkpj8vE&#34;
  &#34;host&#34;: &#34;us-east-1-platform.tealiumapis.com&#34;
}
```

ホスト値は、リージョン固有の後続のAPI呼び出しで使用する必要があります。例えば、訪問APIエンドポイントは次のようになります：

`https://us-east-1-platform.tealiumapis.com/v3/visitor/accounts/{account}/{profile}`

### cURLリクエスト

次のcURLリクエストは、JWTトークンとのAPIキー交換に必要な変数を示しています。URL、ユーザ名、APIキーがエンコードされています。

```bash
curl -X POST \
https://platform.tealiumapis.com/v3/auth/accounts/{account}/profiles/{profile} \
-H &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;username={email}&#39; \
--data-urlencode &#39;key={api_key}&#39;
```

#### 例リクエスト

```bash
curl -X POST \
https://platform.tealiumapis.com/v3/auth/accounts/{account}/profiles/{profile} \
-H &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;username=tealium.user@yourdomain.com&#39; \
--data-urlencode &#39;key=7O4Pjn8tuc0%5B3Nc2)%7DyXJW8EaCuDRA1U8Jn%23p)qc*O94(*ubIeEUz%25%5D%242~)WKlLB&#39;
```

#### 例レスポンス

```bash
* Trying 10.220.2.176...
* Connected to platform.tealiumapis.com (10.220.2.176) port 443 (#0)
* TLS 1.2 connection using TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
* Server certificate: *.tealiumiq.com
* Server certificate: DigiCert SHA2 Secure Server CA
* Server certificate: DigiCert Global Root CA
&gt; POST /v3/auth/accounts/{account}/profiles/{profile} HTTP/1.1
&gt; Host: platform.tealiumapis.com
&gt; User-Agent: curl/7.43.0
&gt; Accept: */*
&gt; cache-control: no-cache
&gt; content-type: application/x-www-form-urlencoded
&gt; Content-Length: 127
&gt;
* upload completely sent off: 127 out of 127 bytes
&lt; HTTP/1.1 200 OK
&lt; Date: Wed, 14 Feb 2018 19:04:22 GMT
&lt; Content-Type: application/json
&lt; Content-Length: 893
&lt; Connection: keep-alive
&lt; Cache-Control: no-cache,no-store,must-revalidate
&lt; Pragma: no-cache
&lt; Expires: 0
&lt; X-XSS-Protection: 1;mode=block
&lt; X-NodeId: i-0afb3e9b53ba15930
&lt; X-Version: 1.0.130-SNAPSHOT
&lt; Set-Cookie: rememberMe=deleteMe; Path=/urest_service; Max-Age=0; Expires=Tue, 13-Feb-2018 19:10:41 GMT
&lt;
* Connection #0 to host platform.tealiumapis.com left intact
{
  &#34;token&#34;:&#34;eyJ0[...]kqkpj8vE&#34;
  &#34;host&#34;: &#34;us-east-1-platform.tealiumapis.com&#34;&lt;br&gt;
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
