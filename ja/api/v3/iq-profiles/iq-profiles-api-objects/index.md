---
title: iQプロファイルAPIオブジェクト
description: このドキュメントでは、Tealium iQプロファイルのJSON構造について説明し、プロファイル内の変数、タグ、ロードルール、拡張機能、イベント間のフィールド、構成、および関係について詳しく説明します。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-profiles-api-objects/
---
## 利用可能なフィールド

|オブジェクト| タイプ| 説明|
|---| ---| ---|
|`account`| 文字列| Tealiumアカウント名。|
|`profile`| 文字列| Tealiumプロファイル名。|
|`versionTitle`| 文字列| このiQプロファイルのバージョンのタイトル。指定されていない場合、`versionTitle`は`API \| {TIMESTAMP}`としてフォーマットされます。|
|`version`| 文字列| このiQプロファイルのバージョンID。|
|`minorVersion`| 文字列| プロファイルを保存するたびに更新されるバージョンID。保存してから公開する場合、`minorVersion`と`version`は一致しません。Save Asを実行した場合のみ一致します。|
|`parentVersion`| 文字列 | `save`または`saveAs`操作の元となるプロファイルバージョン。 |
|`creation`| 日付| プロファイルの作成日。|
|`customTargets`| 文字列| ユーザー定義のカスタムターゲット環境のリスト。 |
|`versionDetails`| オブジェクト| 現在のバージョンに関する詳細情報：現在のプロファイルバージョンが公開されている場所、プロファイルを公開したユーザーのメールアドレス、プロファイルに関するメモ。|
|`environmentVersions`| オブジェクト| 各環境での現在の公開プロファイルバージョンのリスト。 |
|`dataCloudLinkedProfiles`| 文字列| リンクされたサーバーサイドプロファイル名。|
|`libraryType`| 文字列| 継承されるライブラリのタイプ。ライブラリが継承されていない場合、値は`NONE`です。<br> `Required` - すべてのプロファイルが自動的にこのライブラリを含みます。<br> `Optional` - どのプロファイルがこのライブラリを含むかを指定します。<br>`NONE` - 指定されたプロファイルがライブラリではないことを示します。 |
|`linkedProfiles`|  オブジェクトの配列| ライブラリの場合、このフィールドはプロファイルがこのライブラリから継承する値のリストを示します。プロファイルの場合、この値は`null`です。|
|`linkedLibraries`| オブジェクトの配列| プロファイルの場合、このフィールドはプロファイルにリンクされたライブラリを表します。ライブラリの場合、この値は`null`です。|
|`variables`| 変数の配列| プロファイル内の変数オブジェクトの配列。|
|`tags`| タグの配列| プロファイル内のタグオブジェクトの配列。|
|`loadRules`| ロードルールの配列| プロファイル内のロードルールオブジェクトの配列。|
|`extensions`| 拡張機能の配列| プロファイル内の拡張機能オブジェクトの配列。|
|`events`| イベントの配列| プロファイル内のイベントオブジェクトの配列。|
|`versionIds` | 配列 |以前のバージョンのリスト。 |
 |`templateList`|--| プロファイルに関連付けられたすべてのタグテンプレートをリストします。|

**例**

```json
{
    "account": "my_account",
    "profile": "main",
    "versionTitle": "Version 2022.03.22.2108",
    "version": "202203222108",
    "minorVersion": "202203222108",
    "parentVersion": "202309191127",
    "creation": "202201131654",
    "customTargets": null,
    "versionDetails": {},
    "environmentVersions": {},
    "dataCloudLinkedProfiles": "{}",
    "libraryType": "NONE",
    "linkedProfiles": null,
    "linkedLibraries": [],
    "variables": null,
    "extensions": null,
    "loadRules": null,
    "tags": null,
    "events": null,
    "templateList": null,
    "versionIds": null
}
```

## 変数

|オブジェクト| タイプ| 説明|
|---| ---| ---|
|`id`| 数値| 変数ID。|
|`uniqueIdentifier`| 文字列| 拡張機能の`conditions`、タグの`dataMappings`、ロードルールの`conditions`から変数を参照するために使用される変数識別子。|
|`name`| 文字列| 変数のタイトル。|
|`alias`| 文字列| 変数名。|
|`type`| 文字列| 変数タイプを表すプレフィックス。<br>  `ls` - ローカル保存 <br> `ss` - セッション保存 <br> `udo` - ユニバーサルデータオブジェクト<br> `qp` - クエリ文字列パラメータ<br> `cp` - クッキー<br> `js` - JavaScript変数<br> `meta` - メタデータ要素<br> `va` - AudienceStream属性 |
|`notes`| 文字列| 変数に関するメモ。|
|`context`| 配列| AudienceStreamからインポートされた属性の範囲。<br> 値: `current_visit`または`visitor`|
|`library`| 文字列| 変数が継承されるライブラリの名前。|
|`imported`| 文字列| インポートされた変数のソース。これはすべてのAudienceStream属性に対して`AudienceStream`に構成されます。|
|`usedIn`| オブジェクト| この変数が使用されているIDのリスト。|

## タグ

|オブジェクト| タイプ| 説明|
|---| ---| ---|
|`id`| 数値| タグの一意のID。|
|`tagID`| 数値| このタグタイプのシステムID。この値は同じタイプのすべてのタグに対して同じです。たとえば、Facebook Pixelタグの場合は`6037`です。|
|`name`| 文字列| タグ構成から生成されたユーザーのタグ名。|
|`library`| 文字列| タグが継承されるライブラリの名前。|
|`status`| 文字列| オン/オフの状態: `active`または`inactive`。|
|`notes`| 文字列| タグに関するメモ。|
|`dataMappings`| マップ&lt;文字列, 文字列&gt;|  Tealium IQ変数とそれに対応するマップ先を返します。 |
|`selectedTargets`| マップ&lt;文字列, ブール値&gt;|  タグが公開される環境のオブジェクト。 |
|`environmentVersions`| マップ&lt;文字列, ブール値&gt;| このタグが最後に公開された環境の配列。|
|`advancedConfiguration`| オブジェクト|  タグ構成構成に対応する高度な構成のセット。<br> `advConfigBundle` — **True**または**False**<br> `advConfigLoadType` — **True**または**False**<br> `advConfigOptOut` — **True**<br> `advConfigSend`— **True**または**False** `advConfigSrc` — テキストフィールド<br> `tagTiming` — **DOM Ready**または**Prioritized** |
| `configuration` |  マップ &lt;文字列, オブジェクト&gt; |  ベンダーによって提供されるタグ構成の文字列とオブジェクトのマップ。 |
|`rules`| オブジェクト| 適用または除外するロードルール。|
 | `template` |  オブジェクト |  完全なタグテンプレートを返します。リクエストに`includes = tags.template`が必要です。 |

## ロードルール

|オブジェクト| タイプ| 説明|
|---| ---| ---|
|`id`| 数値| ロードルールの一意のID。|
|`name`| 文字列| ロードルールの名前。|
|`status`| 文字列| オン/オフの状態: `active`または`inactive`。|
|`library`| 文字列| 関連するライブラリの名前。|
|`notes`| 文字列| ロードルールに関するメモ。|
|`startDate`| 日付| スケジュールされたロードルールの開始日。|
|`endDate`| 日付| スケジュールされたロードルールの終了日。|
|`environmentVersions`| マップ&lt;文字列, ブール値&gt;| 各環境での現在の公開ロードルールバージョンのリスト。 |
|`usedIn`| オブジェクト| このロードルールが使用されているIDのリスト。|
|`conditions`| オブジェクトの配列| 変数名、演算子、値を含むオブジェクトの配列。配列内の各オブジェクトは`and`演算子で関連付けられ、配列内の各配列は`or`演算子で関連付けられます。|


## 拡張機能

|オブジェクト|タイプ|説明|
|---|---|---|
|`id`|数値|拡張機能の一意のIDです。|
|`extensionId`|数値|この拡張機能タイプのシステムIDです。この値は同じタイプのすべての拡張機能で同じです。例えば、JavaScriptコード拡張の場合は`100036`です。|
|`extensionType`|文字列|この拡張機能タイプのシステム名です。この値は同じタイプのすべての拡張機能で同じです。例えば、JavaScriptコード拡張の場合は`Javascript Code`です。|
|`name`|文字列|拡張機能の名前です。|
|`library`|文字列|関連するライブラリの名前です。|
|`notes`|文字列|拡張機能に入力されたノートです。|
|`loadRule`|混合|ロードルールIDのカンマ区切りリスト、またはすべてのページに対して`all`です。|
|`scope`|文字列|拡張機能のスコープ名、またはタグスコープ拡張機能の場合はタグIDのカンマ区切りリストです。<br>`utag Sync`<br>`Pre Loader`<br>`Before Load Rules`<br>`After Load Rules`<br>`DOM Ready`<br>`Tag Scoped Extensions`<br>`After Tag Extensions` タグスコープ拡張機能とそれが`occurrence`とどのように動作するかについての詳細は、[スコープの理解](https://docs.tealium.com/about-extensions/#understanding-scope)を参照してください。|
|`occurrence`|文字列|ページロードごとにJavaScriptコード拡張が実行される回数を決定します。値: `Run Once`または`Run Always`。|
|`status`|文字列|オン/オフの状態: `active`または`inactive`。|
|`selectedTargets`|マップ&lt;文字列, ブール&gt;|拡張機能が公開される環境です。|
|`environmentVersions`|マップ&lt;文字列, ブール&gt;|拡張機能が公開される環境の配列です。|
|`conditions`|オブジェクトの配列|特定の拡張機能に構成された条件です。|
|`configuration`|マップ &lt;文字列, オブジェクト&gt;|各拡張機能の構成のマップです。|

## イベント

|オブジェクト|タイプ|説明|
|---|---|---|
|`id`|数値|イベントの一意のIDです。|
|`eventID`|数値|このイベントタイプのシステムIDです。この値は同じタイプのすべてのイベントで同じです。|
|`name`|文字列|イベントの名前です。|
|`status`|文字列|オン/オフの状態: `active`または`inactive`。|
|`eventType`|文字列|追跡されるイベントのタイプです。<ul><li>[`mouseEvents`](https://docs.tealium.com/click-event/)\- 次のユーザーアクションを含みます:<ul><li>`click` \- 訪問がページ上でマウスをクリックしたとき。</li><li>`mousedown` \- 訪問がマウスを押し下げたとき。</li><li>`mouseup` \- 訪問がマウスを押し下げたとき。</li></ul><li>[`mouseOver`](https://docs.tealium.com/mouseover-event/) \- 訪問がページ上の特定の要素にマウスをホバーしたとき。</li><li> [`formSubmit`](https://docs.tealium.com/form-submission-event/) \- 訪問がページ上でフォームを提出したとき。</li><li>[`youtubeVideo`](https://docs.tealium.com/youtube-event/) \- 訪問がページ上の埋め込まれたYouTubeビデオと対話したとき。</li><li>[`vimeoVideo`](https://docs.tealium.com/vimeo-event/) \- 訪問がページ上の埋め込まれたVimeoビデオと対話したとき。</li><li>[`html5Video`](https://docs.tealium.com/html5-video-event/) \- 訪問がページ上の埋め込まれたHTML5ビデオと対話したとき。</li><li>[`pageView`](https://docs.tealium.com/page-view-event/) \- 訪問がページを閲覧したとき。</li><li>[`scroll`](https://docs.tealium.com/scroll-event/) \- 訪問がページを縦または横にスクロールしたとき。</li><li>[`elementVisibility`](https://docs.tealium.com/element-visibility-event/) \- ページが訪問に画面要素を表示したとき。</li></li></ul>|
|`scope`|文字列|拡張機能のスコープ名、またはタグスコープイベントの場合はタグIDのカンマ区切りリストです。<br>`After Load Rules`<br>`DOM Ready`<br>タグスコープイベントについての詳細は、[スコープ](https://docs.tealium.com/event-scope/)を参照してください。|
|`trackingEvent`|文字列|イベントが発生したときに行われるイベントコールです。|
|`notes`|文字列|イベントに関するノートです。|
|`library`|文字列|関連するライブラリの名前です。|
|`eventLoadRulesList`|文字列|イベントで使用されるすべてのロードルールのリストです。|
|`eventTrigger`|オブジェクト|各イベントタイプに特有の構成です。イベントトリガーについての詳細は、[イベント > イベントトリガー](https://docs.tealium.com/event-triggers/)を参照してください。|
|`selectedTargets`|マップ\<文字列, ブール>|イベントが公開される環境です。|
|`environmentVersions`|マップ\<文字列, ブール>|イベントが公開される環境の配列です。|
|`eventVariables`|オブジェクト|各イベントタイプに特有の変数です。|
|`rules`|オブジェクト|イベントリスナーがページ上にロードされるタイミングを決定するルールです。|
|`usedIn`|オブジェクト|このイベントが使用されているIDのリストです。|