---
title: PUTユーザーAPI
description: PUTユーザーAPIは、アカウント内の既存のユーザーを置き換えます。
url: https://docs.tealium.com/ja/api/v3/scim-api/put-user-api/
---
## 動作原理

PUTメソッドを使用して既存のユーザーを置き換えます：

```bash
PUT /scim/v2/Users/{id}
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証]()を参照してください。

## PUT操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | ユーザーの一意の識別子。この値はREST API呼び出しの一部として送信されます。 |
| `userName` | オブジェクト | 必須 | ユーザーのユーザー名で、メールアドレス形式です。有効なメールアドレスでなければなりません。APIを通じて`userName`を変更することはできません。|
| `name` | オブジェクト | 任意 | ユーザーの名前を含むリスト。各名前には`givenName`と`familyName`を含むことができます。Nullおよび空の値が許可されます。 |
| `emails` | 配列 | 任意 | この値は`userName`によって自動的に構成されます。 |
| `active` | ブール | 任意 | ユーザーがアクティブかどうかを示します。ユーザーを削除または非アクティブ化しようとしている場合は、[DELETEメソッド]()を使用してください。 |

### 例 cURLリクエスト

```bash
curl -X PUT &#34;https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
  &#34;schemas&#34;: [&#34;urn:ietf:params:scim:schemas:core:2.0:User&#34;],
  &#34;userName&#34;: &#34;updated.user@example.com&#34;,
  &#34;name&#34;: {
    &#34;givenName&#34;: &#34;Updated&#34;,
    &#34;familyName&#34;: &#34;User&#34;
  },
  &#34;emails&#34;: [{
    &#34;value&#34;: &#34;updated.user@example.com&#34;
  }],
  &#34;active&#34;: true
}&#39;
```

### 例 応答



```json
{
  &#34;schemas&#34;: [&#34;urn:ietf:params:scim:schemas:core:2.0:User&#34;],
  &#34;id&#34;: &#34;eb987394-b2b0-4a21-a1d8-7915a91e06b&#34;,
  &#34;userName&#34;: &#34;updated.user@example.com&#34;,
  &#34;name&#34;: {
    &#34;givenName&#34;: &#34;Updated&#34;,
    &#34;familyName&#34;: &#34;User&#34;
  },
  &#34;emails&#34;: [{
    &#34;value&#34;: &#34;updated.user@example.com&#34;
  }],
  &#34;active&#34;: true,
  &#34;meta&#34;: {
    &#34;resourceType&#34;: &#34;User&#34;,
    &#34;location&#34;: &#34;/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6ab&#34;
  }
}
```


### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;userName must be a valid email address.&#34;` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;User not found in account {ACCOUNT}.&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|