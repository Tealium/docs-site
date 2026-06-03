---
title: GETユーザーAPI
description: GETユーザーAPIは、アカウントから既存のユーザーを取得します。
url: https://docs.tealium.com/ja/administration/early-access/api/scim-api/get-user-api/
---
## 動作方法

GETメソッドを使用して既存のユーザーを取得します：

```bash
GET /scim/v2/Users/{id}
```

## 認証

すべてのAPI呼び出しにはOAuthベアラートークンが使用され、APIキーは使用されません。

詳細については、[認証]()を参照してください。

## GET操作のパラメータ

このコマンドは以下のパラメータを取ります：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | URLパラメータ | 必須 | ユーザーの一意の識別子。この値はREST API呼び出しの一部として送信されます。|

### cURLリクエストの例

```bash
curl --location --request GET &#39;https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b&#39; \
```

### 応答の例


```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:User&#34;
    ],
    &#34;id&#34;: &#34;913b0182-2531-402f-a302-fcd9d2aeda6a&#34;,
    &#34;userName&#34;: &#34;fullName@tealiumscimdev.onmicrosoft.com&#34;,
    &#34;displayName&#34;: null,
    &#34;externalId&#34;: null,
    &#34;name&#34;: {
        &#34;givenName&#34;: &#34;Given&#34;,
        &#34;familyName&#34;: &#34;Family&#34;
    },
    &#34;emails&#34;: [
        {
            &#34;value&#34;: &#34;fullName@tealiumscimdev.onmicrosoft.com&#34;
        }
    ],
    &#34;active&#34;: true,
    &#34;meta&#34;: {
        &#34;resourceType&#34;: &#34;User&#34;,
        &#34;location&#34;: &#34;/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6a&#34;
    }
}
```


### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;IDの形式が無効です。&#34;}` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;認証に失敗しました。&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;X-Tealium-Accountヘッダーがありません。&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;アカウント{ACCOUNT}にユーザーが見つかりません。&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;このエンドポイントでは許可されていないメソッドです。許可されているメソッド: GET, PUT, DELETE, PATCH.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;拡張機能のjson処理中にエラーが発生しました - アカウント{ACCOUNT}&#34;}`|