---
title: GETユーザーAPI
description: GETユーザーAPIはアカウントからユーザーのリストを取得します。
url: https://docs.tealium.com/ja/administration/early-access/api/scim-api/get-users-api/
---
## 動作方法

GETメソッドを使用してユーザーのリストを取得します：

```bash
GET /scim/v2/Users/
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証]()を参照してください。

## GET操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `count` | 数値 | 任意 | 返すレコードの数。最大値は `100` です。 |
| `startIndex` | 数値 | 任意 | インデックスで返す最初のレコード。countがレコード数を超える場合、この値は無視されます。 |
| `filter` | 文字列 | 任意 | ユーザー名に基づいてユーザーをフィルタリングします。同等の値を見つけるために `eq` 演算子を使用します。 |

### cURLリクエストの例

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://developer.tealiumapis.com/scim/v2/Users?startIndex=1&amp;count=10&amp;filter=userName%20eq%20%22user@example.com%22
```

### 応答の例



```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:api:messages:2.0:ListResponse&#34;
    ],
    &#34;totalResults&#34;: 1,
    &#34;startIndex&#34;: 1,
    &#34;itemsPerPage&#34;: 1,
    &#34;Resources&#34;: [
        {
            &#34;schemas&#34;: [
                &#34;urn:ietf:params:scim:schemas:core:2.0:User&#34;
            ],
            &#34;id&#34;: &#34;913b0182-2531-402f-a302-fcd9d2aeda6a&#34;,
            &#34;userName&#34;: &#34;test.userxz1@example.com&#34;,
            &#34;displayName&#34;: null,
            &#34;externalId&#34;: null,
            &#34;name&#34;: {
                &#34;givenName&#34;: &#34;Test&#34;,
                &#34;familyName&#34;: &#34;User&#34;
            },
            &#34;emails&#34;: [
                {
                    &#34;value&#34;: &#34;test.userxz1@example.com&#34;
                }
            ],
            &#34;active&#34;: true,
            &#34;meta&#34;: {
                &#34;resourceType&#34;: &#34;User&#34;,
                &#34;location&#34;: &#34;/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6a&#34;
            }
        }
    ]
}
```


### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;{parameter} must be a number.&#34;` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|
