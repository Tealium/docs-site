---
title: GET グループ API
description: GET グループ API はアカウントからグループのリストを取得します。
url: https://docs.tealium.com/ja/api/v3/scim-api/get-groups-api/
---
## 動作方法

GET メソッドを使用してグループのリストを取得します：

```bash
GET /scim/v2/Groups/
```

## 認証

すべての API 呼び出しには OAuth ベアラートークンが使用され、API キーは使用されません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## GET 操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `count` | 数値 | 任意 | 返すレコードの数。最大値は `100`。デフォルト値は `20`。 |
| `startIndex` | 数値 | 任意 | インデックスで返す最初のレコード。count がレコード数を超える場合、この値は無視されます。最小値およびデフォルト値は 1。 |
| `filter` | 文字列 | 任意 | `displayName` に基づいてグループをフィルタリングします。同等の値を見つけるために `eq` 演算子を使用します。例：`filter=displayName eq "Standard User"`。 |
| `excludedAttributes` | 文字列 | 任意 | レスポンスから除外する属性のカンマ区切りリスト。許可される値は `members`, `externalId`, `meta`, `meta.location`, `meta.resourceType` です。 |


<blockquote>
レスポンスには「Standard User」、「Account Admins」、「User Admins」、「Privacy Admins」、「Technical Admins」、「Profile Admins」といった組み込みグループが含まれます。`id` フィールドは各グループの安定した識別子です。詳細については、[グループ](https://docs.tealium.com/about-scim-api/#groups)を参照してください。
</blockquote>


### cURL リクエストの例

```bash
curl -H 'Authorization: Bearer {token}' \
'https://developer.tealiumapis.com/scim/v2/Groups'

curl -H 'Authorization: Bearer {token}' \
'https://developer.tealiumapis.com/scim/v2/Groups?startIndex=1&count=12'

curl -H 'Authorization: Bearer {token}' \
'https://developer.tealiumapis.com/scim/v2/Groups?filter=displayName%20eq%20%22group_name%22'

curl -H 'Authorization: Bearer {token}' \
'https://developer.tealiumapis.com/scim/v2/Groups?excludedAttributes=members%2Cmeta.resourceType&count=21'
```

### 応答の例



```json
{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:ListResponse"
    ],
    "totalResults": 150,
    "startIndex": 27,
    "itemsPerPage": 2,
    "Resources": [
        {
            "schemas": [
                "urn:ietf:params:scim:schemas:core:2.0:Group"
            ],
            "id": "cb869db7-42dd-4adf-a539-0bf2cac621bb",
            "displayName": "group1",
            "members": [
                {
                    "value": "298273b4-74a3-4150-aa0b-e308bbcbf05b",
                    "type": "User",
                    "display": "user1@example.com",
                    "$ref": "/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf05b"
                },
                {
                    "value": "33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb",
                    "type": "User",
                    "display": "user2@example.com",
                    "$ref": "/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb"
                },
                {
                    "value": "53bedf02-0324-471d-9a82-052694f91a60",
                    "type": "User",
                    "display": "user3@example.com",
                    "$ref": "/scim/v2/Users/53bedf02-0324-471d-9a82-052694f91a60"
                }
            ],
            "meta": {
                "resourceType": "Group",
                "location": "/scim/v2/Groups/cb869db7-42dd-4adf-a539-0bf2cac621bb"
            }
        },
        {
            "schemas": [
                "urn:ietf:params:scim:schemas:core:2.0:Group"
            ],
            "id": "d52f469b-3e8e-4126-8a91-e31f74c703b0",
            "displayName": "group2",
            "members": [
                {
                    "value": "298273b4-74a3-4150-aa0b-e308bbcbf05b",
                    "type": "User",
                    "display": "user1@example.com",
                    "$ref": "/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf05b"
                },
                {
                    "value": "33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb",
                    "type": "User",
                    "display": "user2@example.com",
                    "$ref": "/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb"
                },
                {
                    "value": "53bedf02-0324-471d-9a82-052694f91a60",
                    "type": "User",
                    "display": "user3@example.com",
                    "$ref": "/scim/v2/Users/53bedf02-0324-471d-9a82-052694f91a60"
                }
            ],
            "meta": {
                "resourceType": "Group",
                "location": "/scim/v2/Groups/d52f469b-3e8e-4126-8a91-e31f74c703b0"
            }
        }
    ]
}
```


### エラーメッセージ

このエンドポイントに関する潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "{parameter} must be a number."` |
| 401 | `{"returnCode" : 401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Forbidden."}` |
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|