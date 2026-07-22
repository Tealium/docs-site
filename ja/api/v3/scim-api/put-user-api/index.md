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

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## PUT操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | ユーザーの一意の識別子。この値はREST API呼び出しの一部として送信されます。 |
| `userName` | オブジェクト | 必須 | ユーザーのユーザー名で、メールアドレス形式です。有効なメールアドレスでなければなりません。APIを通じて`userName`を変更することはできません。|
| `name` | オブジェクト | 任意 | ユーザーの名前を含むリスト。各名前には`givenName`と`familyName`を含むことができます。Nullおよび空の値が許可されます。 |
| `emails` | 配列 | 任意 | この値は`userName`によって自動的に構成されます。 |
| `active` | ブール | 任意 | ユーザーがアクティブかどうかを示します。ユーザーを削除または非アクティブ化しようとしている場合は、[DELETEメソッド](https://docs.tealium.com/delete-user-api/)を使用してください。 |

### 例 cURLリクエスト

```bash
curl -X PUT "https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
  "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User"],
  "userName": "updated.user@example.com",
  "name": {
    "givenName": "Updated",
    "familyName": "User"
  },
  "emails": [{
    "value": "updated.user@example.com"
  }],
  "active": true
}'
```

### 例 応答



```json
{
  "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User"],
  "id": "eb987394-b2b0-4a21-a1d8-7915a91e06b",
  "userName": "updated.user@example.com",
  "name": {
    "givenName": "Updated",
    "familyName": "User"
  },
  "emails": [{
    "value": "updated.user@example.com"
  }],
  "active": true,
  "meta": {
    "resourceType": "User",
    "location": "/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6ab"
  }
}
```


### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "userName must be a valid email address."` |
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "User not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|