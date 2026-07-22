---
title: iQ変数API
description: iQ変数APIを使用すると、iQタグ管理プロファイル内の変数をプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-variables-api/
---
このAPIと利用可能なオブジェクトフィールドについて詳しくは、[iQプロファイルAPI](https://docs.tealium.com/iq-profiles-v3-api/)および[iQプロファイルオブジェクト](https://docs.tealium.com/iq-profiles-api-objects/)を参照してください。

## 動作原理

`PATCH` メソッドを使用して、iQプロファイルオブジェクト内の変数を作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCHメソッドを使用すると、保存または名前を付けて保存を使用してプログラムでプロファイル変数を変更します。APIで変更を加えた後でも、アプリケーションにログインして公開する必要があります。

### cURLリクエストの例

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{account}/profiles/{profile}' \
  --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9' \
  --header 'Content-Type: application/json' \
  --data '
```

## 認証


<blockquote>
Bearerトークンは、すべてのAPI呼び出しを認証するために使用され、APIキーは認証呼び出しでのみ使用されます。Bearerトークンに加えて、認証応答には、後続のサーバーサイドAPI呼び出しで使用する必要がある地域固有のホスト名が含まれています。
</blockquote>


APIキーからBearerトークンを生成する方法については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。

## プロファイルフィールド

プロファイル変数は、以下の可能なフィールドを含むJSONオブジェクトです：

|フィールド| タイプ| 必須| 説明|
|---| ---| ---| ---|
|`versionTitle`| 文字列| 任意| 保存されたバージョンのタイトル。<br> `saveType`が`saveAs`の場合のデフォルト: `API \| {TIMESTAMP}`<br> `saveType`が`save`の場合のデフォルト: 既存のバージョンタイトル |
|`saveType`| 文字列| 任意| PATCHリクエストで実行する保存のタイプ: `save`または`saveAs`。デフォルトは`saveAs`です。 |
|`notes`| 文字列| 必須| 公開バージョンに関する追加の注記。|
|`operationList`| 配列| 必須| 操作オブジェクトのリスト。例えば、複数の変数。|
|`op`| 文字列| 必須| 実行する操作: `add`、`replace`、または`remove`。|
|`path`| 文字列| 必須| 更新するコンポーネントタイプとIDの形式:`/variables`。|
|`value.object`| 文字列| 必須| 更新されるオブジェクトタイプ: `variable`または`extension`。|
|`value.name`| 文字列| 必須（add/replaceの場合）| 変数のタイトル。|
|`value.alias`| 文字列| 必須| 変数名。|
|`value.type`| 文字列| 必須| 変数タイプを表すプレフィックス。<br> `ls` - ローカル保存 <br> `ss` - セッション保存 <br> `udo` - ユニバーサルデータオブジェクト<br> `qp` - クエリ文字列パラメータ<br> `cp` - クッキー<br> `js_page` - JavaScript変数<br> `meta` - メタデータ要素<br> `va` - AudienceStream属性（読み取り専用。このタイプは他のiQプロファイルAPI要素で使用できますが、APIを使用して作成することはできません。）|
|`value.notes`| 文字列| 任意| 変数に関する注記。|

### リクエストの例

```json
{
  "versionTitle":"Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"add",
      "path":"/variables",
      "value":{
        "object": "variable",
        "name": "page_type",
        "alias": "Page Type",
        "type": "udo",
        "notes":"udo variable"
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-variables-api"]
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
"op" : "add",
"path" : "/variables"

```

特定の変数を更新するには、パスにIDを追加します：

```json
"op" : "replace",
"path" : "/variables/503"
```

## 変数の作成

このPATCHメソッドは、プロファイル変数オブジェクトと追加の変数フィールドを取ります。

### リクエストの例

```json
{
  "versionTitle":"Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"add",
      "path":"/variables",
      "value":{
        "object": "variable",
        "name": "page_type",
        "alias": "Page Type",
        "type": "udo",
        "notes":"udo variable"
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-variables-api"]
}
```

## 変数の更新

このPATCHメソッドは、プロファイル変数オブジェクトと追加の変数フィールドを取ります。

### リクエストの例

```json
{
  "versionTitle":"Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"replace",
      "path":"/variables/503",
      "value":{
        "object": "variable",
        "name": "page_type",
        "alias": "Page Type",
        "type": "udo",
        "notes":"udo variable"
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-variables-api"]
}
```

## 変数の削除

このPATCHメソッドは、プロファイル変数オブジェクトと追加の変数フィールドを取ります。

### リクエストの例

```json
{
  "versionTitle":"Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"remove",
      "path":"/variables/503",
      "value":{
        "object": "variable"
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-variables-api"]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

|エラーコード| エラーメッセージ|
|---| ---|
|400|  `"プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| プロファイル: {PROFILE}"` <br>  `"変数の検証に失敗しました - variableId: {VARIABLE_ID} \| {ACCOUNT} \| プロファイル: {PROFILE}. 原因: {CAUSE}"` <br>  `"patchProfile.arg2.notes: 空であってはなりません"` |
|404|  `"プロファイルが見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>  `"プロファイルライブラリが見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"`<br>   `"プロファイル（レガシー）が見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>  `"同じアカウントを現在閲覧しているユーザー: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>  `"最新バージョンが見つかりません - {ACCOUNT} \| プロファイル: {PROFILE}"` |
|409|  `"プロファイルの保存エラー: {PROFILE} アカウント: {ACCOUNT}, 重複バージョン: {VERSION}"` |
|500|  `"プロファイル: {PROFILE} はライブラリプロファイルから継承されています"`<br>   `"プロファイルメタデータの保存エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>  `"プロファイルの保存エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>  `"プロファイルの保存エラー(レガシー) - {ACCOUNT} \| プロファイル: {PROFILE}"` |
