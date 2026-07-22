---
title: GET グループ API
description: GET グループ API はアカウントから既存のグループを取得します。
url: https://docs.tealium.com/ja/api/v3/scim-api/get-group-api/
---
## 動作方法

既存のグループを取得するには GET メソッドを使用します：

```bash
GET /scim/v2/Groups/{id}
```

## 認証

すべての API 呼び出しには OAuth ベアラートークンが使用され、API キーは使用されません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## GET 操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | グループの一意の識別子。この値は REST API 呼び出しの一部として送信されます。|

### cURL リクエストの例

```bash
curl --location --request GET 'https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b' \
```

### 応答の例


```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:Group"
    ],
    "id": "9d379d2c-2601-42d8-842c-579dc3c58612",
    "displayName": "Group 1",
    "members": [
        {
            "value": "298273b4-74a3-4150-aa0b-e308bbcbf06b",
            "type": "User",
            "display": "user1@example.com",
            "$ref": "/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf06b"
        },
        {
            "value": "33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb",
            "type": "User",
            "display": "user2@example.com",
            "$ref": "/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb"
        }
    ],
    "meta": {
        "resourceType": "Group",
        "location": "/scim/v2/Groups/9d379d2c-2601-42d8-842c-579dc3c58612"
    }
}
```


### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "IDの形式が無効です。"}` |
| 401 | `{"returnCode" : 1401 , "message" : "認証に失敗しました。"}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "X-Tealium-Account ヘッダーがありません。"}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "アカウント {ACCOUNT} にグループが見つかりません。"}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "このエンドポイントでは許可されていないメソッドです。許可されているメソッド: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "拡張機能の json 処理中にエラーが発生しました - アカウント {ACCOUNT}"}`|