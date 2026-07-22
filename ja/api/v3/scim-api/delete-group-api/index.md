---
title: グループ削除API
description: グループ削除APIは、アカウントから既存のグループを削除します。
url: https://docs.tealium.com/ja/api/v3/scim-api/delete-group-api/
---
## 動作方法

既存のグループを削除するにはDELETEメソッドを使用します：

```bash
DELETE /scim/v2/Groups/{id}
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証](https://docs.tealium.com/about-scim-api/#authentication)を参照してください。

## DELETE操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | グループの一意の識別子。この値はREST API呼び出しの一部として送信されます。 |


<blockquote>
組み込みグループ（標準ユーザー、アカウント管理者、ユーザー管理者、プライバシー管理者、技術管理者、プロファイル管理者）は削除できません。組み込みグループの削除を試みるとHTTP 400エラーが返されます。詳細については、[組み込みグループ保護](https://docs.tealium.com/about-scim-api/#built-in-group-protection)を参照してください。
</blockquote>


### cURLリクエストの例

```bash
curl --location --request DELETE 'https://developer.tealiumapis.com/scim/v2/Groups/9d379d2c-2601-42d8-842c-579dc3c58612' \
--header 'Accept: application/scim+json' \
--header 'Authorization: ••••••' \
--header 'Cookie: JSESSIONID=0f9b099a-1284-4e41-89ac-38f72bbff66c'
```

### レスポンスの例

この呼び出しは204ステータスコードを返します。

### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "ID形式が無効です。"}` |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "グループ{uuid}は削除できない組み込みグループです。"}`|
| 401 | `{"returnCode" : 1401 , "message" : "認証に失敗しました。"}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "X-Tealium-Accountヘッダーがありません。"}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "アカウント{ACCOUNT}にグループが見つかりません。"}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "このエンドポイントでは許可されていない方法です。許可されている方法：GET, POST。"}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "拡張のためのjson処理中にエラーが発生しました - アカウント{ACCOUNT}"}`|