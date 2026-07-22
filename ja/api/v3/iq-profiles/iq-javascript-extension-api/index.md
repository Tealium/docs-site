---
title: iQ JavaScript 拡張 API
description: iQ JavaScript 拡張 API を使用すると、iQ タグ管理プロファイルで JavaScript コード拡張をプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-javascript-extension-api/
---
この API および利用可能なオブジェクトフィールドについての詳細は、[iQ プロファイル API](https://docs.tealium.com/iq-profiles-v3-api/) および [iQ プロファイルオブジェクト](https://docs.tealium.com/iq-profiles-api-objects/) を参照してください。

## 動作原理

iQ プロファイルは JSON オブジェクトを使用して iQ タグ管理アカウントプロファイルからデータを取得し、基本的な JavaScript コード拡張を更新します。これにより、カスタムコード展開プロセスを使用して iQ タグ管理プロファイルを管理できます。

`PATCH` メソッドを使用して、iQ プロファイルオブジェクト内のコンポーネントを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCH メソッドを使用すると、保存または名前を付けて保存を使用してプログラムでプロファイル構成を変更します。API を使用して変更を加えた後でも、アプリケーションにログインして公開する必要があります。

### cURL リクエストの例

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}' \
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9' \
--header 'Content-Type: application/json' \
--data-raw '
```

## 認証


<blockquote>
Bearer トークンは、すべての API 呼び出しを認証するために使用され、API キーは認証呼び出しでのみ使用されます。Bearer トークンに加えて、認証応答には、後続のサーバーサイド API 呼び出しで使用する必要がある地域固有のホスト名が含まれています。
</blockquote>


API キーから Bearer トークンを生成する方法については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/) を参照してください。

## プロファイルフィールド

プロファイルは、次の可能なフィールドを含む JSON オブジェクトです：

|フィールド| タイプ| 必須| 説明|
|---| ---| ---| ---|
|`versionTitle`| 文字列| 任意| 保存されたバージョンのタイトル。<br> `saveType` が `saveAs` の場合のデフォルト: `API \| {TIMESTAMP}`<br> `saveType` が `save` の場合のデフォルト: 既存のバージョンタイトル。 |
|`saveType`| 文字列| 任意| PATCH リクエストで実行する保存のタイプ: `save` または `saveAs`。デフォルトは `saveAs`。 |
|`notes`| 文字列| 必須| 公開バージョンに関する追加のノート。|
|`operationList`| 配列| 必須| 操作オブジェクトのリスト。例えば、複数の JavaScript 拡張。|
|`op`| 文字列| 必須| 実行する操作: `add`, `replace`, `remove`。|
|`path`| 文字列| 必須| 更新するコンポーネントタイプと ID の形式: `/{TYPE}/{ID}`。|
|`value.object`| 文字列| 必須| 更新されるオブジェクトタイプ: `variable` または `extension`。|
|`value.name`| 文字列| 必須 (add/replace の場合)| コンポーネントのタイトル。|
|`value.notes`| 文字列| 任意| コンポーネントに関する追加のノート。|
|`value.type`| 文字列| 必須 (拡張の場合)| 追加する拡張のタイプ。|
|`value.scope`| 文字列| 任意| 拡張のスコープ名、またはタグスコープ拡張の場合はタグ ID のカンマ区切りリスト。<br> `Before Load Rules`<br> `After Load Rules`<br> `DOM Ready`<br> `Tag Scoped Extensions`<br> `After Tag Extensions` |
|`value.occurrence`| 文字列| 任意| ページロードごとに JavaScript コード拡張が実行される回数。値: `Run Once` または `Run Always`。デフォルト: `Run Always`。 |
|`value.status`| 文字列| 任意| コンポーネントのオン/オフ状態: `active` または `inactive`。<br> デフォルト: `active`|
|`value.selectedTargets`| マップ &lt;string, Boolean&gt;|  任意 |  コンポーネントを公開する環境のオブジェクト：<br> `{   "prod" : true\|false,   "qa" : true\|false,   "dev" : true\|false }` デフォルト: すべての環境が `true` に構成されています。 |
|`value.conditions`| 配列[オブジェクト]| 任意 | 拡張の条件オブジェクトで、変数、オペレータ、値が含まれます。PATCH リクエストに条件を含めない場合でも、プロファイルに条件が存在する場合、リクエストは `remove` アクションと見なされます。|
| `value.configuration` | 配列[オブジェクト]|  必須 |  コンポーネントの構成オブジェクト。このオブジェクトはコンポーネントのタイプごとに異なります。この配列フィールドには1つのオブジェクトのみが許可されます。例: `{   name: “code”   value: “JSON-escaped JavaScript code here” }` |

### 例のリクエスト

```json
{
  "versionTitle":"Version 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"add",
      "path":"/extensions",
      "value":{
        "object": "extension",
        "name": "My extension",
        "notes": "extension notes here",
        "type": "Javascript Code",
        "scope": "After Load Rules",
        "occurence": "Run Always",
        "status": "active",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "conditions": [
          [
            {
              "variable": "va.badges.30",
              "operator": "is_badge_assigned",
              "value": ""
            }
          , "/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api"]
        ],
        "configuration": [
          {
            "name": "code",
            "value": "b.page_name ||= \"Generic Page\";"
          }
        , "/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api"]
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api"]
}
```

## PATCH 操作パラメータ

`POST`、`PUT`、`DELETE` メソッドの代わりに、`PATCH` メソッドは `op` パラメータを使用して実行するアクションを指定します。

`op` パラメータは次の値をサポートします：

* `add` - コンポーネントを作成します。
* `replace` - コンポーネントを更新します。
* `remove` - コンポーネントを削除します。

コンポーネントのタイプと ID を指定するには、`path` パラメータを使用します。`path` パラメータの形式は `/{TYPE}/{ID}` です。

例えば、拡張を追加するには：

```json
"op" : "add",
"path" : "/extensions"

```

特定の拡張を更新するには、ID をパスに追加します：

```json
"op" : "replace",
"path" : "/extensions/503"
```

## 拡張を作成する

この PATCH メソッドはプロファイルオブジェクトと追加の拡張フィールドを取ります。

### 例のリクエスト

```json
{
  "versionTitle":"Version 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"add",
      "path":"/extensions",
      "value":{
        "object": "extension",
        "name": "Lowercase extension",
        "notes": "extension notes here",
        "type": "Lower-Casing",
        "scope": "After Load Rules",
        "occurence": "Run Always",
        "status": "active",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "configuration":[
          {
           "all": true,
           "lower_case_arrays": "true",
            "constructor": "",
            "initialize": ""
          }
        , "/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api"]
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api"]
}
```

## 拡張を更新する

この PATCH メソッドはプロファイルオブジェクトと追加の拡張フィールドを取ります。

### 例のリクエスト

```json
{
  "versionTitle":"Version 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"replace",
      "path":"/extensions",
      "value":{
        "object": "extension/86",
        "name": "Lowercase extension",
        "notes": "extension notes here",
        "type": "Lower-Casing",
        "scope": "After Load Rules",
        "occurence": "Run Always",
        "status": "active",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "configuration":[
          {
           "all": true,
           "lower_case_arrays": "true",
            "constructor": "",
            "initialize": ""
          }
        , "/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api"]
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api"]
}
```

## 拡張を削除する

この PATCH メソッドはプロファイルオブジェクトと追加の拡張フィールドを取ります。
### 例のリクエスト

```json
{
  "versionTitle":"Version 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"remove",
      "path":"/extensions/86",
      "value":{
        "object": "extension",
      }
    }
  , "/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api"]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ:

|エラーコード| エラーメッセージ|
|---| ---|
|400| `"Validate patch request failed due to unsupported extension type {TYPE}"`<br>    `"Unsupported extension type {TYPE}"`<br>    `"Validate patch request failed due to %s"`<br>    `"Cannot set tag scope extension with tags that do not exist, id: {ID} - {ACCOUNT} \| profile: {PROFILE}"`<br>    `"Cannot set extension scope to sync if the setting is not turned on - {ACCOUNT} \| profile: {PROFILE}"` <br>   `"Error in getting next extension id - {ACCOUNT} \| profile: {PROFILE}"`<br>    `"Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}"` <br>  `"patchProfile.arg2.notes: must not be empty"` |
| 404 |  `"Extension validation failed - extensionId: {ID} \| account: {ACCOUNT} \| profile: {PROFILE}. Cause: not found"` <br>    `"Extension ID {ID} not found in the profile {PROFILE}"`<br>    `"Account: {ACCOUNT}, profile: {PROFILE} not found"` |
| 409 |  `"Conflict with profile extension: _id: {ID}, extType: {EXT_TYPE}, title: {TITLE}"` <br>  `"Users are currently viewing the same account: {ACCOUNT} profile: {PROFILE}"`<br>   `"Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSIONS}"`  |
|500|  `"An error occurred"` <br>   `"Profile: {PROFILE} inherits from library profile"`<br>    `"Unable to invoke request: unknown host, see logs for more detail."`<br>    `"Error processing json for extension - account: {ACCOUNT} \| profile: {PROFILE}"` <br>   `"Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}"`<br>    `"Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}"` <br>   `"Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}"` |