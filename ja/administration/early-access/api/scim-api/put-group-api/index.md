---
title: PUT グループ API
description: PUT グループ API はアカウント内の既存のグループを置き換えます。
url: https://docs.tealium.com/ja/administration/early-access/api/scim-api/put-group-api/
---
## 動作方法

PUT メソッドを使用して既存のグループを置き換えます：

```bash
PUT /scim/v2/Groups/{id}
```

## 認証

すべての API 呼び出しには OAuth ベアラートークンが使用され、API キーは使用されません。

詳細については、[認証]()を参照してください。

## PUT 操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | グループの一意の識別子。この値は REST API 呼び出しの一部として送信されます。 |
| `displayName` | 文字列 | 必須 | グループの名前。文字、数字、およびスペースのみを使用してください。名前は 63 文字を超えることはできません。 |
| `members` | 配列 | 任意 | グループ内のメンバーのリスト。各メンバーは `value`、`type`、`display`、`$ref` を含むことができます。 |

組み込みグループの名前は変更できず、カスタムグループは組み込みグループと同じ名前を持つことはできません。詳細については、を参照してください。

### cURL リクエストの例

```bash
curl -X PUT &#34;https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
    ],
    &#34;displayName&#34;: &#34;Group 1&#34;,
    &#34;id&#34;: &#34;3268d9ce-54a2-4758-a19c-beb2b47059d3&#34;,
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
    , &#34;/ja/early-access/api/scim-api/put-group-api&#34;]
}&#39;
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

このエンドポイントに関する潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;グループ名 (%very long name with symbols%) に特殊文字を含めることはできず、63文字を超えることはできません。&#34;}` |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;組み込みグループ &#39;Standard User&#39; の名前を変更することはできません。組み込みグループの名前は変更不可です。&#34;}`|
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;認証に失敗しました。&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;X-Tealium-Account ヘッダーがありません。&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;アカウント {ACCOUNT} にグループが見つかりません。&#34;}`|
| 404 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;アカウント {ACCOUNT} にユーザー UUID {uuid} が見つかりません。&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;このエンドポイントでは許可されていない方法です。許可されている方法：GET, PUT, DELETE, PATCH.&#34;}`|
| 409 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;409&#34;,&#34;scimType&#34;: &#34;uniqueness&#34;,&#34;detail&#34;: &#34;アカウント accounttest に &#39;grouptest&#39; というグループ名が既に存在します。&#34;}` |
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;拡張機能の json 処理中にエラーが発生しました - アカウント {ACCOUNT}&#34;}`|