---
title: PUT グループ API
description: PUT グループ API はアカウント内の既存のグループを置き換えます。
url: https://docs.tealium.com/ja/api/v3/scim-api/put-group-api/
---
## 動作方法

PUT メソッドを使用して既存のグループを置き換えます：

```bash
PUT /scim/v2/Groups/{id}
```

## 認証

すべての API 呼び出しには OAuth ベアラートークンが使用され、API キーは使用されません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## PUT 操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | グループの一意の識別子。この値は REST API 呼び出しの一部として送信されます。 |
| `displayName` | 文字列 | 必須 | グループの名前。文字、数字、およびスペースのみを使用してください。名前は 63 文字を超えることはできません。 |
| `members` | 配列 | 任意 | グループ内のメンバーのリスト。各メンバーは `value`、`type`、`display`、`$ref` を含むことができます。 |


<blockquote>
組み込みグループの名前は変更できず、カスタムグループは組み込みグループと同じ名前を持つことはできません。詳細については、を参照してください。
</blockquote>


### cURL リクエストの例

```bash
curl -X PUT "https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:Group"
    ],
    "displayName": "Group 1",
    "id": "3268d9ce-54a2-4758-a19c-beb2b47059d3",
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
    , "/ja/early-access/api/scim-api/put-group-api"]
}'
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

このエンドポイントに関する潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "グループ名 (%very long name with symbols%) に特殊文字を含めることはできず、63文字を超えることはできません。"}` |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "組み込みグループ 'Standard User' の名前を変更することはできません。組み込みグループの名前は変更不可です。"}`|
| 401 | `{"returnCode" : 1401 , "message" : "認証に失敗しました。"}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "X-Tealium-Account ヘッダーがありません。"}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "アカウント {ACCOUNT} にグループが見つかりません。"}`|
| 404 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "アカウント {ACCOUNT} にユーザー UUID {uuid} が見つかりません。"}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "このエンドポイントでは許可されていない方法です。許可されている方法：GET, PUT, DELETE, PATCH."}`|
| 409 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "409","scimType": "uniqueness","detail": "アカウント accounttest に 'grouptest' というグループ名が既に存在します。"}` |
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "拡張機能の json 処理中にエラーが発生しました - アカウント {ACCOUNT}"}`|