---
title: GET グループ API
description: GET グループ API はアカウントからグループのリストを取得します。
url: https://docs.tealium.com/ja/administration/early-access/api/scim-api/get-groups-api/
---
## 動作方法

GET メソッドを使用してグループのリストを取得します：

```bash
GET /scim/v2/Groups/
```

## 認証

すべての API 呼び出しには OAuth ベアラートークンが使用され、API キーは使用されません。

詳細については、[認証]()を参照してください。

## GET 操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `count` | 数値 | 任意 | 返すレコードの数。最大値は `100`。デフォルト値は `20`。 |
| `startIndex` | 数値 | 任意 | インデックスで返す最初のレコード。count がレコード数を超える場合、この値は無視されます。最小値およびデフォルト値は 1。 |
| `filter` | 文字列 | 任意 | `displayName` に基づいてグループをフィルタリングします。同等の値を見つけるために `eq` 演算子を使用します。例：`filter=displayName eq &#34;Standard User&#34;`。 |
| `excludedAttributes` | 文字列 | 任意 | レスポンスから除外する属性のカンマ区切りリスト。許可される値は `members`, `externalId`, `meta`, `meta.location`, `meta.resourceType` です。 |

レスポンスには「Standard User」、「Account Admins」、「User Admins」、「Privacy Admins」、「Technical Admins」、「Profile Admins」といった組み込みグループが含まれます。`id` フィールドは各グループの安定した識別子です。詳細については、[グループ]()を参照してください。

### cURL リクエストの例

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://developer.tealiumapis.com/scim/v2/Groups&#39;

curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://developer.tealiumapis.com/scim/v2/Groups?startIndex=1&amp;count=12&#39;

curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://developer.tealiumapis.com/scim/v2/Groups?filter=displayName%20eq%20%22group_name%22&#39;

curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://developer.tealiumapis.com/scim/v2/Groups?excludedAttributes=members%2Cmeta.resourceType&amp;count=21&#39;
```

### 応答の例



```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:api:messages:2.0:ListResponse&#34;
    ],
    &#34;totalResults&#34;: 150,
    &#34;startIndex&#34;: 27,
    &#34;itemsPerPage&#34;: 2,
    &#34;Resources&#34;: [
        {
            &#34;schemas&#34;: [
                &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
            ],
            &#34;id&#34;: &#34;cb869db7-42dd-4adf-a539-0bf2cac621bb&#34;,
            &#34;displayName&#34;: &#34;group1&#34;,
            &#34;members&#34;: [
                {
                    &#34;value&#34;: &#34;298273b4-74a3-4150-aa0b-e308bbcbf05b&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user1@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf05b&#34;
                },
                {
                    &#34;value&#34;: &#34;33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user2@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb&#34;
                },
                {
                    &#34;value&#34;: &#34;53bedf02-0324-471d-9a82-052694f91a60&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user3@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/53bedf02-0324-471d-9a82-052694f91a60&#34;
                }
            ],
            &#34;meta&#34;: {
                &#34;resourceType&#34;: &#34;Group&#34;,
                &#34;location&#34;: &#34;/scim/v2/Groups/cb869db7-42dd-4adf-a539-0bf2cac621bb&#34;
            }
        },
        {
            &#34;schemas&#34;: [
                &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
            ],
            &#34;id&#34;: &#34;d52f469b-3e8e-4126-8a91-e31f74c703b0&#34;,
            &#34;displayName&#34;: &#34;group2&#34;,
            &#34;members&#34;: [
                {
                    &#34;value&#34;: &#34;298273b4-74a3-4150-aa0b-e308bbcbf05b&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user1@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf05b&#34;
                },
                {
                    &#34;value&#34;: &#34;33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user2@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb&#34;
                },
                {
                    &#34;value&#34;: &#34;53bedf02-0324-471d-9a82-052694f91a60&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user3@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/53bedf02-0324-471d-9a82-052694f91a60&#34;
                }
            ],
            &#34;meta&#34;: {
                &#34;resourceType&#34;: &#34;Group&#34;,
                &#34;location&#34;: &#34;/scim/v2/Groups/d52f469b-3e8e-4126-8a91-e31f74c703b0&#34;
            }
        }
    ]
}
```


### エラーメッセージ

このエンドポイントに関する潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;{parameter} must be a number.&#34;` |
| 401 | `{&#34;returnCode&#34; : 401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Forbidden.&#34;}` |
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|