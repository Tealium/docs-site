---
title: PATCH ユーザー API
description: PATCH ユーザー API は既存のユーザーを更新します。
url: https://docs.tealium.com/ja/api/v3/scim-api/patch-user-api/
---
## 動作方法

既存のユーザーを更新するには、PATCH メソッドを使用します：

```bash
PATCH /scim/v2/Users/{id}
```

## 認証

すべての API 呼び出しには OAuth ベアラートークンが使用され、API キーは使用されません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## PATCH 操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | ユーザーの一意の識別子。この値は REST API 呼び出しの一部として送信されます。|
| `op` | 文字列 | 任意 | 実行する操作。サポートされる値は `add`、`replace`、`remove` です。 |
| `path` | 文字列 | 任意 | 操作の対象を指定する属性パス。省略された場合、操作はリソース全体に対して実行されます。 |
| `active` | ブール値 | 任意 | ユーザーがアクティブかどうか。このパラメータは削除できません。`false` に構成するには `replace` 操作を使用します。 |
| `displayName` | 文字列 | 任意 | ユーザーの表示名。 |
| `externalId` | 文字列 | 任意 | ユーザーの外部 ID。 |
| `name.givenName` | 文字列 | 任意 | ユーザーの名。 |
| `name.familyName` | 文字列 | 任意 | ユーザーの姓。 |

`userName` は変更できません。

### 例 cURL リクエスト

#### Microsoft Entra ID

```bash
curl -X PATCH "https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"
    ],
    "Operations": [
        {
            "op": "replace",
            "path": "active",
            "value": "false"
        }
    , "/ja/early-access/api/scim-api/patch-user-api"]
}'
```

#### Okta

```bash
curl -X PATCH "https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
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
                "active": false
            }
        }
    , "/ja/early-access/api/scim-api/patch-user-api"]
}'
```

### 例応答

この呼び出しは 204 ステータスコードを返します。

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "User payload is required."}` |
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "User not found in account {ACCOUNT}."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|