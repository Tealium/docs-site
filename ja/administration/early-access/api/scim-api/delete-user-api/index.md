---
title: ユーザー削除API
description: ユーザー削除APIは、アカウントから既存のユーザーを削除します。
url: https://docs.tealium.com/ja/administration/early-access/api/scim-api/delete-user-api/
---
## 動作方法

既存のユーザーを削除するにはDELETEメソッドを使用します：

```bash
DELETE /scim/v2/Users/{id}
```

ユーザーが複数のアカウントに存在する場合、その他のアカウントにはユーザーが残ります。ユーザーが所属する唯一のアカウントから削除された場合、ユーザーはどのアカウントにもアクセスできなくなります。

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証]()を参照してください。

## DELETE操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | ユーザーの一意の識別子。この値はREST API呼び出しの一部として送信されます。 |

### cURLリクエストの例

```bash
curl --location --request DELETE &#39;https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b&#39;
```

### レスポンスの例

この呼び出しは204ステータスコードを返します。

### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;IDの形式が無効です。&#34;}` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;認証に失敗しました。&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;X-Tealium-Accountヘッダーがありません。&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;アカウント{ACCOUNT}にユーザーが見つかりません。&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;このエンドポイントでは許可されていないメソッドです。許可されているメソッド: GET, PUT, DELETE, PATCH.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;拡張のためのjson処理エラー - アカウント{ACCOUNT}&#34;}`|