---
title: iQ ロードルール API
description: iQ Variables APIを使用すると、iQタグ管理プロファイル内でロードルールをプログラム的に作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-load-rules-api/
---
このAPIと利用可能なオブジェクトフィールドについて詳しくは、[iQプロファイルAPI]()および[iQプロファイルオブジェクト]()を参照してください。

## 動作方法

`PATCH` メソッドを使用して、iQプロファイルオブジェクト内のロードルールを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCHメソッドを使用するときは、プログラムを使用してプロファイルのロードルールを変更しています。APIを使用して変更した後でも、アプリケーションにログインして公開する必要があります。

### cURLリクエストの例

```bash
curl --location --request PATCH &#39;https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}&#39; \
  --header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39; \
  --header &#39;Content-Type: application/json&#39; \
  --data &#39;
```

## 認証

Bearerトークンは、すべてのAPI呼び出しを認証するために使用され、APIキーは認証呼び出しでのみ使用されます。Bearerトークンに加えて、認証応答には、後続のサーバーサイドAPI呼び出しで使用する必要がある地域固有のホスト名が含まれています。

APIキーからBearerトークンを生成する方法については、[認証]()を参照してください。

## プロファイルフィールド

プロファイルロードルールは、以下の可能なフィールドを含むJSONオブジェクトです：

|フィールド| タイプ| 必須| 説明|
|---| ---| ---| ---|
|`versionTitle`| 文字列| 任意| 保存されたバージョンのタイトル。&lt;br&gt; `saveType`が`saveAs`の場合のデフォルト：`API \| {TIMESTAMP}`&lt;br&gt; `saveType`が`save`の場合のデフォルト：既存のバージョンタイトル |
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
|`value.conditions`| オブジェクトの配列| 必須| 変数名、オペレータ、値を含むオブジェクトの配列。配列内の各オブジェクトは`and`オペレータで関連付けられ、配列内の各配列は`or`オペレータで関連付けられます。次のオペレータは値を受け付けません：&lt;br&gt;`is defined`&lt;br&gt; `is badge assigned`&lt;br&gt; `is badge not assigned`&lt;br&gt; `is not defined`&lt;br&gt; `is not populated` |

### リクエストの例

```json
{
  &#34;versionTitle&#34;: &#34;Adding Rule&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/loadRules&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;loadRule&#34;,
        &#34;name&#34;: &#34;new rule API Dom variable&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;Load Rule notes here&#34;,
        &#34;startDate&#34;: &#34;202202020000&#34;,
        &#34;endDate&#34;: &#34;202202020000&#34;,
        &#34;conditions&#34;: [
          [
            {
              &#34;variable&#34;: &#34;udo.new_name&#34;,
              &#34;operator&#34;: &#34;does_not_equal&#34;,
              &#34;value&#34;: 10
            }
          , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-load-rules-api&#34;]
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
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/loadRules&#34;
```

特定のロードルールを更新するには、パスにIDを追加します：

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/loadRules/503&#34;
```

## ロードルールの作成

このPATCHメソッドは、プロファイルロードルールオブジェクトと追加のロードルールフィールドを取ります。

### リクエストの例

```json
{
  &#34;versionTitle&#34;: &#34;Adding Rule&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/loadRules&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;loadRule&#34;,
        &#34;name&#34;: &#34;new rule API Dom variable&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;Load Rule notes here&#34;,
        &#34;startDate&#34;: &#34;202202020000&#34;,
        &#34;endDate&#34;: &#34;202202020000&#34;,
        &#34;conditions&#34;: [
          [
            {
              &#34;variable&#34;: &#34;udo.new_name&#34;,
              &#34;operator&#34;: &#34;does_not_equal&#34;,
              &#34;value&#34;: 10
            }
          , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-load-rules-api&#34;]
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
  &#34;versionTitle&#34;: &#34;Adding Rule&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;replace&#34;,
      &#34;path&#34;: &#34;/loadRules/49&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;loadRule&#34;,
        &#34;name&#34;: &#34;new rule API Dom variable&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;Load Rule notes here&#34;,
        &#34;startDate&#34;: &#34;202202020000&#34;,
        &#34;endDate&#34;: &#34;202202020000&#34;,
        &#34;conditions&#34;: [
          [
            {
              &#34;variable&#34;: &#34;udo.new_name&#34;,
              &#34;operator&#34;: &#34;does_not_equal&#34;,
              &#34;value&#34;: 10
            }
          , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-load-rules-api&#34;]
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
  &#34;versionTitle&#34;: &#34;Adding Rule&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;remove&#34;,
      &#34;path&#34;: &#34;/loadRules/49&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;loadRule&#34;
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-load-rules-api&#34;]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

|エラーコード| エラーメッセージ|
|---| ---|
|400|  `&#34;Validate patch request failed due to %s&#34;`&lt;br&gt;   `&#34;Cannot set tag scope extension with tags that do not exist, id: {ID} - {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Cannot set extension scope to sync if the setting is not turned on - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Error in getting next extension id - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Not Supported&#34;` &lt;br&gt; `&#34;patchProfile.arg2.notes: must not be empty&#34;` |
| 404 |    `&#34;Account: {ACCOUNT}, profile: {PROFILE} not found&#34;` |
| 409 |  `&#34;Users are currently viewing the same account: {ACCOUNT} profile: {PROFILE}&#34;` &lt;br&gt; `Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSIONS}` |
|500|  `&#34;An error occurred&#34;` &lt;br&gt;  `&#34;Profile: {PROFILE} inherits from library profile&#34;`&lt;br&gt;   `&#34;Unable to invoke request: unknown host, see logs for more detail.&#34;`&lt;br&gt;  `&#34;Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}&#34;` |