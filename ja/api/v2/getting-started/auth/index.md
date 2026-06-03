---
title: 認証
description: この記事では、Tealium V2 APIで使用される認証方法について説明します。
url: https://docs.tealium.com/ja/api/v2/getting-started/auth/
---
この記事では、Tealium v2 APIの使用を開始するために必要な情報を提供します。[以前のv1 API]()もまだ利用可能ですが、最終的には非推奨となります。

## 認証

認証（ログイン）には、Tealium iQタグ管理からのAPIキーが必要です。[APIキーの管理と生成]()について詳しく学びましょう。

認証コールには2つのパラメータがあります：ユーザー名とAPIキーです。APIキーはパスワードの代わりにAPIにログインするために使用されます。APIへのログインが成功すると、認証コールはJWTを返し、これをベアラートークンと呼びます。ベアラートークンは30分間有効で、後続のAPIコールを認証するために使用する必要があります。

各コールごとに新しいベアラートークンを生成しないでください。トークンが期限切れになるまで使用してください。この方法でトークンを使用しないと、Tealiumの裁量により認証コールの制限が行われる可能性があります。

## cURLリクエスト

次のcURLリクエストは、JWTトークンの交換に必要な変数を示しています。URL、ユーザー名、およびAPIキーはエンコードされています。

```bash
curl -X POST \
https://api.tealiumiq.com/v2/auth \
-H &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;username={email}&#39; \
--data-urlencode &#39;key={api_key}&#39;
```

## 例のリクエスト

```bash
curl -X POST \
https://api.tealiumiq.com/v2/auth \
-H &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;username=tealium.user@yourdomain.com&#39; \
--data-urlencode &#39;key=7O4Pjn8tuc0%5B3Nc2)%7DyXJW8EaCuDRA1U8Jn%23p)qc*O94(*ubIeEUz%25%5D%242~)WKlLB&#39;
```

## 例のレスポンス

```bash
* Trying 192.0.2.0...
* Connected to api.tealiumiq.com (192.0.2.0) port 443 (#0)
* TLS 1.2 connection using TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
* Server certificate: *.tealiumiq.com
* Server certificate: DigiCert SHA2 Secure Server CA
* Server certificate: DigiCert Global Root CA
&gt; POST /v2/auth HTTP/1.1
&gt; Host: qa20-api.tealiumiq.com
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
* Connection #0 to host api.tealiumiq.com left intact
{&#34;token&#34;:&#34;eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJtYXJjLmhpcG9saXRvQHRlYWxpdW0uY29tIiwibmJmIjoxNTE4NjM1NDQxLCJpc3MiOiJodHRwczovL2FwaS50ZWFsaXVtaXEuY29tIiwiZXhwIjoxNTE4NjM3MjQxLCJpYXQiOjE1MTg2MzU0NDF9.EPM_hfocfiF4SJnW0gBrGb9BuYIxsyoRdIWeuMTDLEBroVixmkFnPRC3G9zfn1hEpGfOGL6OKSHPIm5GwJQCNyIX7cE8umheIyTk8xxOuCAKjTOCip_6-AaFBcj6nLxgyez4OgxLral1XmZxyb9mP-vrKeDDQUf4ygdhgeDYoqnfQtIZ8TA68Pcx3H7BLgd0MJjTh7S74-9bWX95PkDDizTg0ia1dIbHsMXsB1ZA6gS-WPrCuy0CNA0IvJo0XuFNoOF2mazREYvG-Yp0-EzlMTa3W_EoI_93F9RbG-soUrLdV5IKav4TjwWfvyOZTx4Tb_Je9NgJ_EfeWW_E84pSAtCo7QX2yXZ3MYROkNnRdsQG4XhaFUbXwJnUghl65MHyjQxINDtbB5vujk04ctnuQvSO-sZslQxXGJm1sBiY3eFa5U4-L0V4MCJ3s9h_RbRyPt07CD4YX85kRJ5mj8x6nFHDE2iwrpSnNlQ_3KctqlJHSNdYhWzSnLpfz5qKq_Uv6XA88lUoRMiCC-Hy2uZe_vrqA0p_-BbrXPvw8olhd0SGD36D982bxKkcJR84ACUPU36FSBRWs_HRWEyjTwWR33oRv3vEIpzlUvp7TEGiD7A5ucNvLUT1yV_8YdsNLEevFg7WWjXkKnYDprq1QikO6KV1drWfrJnLldJ4ziTtK20&#34;}

```