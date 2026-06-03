---
title: iQ タグ API
description: iQ タグ API を使用すると、iQ タグ管理プロファイルでタグ構成をプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-tags-api/
---
この API と利用可能なオブジェクトフィールドについて詳しくは、[iQ プロファイル API]() および [iQ プロファイルオブジェクト]() を参照してください。

## 動作原理

`PATCH` メソッドを使用して、iQ プロファイルオブジェクトのコンポーネントを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCH メソッドを使用すると、保存または名前を付けて保存を使用してプロファイルタグをプログラムで変更します。API を使用して変更した後でも、アプリケーションにログインして公開する必要があります。

### cURL リクエストの例

```bash
curl --location --request PATCH &#39;https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}&#39; \
  --header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39;  \
  --header &#39;Content-Type: application/json&#39; \
  --data &#39;
```

## 認証

Bearer トークンは、すべての API 呼び出しを認証するために使用され、API キーは認証呼び出しでのみ使用されます。Bearer トークンに加えて、認証応答には、後続のサーバーサイド API 呼び出しで使用する必要がある地域固有のホスト名が含まれています。

API キーから Bearer トークンを生成する方法については、[認証]() を参照してください。

## プロファイルフィールド

プロファイルタグは、以下の可能なフィールドを含む JSON オブジェクトです：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `versionTitle` | 文字列 | 任意 | 結果として保存されるバージョンのタイトル。&lt;br&gt;デフォルトで `saveType` が `saveAs` に構成されている場合: `API \| {TIMESTAMP}`&lt;br&gt;デフォルトで `saveType` が `save` に構成されている場合: 既存のバージョンタイトル |
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
|`value.selectedTargets`| マップ &amp;lt;string, Boolean&amp;gt;|  任意 |  コンポーネントを公開する環境のオブジェクト。`{   &#34;prod&#34; : true\|false,   &#34;qa&#34; : true\|false,   &#34;dev&#34; : true\|false }` &lt;br&gt;デフォルト: すべての環境が `true` に構成されています。 |
| `value.configuration` |マップ &amp;lt;String, Object&amp;gt; |任意 | ベンダーによって提供されるタグ構成の文字列とオブジェクトのマップ。構成は各タグに固有です。詳細については、タグのドキュメントを参照してください。|
|`value.advancedConfiguration`| オブジェクト |任意 |  タグ構成構成に対応する高度な構成のセット。 &lt;br&gt;`advConfigBundle` — **True** または **False**&lt;br&gt; `advConfigLoadType` — **True** または **False**&lt;br&gt; `advConfigOptOut` — **True**&lt;br&gt; `advConfigSend`— **True** または **False** &lt;br&gt; `advConfigSrc` — テキストフィールド&lt;br&gt; `tagTiming` — **DOM Ready** または **Prioritized** |
|`value.rules`| オブジェクト |任意 | タグに適用または除外するロードルール。|
|`value.dataMappings`| マップ &amp;lt;String, String&amp;gt; |任意 | Tealium IQ 変数とその対応するマップ先、変数名、データタイプを含むオブジェクト。マップされた変数トリガーの特定の形式は、タグ構成の **Data Mappings** 画面で確認できます。|
|`value.dataMappings.variable`| 文字列 |任意 | マップされる変数の名前。|
|`value.dataMappings.type`| 文字列 |任意 | マップされる変数のデータタイプ。このフィールドは次の変数タイプをサポートしています：&lt;br&gt;`ls` - ローカル保存&lt;br&gt;`ss` - セッション保存&lt;br&gt;`udo` - ユニバーサルデータオブジェクト&lt;br&gt;`qp` - クエリ文字列パラメータ&lt;br&gt;`cp` - クッキー&lt;br&gt;`js_page` - JavaScript 変数&lt;br&gt;`dom` - DOM 変数&lt;br&gt;`meta` - メタデータ要素&lt;br&gt;`static.text` - 静的テキスト&lt;br&gt;`static.js` - JavaScript コード|
|`value.dataMappings.mappings`| 文字列または文字列の配列 |任意 | 変数のマップ先。|

### リクエストの例

```json
{
  &#34;versionTitle&#34;: &#34;バージョンタイトル&#34;,
  &#34;notes&#34;: &#34;注記&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/tags&#34;,
      &#34;value&#34;: {
        &#34;object&#34;: &#34;tag&#34;,
        &#34;tagId&#34;: &#34;7133&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;タグ追加&#34;,
        &#34;name&#34;: &#34;7133 タグ Google Analytics&#34;,
        &#34;dataMappings&#34;: [
          {
            &#34;variable&#34;: &#34;variable_name&#34;,
            &#34;type&#34;: &#34;udo&#34;,
            &#34;mappings&#34;: [&#34;a1&#34;, &#34;a2&#34;, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
          }
        ],
        &#34;selectedTargets&#34;: {
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;advancedConfiguration&#34;: {
          &#34;bundleFlag&#34;: true,
          &#34;syncLoadType&#34;: false,
          &#34;optout&#34;: true,
          &#34;scriptSource&#34;: &#34;&#34;,
          &#34;sendFlag&#34;: false,
          &#34;tagTiming&#34;: &#34;Dom Ready&#34;
        },
        &#34;configuration&#34;: {
          &#34;tracking_id&#34;: &#34;123&#34;
        },
        &#34;rules&#34;: {
          &#34;apply&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}],
          &#34;exclude&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;3&#34;, &#34;type&#34;: &#34;loadRule&#34;}, {&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
        }
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
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
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/tags&#34;
```

特定のタグを更新するには、パスに ID を追加します：

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/tags/503&#34;
```

## タグの作成

この PATCH メソッドは、プロファイルオブジェクトと追加のタグフィールドを取ります。

### リクエストの例

```json
{
  &#34;versionTitle&#34;: &#34;バージョンタイトル&#34;,
  &#34;notes&#34;: &#34;注記&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/tags&#34;,
      &#34;value&#34;: {
        &#34;object&#34;: &#34;tag&#34;,
        &#34;tagId&#34;: &#34;7133&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;タグ追加&#34;,
        &#34;name&#34;: &#34;7133 タグ Google Analytics&#34;,
        &#34;dataMappings&#34;: [
          {
            &#34;variable&#34;: &#34;variable_name&#34;,
            &#34;type&#34;: &#34;udo&#34;,
            &#34;mappings&#34;: [&#34;a1&#34;, &#34;a2&#34;, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
          }
        ],
        &#34;selectedTargets&#34;: {
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;advancedConfiguration&#34;: {
          &#34;bundleFlag&#34;: true,
          &#34;syncLoadType&#34;: false,
          &#34;optout&#34;: true,
          &#34;scriptSource&#34;: &#34;&#34;,
          &#34;sendFlag&#34;: false,
          &#34;tagTiming&#34;: &#34;Dom Ready&#34;
        },
        &#34;Configuration&#34;: {
          &#34;tracking_id&#34;: &#34;123&#34;
        },
        &#34;rules&#34;: {
          &#34;apply&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}],
          &#34;exclude&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;3&#34;, &#34;type&#34;: &#34;loadRule&#34;}, {&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
        }
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
}
```

## タグの更新

この PATCH メソッドは、プロファイルオブジェクトと追加のタグフィールドを取ります。
### 例のリクエスト

```json
{
  &#34;versionTitle&#34;: &#34;version title&#34;,
  &#34;notes&#34;: &#34;notes&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;replace&#34;,
      &#34;path&#34;: &#34;/tags/21&#34;,
      &#34;value&#34;: {
        &#34;object&#34;: &#34;tag&#34;,
        &#34;tagId&#34;: &#34;7133&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;adding tag&#34;,
        &#34;name&#34;: &#34;Replace name by API Google Analytics&#34;,
        &#34;dataMappings&#34;: [
          {
            &#34;variable&#34;: &#34;variable_name&#34;,
            &#34;type&#34;: &#34;udo&#34;,
            &#34;mappings&#34;: [&#34;a1&#34;, &#34;a2&#34;, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
          }
        ],
        &#34;selectedTargets&#34;: {
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;advancedConfiguration&#34;: {
          &#34;bundleFlag&#34;: true,
          &#34;syncLoadType&#34;: false,
          &#34;optout&#34;: true,
          &#34;scriptSource&#34;: &#34;&#34;,
          &#34;sendFlag&#34;: false,
          &#34;tagTiming&#34;: &#34;Dom Ready&#34;
        },
        &#34;Configuration&#34;: {
          &#34;tracking_id&#34;: &#34;123&#34;
        },
        &#34;rules&#34;: {
          &#34;apply&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}],
          &#34;exclude&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;3&#34;, &#34;type&#34;: &#34;loadRule&#34;}, {&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
        }
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
}
```

## タグの削除

このPATCHメソッドはプロファイルオブジェクトと追加のタグフィールドを取ります。

### 例のリクエスト

```json
{
  &#34;versionTitle&#34;: &#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;:&#34;&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;remove&#34;,
      &#34;path&#34;: &#34;/tags/230&#34;,
      &#34;value&#34;:{
        &#34;object&#34;:&#34;tag&#34;
      }
    }
  , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-tags-api&#34;]
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `&#34;プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;patchProfile.arg2.notes: 空であってはなりません&#34;`|
| 404 | `&#34;プロファイルが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイルライブラリが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイル（レガシー）が見つかりません - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;同じアカウントを現在他のユーザーが閲覧しています: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;最新バージョンが見つかりません - {ACCOUNT} \| profile: {PROFILE}&#34;` |
| 409 | `&#34;プロファイルの保存エラー: {PROFILE} for account: {ACCOUNT}, 重複バージョン: {VERSION}&#34;` |
| 500 | `&#34;プロファイル: {PROFILE} はライブラリプロファイルを継承しています&#34;`&lt;br&gt;`&#34;プロファイルメタデータの保存エラー - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイルの保存エラー - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイル（レガシー）の保存エラー - {ACCOUNT} \| profile: {PROFILE}&#34;`|