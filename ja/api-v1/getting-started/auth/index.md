---
title: 認証
description: この記事では、Tealium V1 APIで使用される認証方法について説明します。
url: https://docs.tealium.com/ja/api-v1/getting-started/auth/
---
 これは[現在のTealium API]()の古いバージョンです。 

APIは、有効なTealiumアカウントを持つユーザーのみが使用できます。APIは、ユーザーの身元を確認するためにメールアドレスとパスワードを使用した認証をサポートしています。APIエンドポイントにアクセスする前に、セッションを開始するために認証を行う必要があります。その後のすべての呼び出しは、セキュリティ目的でセッションクッキーと[CSRFトークン](https://en.wikipedia.org/wiki/Cross-site_request_forgery)を使用します。

## ログイン

ログインに成功すると、次の2つのアイテムが付与されます：

* `JSESSIONID`という名前のクッキー。
* `utk`という名前のトークン。

これらの値は、その後のすべてのAPI呼び出しで認証に使用されます。

### リソースURL

`POST /v1/login`

cURLリクエスト：

```bash
curl -i -d username=&#39;{email}&#39; -d password=&#39;{password}&#39; https://api.tealiumiq.com/v1/login
```

例のリクエスト：

```bash
curl -i -d username=&#39;user@example.com&#39; -d password=&#39;password123&#39; https://api.tealiumiq.com/v1/login
```

例のレスポンス：

```bash
HTTP/1.1 200 OK

Cache-Control: no-cache,no-store,must-revalidate
Content-Type: application/json
Date: Mon, 31 Oct 2016 20:39:29 GMT
Expires: 0
Pragma: no-cache
Set-Cookie: JSESSIONID=3513642946826543477; Path=/urest_service; Secure; HttpOnly
Set-Cookie: rememberMe=deleteMe; Path=/urest_service; Max-Age=0; Expires=Sun, 30-Oct-2016 20:39:29 GMT
X-NodeId: i-6c3ba529
X-Version: 0.0.528
X-XSS-Protection: 1;mode=block
Content-Length: 60
Connection: keep-alive

{
   &#34;utk&#34;: &#34;65489FMSTJGF549870KSH&#34;,
}
```

このレスポンスから、次の値をすべての後続のAPI呼び出しでメモしておく必要があります：

(サンプル値)

* JSESSION = `3513642946826543477`
* utk = `65489FMSTJGF549870KSH`

### エラーメッセージ

呼び出しが失敗した場合、APIは`401 Authentication Failure`エラーを返します。期待されるエラーメッセージは次のとおりです：

`{ &lt;br&gt;   &#34;returnCode&#34; : 1401,&lt;br&gt;  &#34;message&#34; : &#34;Authentication Failed&#34;&lt;br&gt;}`

`{ &lt;br&gt;   &#34;returnCode&#34; : 1402,&lt;br&gt;  &#34;message&#34; : &#34;Too many unsuccessful login attempts. Please try again in 10 minutes&#34; &lt;br&gt;}`

`{ &lt;br&gt;   &#34;returnCode&#34; : 1469,&lt;br&gt;  &#34;message&#34; : &#34;Although the user is authenticated, the request is denied due of lack of proper permissions&#34; &lt;br&gt;}`

## ログアウト

ログイン中のユーザーの現在のセッションを終了します。

 このAPI呼び出しはオプショナルです。ユーザーのセッションが期限切れになると自動的にログアウトされます。

### リソースURL

POST &lt;https://api.tealiumiq.com/v1/logout&gt;

### リクエストヘッダ

| ヘッダーフィールド名 | 説明 | 例の値 |
| --- | --- | --- |
| [Content-type](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields) | GETリクエストの本体のMIMEタイプを示します | `application/x-www-form-urlencoded` |
| JSESSION cookie | jsession IDを送信するためのクッキー。例えば、一意のセッション識別子。 | `JSESSIONID=415072043799098022` |

### 例のレスポンス

ログアウトに成功すると、APIは`status 200 OK`を返します。