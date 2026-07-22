---
title: iQ イベント API
description: iQ イベント API を使用すると、iQ タグ管理プロファイルでイベントリスナーをプログラムで作成、更新、削除できます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-events-api/
---
この API と利用可能なオブジェクトフィールドについての詳細は、[iQ プロファイル API](https://docs.tealium.com/iq-profiles-v3-api/) および [iQ プロファイルオブジェクト](https://docs.tealium.com/iq-profiles-api-objects/) を参照してください。

## 仕組み

`PATCH` メソッドを使用して、iQ プロファイルオブジェクトのコンポーネントを作成、更新、削除します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

PATCH メソッドを使用すると、保存または名前を付けて保存を使用してプログラムでプロファイルイベントを変更します。API を使用して変更を加えた後でも、アプリケーションにログインして公開する必要があります。

### cURL リクエストの例

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}' \
  --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9' \
  --header 'Content-Type: application/json' \
  --data '
```

## 認証


<blockquote>
API キーではなく、すべての API 呼び出しを認証するためにベアラートークンが使用されます。API キーは認証呼び出しでのみ使用されます。ベアラートークンに加えて、認証応答には、後続のサーバーサイド API 呼び出しで使用する必要がある地域固有のホスト名が含まれています。
</blockquote>


API キーからベアラートークンを生成する方法については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/) を参照してください。

## プロファイルフィールド

プロファイルイベントは、以下の可能なフィールドを含む JSON オブジェクトです：

| オブジェクト | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `versionTitle` | 文字列 | 任意 | 結果として保存されるバージョンのタイトル。<br> `saveType` が `saveAs` に構成されている場合のデフォルト： `API \| {TIMESTAMP}`<br> `saveType` が `save` に構成されている場合のデフォルト：既存のバージョンタイトル |
| `saveType` | 文字列| 任意| PATCH リクエストで実行する保存のタイプ： `save` または `saveAs`。デフォルトは `saveAs`。 |
| `notes` | 文字列| 必須 | 公開バージョンに関する追加の注記。 |
| `operationList` | 配列 | 必須 | 操作オブジェクトのリスト。例えば、複数のイベント。<br> |
| `op` | 文字列 | 必須 | 実行する操作： `add`、`replace`、または `remove`。<br> |
| `path` | 文字列 | 必須 | 更新するコンポーネントタイプと ID、形式：`/{TYPE}/{ID}`。<br> |
| `value.object` | 文字列 | 必須 | 更新されるオブジェクトタイプ： `variable`、`extension`、または `event`。<br> |
| `value.name` | 文字列 | 必須 (add/replaceの場合)| イベントの名前。 |
| `value.notes` | 文字列 | 任意 | イベントに関する注記。 |
| `value.status` | 文字列 | 必須 | オン/オフの状態： `active` または `inactive`。 |
|`value.occurrence`| 文字列| 任意| イベントトリガーがトラッキングコールを結果として発生させる回数を決定します。値： `Run Once` または `Run Always`。デフォルト： `Run Always`。 |
| `value.type` | 文字列 | 必須 | 追跡されるイベントのタイプ。追跡されるイベントのタイプ。<ul><li>[`mouseEvents`](https://docs.tealium.com/click-event/)\- 次のユーザーアクションを含みます：<ul><li>`click` \- 訪問がページ上でマウスをクリックしたとき。</li><li>`mousedown` \- 訪問がマウスを押し下げたとき。</li><li>`mouseup` \- 訪問がマウスを押し下げたとき。</li></ul><li>[`mouseOver`](https://docs.tealium.com/mouseover-event/) \- 訪問がページ上の特定の要素にマウスをホバーしたとき。</li><li> [`formSubmit`](https://docs.tealium.com/form-submission-event/) \- 訪問がページ上のフォームを提出したとき。</li><li>[`youtubeVideo`](https://docs.tealium.com/youtube-event/) \- 訪問がページ上の埋め込まれた YouTube ビデオと対話したとき。</li><li>[`vimeoVideo`](https://docs.tealium.com/vimeo-event/) \- 訪問がページ上の埋め込まれた Vimeo ビデオと対話したとき。</li><li>[`html5Video`](https://docs.tealium.com/html5-video-event/) \- 訪問がページ上の埋め込まれた HTML5 ビデオと対話したとき。</li><li>[`pageView`](https://docs.tealium.com/page-view-event/) \- 訪問がページを閲覧したとき。</li><li>[`scroll`](https://docs.tealium.com/scroll-event/) \- 訪問がページを縦または横にスクロールしたとき。</li><li>[`elementVisibility`](https://docs.tealium.com/element-visibility-event/) \- ページが訪問に画面要素を表示したとき。</li></li></ul>|
|`value.scope`| 文字列| 任意|  イベントのスコープの名前。<br>`DOM Ready`<br> `After Load Rules` |
| `value.trackingEvent` | 文字列 | 必須 |イベントリスナーのトラッキングイベント：<br>`link` <br> `view`<br>`custom-event-of-anytype `|
|`value.selectedTargets`| マップ &lt;string, Boolean&gt;|  任意 |  コンポーネントを公開する環境のオブジェクト：<br> `{   "prod" : true\|false,   "qa" : true\|false,   "dev" : true\|false }` <br>デフォルト：すべての環境が `true` に構成されています。 |
| `value.eventTriggers` | オブジェクト | 必須 | 各イベントタイプに固有の構成。値は `"object": "[value.Type]"` の形式で、イベントの構成に続きます。 |
|  `value.eventVariables` | 配列 | 必須| 各イベントタイプに固有の変数。 |
| `value.bufferingEventVariables` | 配列 | 必須 | バッファリングイベントが発生したことを示す変数。 |
| `value.rules` | オブジェクト | 必須 | イベントリスナーがページ上でロードされるタイミングを決定するルール。  |

### リクエストの例

```json
{
  "versionTitle": "イベントの追加",
  "saveType": "saveAs",
  "notes": "新しいイベントを追加しました", 
  "operationList": [
    {
      "op": "add",
      "path": "/events",
      "value":{
        "object": "event",
        "name": "新しいAPIイベント",
        "notes": "イベントの注記",
        "status": "active",
        "occurence": "Run Always",
        "type": "youtubeVideo",
        "scope": "After Load Rules",
        "trackingEvent": "link",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "eventTriggers": {
          "object": "youtubeVideo",
           "enabledVideoEventsList": [
            "play", "pause", "buffering", "milestones"
          ],
           "cssSelector": "mycss.selector",
           "milestoneOption": "percentageComplete",
           "milestonesList": [25,50,75,100],
         },
         "eventVariables":
         [
          {
            "variable": "tealium_event",
            "type": "text",
            "value": "youTube_video"
          }
        ],
         "bufferingEventVariables": [
          {
            "variable": "buffering",
            "type": "text",
            "value": "true"
          }
        ],
         "rules": {
          "apply": [ 
            {
              "and": [{"or": [{"uid": 52, "type": "loadRule"}]}]}
            ],
          "exclude": [, "/ja/early-access/api/api-v3/iq-profiles/iq-events-api"]
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
"op" : "add",
"path" : "/events"
```

特定のイベントを更新するには、パスに ID を追加します：

```json
"op" : "replace",
"path" : "/events/503"
```

## イベントの作成

この PATCH メソッドは、プロファイルオブジェクトと追加のイベントフィールドを取ります。
### 例のリクエスト

```json
{
  "versionTitle": "イベントの追加",
  "saveType": "saveAs",
  "notes": "新しいイベントを追加しました",
  "operationList": [
    {
      "op": "add",
      "path": "/events",
      "value":{
        "object": "event",
        "name": "新しいAPIイベント",
        "status": "active",
        "occurence": "常に実行",
        "type": "youtubeVideo",
        "scope": "ロードルール後",
        "trackingEvent": "link",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "eventTriggers": {
          "object": "youtubeVideo",
           "enabledVideoEventsList": [
            "play", "pause", "buffering", "milestones"
          ],
           "cssSelector": "mycss.selector",
           "milestoneOption": "percentageComplete",
           "milestonesList": [25,50,75,100],
         },
         "eventVariables":
         [
          {
            "variable": "tealium_event",
            "type": "text",
            "value": "youTube_video"
          }
        ],
         "bufferingEventVariables": [
          {
            "variable": "buffering",
            "type": "text",
            "value": "true"
          }
        ],
         "rules": {
          "apply": [ 
            {
              "and": [{"or": [{"uid": 52, "type": "loadRule"}]}]}
            ],
          "exclude": [, "/ja/early-access/api/api-v3/iq-profiles/iq-events-api"]
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
  "versionTitle": "イベントの追加",
  "saveType": "saveAs",
  "notes": "新しいイベントを追加しました",
  "operationList": [
    {
      "op": "replace",
      "path": "/events/503",
     "value":{
        "object": "event",
        "name": "新しいAPIイベント",
        "status": "active",
        "occurence": "常に実行",
        "type": "youtubeVideo",
        "scope": "ロードルール後",
        "trackingEvent": "link",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "eventTriggers": {
          "object": "youtubeVideo",
           "enabledVideoEventsList": [
            "play", "pause", "buffering", "milestones"
          ],
           "cssSelector": "mycss.selector",
           "milestoneOption": "percentageComplete",
           "milestonesList": [25,50,75,100],
         },
         "eventVariables":
         [
          {
            "variable": "tealium_event",
            "type": "text",
            "value": "youTube_video"
          }
        ],
         "bufferingEventVariables": [
          {
            "variable": "buffering",
            "type": "text",
            "value": "true"
          }
        ],
         "rules": {
          "apply": [ 
            {
              "and": [{"or": [{"uid": 52, "type": "loadRule"}]}]}
            ],
          "exclude": [, "/ja/early-access/api/api-v3/iq-profiles/iq-events-api"]
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
  "versionTitle": "イベントの追加",
  "saveType": "saveAs",
  "notes": "新しいイベントを追加しました",
  "operationList": [
    {
      "op": "remove",
      "path": "/events/503",
      "value":{
        "object": "event"
      }
    }
  ] 
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| エラーコード | エラーメッセージ |
| --- | --- |
| 400 | `"プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| profile: {PROFILE}"`<br>`"patchProfile.arg2.notes: 空であってはなりません"`|
| 404 | `"プロファイルが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイルライブラリが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイル（レガシー）が見つかりません - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"最新バージョンが見つかりません - {ACCOUNT} \| profile: {PROFILE}"` |
| 409 |  `"同じアカウントを現在他のユーザーが閲覧しています: {ACCOUNT} \| profile: {PROFILE}"` |
| 500 | `"プロファイル: {PROFILE} はライブラリプロファイルを継承しています"`<br>`"プロファイルメタデータの保存中にエラーが発生しました - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイルの保存中にエラーが発生しました - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイル（レガシー）の保存中にエラーが発生しました - {ACCOUNT} \| profile: {PROFILE}"`|