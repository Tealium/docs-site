---
title: POSTユーザーAPI
description: POSTユーザーAPIはアカウントに新しいユーザーを作成します。
url: https://docs.tealium.com/ja/administration/early-access/api/scim-api/post-user-api/
---
## 動作原理

POSTメソッドを使用して新しいユーザーを作成します：

```bash
POST /scim/v2/Users/
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証]()を参照してください。

## POST操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `userName` | オブジェクト | 必須 | ユーザーのユーザー名（メールアドレス形式）。これは有効なメールアドレスでなければなりません。 |
| `emails` | 配列 | 任意 | この値が`userName`と一致しない場合、値は無視されます。 |
| `active` | ブール値 | 任意 | ユーザーがアクティブかどうかを示します。 |
| `name` | オブジェクト | 任意 | ユーザーの名前を含むリスト。各名前には`givenName`と`familyName`を含むことができます。Nullや空の値が許可されます。 |

### cURLリクエストの例

```bash
curl -X POST &#34;https://developer.tealiumapis.com/scim/v2/Users/&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
  &#34;schemas&#34;: [&#34;urn:ietf:params:scim:schemas:core:2.0:User&#34;],
  &#34;userName&#34;: &#34;user@example.com&#34;,
  &#34;name&#34;: {
    &#34;givenName&#34;: &#34;New&#34;,
    &#34;familyName&#34;: &#34;User&#34;
  },
  &#34;emails&#34;: [{
    &#34;value&#34;: &#34;user@example.com&#34;
  }],
  &#34;active&#34;: true
}&#39;
```

### 応答の例


```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:User&#34;
    ],
    &#34;id&#34;: &#34;913b0182-2531-402f-a302-fcd9d2aeda6a&#34;,
    &#34;userName&#34;: &#34;user@example.com&#34;,
    &#34;displayName&#34;: null,
    &#34;externalId&#34;: null,
    &#34;name&#34;: {
        &#34;givenName&#34;: &#34;New&#34;,
        &#34;familyName&#34;: &#34;User&#34;
    },
    &#34;emails&#34;: [
        {
            &#34;value&#34;: &#34;user@example.com&#34;
        }
    ],
    &#34;active&#34;: true,
    &#34;meta&#34;: {
        &#34;resourceType&#34;: &#34;User&#34;,
        &#34;location&#34;: &#34;/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6a&#34;
    }
}
```


### エラーメッセージ

このエンドポイントに関する潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;User payload is required.&#34;` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH.&#34;}`|
| 409 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;409&#34;,&#34;scimType&#34;: &#34;uniqueness&#34;,&#34;detail&#34;: &#34;User already exists in the given account.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|