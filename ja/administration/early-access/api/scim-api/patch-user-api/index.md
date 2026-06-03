---
title: PATCH ユーザー API
description: PATCH ユーザー API は既存のユーザーを更新します。
url: https://docs.tealium.com/ja/administration/early-access/api/scim-api/patch-user-api/
---
## 動作方法

既存のユーザーを更新するには、PATCH メソッドを使用します：

```bash
PATCH /scim/v2/Users/{id}
```

## 認証

すべての API 呼び出しには OAuth ベアラートークンが使用され、API キーは使用されません。

詳細については、[認証]()を参照してください。

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
curl -X PATCH &#34;https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:api:messages:2.0:PatchOp&#34;
    ],
    &#34;Operations&#34;: [
        {
            &#34;op&#34;: &#34;replace&#34;,
            &#34;path&#34;: &#34;active&#34;,
            &#34;value&#34;: &#34;false&#34;
        }
    , &#34;/ja/early-access/api/scim-api/patch-user-api&#34;]
}&#39;
```

#### Okta

```bash
curl -X PATCH &#34;https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:api:messages:2.0:PatchOp&#34;
    ],
    &#34;Operations&#34;: [
        {
            &#34;op&#34;: &#34;replace&#34;,
            &#34;value&#34;: {
                &#34;active&#34;: false
            }
        }
    , &#34;/ja/early-access/api/scim-api/patch-user-api&#34;]
}&#39;
```

### 例応答

この呼び出しは 204 ステータスコードを返します。

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;User payload is required.&#34;}` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;User not found in account {ACCOUNT}.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|