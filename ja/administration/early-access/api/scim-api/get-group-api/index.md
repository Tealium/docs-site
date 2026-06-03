---
title: GET グループ API
description: GET グループ API はアカウントから既存のグループを取得します。
url: https://docs.tealium.com/ja/administration/early-access/api/scim-api/get-group-api/
---
## 動作方法

既存のグループを取得するには GET メソッドを使用します：

```bash
GET /scim/v2/Groups/{id}
```

## 認証

すべての API 呼び出しには OAuth ベアラートークンが使用され、API キーは使用されません。

詳細については、[認証]()を参照してください。

## GET 操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | グループの一意の識別子。この値は REST API 呼び出しの一部として送信されます。|

### cURL リクエストの例

```bash
curl --location --request GET &#39;https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b&#39; \
```

### 応答の例


```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
    ],
    &#34;id&#34;: &#34;9d379d2c-2601-42d8-842c-579dc3c58612&#34;,
    &#34;displayName&#34;: &#34;Group 1&#34;,
    &#34;members&#34;: [
        {
            &#34;value&#34;: &#34;298273b4-74a3-4150-aa0b-e308bbcbf06b&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user1@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf06b&#34;
        },
        {
            &#34;value&#34;: &#34;33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user2@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb&#34;
        }
    ],
    &#34;meta&#34;: {
        &#34;resourceType&#34;: &#34;Group&#34;,
        &#34;location&#34;: &#34;/scim/v2/Groups/9d379d2c-2601-42d8-842c-579dc3c58612&#34;
    }
}
```


### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;IDの形式が無効です。&#34;}` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;認証に失敗しました。&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;X-Tealium-Account ヘッダーがありません。&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;アカウント {ACCOUNT} にグループが見つかりません。&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;このエンドポイントでは許可されていないメソッドです。許可されているメソッド: GET, PUT, DELETE, PATCH.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;拡張機能の json 処理中にエラーが発生しました - アカウント {ACCOUNT}&#34;}`|