---
title: iQ変数API
description: iQ変数APIを使用すると、iQタグ管理プロファイル内の変数をプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-variables-api/
---
このAPIと利用可能なオブジェクトフィールドについて詳しくは、[iQプロファイルAPI]()および[iQプロファイルオブジェクト]()を参照してください。

## 動作原理

`PATCH` メソッドを使用して、iQプロファイルオブジェクト内の変数を作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCHメソッドを使用すると、保存または名前を付けて保存を使用してプログラムでプロファイル変数を変更します。APIで変更を加えた後でも、アプリケーションにログインして公開する必要があります。

### cURLリクエストの例

```bash
curl --location --request PATCH &#39;https://platform.tealiumapis.com/v3/tiq/accounts/{account}/profiles/{profile}&#39; \
  --header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39; \
  --header &#39;Content-Type: application/json&#39; \
  --data &#39;
```

## 認証

Bearerトークンは、すべてのAPI呼び出しを認証するために使用され、APIキーは認証呼び出しでのみ使用されます。Bearerトークンに加えて、認証応答には、後続のサーバーサイドAPI呼び出しで使用する必要がある地域固有のホスト名が含まれています。

APIキーからBearerトークンを生成する方法については、[認証]()を参照してください。

## プロファイルフィールド

プロファイル変数は、以下の可能なフィールドを含むJSONオブジェクトです：

|フィールド| タイプ| 必須| 説明|
|---| ---| ---| ---|
|`versionTitle`| 文字列| 任意| 保存されたバージョンのタイトル。&lt;br&gt; `saveType`が`saveAs`の場合のデフォルト: `API \| {TIMESTAMP}`&lt;br&gt; `saveType`が`save`の場合のデフォルト: 既存のバージョンタイトル |
|`saveType`| 文字列| 任意| PATCHリクエストで実行する保存のタイプ: `save`または`saveAs`。デフォルトは`saveAs`です。 |
|`notes`| 文字列| 必須| 公開バージョンに関する追加の注記。|
|`operationList`| 配列| 必須| 操作オブジェクトのリスト。例えば、複数の変数。|
|`op`| 文字列| 必須| 実行する操作: `add`、`replace`、または`remove`。|
|`path`| 文字列| 必須| 更新するコンポーネントタイプとIDの形式:`/variables`。|
|`value.object`| 文字列| 必須| 更新されるオブジェクトタイプ: `variable`または`extension`。|
|`value.name`| 文字列| 必須（add/replaceの場合）| 変数のタイトル。|
|`value.alias`| 文字列| 必須| 変数名。|
|`value.type`| 文字列| 必須| 変数タイプを表すプレフィックス。&lt;br&gt; `ls` - ローカル保存 &lt;br&gt; `ss` - セッション保存 &lt;br&gt; `udo` - ユニバーサルデータオブジェクト&lt;br&gt; `qp` - クエリ文字列パラメータ&lt;br&gt; `cp` - クッキー&lt;br&gt; `js_page` - JavaScript変数&lt;br&gt; `meta` - メタデータ要素&lt;br&gt; `va` - AudienceStream属性（読み取り専用。このタイプは他のiQプロファイルAPI要素で使用できますが、APIを使用して作成することはできません。）|
|`value.notes`| 文字列| 任意| 変数に関する注記。|

### リクエストの例

```json
{
  &#34;versionTitle&#34;:&#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;add&#34;,
      &#34;path&#34;:&#34;/variables&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;variable&#34;,
        &#34;name&#34;: &#34;page_type&#34;,
        &#34;alias&#34;: &#34;Page Type&#34;,
        &#34;type&#34;: &#34;udo&#34;,
        &#34;notes&#34;:&#34;udo variable&#34;
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-variables-api&#34;]
}
```

## PATCH操作パラメータ

`POST`、`PUT`、`DELETE`メソッドの代わりに、`PATCH`メソッドは`op`パラメータを使用して実行するアクションを指定します。

`op`パラメータは次の値をサポートしています：

* `add` - コンポーネントを作成します。
* `replace` - コンポーネントを更新します。
* `remove` - コンポーネントを削除します。

コンポーネントのタイプとIDを指定するには、`path`パラメータを使用します。`path`パラメータの形式は`/{TYPE}/{ID}`です。

例えば、変数を追加するには：

```json
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/variables&#34;

```

特定の変数を更新するには、パスにIDを追加します：

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/variables/503&#34;
```

## 変数の作成

このPATCHメソッドは、プロファイル変数オブジェクトと追加の変数フィールドを取ります。

### リクエストの例

```json
{
  &#34;versionTitle&#34;:&#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;add&#34;,
      &#34;path&#34;:&#34;/variables&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;variable&#34;,
        &#34;name&#34;: &#34;page_type&#34;,
        &#34;alias&#34;: &#34;Page Type&#34;,
        &#34;type&#34;: &#34;udo&#34;,
        &#34;notes&#34;:&#34;udo variable&#34;
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-variables-api&#34;]
}
```

## 変数の更新

このPATCHメソッドは、プロファイル変数オブジェクトと追加の変数フィールドを取ります。

### リクエストの例

```json
{
  &#34;versionTitle&#34;:&#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;replace&#34;,
      &#34;path&#34;:&#34;/variables/503&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;variable&#34;,
        &#34;name&#34;: &#34;page_type&#34;,
        &#34;alias&#34;: &#34;Page Type&#34;,
        &#34;type&#34;: &#34;udo&#34;,
        &#34;notes&#34;:&#34;udo variable&#34;
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-variables-api&#34;]
}
```

## 変数の削除

このPATCHメソッドは、プロファイル変数オブジェクトと追加の変数フィールドを取ります。

### リクエストの例

```json
{
  &#34;versionTitle&#34;:&#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;remove&#34;,
      &#34;path&#34;:&#34;/variables/503&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;variable&#34;
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-variables-api&#34;]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

|エラーコード| エラーメッセージ|
|---| ---|
|400|  `&#34;プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| プロファイル: {PROFILE}&#34;` &lt;br&gt;  `&#34;変数の検証に失敗しました - variableId: {VARIABLE_ID} \| {ACCOUNT} \| プロファイル: {PROFILE}. 原因: {CAUSE}&#34;` &lt;br&gt;  `&#34;patchProfile.arg2.notes: 空であってはなりません&#34;` |
|404|  `&#34;プロファイルが見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}&#34;` &lt;br&gt;  `&#34;プロファイルライブラリが見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}&#34;`&lt;br&gt;   `&#34;プロファイル（レガシー）が見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}&#34;` &lt;br&gt;  `&#34;同じアカウントを現在閲覧しているユーザー: {ACCOUNT} \| プロファイル: {PROFILE}&#34;` &lt;br&gt;  `&#34;最新バージョンが見つかりません - {ACCOUNT} \| プロファイル: {PROFILE}&#34;` |
|409|  `&#34;プロファイルの保存エラー: {PROFILE} アカウント: {ACCOUNT}, 重複バージョン: {VERSION}&#34;` |
|500|  `&#34;プロファイル: {PROFILE} はライブラリプロファイルから継承されています&#34;`&lt;br&gt;   `&#34;プロファイルメタデータの保存エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}&#34;` &lt;br&gt;  `&#34;プロファイルの保存エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}&#34;` &lt;br&gt;  `&#34;プロファイルの保存エラー(レガシー) - {ACCOUNT} \| プロファイル: {PROFILE}&#34;` |
