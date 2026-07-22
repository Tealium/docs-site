---
title: POSTグループAPI
description: POSTグループAPIはアカウントに新しいグループを作成します。
url: https://docs.tealium.com/ja/api/v3/scim-api/post-group-api/
---
## 動作方法

POSTメソッドを使用してグループを作成します：

```bash
POST /scim/v2/Groups/
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## POST操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `displayName` | String | 必須 | グループの名前。文字、数字、スペースのみ使用可能。名前は63文字を超えることはできません。 |
| `members` | Array | 任意 | グループ内のメンバーのリスト。各メンバーは `value`, `type`, `display`, `$ref` を含むことができます。 |


<blockquote>
組み込みグループは名前を変更できず、カスタムグループは組み込みグループと同じ名前を持つことはできません。詳細については、を参照してください。
</blockquote>


### cURLリクエストの例

```bash
curl -X POST "https://developer.tealiumapis.com/scim/v2/Groups/" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:Group"
    ],
    "displayName": "Group 1",
    "members": [
        {
            "value": "aa3b970c-b459-4843-9f95-853a49b65f87",
            "type": "User",
            "display": "user1@example.com",
            "$ref": "/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f87"
        },
        {
            "value": "aa3b970c-b459-4843-9f95-853a49b65f88",
            "type": "User",
            "display": "user2@example.com",
            "$ref": "/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f88"
        }
    , "/ja/early-access/api/scim-api/post-group-api"]
}'
```

### 応答の例


```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:Group"
    ],
    "id": "c177ba78-88d9-43e0-8670-9f2d8c3cc83d",
    "displayName": "Group 1",
    "members": [
        {
            "value": "aa3b970c-b459-4843-9f95-853a49b65f87",
            "type": "User",
            "display": "user1@example.com",
            "$ref": "/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f87"
        },
        {
            "value": "aa3b970c-b459-4843-9f95-853a49b65f88",
            "type": "User",
            "display": "user2@example.com",
            "$ref": "/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f88"
        }
    ],
    "meta": {
        "resourceType": "Group",
        "location": "/scim/v2/Groups/c177ba78-88d9-43e0-8670-9f2d8c3cc83d"
    }
}
```


### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "User payload is required."}` |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Group name 'Standard User' is reserved and cannot be used."}`|
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "User UUID {uuid} not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, POST."}`|
| 409 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "409","scimType": "uniqueness","detail": "Group name 'group 1' already exists in the given account."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|