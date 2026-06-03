---
title: iQ JavaScript 拡張 API
description: iQ JavaScript 拡張 API を使用すると、iQ タグ管理プロファイルで JavaScript コード拡張をプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-javascript-extension-api/
---
この API および利用可能なオブジェクトフィールドについての詳細は、[iQ プロファイル API]() および [iQ プロファイルオブジェクト]() を参照してください。

## 動作原理

iQ プロファイルは JSON オブジェクトを使用して iQ タグ管理アカウントプロファイルからデータを取得し、基本的な JavaScript コード拡張を更新します。これにより、カスタムコード展開プロセスを使用して iQ タグ管理プロファイルを管理できます。

`PATCH` メソッドを使用して、iQ プロファイルオブジェクト内のコンポーネントを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCH メソッドを使用すると、保存または名前を付けて保存を使用してプログラムでプロファイル構成を変更します。API を使用して変更を加えた後でも、アプリケーションにログインして公開する必要があります。

### cURL リクエストの例

```bash
curl --location --request PATCH &#39;https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}&#39; \
--header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39; \
--header &#39;Content-Type: application/json&#39; \
--data-raw &#39;
```

## 認証

Bearer トークンは、すべての API 呼び出しを認証するために使用され、API キーは認証呼び出しでのみ使用されます。Bearer トークンに加えて、認証応答には、後続のサーバーサイド API 呼び出しで使用する必要がある地域固有のホスト名が含まれています。

API キーから Bearer トークンを生成する方法については、[認証]() を参照してください。

## プロファイルフィールド

プロファイルは、次の可能なフィールドを含む JSON オブジェクトです：

|フィールド| タイプ| 必須| 説明|
|---| ---| ---| ---|
|`versionTitle`| 文字列| 任意| 保存されたバージョンのタイトル。&lt;br&gt; `saveType` が `saveAs` の場合のデフォルト: `API \| {TIMESTAMP}`&lt;br&gt; `saveType` が `save` の場合のデフォルト: 既存のバージョンタイトル。 |
|`saveType`| 文字列| 任意| PATCH リクエストで実行する保存のタイプ: `save` または `saveAs`。デフォルトは `saveAs`。 |
|`notes`| 文字列| 必須| 公開バージョンに関する追加のノート。|
|`operationList`| 配列| 必須| 操作オブジェクトのリスト。例えば、複数の JavaScript 拡張。|
|`op`| 文字列| 必須| 実行する操作: `add`, `replace`, `remove`。|
|`path`| 文字列| 必須| 更新するコンポーネントタイプと ID の形式: `/{TYPE}/{ID}`。|
|`value.object`| 文字列| 必須| 更新されるオブジェクトタイプ: `variable` または `extension`。|
|`value.name`| 文字列| 必須 (add/replace の場合)| コンポーネントのタイトル。|
|`value.notes`| 文字列| 任意| コンポーネントに関する追加のノート。|
|`value.type`| 文字列| 必須 (拡張の場合)| 追加する拡張のタイプ。|
|`value.scope`| 文字列| 任意| 拡張のスコープ名、またはタグスコープ拡張の場合はタグ ID のカンマ区切りリスト。&lt;br&gt; `Before Load Rules`&lt;br&gt; `After Load Rules`&lt;br&gt; `DOM Ready`&lt;br&gt; `Tag Scoped Extensions`&lt;br&gt; `After Tag Extensions` |
|`value.occurrence`| 文字列| 任意| ページロードごとに JavaScript コード拡張が実行される回数。値: `Run Once` または `Run Always`。デフォルト: `Run Always`。 |
|`value.status`| 文字列| 任意| コンポーネントのオン/オフ状態: `active` または `inactive`。&lt;br&gt; デフォルト: `active`|
|`value.selectedTargets`| マップ &amp;lt;string, Boolean&amp;gt;|  任意 |  コンポーネントを公開する環境のオブジェクト：&lt;br&gt; `{   &#34;prod&#34; : true\|false,   &#34;qa&#34; : true\|false,   &#34;dev&#34; : true\|false }` デフォルト: すべての環境が `true` に構成されています。 |
|`value.conditions`| 配列[オブジェクト]| 任意 | 拡張の条件オブジェクトで、変数、オペレータ、値が含まれます。PATCH リクエストに条件を含めない場合でも、プロファイルに条件が存在する場合、リクエストは `remove` アクションと見なされます。|
| `value.configuration` | 配列[オブジェクト]|  必須 |  コンポーネントの構成オブジェクト。このオブジェクトはコンポーネントのタイプごとに異なります。この配列フィールドには1つのオブジェクトのみが許可されます。例: `{   name: “code”   value: “JSON-escaped JavaScript code here” }` |

### 例のリクエスト

```json
{
  &#34;versionTitle&#34;:&#34;Version 2023.09.19.1127&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;add&#34;,
      &#34;path&#34;:&#34;/extensions&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;extension&#34;,
        &#34;name&#34;: &#34;My extension&#34;,
        &#34;notes&#34;: &#34;extension notes here&#34;,
        &#34;type&#34;: &#34;Javascript Code&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;conditions&#34;: [
          [
            {
              &#34;variable&#34;: &#34;va.badges.30&#34;,
              &#34;operator&#34;: &#34;is_badge_assigned&#34;,
              &#34;value&#34;: &#34;&#34;
            }
          , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api&#34;]
        ],
        &#34;configuration&#34;: [
          {
            &#34;name&#34;: &#34;code&#34;,
            &#34;value&#34;: &#34;b.page_name ||= \&#34;Generic Page\&#34;;&#34;
          }
        , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api&#34;]
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api&#34;]
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
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/extensions&#34;

```

特定の拡張を更新するには、ID をパスに追加します：

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/extensions/503&#34;
```

## 拡張を作成する

この PATCH メソッドはプロファイルオブジェクトと追加の拡張フィールドを取ります。

### 例のリクエスト

```json
{
  &#34;versionTitle&#34;:&#34;Version 2023.09.19.1127&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;add&#34;,
      &#34;path&#34;:&#34;/extensions&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;extension&#34;,
        &#34;name&#34;: &#34;Lowercase extension&#34;,
        &#34;notes&#34;: &#34;extension notes here&#34;,
        &#34;type&#34;: &#34;Lower-Casing&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;configuration&#34;:[
          {
           &#34;all&#34;: true,
           &#34;lower_case_arrays&#34;: &#34;true&#34;,
            &#34;constructor&#34;: &#34;&#34;,
            &#34;initialize&#34;: &#34;&#34;
          }
        , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api&#34;]
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api&#34;]
}
```

## 拡張を更新する

この PATCH メソッドはプロファイルオブジェクトと追加の拡張フィールドを取ります。

### 例のリクエスト

```json
{
  &#34;versionTitle&#34;:&#34;Version 2023.09.19.1127&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;replace&#34;,
      &#34;path&#34;:&#34;/extensions&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;extension/86&#34;,
        &#34;name&#34;: &#34;Lowercase extension&#34;,
        &#34;notes&#34;: &#34;extension notes here&#34;,
        &#34;type&#34;: &#34;Lower-Casing&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;configuration&#34;:[
          {
           &#34;all&#34;: true,
           &#34;lower_case_arrays&#34;: &#34;true&#34;,
            &#34;constructor&#34;: &#34;&#34;,
            &#34;initialize&#34;: &#34;&#34;
          }
        , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api&#34;]
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api&#34;]
}
```

## 拡張を削除する

この PATCH メソッドはプロファイルオブジェクトと追加の拡張フィールドを取ります。
### 例のリクエスト

```json
{
  &#34;versionTitle&#34;:&#34;Version 2023.09.19.1127&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;remove&#34;,
      &#34;path&#34;:&#34;/extensions/86&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;extension&#34;,
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-javascript-extension-api&#34;]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ:

|エラーコード| エラーメッセージ|
|---| ---|
|400| `&#34;Validate patch request failed due to unsupported extension type {TYPE}&#34;`&lt;br&gt;    `&#34;Unsupported extension type {TYPE}&#34;`&lt;br&gt;    `&#34;Validate patch request failed due to %s&#34;`&lt;br&gt;    `&#34;Cannot set tag scope extension with tags that do not exist, id: {ID} - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;    `&#34;Cannot set extension scope to sync if the setting is not turned on - {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;   `&#34;Error in getting next extension id - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;    `&#34;Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;patchProfile.arg2.notes: must not be empty&#34;` |
| 404 |  `&#34;Extension validation failed - extensionId: {ID} \| account: {ACCOUNT} \| profile: {PROFILE}. Cause: not found&#34;` &lt;br&gt;    `&#34;Extension ID {ID} not found in the profile {PROFILE}&#34;`&lt;br&gt;    `&#34;Account: {ACCOUNT}, profile: {PROFILE} not found&#34;` |
| 409 |  `&#34;Conflict with profile extension: _id: {ID}, extType: {EXT_TYPE}, title: {TITLE}&#34;` &lt;br&gt;  `&#34;Users are currently viewing the same account: {ACCOUNT} profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSIONS}&#34;`  |
|500|  `&#34;An error occurred&#34;` &lt;br&gt;   `&#34;Profile: {PROFILE} inherits from library profile&#34;`&lt;br&gt;    `&#34;Unable to invoke request: unknown host, see logs for more detail.&#34;`&lt;br&gt;    `&#34;Error processing json for extension - account: {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;   `&#34;Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;    `&#34;Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;   `&#34;Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}&#34;` |