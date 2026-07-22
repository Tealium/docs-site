---
title: GETユーザーAPI
description: GETユーザーAPIはアカウントからユーザーリストを取得します。
url: https://docs.tealium.com/ja/api/v3/scim-api/get-users-api/
---
## 動作方法

GETメソッドを使用してユーザーリストを取得します：

```bash
GET /scim/v2/Users/
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## GET操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `count` | 数値 | 任意 | 返すレコードの数。最大値は `100` です。 |
| `startIndex` | 数値 | 任意 | インデックスで最初に返すレコード。countがレコード数を超える場合、この値は無視されます。 |
| `filter` | 文字列 | 任意 | ユーザー名に基づいてユーザーをフィルタリングします。同等の値を見つけるために `eq` 演算子を使用します。 |

### 例のcURLリクエスト

```bash
curl -H 'Authorization: Bearer {token}' \
https://developer.tealiumapis.com/scim/v2/Users?startIndex=1&count=10&filter=userName%20eq%20%22user@example.com%22
```

### 例のレスポンス



```json
{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:ListResponse"
    ],
    "totalResults": 1,
    "startIndex": 1,
    "itemsPerPage": 1,
    "Resources": [
        {
            "schemas": [
                "urn:ietf:params:scim:schemas:core:2.0:User"
            ],
            "id": "913b0182-2531-402f-a302-fcd9d2aeda6a",
            "userName": "test.userxz1@example.com",
            "displayName": null,
            "externalId": null,
            "name": {
                "givenName": "Test",
                "familyName": "User"
            },
            "emails": [
                {
                    "value": "test.userxz1@example.com"
                }
            ],
            "active": true,
            "meta": {
                "resourceType": "User",
                "location": "/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6a"
            }
        }
    ]
}
```


### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "{parameter} must be a number."` |
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|