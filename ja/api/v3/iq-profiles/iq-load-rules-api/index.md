---
title: iQ ロードルール API
description: iQ Variables APIを使用すると、iQタグ管理プロファイル内でロードルールをプログラム的に作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-load-rules-api/
---
このAPIと利用可能なオブジェクトフィールドについて詳しくは、[iQプロファイルAPI](https://docs.tealium.com/iq-profiles-v3-api/)および[iQプロファイルオブジェクト](https://docs.tealium.com/iq-profiles-api-objects/)を参照してください。

## 動作方法

`PATCH` メソッドを使用して、iQプロファイルオブジェクト内のロードルールを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCHメソッドを使用するときは、プログラムを使用してプロファイルのロードルールを変更しています。APIを使用して変更した後でも、アプリケーションにログインして公開する必要があります。

### cURLリクエストの例

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}' \
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

プロファイルロードルールは、以下の可能なフィールドを含むJSONオブジェクトです：

|フィールド| タイプ| 必須| 説明|
|---| ---| ---| ---|
|`versionTitle`| 文字列| 任意| 保存されたバージョンのタイトル。<br> `saveType`が`saveAs`の場合のデフォルト：`API \| {TIMESTAMP}`<br> `saveType`が`save`の場合のデフォルト：既存のバージョンタイトル |
|`saveType`| 文字列| 任意| PATCHリクエストで実行する保存のタイプ：`save`または`saveAs`。デフォルトは`saveAs`です。 |
|`notes`| 文字列| 必須| 公開バージョンに関する追加のノート。|
|`op`| 文字列| 必須| 実行する操作：`add`、`replace`、または`remove`。|
|`path`| 文字列| 必須| 更新するコンポーネントタイプとIDの形式：`/loadRules`。|
|`value.object`| 文字列| 必須| 更新されるオブジェクトタイプ：`variable`、`loadRule`、または`extension`。|
|`value.name`| 文字列| 必須（add/replaceの場合）| ロードルールの名前。|
|`value.status`| 文字列| 必須| オン/オフの状態：`active`または`inactive`。|
|`value.notes`| 文字列| 任意| ロードルールに関するノート。|
|`value.startDate`| 日付| `value.endDate`が空の場合は任意。 | スケジュールされたロードルールの開始日。日付形式は`yyyyMMddHHmm`でなければなりません。|
|`value.endDate`| 日付| 任意| スケジュールされたロードルールの終了日。日付形式は`yyyyMMddHHmm`でなければなりません。|
|`value.conditions`| オブジェクトの配列| 必須| 変数名、オペレータ、値を含むオブジェクトの配列。配列内の各オブジェクトは`and`オペレータで関連付けられ、配列内の各配列は`or`オペレータで関連付けられます。次のオペレータは値を受け付けません：<br>`is defined`<br> `is badge assigned`<br> `is badge not assigned`<br> `is not defined`<br> `is not populated` |

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
          , "/ja/early-access/api/api-v3/iq-profiles/iq-load-rules-api"]
        ]   
      }
    }
  ] 
}
```

## PATCH操作パラメータ

`POST`、`PUT`、`DELETE`メソッドの代わりに、`PATCH`メソッドは`op`パラメータを使用して実行するアクションを指定します。

`op`パラメータは次の値をサポートしています：

* `add` - コンポーネントを作成します。
* `replace` - コンポーネントを更新します。
* `remove` - コンポーネントを削除します。

コンポーネントのタイプとIDを指定するには、`path`パラメータを使用します。`path`パラメータの形式は`/{TYPE}/{ID}`です。

例えば、ロードルールを追加するには：

```json
"op" : "add",
"path" : "/loadRules"
```

特定のロードルールを更新するには、パスにIDを追加します：

```json
"op" : "replace",
"path" : "/loadRules/503"
```

## ロードルールの作成

このPATCHメソッドは、プロファイルロードルールオブジェクトと追加のロードルールフィールドを取ります。

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
          , "/ja/early-access/api/api-v3/iq-profiles/iq-load-rules-api"]
        ]   
      }
    }
  ] 
}
```

## ロードルールの更新

このPATCHメソッドは、プロファイルロードルールオブジェクトと追加のロードルールフィールドを取ります。

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
          , "/ja/early-access/api/api-v3/iq-profiles/iq-load-rules-api"]
        ]   
      }
    }
  ] 
}
```

## ロードルールの削除

このPATCHメソッドは、プロファイルロードルールオブジェクトと追加のロードルールフィールドを取ります。

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
  , "/ja/early-access/api/api-v3/iq-profiles/iq-load-rules-api"]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

|エラーコード| エラーメッセージ|
|---| ---|
|400|  `"Validate patch request failed due to %s"`<br>   `"Cannot set tag scope extension with tags that do not exist, id: {ID} - {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Cannot set extension scope to sync if the setting is not turned on - {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Error in getting next extension id - {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Not Supported"` <br> `"patchProfile.arg2.notes: must not be empty"` |
| 404 |    `"Account: {ACCOUNT}, profile: {PROFILE} not found"` |
| 409 |  `"Users are currently viewing the same account: {ACCOUNT} profile: {PROFILE}"` <br> `Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSIONS}` |
|500|  `"An error occurred"` <br>  `"Profile: {PROFILE} inherits from library profile"`<br>   `"Unable to invoke request: unknown host, see logs for more detail."`<br>  `"Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}"` |