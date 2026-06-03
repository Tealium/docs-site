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
|`libraryType`| 文字列| 継承されるライブラリのタイプ。ライブラリが継承されていない場合、値は`NONE`です。&lt;br&gt; `Required` - すべてのプロファイルが自動的にこのライブラリを含みます。&lt;br&gt; `Optional` - どのプロファイルがこのライブラリを含むかを指定します。&lt;br&gt;`NONE` - 指定されたプロファイルがライブラリではないことを示します。 |
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
    &#34;account&#34;: &#34;my_account&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;versionTitle&#34;: &#34;Version 2022.03.22.2108&#34;,
    &#34;version&#34;: &#34;202203222108&#34;,
    &#34;minorVersion&#34;: &#34;202203222108&#34;,
    &#34;parentVersion&#34;: &#34;202309191127&#34;,
    &#34;creation&#34;: &#34;202201131654&#34;,
    &#34;customTargets&#34;: null,
    &#34;versionDetails&#34;: {},
    &#34;environmentVersions&#34;: {},
    &#34;dataCloudLinkedProfiles&#34;: &#34;{}&#34;,
    &#34;libraryType&#34;: &#34;NONE&#34;,
    &#34;linkedProfiles&#34;: null,
    &#34;linkedLibraries&#34;: [],
    &#34;variables&#34;: null,
    &#34;extensions&#34;: null,
    &#34;loadRules&#34;: null,
    &#34;tags&#34;: null,
    &#34;events&#34;: null,
    &#34;templateList&#34;: null,
    &#34;versionIds&#34;: null
}
```

## 変数

|オブジェクト| タイプ| 説明|
|---| ---| ---|
|`id`| 数値| 変数ID。|
|`uniqueIdentifier`| 文字列| 拡張機能の`conditions`、タグの`dataMappings`、ロードルールの`conditions`から変数を参照するために使用される変数識別子。|
|`name`| 文字列| 変数のタイトル。|
|`alias`| 文字列| 変数名。|
|`type`| 文字列| 変数タイプを表すプレフィックス。&lt;br&gt;  `ls` - ローカル保存 &lt;br&gt; `ss` - セッション保存 &lt;br&gt; `udo` - ユニバーサルデータオブジェクト&lt;br&gt; `qp` - クエリ文字列パラメータ&lt;br&gt; `cp` - クッキー&lt;br&gt; `js` - JavaScript変数&lt;br&gt; `meta` - メタデータ要素&lt;br&gt; `va` - AudienceStream属性 |
|`notes`| 文字列| 変数に関するメモ。|
|`context`| 配列| AudienceStreamからインポートされた属性の範囲。&lt;br&gt; 値: `current_visit`または`visitor`|
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
|`dataMappings`| マップ&amp;lt;文字列, 文字列&amp;gt;|  Tealium IQ変数とそれに対応するマップ先を返します。 |
|`selectedTargets`| マップ&amp;lt;文字列, ブール値&amp;gt;|  タグが公開される環境のオブジェクト。 |
|`environmentVersions`| マップ&amp;lt;文字列, ブール値&amp;gt;| このタグが最後に公開された環境の配列。|
|`advancedConfiguration`| オブジェクト|  タグ構成構成に対応する高度な構成のセット。&lt;br&gt; `advConfigBundle` — **True**または**False**&lt;br&gt; `advConfigLoadType` — **True**または**False**&lt;br&gt; `advConfigOptOut` — **True**&lt;br&gt; `advConfigSend`— **True**または**False** `advConfigSrc` — テキストフィールド&lt;br&gt; `tagTiming` — **DOM Ready**または**Prioritized** |
| `configuration` |  マップ &amp;lt;文字列, オブジェクト&amp;gt; |  ベンダーによって提供されるタグ構成の文字列とオブジェクトのマップ。 |
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
|`environmentVersions`| マップ&amp;lt;文字列, ブール値&amp;gt;| 各環境での現在の公開ロードルールバージョンのリスト。 |
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
|`scope`|文字列|拡張機能のスコープ名、またはタグスコープ拡張機能の場合はタグIDのカンマ区切りリストです。&lt;br&gt;`utag Sync`&lt;br&gt;`Pre Loader`&lt;br&gt;`Before Load Rules`&lt;br&gt;`After Load Rules`&lt;br&gt;`DOM Ready`&lt;br&gt;`Tag Scoped Extensions`&lt;br&gt;`After Tag Extensions` タグスコープ拡張機能とそれが`occurrence`とどのように動作するかについての詳細は、[スコープの理解]()を参照してください。|
|`occurrence`|文字列|ページロードごとにJavaScriptコード拡張が実行される回数を決定します。値: `Run Once`または`Run Always`。|
|`status`|文字列|オン/オフの状態: `active`または`inactive`。|
|`selectedTargets`|マップ&amp;lt;文字列, ブール&amp;gt;|拡張機能が公開される環境です。|
|`environmentVersions`|マップ&amp;lt;文字列, ブール&amp;gt;|拡張機能が公開される環境の配列です。|
|`conditions`|オブジェクトの配列|特定の拡張機能に構成された条件です。|
|`configuration`|マップ &amp;lt;文字列, オブジェクト&amp;gt;|各拡張機能の構成のマップです。|

## イベント

|オブジェクト|タイプ|説明|
|---|---|---|
|`id`|数値|イベントの一意のIDです。|
|`eventID`|数値|このイベントタイプのシステムIDです。この値は同じタイプのすべてのイベントで同じです。|
|`name`|文字列|イベントの名前です。|
|`status`|文字列|オン/オフの状態: `active`または`inactive`。|
|`eventType`|文字列|追跡されるイベントのタイプです。&lt;ul&gt;&lt;li&gt;[`mouseEvents`]()\- 次のユーザーアクションを含みます:&lt;ul&gt;&lt;li&gt;`click` \- 訪問がページ上でマウスをクリックしたとき。&lt;/li&gt;&lt;li&gt;`mousedown` \- 訪問がマウスを押し下げたとき。&lt;/li&gt;&lt;li&gt;`mouseup` \- 訪問がマウスを押し下げたとき。&lt;/li&gt;&lt;/ul&gt;&lt;li&gt;[`mouseOver`]() \- 訪問がページ上の特定の要素にマウスをホバーしたとき。&lt;/li&gt;&lt;li&gt; [`formSubmit`]() \- 訪問がページ上でフォームを提出したとき。&lt;/li&gt;&lt;li&gt;[`youtubeVideo`]() \- 訪問がページ上の埋め込まれたYouTubeビデオと対話したとき。&lt;/li&gt;&lt;li&gt;[`vimeoVideo`]() \- 訪問がページ上の埋め込まれたVimeoビデオと対話したとき。&lt;/li&gt;&lt;li&gt;[`html5Video`]() \- 訪問がページ上の埋め込まれたHTML5ビデオと対話したとき。&lt;/li&gt;&lt;li&gt;[`pageView`]() \- 訪問がページを閲覧したとき。&lt;/li&gt;&lt;li&gt;[`scroll`]() \- 訪問がページを縦または横にスクロールしたとき。&lt;/li&gt;&lt;li&gt;[`elementVisibility`]() \- ページが訪問に画面要素を表示したとき。&lt;/li&gt;&lt;/li&gt;&lt;/ul&gt;|
|`scope`|文字列|拡張機能のスコープ名、またはタグスコープイベントの場合はタグIDのカンマ区切りリストです。&lt;br&gt;`After Load Rules`&lt;br&gt;`DOM Ready`&lt;br&gt;タグスコープイベントについての詳細は、[スコープ]()を参照してください。|
|`trackingEvent`|文字列|イベントが発生したときに行われるイベントコールです。|
|`notes`|文字列|イベントに関するノートです。|
|`library`|文字列|関連するライブラリの名前です。|
|`eventLoadRulesList`|文字列|イベントで使用されるすべてのロードルールのリストです。|
|`eventTrigger`|オブジェクト|各イベントタイプに特有の構成です。イベントトリガーについての詳細は、[イベント &gt; イベントトリガー]()を参照してください。|
|`selectedTargets`|マップ\&lt;文字列, ブール&gt;|イベントが公開される環境です。|
|`environmentVersions`|マップ\&lt;文字列, ブール&gt;|イベントが公開される環境の配列です。|
|`eventVariables`|オブジェクト|各イベントタイプに特有の変数です。|
|`rules`|オブジェクト|イベントリスナーがページ上にロードされるタイミングを決定するルールです。|
|`usedIn`|オブジェクト|このイベントが使用されているIDのリストです。|