---
title: POSTユーザーAPI
description: POSTユーザーAPIはアカウントに新しいユーザーを作成します。
url: https://docs.tealium.com/ja/api/v3/scim-api/post-user-api/
---
## 動作原理

POSTメソッドを使用して新しいユーザーを作成します：

```bash
POST /scim/v2/Users/
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

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
curl -X POST "https://developer.tealiumapis.com/scim/v2/Users/" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
  "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User"],
  "userName": "user@example.com",
  "name": {
    "givenName": "New",
    "familyName": "User"
  },
  "emails": [{
    "value": "user@example.com"
  }],
  "active": true
}'
```

### 応答の例


```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User"
    ],
    "id": "913b0182-2531-402f-a302-fcd9d2aeda6a",
    "userName": "user@example.com",
    "displayName": null,
    "externalId": null,
    "name": {
        "givenName": "New",
        "familyName": "User"
    },
    "emails": [
        {
            "value": "user@example.com"
        }
    ],
    "active": true,
    "meta": {
        "resourceType": "User",
        "location": "/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6a"
    }
}
```


### エラーメッセージ

このエンドポイントに関する潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "User payload is required."` |
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 409 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "409","scimType": "uniqueness","detail": "User already exists in the given account."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|