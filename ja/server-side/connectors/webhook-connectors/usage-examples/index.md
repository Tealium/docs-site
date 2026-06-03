---
title: 使用例
description: この記事ではHTTPリクエストの例を提供します。
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/usage-examples/
---
これらの例では、明確さのために単純なJSONオブジェクトが使用されています。実際に送信されるデータは完全なイベントまたは訪問オブジェクトです。また、追加のパラメータがどのように送信されるかを示すために、`param1` が `value1` の値を受け取る単一のURLパラメータも含まれています。

### イベント/訪問の送信 - GETメソッド

Send Event DataまたはSend Visitor DataアクションでGETメソッドを使用する場合、データは `data` という名前の単一のクエリ文字列パラメータとして送信されます。値はイベント/訪問データオブジェクトのURLエンコードされたJSON文字列です。構成されたURLパラメータは追加のクエリ文字列パラメータとして追加されます。

この例では、データは以下の通りです：

```json
{
    &#34;foo&#34; : &#34;bar&#34;
}
```

結果のURLエンコードされたJSON文字列は以下の通りです：

`%7B%22foo%22%3A%22bar%22%7D`

この文字列が最終的なGETリクエストで以下のクエリ文字列パラメータとして現れます：

`data=%7B%22foo%22%3A%22bar%22%7D`

```
GET /webhook-service?data=%7B%22foo%22%3A%22bar%22%7D&amp;param1=value1

VERSION: HTTP/1.1
CONNECTION: close
ACCEPT-ENCODING: gzip
X-HEADER-KEY: header_value
COOKIE: cookie_key=cookie_valie,__cfduid=d63c6b0e0a23195e9a7142f314360b4e11502122913
USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
```

### イベント/訪問の送信 - POSTメソッド

以下は、**`application/json`** および `application/x-www-form-urlencoded` コンテンツタイプのサンプルPOSTリクエストです。

##### **Content-Type: application/json**

本文データはJSONペイロードとして送信されます。

```
POST /webhook-service?param1=value1

VERSION: HTTP/1.1
CONNECTION: close
ACCEPT-ENCODING: gzip
X-HEADER-KEY: header_value
COOKIE: cookie_key=cookie_valie
CONTENT-TYPE: application/json; charset=UTF-8
USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
CONTENT-LENGTH: 13

{
    &#34;foo&#34;: &#34;bar&#34;
}

```

##### **Content-Type: application/x-form-urlencoded**

本文データは `data` という名前のフォームデータフィールドを使用してURLエンコードされたJSON文字列として送信されます。

```
POST /webhook-service?param1=value1

VERSION: HTTP/1.1
CONNECTION: close
ACCEPT-ENCODING: gzip
X-HEADER-KEY: header_value
COOKIE: cookie_key=cookie_valie,__cfduid=d63c6b0e0a23195e9a7142f314360b4e11502122913
CONTENT-TYPE: application/x-www-form-urlencoded; charset=UTF-8
USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
CONTENT-LENGTH: 32

data=%7B%22foo%22%3A%22bar%22%7D
```