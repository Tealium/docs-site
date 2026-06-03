---
title: グループ削除API
description: グループ削除APIは、アカウントから既存のグループを削除します。
url: https://docs.tealium.com/ja/administration/early-access/api/scim-api/delete-group-api/
---
## 動作方法

既存のグループを削除するにはDELETEメソッドを使用します：

```bash
DELETE /scim/v2/Groups/{id}
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証]()を参照してください。

## DELETE操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | グループの一意の識別子。この値はREST API呼び出しの一部として送信されます。 |

組み込みグループ（標準ユーザー、アカウント管理者、ユーザー管理者、プライバシー管理者、技術管理者、プロファイル管理者）は削除できません。組み込みグループの削除を試みるとHTTP 400エラーが返されます。詳細については、[組み込みグループ保護]()を参照してください。

### cURLリクエストの例

```bash
curl --location --request DELETE &#39;https://developer.tealiumapis.com/scim/v2/Groups/9d379d2c-2601-42d8-842c-579dc3c58612&#39; \
--header &#39;Accept: application/scim&#43;json&#39; \
--header &#39;Authorization: ••••••&#39; \
--header &#39;Cookie: JSESSIONID=0f9b099a-1284-4e41-89ac-38f72bbff66c&#39;
```

### レスポンスの例

この呼び出しは204ステータスコードを返します。

### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;ID形式が無効です。&#34;}` |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;グループ{uuid}は削除できない組み込みグループです。&#34;}`|
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;認証に失敗しました。&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;X-Tealium-Accountヘッダーがありません。&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;アカウント{ACCOUNT}にグループが見つかりません。&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;このエンドポイントでは許可されていない方法です。許可されている方法：GET, POST。&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;拡張のためのjson処理中にエラーが発生しました - アカウント{ACCOUNT}&#34;}`|