---
title: iQ イベント API
description: iQ イベント API を使用すると、iQ タグ管理プロファイルでイベントリスナーをプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-events-api/
---
この API と利用可能なオブジェクトフィールドについての詳細は、[iQ プロファイル API]() および [iQ プロファイルオブジェクト]() を参照してください。

## 仕組み

`PATCH` メソッドを使用して、iQ プロファイルオブジェクトのコンポーネントを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCH メソッドを使用すると、保存または名前を付けて保存を使用してプログラムでプロファイルイベントを変更します。API を使用して変更を加えた後でも、アプリケーションにログインして公開する必要があります。

### cURL リクエストの例

```bash
curl --location --request PATCH &#39;https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}&#39; \
  --header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39; \
  --header &#39;Content-Type: application/json&#39; \
  --data &#39;
```

## 認証

API キーではなく、すべての API 呼び出しを認証するためにベアラートークンが使用されます。API キーは認証呼び出しでのみ使用されます。ベアラートークンに加えて、認証応答には、後続のサーバーサイド API 呼び出しで使用する必要がある地域固有のホスト名が含まれています。

API キーからベアラートークンを生成する方法については、[認証]() を参照してください。

## プロファイルフィールド

プロファイルイベントは、以下の可能なフィールドを含む JSON オブジェクトです：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `versionTitle` | 文字列 | 任意 | 結果として保存されるバージョンのタイトル。&lt;br&gt; `saveType` が `saveAs` に構成されている場合のデフォルト： `API \| {TIMESTAMP}`&lt;br&gt; `saveType` が `save` に構成されている場合のデフォルト：既存のバージョンタイトル |
| `saveType` | 文字列| 任意| PATCH リクエストで実行する保存のタイプ： `save` または `saveAs`。デフォルトは `saveAs`。 |
| `notes` | 文字列| 必須 | 公開バージョンに関する追加の注記。 |
| `operationList` | 配列 | 必須 | 操作オブジェクトのリスト。例えば、複数のイベント。&lt;br&gt; |
| `op` | 文字列 | 必須 | 実行する操作： `add`、`replace`、または `remove`。&lt;br&gt; |
| `path` | 文字列 | 必須 | 更新するコンポーネントタイプと ID、形式：`/{TYPE}/{ID}`。&lt;br&gt; |
| `value.object` | 文字列 | 必須 | 更新されるオブジェクトタイプ： `variable`、`extension`、または `event`。&lt;br&gt; |
| `value.name` | 文字列 | 必須 (add/replaceの場合)| イベントの名前。 |
| `value.notes` | 文字列 | 任意 | イベントに関する注記。 |
| `value.status` | 文字列 | 必須 | オン/オフの状態： `active` または `inactive`。 |
|`value.occurrence`| 文字列| 任意| イベントトリガーがトラッキングコールを結果として発生させる回数を決定します。値： `Run Once` または `Run Always`。デフォルト： `Run Always`。 |
| `value.type` | 文字列 | 必須 | 追跡されるイベントのタイプ。追跡されるイベントのタイプ。&lt;ul&gt;&lt;li&gt;[`mouseEvents`]()\- 次のユーザーアクションを含みます：&lt;ul&gt;&lt;li&gt;`click` \- 訪問がページ上でマウスをクリックしたとき。&lt;/li&gt;&lt;li&gt;`mousedown` \- 訪問がマウスを押し下げたとき。&lt;/li&gt;&lt;li&gt;`mouseup` \- 訪問がマウスを押し下げたとき。&lt;/li&gt;&lt;/ul&gt;&lt;li&gt;[`mouseOver`]() \- 訪問がページ上の特定の要素にマウスをホバーしたとき。&lt;/li&gt;&lt;li&gt; [`formSubmit`]() \- 訪問がページ上のフォームを提出したとき。&lt;/li&gt;&lt;li&gt;[`youtubeVideo`]() \- 訪問がページ上の埋め込まれた YouTube ビデオと対話したとき。&lt;/li&gt;&lt;li&gt;[`vimeoVideo`]() \- 訪問がページ上の埋め込まれた Vimeo ビデオと対話したとき。&lt;/li&gt;&lt;li&gt;[`html5Video`]() \- 訪問がページ上の埋め込まれた HTML5 ビデオと対話したとき。&lt;/li&gt;&lt;li&gt;[`pageView`]() \- 訪問がページを閲覧したとき。&lt;/li&gt;&lt;li&gt;[`scroll`]() \- 訪問がページを縦または横にスクロールしたとき。&lt;/li&gt;&lt;li&gt;[`elementVisibility`]() \- ページが訪問に画面要素を表示したとき。&lt;/li&gt;&lt;/li&gt;&lt;/ul&gt;|
|`value.scope`| 文字列| 任意|  イベントのスコープの名前。&lt;br&gt;`DOM Ready`&lt;br&gt; `After Load Rules` |
| `value.trackingEvent` | 文字列 | 必須 |イベントリスナーのトラッキングイベント：&lt;br&gt;`link` &lt;br&gt; `view`&lt;br&gt;`custom-event-of-anytype `|
|`value.selectedTargets`| マップ &amp;lt;string, Boolean&amp;gt;|  任意 |  コンポーネントを公開する環境のオブジェクト：&lt;br&gt; `{   &#34;prod&#34; : true\|false,   &#34;qa&#34; : true\|false,   &#34;dev&#34; : true\|false }` &lt;br&gt;デフォルト：すべての環境が `true` に構成されています。 |
| `value.eventTriggers` | オブジェクト | 必須 | 各イベントタイプに固有の構成。値は `&#34;object&#34;: &#34;[value.Type]&#34;` の形式で、イベントの構成に続きます。 |
|  `value.eventVariables` | 配列 | 必須| 各イベントタイプに固有の変数。 |
| `value.bufferingEventVariables` | 配列 | 必須 | バッファリングイベントが発生したことを示す変数。 |
| `value.rules` | オブジェクト | 必須 | イベントリスナーがページ上でロードされるタイミングを決定するルール。  |

### リクエストの例

```json
{
  &#34;versionTitle&#34;: &#34;イベントの追加&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;新しいイベントを追加しました&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/events&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;event&#34;,
        &#34;name&#34;: &#34;新しいAPIイベント&#34;,
        &#34;notes&#34;: &#34;イベントの注記&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;type&#34;: &#34;youtubeVideo&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;trackingEvent&#34;: &#34;link&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;eventTriggers&#34;: {
          &#34;object&#34;: &#34;youtubeVideo&#34;,
           &#34;enabledVideoEventsList&#34;: [
            &#34;play&#34;, &#34;pause&#34;, &#34;buffering&#34;, &#34;milestones&#34;
          ],
           &#34;cssSelector&#34;: &#34;mycss.selector&#34;,
           &#34;milestoneOption&#34;: &#34;percentageComplete&#34;,
           &#34;milestonesList&#34;: [25,50,75,100],
         },
         &#34;eventVariables&#34;:
         [
          {
            &#34;variable&#34;: &#34;tealium_event&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;youTube_video&#34;
          }
        ],
         &#34;bufferingEventVariables&#34;: [
          {
            &#34;variable&#34;: &#34;buffering&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;true&#34;
          }
        ],
         &#34;rules&#34;: {
          &#34;apply&#34;: [ 
            {
              &#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: 52, &#34;type&#34;: &#34;loadRule&#34;}]}]}
            ],
          &#34;exclude&#34;: [, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-events-api&#34;]
        }
      }
    } 
  ] 
}
```

## PATCH 操作パラメータ

`POST`、`PUT`、`DELETE` メソッドの代わりに、`PATCH` メソッドは `op` パラメータを使用して実行するアクションを指定します。

`op` パラメータは次の値をサポートしています：

*   `add` \- コンポーネントを作成します。
*   `replace` \- コンポーネントを更新します。
*   `remove` \- コンポーネントを削除します。

コンポーネントのタイプと ID を指定するには、`path` パラメータを使用します。`path` パラメータの形式は `/{TYPE}/{ID}` です。

例えば、イベントを追加するには：

```json
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/events&#34;
```

特定のイベントを更新するには、パスに ID を追加します：

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/events/503&#34;
```

## イベントの作成

この PATCH メソッドは、プロファイルオブジェクトと追加のイベントフィールドを取ります。
### 例のリクエスト

```json
{
  &#34;versionTitle&#34;: &#34;イベントの追加&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;新しいイベントを追加しました&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/events&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;event&#34;,
        &#34;name&#34;: &#34;新しいAPIイベント&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;occurence&#34;: &#34;常に実行&#34;,
        &#34;type&#34;: &#34;youtubeVideo&#34;,
        &#34;scope&#34;: &#34;ロードルール後&#34;,
        &#34;trackingEvent&#34;: &#34;link&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;eventTriggers&#34;: {
          &#34;object&#34;: &#34;youtubeVideo&#34;,
           &#34;enabledVideoEventsList&#34;: [
            &#34;play&#34;, &#34;pause&#34;, &#34;buffering&#34;, &#34;milestones&#34;
          ],
           &#34;cssSelector&#34;: &#34;mycss.selector&#34;,
           &#34;milestoneOption&#34;: &#34;percentageComplete&#34;,
           &#34;milestonesList&#34;: [25,50,75,100],
         },
         &#34;eventVariables&#34;:
         [
          {
            &#34;variable&#34;: &#34;tealium_event&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;youTube_video&#34;
          }
        ],
         &#34;bufferingEventVariables&#34;: [
          {
            &#34;variable&#34;: &#34;buffering&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;true&#34;
          }
        ],
         &#34;rules&#34;: {
          &#34;apply&#34;: [ 
            {
              &#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: 52, &#34;type&#34;: &#34;loadRule&#34;}]}]}
            ],
          &#34;exclude&#34;: [, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-events-api&#34;]
        }
      }
    } 
  ] 
}
```

## イベントの更新

このPATCHメソッドはプロファイルオブジェクトと追加のイベントフィールドを取ります。

### 例のリクエスト

```json
{
  &#34;versionTitle&#34;: &#34;イベントの追加&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;新しいイベントを追加しました&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;replace&#34;,
      &#34;path&#34;: &#34;/events/503&#34;,
     &#34;value&#34;:{
        &#34;object&#34;: &#34;event&#34;,
        &#34;name&#34;: &#34;新しいAPIイベント&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;occurence&#34;: &#34;常に実行&#34;,
        &#34;type&#34;: &#34;youtubeVideo&#34;,
        &#34;scope&#34;: &#34;ロードルール後&#34;,
        &#34;trackingEvent&#34;: &#34;link&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;eventTriggers&#34;: {
          &#34;object&#34;: &#34;youtubeVideo&#34;,
           &#34;enabledVideoEventsList&#34;: [
            &#34;play&#34;, &#34;pause&#34;, &#34;buffering&#34;, &#34;milestones&#34;
          ],
           &#34;cssSelector&#34;: &#34;mycss.selector&#34;,
           &#34;milestoneOption&#34;: &#34;percentageComplete&#34;,
           &#34;milestonesList&#34;: [25,50,75,100],
         },
         &#34;eventVariables&#34;:
         [
          {
            &#34;variable&#34;: &#34;tealium_event&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;youTube_video&#34;
          }
        ],
         &#34;bufferingEventVariables&#34;: [
          {
            &#34;variable&#34;: &#34;buffering&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;true&#34;
          }
        ],
         &#34;rules&#34;: {
          &#34;apply&#34;: [ 
            {
              &#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: 52, &#34;type&#34;: &#34;loadRule&#34;}]}]}
            ],
          &#34;exclude&#34;: [, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-events-api&#34;]
        }
      }
    } 
  ] 
}
```

## イベントの削除

このPATCHメソッドはプロファイルオブジェクトと追加のイベントフィールドを取ります。

### 例のリクエスト

```json
{
  &#34;versionTitle&#34;: &#34;イベントの追加&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;新しいイベントを追加しました&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;remove&#34;,
      &#34;path&#34;: &#34;/events/503&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;event&#34;
      }
    }
  ] 
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `&#34;プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;patchProfile.arg2.notes: 空であってはなりません&#34;`|
| 404 | `&#34;プロファイルが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイルライブラリが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイル（レガシー）が見つかりません - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;最新バージョンが見つかりません - {ACCOUNT} \| profile: {PROFILE}&#34;` |
| 409 |  `&#34;同じアカウントを現在他のユーザーが閲覧しています: {ACCOUNT} \| profile: {PROFILE}&#34;` |
| 500 | `&#34;プロファイル: {PROFILE} はライブラリプロファイルを継承しています&#34;`&lt;br&gt;`&#34;プロファイルメタデータの保存中にエラーが発生しました - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイルの保存中にエラーが発生しました - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイル（レガシー）の保存中にエラーが発生しました - {ACCOUNT} \| profile: {PROFILE}&#34;`|