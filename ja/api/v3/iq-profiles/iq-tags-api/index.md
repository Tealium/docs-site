---
title: iQ タグ API
description: iQ タグ API を使用すると、iQ タグ管理プロファイルでタグ構成をプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-tags-api/
---
この API と利用可能なオブジェクトフィールドについて詳しくは、[iQ プロファイル API](https://docs.tealium.com/iq-profiles-v3-api/) および [iQ プロファイルオブジェクト](https://docs.tealium.com/iq-profiles-api-objects/) を参照してください。

## 動作原理

`PATCH` メソッドを使用して、iQ プロファイルオブジェクトのコンポーネントを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCH メソッドを使用すると、保存または名前を付けて保存を使用してプロファイルタグをプログラムで変更します。API を使用して変更した後でも、アプリケーションにログインして公開する必要があります。

### cURL リクエストの例

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}' \
  --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9'  \
  --header 'Content-Type: application/json' \
  --data '
```

## 認証


<blockquote>
Bearer トークンは、すべての API 呼び出しを認証するために使用され、API キーは認証呼び出しでのみ使用されます。Bearer トークンに加えて、認証応答には、後続のサーバーサイド API 呼び出しで使用する必要がある地域固有のホスト名が含まれています。
</blockquote>


API キーから Bearer トークンを生成する方法については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/) を参照してください。

## プロファイルフィールド

プロファイルタグは、以下の可能なフィールドを含む JSON オブジェクトです：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `versionTitle` | 文字列 | 任意 | 結果として保存されるバージョンのタイトル。<br>デフォルトで `saveType` が `saveAs` に構成されている場合: `API \| {TIMESTAMP}`<br>デフォルトで `saveType` が `save` に構成されている場合: 既存のバージョンタイトル |
| `saveType` | 文字列 | 任意 | PATCH リクエストで実行する保存のタイプ: `save` または `saveAs`。デフォルトは `saveAs`。 |
| `notes` | 文字列| 必須 | 公開バージョンに関する追加の注記。 |
| `operationList` | 配列 | 必須| 操作オブジェクトのリスト。例えば、複数のタグ。|
| `op` | 文字列 | 必須 | 実行する操作: `add`, `replace`, または `remove`。 |
| `path` | 文字列 | 必須| 更新するコンポーネントタイプと ID の形式:`/{TYPE}/{ID}`。 |
| `value.object` | 文字列 | 必須| 更新されるオブジェクトタイプ: `variable`, `extension`, `event`, または `tag`。|
|`value.tagID`| 文字列 |必須 | ユニークなタグテンプレート ID。タグ ID を取得するには GET リクエストを使用します。この値はタグ UID とは異なります。|
| `value.status` | 文字列 | 任意 | オン/オフの状態: `active` または `inactive`。 |
| `value.notes` | 文字列 | 任意 | タグに関する注記。 |
| `value.name` | 文字列 | 必須 (add/replaceの場合)| タグの名前。 |
|`value.selectedTargets`| マップ &lt;string, Boolean&gt;|  任意 |  コンポーネントを公開する環境のオブジェクト。`{   "prod" : true\|false,   "qa" : true\|false,   "dev" : true\|false }` <br>デフォルト: すべての環境が `true` に構成されています。 |
| `value.configuration` |マップ &lt;String, Object&gt; |任意 | ベンダーによって提供されるタグ構成の文字列とオブジェクトのマップ。構成は各タグに固有です。詳細については、タグのドキュメントを参照してください。|
|`value.advancedConfiguration`| オブジェクト |任意 |  タグ構成構成に対応する高度な構成のセット。 <br>`advConfigBundle` — **True** または **False**<br> `advConfigLoadType` — **True** または **False**<br> `advConfigOptOut` — **True**<br> `advConfigSend`— **True** または **False** <br> `advConfigSrc` — テキストフィールド<br> `tagTiming` — **DOM Ready** または **Prioritized** |
|`value.rules`| オブジェクト |任意 | タグに適用または除外するロードルール。|
|`value.dataMappings`| マップ &lt;String, String&gt; |任意 | Tealium IQ 変数とその対応するマップ先、変数名、データタイプを含むオブジェクト。マップされた変数トリガーの特定の形式は、タグ構成の **Data Mappings** 画面で確認できます。|
|`value.dataMappings.variable`| 文字列 |任意 | マップされる変数の名前。|
|`value.dataMappings.type`| 文字列 |任意 | マップされる変数のデータタイプ。このフィールドは次の変数タイプをサポートしています：<br>`ls` - ローカル保存<br>`ss` - セッション保存<br>`udo` - ユニバーサルデータオブジェクト<br>`qp` - クエリ文字列パラメータ<br>`cp` - クッキー<br>`js_page` - JavaScript 変数<br>`dom` - DOM 変数<br>`meta` - メタデータ要素<br>`static.text` - 静的テキスト<br>`static.js` - JavaScript コード|
|`value.dataMappings.mappings`| 文字列または文字列の配列 |任意 | 変数のマップ先。|

### リクエストの例

```json
{
  "versionTitle": "バージョンタイトル",
  "notes": "注記",
  "operationList": [
    {
      "op": "add",
      "path": "/tags",
      "value": {
        "object": "tag",
        "tagId": "7133",
        "status": "active",
        "notes": "タグ追加",
        "name": "7133 タグ Google Analytics",
        "dataMappings": [
          {
            "variable": "variable_name",
            "type": "udo",
            "mappings": ["a1", "a2", "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
          }
        ],
        "selectedTargets": {
          "qa": true,
          "dev": true,
          "prod": true
        },
        "advancedConfiguration": {
          "bundleFlag": true,
          "syncLoadType": false,
          "optout": true,
          "scriptSource": "",
          "sendFlag": false,
          "tagTiming": "Dom Ready"
        },
        "configuration": {
          "tracking_id": "123"
        },
        "rules": {
          "apply": [{"and": [{"or": [{"uid": "2", "type": "loadRule"}]}]}],
          "exclude": [{"and": [{"or": [{"uid": "3", "type": "loadRule"}, {"uid": "2", "type": "loadRule"}]}]}, "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
        }
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
}
```

## PATCH 操作パラメータ

`POST`、`PUT`、`DELETE` メソッドの代わりに、`PATCH` メソッドは `op` パラメータを使用して実行するアクションを指定します。

`op` パラメータは次の値をサポートしています：

*   `add` - コンポーネントを作成します。
*   `replace` - コンポーネントを更新します。
*   `remove` - コンポーネントを削除します。

コンポーネントのタイプと ID を指定するには、`path` パラメータを使用します。`path` パラメータの形式は `/{TYPE}/{ID}` です。

例えば、タグを追加するには：

```json
"op" : "add",
"path" : "/tags"
```

特定のタグを更新するには、パスに ID を追加します：

```json
"op" : "replace",
"path" : "/tags/503"
```

## タグの作成

この PATCH メソッドは、プロファイルオブジェクトと追加のタグフィールドを取ります。

### リクエストの例

```json
{
  "versionTitle": "バージョンタイトル",
  "notes": "注記",
  "operationList": [
    {
      "op": "add",
      "path": "/tags",
      "value": {
        "object": "tag",
        "tagId": "7133",
        "status": "active",
        "notes": "タグ追加",
        "name": "7133 タグ Google Analytics",
        "dataMappings": [
          {
            "variable": "variable_name",
            "type": "udo",
            "mappings": ["a1", "a2", "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
          }
        ],
        "selectedTargets": {
          "qa": true,
          "dev": true,
          "prod": true
        },
        "advancedConfiguration": {
          "bundleFlag": true,
          "syncLoadType": false,
          "optout": true,
          "scriptSource": "",
          "sendFlag": false,
          "tagTiming": "Dom Ready"
        },
        "Configuration": {
          "tracking_id": "123"
        },
        "rules": {
          "apply": [{"and": [{"or": [{"uid": "2", "type": "loadRule"}]}]}],
          "exclude": [{"and": [{"or": [{"uid": "3", "type": "loadRule"}, {"uid": "2", "type": "loadRule"}]}]}, "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
        }
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
}
```

## タグの更新

この PATCH メソッドは、プロファイルオブジェクトと追加のタグフィールドを取ります。
### 例のリクエスト

```json
{
  "versionTitle": "version title",
  "notes": "notes",
  "operationList": [
    {
      "op": "replace",
      "path": "/tags/21",
      "value": {
        "object": "tag",
        "tagId": "7133",
        "status": "active",
        "notes": "adding tag",
        "name": "Replace name by API Google Analytics",
        "dataMappings": [
          {
            "variable": "variable_name",
            "type": "udo",
            "mappings": ["a1", "a2", "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
          }
        ],
        "selectedTargets": {
          "qa": true,
          "dev": true,
          "prod": true
        },
        "advancedConfiguration": {
          "bundleFlag": true,
          "syncLoadType": false,
          "optout": true,
          "scriptSource": "",
          "sendFlag": false,
          "tagTiming": "Dom Ready"
        },
        "Configuration": {
          "tracking_id": "123"
        },
        "rules": {
          "apply": [{"and": [{"or": [{"uid": "2", "type": "loadRule"}]}]}],
          "exclude": [{"and": [{"or": [{"uid": "3", "type": "loadRule"}, {"uid": "2", "type": "loadRule"}]}]}, "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
        }
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
}
```

## タグの削除

このPATCHメソッドはプロファイルオブジェクトと追加のタグフィールドを取ります。

### 例のリクエスト

```json
{
  "versionTitle": "Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes":"",
  "operationList": [
    {
      "op": "remove",
      "path": "/tags/230",
      "value":{
        "object":"tag"
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-tags-api"]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `"プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| profile: {PROFILE}"`<br>`"patchProfile.arg2.notes: 空であってはなりません"`|
| 404 | `"プロファイルが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイルライブラリが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイル（レガシー）が見つかりません - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"同じアカウントを現在他のユーザーが閲覧しています: {ACCOUNT} \| profile: {PROFILE}"`<br>`"最新バージョンが見つかりません - {ACCOUNT} \| profile: {PROFILE}"` |
| 409 | `"プロファイルの保存エラー: {PROFILE} for account: {ACCOUNT}, 重複バージョン: {VERSION}"` |
| 500 | `"プロファイル: {PROFILE} はライブラリプロファイルを継承しています"`<br>`"プロファイルメタデータの保存エラー - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイルの保存エラー - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイル（レガシー）の保存エラー - {ACCOUNT} \| profile: {PROFILE}"`|