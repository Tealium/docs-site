---
title: iQ ロードルール API
description: iQ ロードルール API を使用すると、iQ タグ管理プロファイル内でロードルールをプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-load-rules-api/
---
この API と利用可能なオブジェクトフィールドについての詳細は、[iQ プロファイル API](https://docs.tealium.com/iq-profiles-v3-api/) および [iQ プロファイルオブジェクト](https://docs.tealium.com/iq-profiles-api-objects/) を参照してください。

## 動作原理

`PATCH` メソッドを使用して、iQ プロファイルオブジェクト内のロードルールを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCH メソッドを使用すると、保存または名前を付けて保存を使用してプロファイルのロードルールをプログラムで変更します。保存後に公開するには、[iQ 公開 API](https://docs.tealium.com/iq-publish-api/) を使用します。

### cURL リクエストの例

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}' \
  --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9' \
  --header 'Content-Type: application/json' \
  --data '
```

## 認証


<blockquote>
Bearer トークンは、すべての API 呼び出しで認証に使用され、API キーは認証呼び出しでのみ使用されます。Bearer トークンに加えて、認証応答には、後続のサーバーサイド API 呼び出しで使用する必要がある地域固有のホスト名が含まれています。
</blockquote>


API キーから Bearer トークンを生成する方法については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/) を参照してください。

## プロファイルフィールド

プロファイルのロードルールは、以下の可能なフィールドを含む JSON オブジェクトです：

|フィールド| タイプ| 必須| 説明|
|---| ---| ---| ---|
|`versionTitle`| 文字列| 任意| 保存されたバージョンのタイトル。<br> `saveType` が `saveAs` の場合のデフォルト: `API \| {TIMESTAMP}`<br> `saveType` が `save` の場合のデフォルト: 既存のバージョンタイトル |
|`saveType`| 文字列| 任意| PATCH リクエストで実行する保存のタイプ: `save` または `saveAs`。デフォルトは `saveAs`。 |
|`notes`| 文字列| 必須| 公開バージョンに関する追加の注記。|
|`op`| 文字列| 必須| 実行する操作: `add`, `replace`, または `remove`。|
|`path`| 文字列| 必須| 更新するコンポーネントタイプと ID の形式: `/loadRules`。|
|`value.object`| 文字列| 必須| 更新されるオブジェクトタイプ: `variable`, `loadRule`, または `extension`。|
|`value.name`| 文字列| 必須 (add/replace の場合)| ロードルールの名前。|
|`value.status`| 文字列| 必須| オン/オフの状態: `active` または `inactive`。|
|`value.notes`| 文字列| 任意| ロードルールに関する注記。|
|`value.startDate`| 日付| `value.endDate` が空の場合は任意。 | スケジュールされたロードルールの開始日。日付形式は `yyyyMMddHHmm`。|
|`value.endDate`| 日付| 任意| スケジュールされたロードルールの終了日。日付形式は `yyyyMMddHHmm`。|
|`value.conditions`| オブジェクトの配列| 必須| 変数名、演算子、値を含むオブジェクトの配列。配列内の各オブジェクトは `and` 演算子で関連付けられ、配列内の各配列は `or` 演算子で関連付けられます。次の演算子は値を受け付けません：<br>`is defined`<br> `is badge assigned`<br> `is badge not assigned`<br> `is not defined`<br> `is not populated` |

### リクエストの例

```json
{
  "versionTitle": "Adding Rule",
  "saveType": "saveAs",
  "notes": "version notes here", 
  "operationList": [
    {
      "op": "add",
      "path": "/loadRules",
      "value":{
        "object": "loadRule",
        "name": "new rule API Dom variable",
        "status": "active",
        "notes": "Load Rule notes here",
        "startDate": "202202020000",
        "endDate": "202202020000",
        "conditions": [
          [
            {
              "variable": "udo.new_name",
              "operator": "does_not_equal",
              "value": 10
            }
          ]
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

例えば、ロードルールを追加するには：

```json
"op" : "add",
"path" : "/loadRules"
```

特定のロードルールを更新するには、パスに ID を追加します：

```json
"op" : "replace",
"path" : "/loadRules/503"
```

## ロードルールの作成

この PATCH メソッドは、プロファイルのロードルールオブジェクトと追加のロードルールフィールドを取ります。

### リクエストの例

```json
{
  "versionTitle": "Adding Rule",
  "saveType": "saveAs",
  "notes": "version notes here", 
  "operationList": [
    {
      "op": "add",
      "path": "/loadRules",
      "value":{
        "object": "loadRule",
        "name": "new rule API Dom variable",
        "status": "active",
        "notes": "Load Rule notes here",
        "startDate": "202202020000",
        "endDate": "202202020000",
        "conditions": [
          [
            {
              "variable": "udo.new_name",
              "operator": "does_not_equal",
              "value": 10
            }
          ]
        ]   
      }
    }
  ] 
}
```

## ロードルールの更新

この PATCH メソッドは、プロファイルのロードルールオブジェクトと追加のロードルールフィールドを取ります。

### リクエストの例

```json
{
  "versionTitle": "Adding Rule",
  "saveType": "saveAs",
  "notes": "version notes here", 
  "operationList": [
    {
      "op": "replace",
      "path": "/loadRules/49",
      "value":{
        "object": "loadRule",
        "name": "new rule API Dom variable",
        "status": "active",
        "notes": "Load Rule notes here",
        "startDate": "202202020000",
        "endDate": "202202020000",
        "conditions": [
          [
            {
              "variable": "udo.new_name",
              "operator": "does_not_equal",
              "value": 10
            }
          ]
        ]   
      }
    }
  ] 
}
```

## ロードルールの削除

この PATCH メソッドは、プロファイルのロードルールオブジェクトと追加のロードルールフィールドを取ります。

### リクエストの例

```json
{
  "versionTitle": "Adding Rule",
  "saveType": "saveAs",
  "notes": "version notes here", 
  "operationList": [
    {
      "op": "remove",
      "path": "/loadRules/49",
      "value":{
        "object": "loadRule"
      }
    }
  ]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

|エラーコード| エラーメッセージ|
|---| ---|
|400|  `"パッチリクエストの検証に失敗しました：%s"`<br>   `"存在しないタグでタグスコープ拡張を構成できません、id: {ID} - {ACCOUNT} \| profile: {PROFILE}"` <br>  `"構成がオンになっていない場合、拡張スコープを同期に構成することはできません - {ACCOUNT} \| profile: {PROFILE}"`<br>   `"次の拡張 ID の取得エラー - {ACCOUNT} \| profile: {PROFILE}"`<br>   `"プロファイルライブラリが古くなっています、パッチングプロファイル前に変更をマージしてください - {ACCOUNT} \| profile: {PROFILE}"` <br>  `"サポートされていません"` <br> `"patchProfile.arg2.notes: 空であってはなりません"` |
| 404 |    `"アカウント: {ACCOUNT}, プロファイル: {PROFILE} が見つかりません"` |
| 409 |  `"同じアカウントを現在閲覧しているユーザー: {ACCOUNT} プロファイル: {PROFILE}"` <br> `プロファイルの保存エラー: {PROFILE} アカウント: {ACCOUNT}, 重複バージョン: {VERSIONS}` |
|500|  `"エラーが発生しました"` <br>  `"プロファイル: {PROFILE} はライブラリプロファイルから継承されています"`<br>   `"リクエストの呼び出しに失敗しました: 不明なホスト、詳細はログを参照してください。"`<br>   `"プロファイルメタデータの保存エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"`<br>   `"プロファイルの保存エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}"`<br>   `"プロファイルの保存エラー(レガシー) - {ACCOUNT} \| プロファイル: {PROFILE}"` |
