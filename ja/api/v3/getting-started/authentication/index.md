---
title: Tealium V3 API認証
description: この記事では、Tealium v3 APIの認証情報について説明します。
url: https://docs.tealium.com/ja/api/v3/getting-started/authentication/
---
## 認証

認証（ログイン）には、Tealium iQタグ管理からのAPIキーが必要です。Tealium APIキーについての詳細は、[APIキーの管理と生成](https://docs.tealium.com/api-keys/)を参照してください。

認証コールには2つのパラメーターがあります：ユーザー名とAPIキー。APIキーはパスワードの代わりにAPIにログインするために使用されます。APIへのログインが成功すると、認証コールはJWTを返し、これをベアラートークンと呼びます。ベアラートークンは30分間有効で、その後のAPIコールを認証するために使用する必要があります。


<blockquote>
各コールごとに新しいベアラートークンを生成しないでください。トークンが期限切れになるまで使用してください。各トークンは30分で期限切れになります。この方法でトークンを使用しないと、Tealiumの裁量により認証コールの制限が行われる可能性があります。
</blockquote>


### 権限要件

認証エンドポイントはAPIキーのみを要求します。ベアラートークンを取得するために追加のプラットフォーム権限は必要ありません。ただし、各v3 APIエンドポイントへのアクセスは、ユーザーのプラットフォーム権限レベルによって決まります。権限要件については、各エンドポイントのドキュメントを参照してください。

### 地域固有のホスト

認証応答にはトークンとホスト値が含まれます。

```json
{
  "token":"eyJ0[...]kqkpj8vE"
  "host": "us-east-1-platform.tealiumapis.com"
}
```

ホスト値は、地域固有のAPIコールで使用する必要があります。たとえば、訪問APIエンドポイントは以下のようになります：

```none
https://us-east-1-platform.tealiumapis.com/v3/visitor/accounts/{account}/profiles/{profile}
```

### cURLリクエスト

次のcURLリクエストは、JWTトークンの交換に必要な変数を示しています。URL、ユーザー名、およびAPIキーはエンコードされています。

```bash
curl -X POST \
https://platform.tealiumapis.com/v3/auth/accounts/{account}/profiles/{profile} \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'username={email}' \
--data-urlencode 'key={api_key}'
```

#### 例のリクエスト

```bash
curl -X POST \
https://platform.tealiumapis.com/v3/auth/accounts/{account}/profiles/{profile} \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'username=tealium.user@yourdomain.com' \
--data-urlencode 'key=7O4Pjn8tuc0%5B3Nc2)%7DyXJW8EaCuDRA1U8Jn%23p)qc*O94(*ubIeEUz%25%5D%242~)WKlLB'
```

#### 例の応答

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
  "host": "us-east-1-platform.tealiumapis.com"
}

```