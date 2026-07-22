---
title: GETユーザーAPI
description: GETユーザーAPIは、アカウントから既存のユーザーを取得します。
url: https://docs.tealium.com/ja/api/v3/scim-api/get-user-api/
---
## 動作方法

GETメソッドを使用して既存のユーザーを取得します：

```bash
GET /scim/v2/Users/{id}
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## GET操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | ユーザーの一意の識別子。この値はREST API呼び出しの一部として送信されます。|

### cURLリクエストの例

```bash
curl --location --request GET 'https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b' \
```

### 応答の例


```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User"
    ],
    "id": "913b0182-2531-402f-a302-fcd9d2aeda6a",
    "userName": "fullName@tealiumscimdev.onmicrosoft.com",
    "displayName": null,
    "externalId": null,
    "name": {
        "givenName": "Given",
        "familyName": "Family"
    },
    "emails": [
        {
            "value": "fullName@tealiumscimdev.onmicrosoft.com"
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

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "IDの形式が無効です。"}` |
| 401 | `{"returnCode" : 1401 , "message" : "認証に失敗しました。"}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "X-Tealium-Accountヘッダーがありません。"}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "アカウント{ACCOUNT}にユーザーが見つかりません。"}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "このエンドポイントでは許可されていないメソッドです。許可されているメソッド: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "拡張機能のjson処理中にエラーが発生しました - アカウント{ACCOUNT}"}`|