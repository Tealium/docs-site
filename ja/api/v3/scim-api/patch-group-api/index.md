---
title: PATCH グループ API
description: PATCH グループ API は既存のグループを更新します。
url: https://docs.tealium.com/ja/api/v3/scim-api/patch-group-api/
---
## 動作方法

既存のグループを更新するには、PATCH メソッドを使用します：

```bash
PATCH /scim/v2/Groups/{id}
```

## 認証

すべての API 呼び出しには OAuth ベアラートークンを使用して認証します。API キーではありません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## PATCH 操作パラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | ユーザーの一意の識別子。この値は REST API 呼び出しの一部として送信されます。|
| `op` | 文字列 | 任意 | 実行する操作。サポートされる値は `add`、`replace`、`remove` です。 |
| `path` | 文字列 | 任意 | 操作の対象を指定する属性パス。省略された場合、操作はリソース全体に対して実行されます。 |
| `value` | 配列 | 任意 | ユーザー ID の配列。 |

### cURL リクエストの例

#### Microsoft Entra ID

```bash
curl -X PATCH "https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"
    ],
    "Operations": [
        {
            "op": "replace",
            "path": "members",
            "value": [
               {
                   "value": "cb300cb6-9702-45a9-a909-f8b7c972ab7e"
               }
           , "/ja/early-access/api/scim-api/patch-group-api"]
        }
    , "/ja/early-access/api/scim-api/patch-group-api"]
}'
```

#### Okta

```bash
curl -X PATCH "https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"
    ],
    "Operations": [
        {
            "op": "replace",
            "value": {
                "members": [
                   {
                       "value": "cb300cb6-9702-45a9-a909-f8b7c972ab7e"
                   }
               , "/ja/early-access/api/scim-api/patch-group-api"]
            }
        }
    , "/ja/early-access/api/scim-api/patch-group-api"]
}'
```

### 応答例



```json
{
   "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:Group"
    ],
    "id": "eb987394-b2b0-4a21-a1d8-7915a91e06b",
    "displayName": "example group",
    "members": [
        {
            "value": "cb300cb6-9702-45a9-a909-f8b7c972ab7e",
            "type": "User",
            "display": "exampleuser@example.onmicrosoft.com",
            "$ref": "/scim/v2/Users/cb300cb6-9702-45a9-a909-f8b7c972ab7e"
        },
        {
            "value": "3bfa1b1f-5f1f-45c1-bcb8-25a70b1a4bb2",
            "type": "User",
            "display": "exampleuser@okta.com",
            "$ref": "/scim/v2/Users/3bfa1b1f-5f1f-45c1-bcb8-25a70b1a4bb2"
        }
    ],
    "meta": {
        "resourceType": "Group",
        "location": "/scim/v2/Groups/7987a965-411b-4816-b485-29fd81ca81ac"
    }
}
```


## エラーメッセージ

このエンドポイントに関する潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "User payload is required."}` |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Cannot rename built-in group 'Account Admins'. Built-in group names are immutable."}`|
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 |` {"schemas":["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404", "scimType": "noTarget", "detail":"Group uuid 1987a965-411b-4816-b485-29fd81ca81ac not found in account testaccount"}`|
| 404 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "User UUID {uuid} not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"], "status": "405", "scimType": "invalidMethod", "detail": "Method is not allowed on this endpoint. Allowed methods: GET, POST."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|
| 501 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "501","scimType": "unsupported","detail": "The operation {operation} is not supported."}`|