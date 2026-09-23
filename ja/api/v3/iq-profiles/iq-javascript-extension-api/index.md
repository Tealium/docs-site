---
title: iQ JavaScript 拡張 API
description: iQ JavaScript 拡張 API を使用すると、タグ管理プロファイルで JavaScript コード拡張をプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-javascript-extension-api/
---
この API と利用可能なオブジェクトフィールドについて詳しくは、[iQ プロファイル API](https://docs.tealium.com/iq-profiles-v3-api/) および [iQ プロファイルオブジェクト](https://docs.tealium.com/iq-profiles-api-objects/) を参照してください。

## 動作原理

iQ プロファイルは JSON オブジェクトを使用してタグ管理アカウントプロファイルからデータを取得し、[JavaScript コード拡張](https://docs.tealium.com/javascript-code-extension/)を更新します。このエンドポイントを使用して、タグ管理プロファイルを通じてカスタムコードをデプロイします。


<blockquote>
サポートされているのは [JavaScript コード拡張](https://docs.tealium.com/javascript-code-extension/) のみです。このエンドポイントでは、高度な JavaScript コード拡張やその他のタイプの拡張を管理することはできません。
</blockquote>


`PATCH` メソッドを使用して、iQ プロファイルオブジェクト内のコンポーネントを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCH メソッドを使用すると、保存または名前を付けて保存を使用してプログラムでプロファイル構成を変更します。保存後に公開するには、[iQ 公開 API](https://docs.tealium.com/iq-publish-api/) を使用します。

### cURL リクエストの例

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}' \
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9' \
--header 'Content-Type: application/json' \
--data-raw
```

## 認証


<blockquote>
すべての API 呼び出しにはベアラートークンが使用され、API キーは認証呼び出しでのみ使用されます。ベアラートークンに加えて、認証応答には後続のサーバーサイド API 呼び出しで使用する必要がある地域固有のホスト名が含まれています。
</blockquote>


API キーからベアラートークンを生成する方法については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/) を参照してください。

## プロファイルフィールド

プロファイルは以下の可能なフィールドを含む JSON オブジェクトです：

|フィールド| タイプ| 必須| 説明|
|---| ---| ---| ---|
|`versionTitle`| 文字列| オプション| 保存されたバージョンのタイトル。<br> `saveType` が `saveAs` の場合のデフォルト: `API \| {TIMESTAMP}`<br> `saveType` が `save` の場合のデフォルト: 既存のバージョンタイトル。 |
|`saveType`| 文字列| オプション| PATCH リクエストで実行する保存のタイプ: `save` または `saveAs`。デフォルトは `saveAs`。 |
|`notes`| 文字列| 必須| 公開バージョンに関する追加のノート。|
|`operationList`| 配列| 必須| 操作オブジェクトのリスト。例えば、複数の JavaScript コード拡張。|
|`op`| 文字列| 必須| 実行する操作: `add`, `replace`, `remove`。|
|`path`| 文字列| 必須| 追加するコンポーネントタイプ、または更新するタイプと ID の形式: `/{TYPE}/{ID}`。例えば、`/extensions/12` または `/extensions`。|
|`value.object`| 文字列| 必須| 更新されるオブジェクトタイプ: `variable` または `extension`。|
|`value.name`| 文字列| 必須 (追加/置換の場合)| コンポーネントのタイトル。|
|`value.notes`| 文字列| オプション| コンポーネントに関する追加のノート。|
|`value.type`| 文字列| 必須<br> (拡張の場合)| 追加する拡張のタイプ。サポートされているのは [JavaScript コード拡張](https://docs.tealium.com/javascript-code-extension/) のみです。この値は `Javascript Code` でなければなりません。|
|`value.scope`| 文字列| オプション| 拡張のスコープの名前、またはタグスコープの拡張の場合はタグ ID のカンマ区切りリスト。<br> `Before Load Rules`<br> `After Load Rules`<br> `DOM Ready`<br> `Tag Scoped Extensions`<br> `After Tag Extensions` |
|`value.occurrence`| 文字列| オプション| ページロードごとに JavaScript コード拡張が実行される回数。値: `Run Once` または `Run Always`。デフォルト: `Run Always`。 |
|`value.status`| 文字列| オプション| コンポーネントのオン/オフ状態: `active` または `inactive`。<br> デフォルト: `active`|
|`value.selectedTargets`| マップ &lt;string, Boolean&gt;|  オプション |  コンポーネントを公開する環境のオブジェクト:<br> `{   "prod" : true\|false,   "qa" : true\|false,   "dev" : true\|false }` デフォルト: すべての環境が `true` に構成されています。 |
|`value.conditions`| 配列[オブジェクト]| オプション | 拡張の条件オブジェクトで、変数、オペレータ、値が含まれます。PATCH リクエストに条件を含めない場合でも、プロファイルに条件が存在する場合、リクエストは `remove` アクションと見なされます。|
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
          ]
        ],
        "configuration": [
          {
            "name": "code",
            "value": "b.page_name ||= \"Generic Page\"!!;"
          }
        ]
      }
    }
  ]
}
```

## PATCH 操作パラメータ

`POST`、`PUT`、`DELETE` メソッドの代わりに、`PATCH` メソッドは `op` パラメータを使用して実行するアクションを指定します。

`op` パラメータは次の値をサポートしています：

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
        "name": "Javscript Code extension",
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
        "configuration":[
          {
           "name": "code",
            "value": "b.page_name ||= \"Generic Page\"!!;"
          }
        ]
      }
    }
  ]
}
```

## 拡張を更新する

この PATCH メソッドはプロファイルオブジェクトと追加の拡張フィールドを取ります。
### 例のリクエスト

```json
{
  "versionTitle":"バージョン 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "バージョンのノート",
  "operationList":[
    {
      "op":"replace",
      "path":"/extensions",
      "value":{
        "object": "extension/86",
        "name": "Javscript Code extension",
        "notes": "拡張機能のノート",
        "type": "Javascript Code",
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
           "name": "code",
            "value": "b.page_name ||= \"Generic Page\"!!;"
          }
        ]
      }
    }
  ]
}
```

## 拡張機能の削除

このPATCHメソッドはプロファイルオブジェクトと追加の拡張フィールドを取ります。

### 例のリクエスト

```json
{
  "versionTitle":"バージョン 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "バージョンのノート",
  "operationList":[
    {
      "op":"remove",
      "path":"/extensions/86",
      "value":{
        "object": "extension",
      }
    }
  ]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

|エラーコード| エラーメッセージ|
|---| ---|
|400| `"拡張タイプ {TYPE} がサポートされていないため、パッチリクエストの検証に失敗しました"`<br>    `"サポートされていない拡張タイプ {TYPE}"`<br>    `"パッチリクエストの検証に %s により失敗しました"`<br>    `"存在しないタグでタグスコープ拡張を構成できません、id: {ID} - {ACCOUNT} \| プロファイル: {PROFILE}"`<br>    `"構成がオンになっていない場合、拡張スコープを同期に構成できません - {ACCOUNT} \| プロファイル: {PROFILE}"` <br>   `"次の拡張IDの取得エラー - {ACCOUNT} \| プロファイル: {PROFILE}"`<br>    `"プロファイルライブラリが古くなっています、パッチング前に変更をマージしてください - {ACCOUNT} \| プロファイル: {PROFILE}"` <br>  `"patchProfile.arg2.notes: 空であってはなりません"` |
| 404 |  `"拡張検証に失敗しました - extensionId: {ID} \| アカウント: {ACCOUNT} \| プロファイル: {PROFILE}. 原因: 見つかりません"` <br>    `"拡張ID {ID} がプロファイル {PROFILE} に見つかりません"`<br>    `"アカウント: {ACCOUNT}, プロファイル: {PROFILE} が見つかりません"` |
| 409 |  `"プロファイル拡張との競合: _id: {ID}, extType: {EXT_TYPE}, title: {TITLE}"` <br>  `"同じアカウント: {ACCOUNT} プロファイル: {PROFILE} を現在ユーザーが閲覧しています"`<br>   `"プロファイル: {PROFILE} の保存エラー: アカウント: {ACCOUNT}, 重複するバージョン: {VERSIONS}"`  |
|500|  `"エラーが発生しました"` <br>   `"プロファイル: {PROFILE} はライブラリプロファイルから継承しています"`<br>    `"リクエストを呼び出すことができません: 不明なホスト、詳細はログを参照してください。"`<br>    `"拡張のためのjson処理エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>   `"プロファイルメタデータの保存エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"`<br>    `"プロファイルの保存エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"` <br>   `"プロファイルの保存エラー(レガシー) - {ACCOUNT} \| プロファイル: {PROFILE}"` |