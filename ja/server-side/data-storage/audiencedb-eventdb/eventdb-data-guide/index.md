---
title: EventDBデータガイド
description: このガイドでは、EventDBで利用可能なデータについて説明します。これには、組み込みの列、クッキー変数、タグ実行データ、およびパフォーマンスタイミングメトリクスが含まれます。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencedb-eventdb/eventdb-data-guide/
---

<blockquote>
EventDBをアカウントの適切なプロファイルで有効にするには、アカウントマネージャーに連絡してください。EventDBに格納される属性を構成する方法については、[AudienceDBおよびEventDBの構成]()を参照してください。
</blockquote>


EventDBは、[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)または他のCollectライブラリによってキャプチャされたイベントレベルのデータを保存します。EventDBは[EventStore](https://docs.tealium.com/audiencestore-and-eventstore/)をデータソースとして使用し、そのデータをAmazon RedshiftにロードしてSQLベースのクエリを実行します。

## 動作方法

EventDBは、以下のステップでEventStoreからデータをロードします：

1. Tealium CollectタグがイベントデータをEventStoreに送信し、そこでデータはフラット化されたJSONとしてAmazon S3バケットに保存されます。
1. S3バケットが100MBの非圧縮サイズに達するか、または1時間が経過すると、どちらか早い方で、システムはデータを圧縮してRedshiftの準備を行います。
1. 圧縮後、システムはデータをコピーしてあなたのアカウントのRedshiftデータベースにインポートします。

新しいデータは、Redshiftクラスターの負荷に応じて、30分から90分以内にEventDBに保存されます。

## イベントフィードとテーブル

各イベントフィードはRedshiftスキーマ `ACCOUNT__PROFILE` に保存されます。ここで `ACCOUNT__PROFILE` は、例えば `mycompany__main` のように、Tealiumアカウントとプロファイルがダブルアンダースコアで区切られたものです。そのスキーマ内で、各[イベントフィード](https://docs.tealium.com/about-event-feeds/)は：

* 基本テーブル名：`events__{event-feed-id}`
* 説明的な列名を持つビュー：`events_view__{feed-name}__{event-feed-id}`

イベントフィードIDはEventStreamでのフィードの識別子です。フィードIDを見つけるには、**Live Events**に行き、フィードをクリックし、URLを調べます。

![](https://docs.tealium.com/images/server-side/eventstore-id-in-url-highlighted.png)

たとえば、「Conversions」という名前のフィードでIDが `7f78639b-34c2-4f8e-a575-d132c1008c80` の場合、スキーマ `mycompany__main` では：

| テーブルタイプ | 完全なテーブル参照 |
|---|---|
| 基本テーブル | `mycompany__main.events__7f78639b_34c2_4f8e_a575_d132c1008c80` |
| ビュー | `mycompany__main.events_view__conversions__7f78639b_34c2_4f8e_a575_d132c1008c80` |

All EventsフィードはフィードIDの代わりに固定名を使用します：

| テーブルタイプ | 完全なテーブル参照 |
|---|---|
| 基本テーブル | `mycompany__main.events__all_events` |
| ビュー | `mycompany__main.events_view__all_events__all_events` |

## 列命名規則

EventDBは同じデータにアクセスするための2つの方法を提供します。基本テーブルは `pageurl_full_url` や `firstpartycookies_utag_main_ses_id` のような短い、接頭辞付きの列名を使用します。ビューは `event - page url - full_url` や `event - first party cookies - utag_main_ses_id` のような説明的な列名を使用します。

このガイドでは基本テーブルの列名を文書化しています。以下の接頭辞はデータのカテゴリを示します：

| 接頭辞 | データカテゴリ |
|---|---|
| *(なし)* | 組み込みの列 |
| `dom_` | ページからキャプチャされたDOM変数 |
| `firstpartycookies_` | 第一者クッキーの値 |
| `js_` | ページのJavaScript変数 |
| `meta_` | ページのメタデータ |
| `pageurl_` | ページURLのコンポーネント |
| `referrerurl_` | リファラーURLのコンポーネント |
| `tags_` | タグ実行データ |
| `udo_` | データレイヤー変数 |

すべての接頭辞がすべてのEventDBテーブルに現れるわけではありません。以下の列は常に含まれます：

* DOM属性 (`dom_`)
* プリロードされたTealiumイベント属性 (`udo_tealium_*`, `udo_ut_*`)
* タグ実行データ (`tags_`)
* 第一者クッキーの値 (`firstpartycookies_`)
* ページURLおよびリファラーURLのコンポーネント (`pageurl_`, `referrerurl_`)

以下の列は、対応するイベント属性がEventDBで有効になっている場合にのみ表示されます：

* JavaScript変数 (`js_`)
* ページのメタデータ (`meta_`)
* カスタムデータレイヤー変数 (`udo_`) — データレイヤーに変数が存在する場合のみ存在

詳細については、[AudienceDBおよびEventDBの構成]()を参照してください。

## 組み込みの列

Tealium Collectタグは、以下のセクションで説明されているように、イベントデータと一緒にいくつかの事前定義された変数を送信します。

### デフォルトの列

| 列 | 説明 |
|---|---|
| `visitorid` | 訪問の一意のIDです。 |
| `eventid` | イベントに固有の英数字識別子です。 |
| `eventtime` | イベントのタイムスタンプがUTC日時としてAmazon Redshiftに保存されます（例：`2024-08-01 00:00:02`）。これはEventStoreのエポックミリ秒表現とは異なります。 |
| `useragent` | クライアントのユーザーエージェントヘッダーです。 |
| `clientip` | クライアントのIPアドレスです。[サーバーサイドアカウント構成](https://docs.tealium.com/server-side-account-settings/#general-settings)で**訪問IP属性を有効にする**構成が必要です。 |

### DOM変数

ページのDOMデータは、`dom_`で始まる列として現れます。DOM属性は常にEventDBに送信され、除外することはできません。詳細については、[AudienceDBおよびEventDBの構成]()を参照してください。

| 列 | 説明 |
|---|---|
| `dom_domain` | サイトのドメインです。 |
| `dom_pathname` | URLのパス名です。 |
| `dom_query_string` | URLのクエリ文字列部分で、DOMから直接キャプチャされます（`document.location.search`）。 |
| `dom_url` | HTMLドキュメントの完全なURLです。 |
| `dom_title` | HTMLドキュメントのタイトルです。 |
| `dom_viewport_width` | デバイスの画面幅です。 |
| `dom_viewport_height` | デバイスの画面高さです。 |

### ページURL変数

| 列 | 説明 |
|---|---|
| `pageurl_scheme` | URIプロトコル、例えば `http` や `https` です。 |
| `pageurl_domain` | サイトのドメインです。 |
| `pageurl_path` | URLのパス名です。 |
| `pageurl_querystring` | ページの完全なURLから解析されたURLのクエリ文字列部分です。 |
| `pageurl_query_params_KEY` | 各クエリ文字列パラメータに対して、パラメータ名が `KEY` であるパラメータ値を含む列です。 |
| `pageurl_full_url` | ページの完全なURLです。 |

### リファラーURL変数

| 列 | 説明 |
|---|---|
| `referrerurl_scheme` | 参照元URLのURIプロトコルです。 |
| `referrerurl_domain` | 参照元サイトのドメインです。 |
| `referrerurl_path` | 参照元URLのパス名です。 |
| `referrerurl_querystring` | `?` 文字に続く参照元URLのクエリ文字列部分です。 |
| `referrerurl_query_params_KEY` | 各参照元URLクエリ文字列パラメータに対して、パラメータ名が `KEY` であるパラメータ値を含む列です。 |
| `referrerurl_full_url` | 参照元ページの完全なURLです。 |


### ファーストパーティクッキー変数

ファーストパーティクッキーの値は、`firstpartycookies_`で始まる列名を使用します。EventDBは`utag_main`だけでなく、すべてのブラウザクッキーから値を取得します。列名はクッキー名とキーを反映しています。例えば、`firstpartycookies_utag_main_ses_id`は`utag_main`クッキーの`ses_id`キーに対応します。

| 列 | 説明 |
|---|---|
| `firstpartycookies_utag_main_ses_id` | セッションの一意の識別子です。 |
| `firstpartycookies_utag_main__st` | 現在の訪問セッションが終了する時刻（ミリ秒単位）。 |
| `firstpartycookies_utag_main_v_id` | 訪問ID。 |
| `firstpartycookies_utag_main__ss` | セッション開始を示すフラグ。値は`0`または`1`です。 |
| `firstpartycookies_utag_main__pn` | 現在のセッション内のページ番号。ページを読み込むたびに増加します。 |
| `firstpartycookies_utag_main__sn` | この訪問のセッション数。 |
| `firstpartycookies_utag_main__se` | 現在のセッション中のイベント数。 |
| `firstpartycookies_utag_main_dc_region` | 訪問セッションデータが保持されるAudienceStream地域。HTTPレスポンスヘッダーから収集されます。 |
| `firstpartycookies_utag_main_dc_group` | Tealium Collectタグの**サンプルサイズ**構成で、どのイベントがサンプリングされるかを決定するために使用されるランダムな数値。 |
| `firstpartycookies_utag_main_dc_visit` | （レガシー）Collectタグが発火したセッション数。最初の訪問で`1`から始まります。 |
| `firstpartycookies_utag_main_dc_event` | （レガシー）Collectタグが発火したイベント数。訪問の最初のページビューで`1`から始まります。 |
| `firstpartycookies_COOKIENAME` | クッキー値。`COOKIENAME`はクッキー名です。例えば、`_ga`クッキーは`firstpartycookies__ga`として表示されます。 |

### JavaScript変数

ページのJavaScript変数は、`js_`で始まる列名として表示されます。サイトに存在する変数に応じて正確な列名が異なります。EventDBスキーマまたは[Live Events](https://docs.tealium.com/about-live-events/)を確認して命名を確認してください。

| 列 | 説明 |
|---|---|
| `js_VARIABLE` | ページのJavaScript変数。 |

例えば、`js_screen_availheight`は利用可能な画面の高さをキャプチャし、`js__tealplc_libraryversion`はTealium Private Label Cloudライブラリのバージョンをキャプチャします。

### メタ変数

ページのHTMLメタデータは、`meta_`で始まる列名として表示されます。

| 列 | 説明 |
|---|---|
| `meta_VARIABLE` | HTMLメタタグの値。`VARIABLE`はメタタグ名です。 |

例えば、`meta_description`はページのメタ説明をキャプチャし、`meta_og_title`はOpen Graphタイトルをキャプチャします。

### 実行されたタグ

イベントで発火する各タグは、次の形式で列を生成します：

```
tags_PROFILE_TAGID_executed
```

`PROFILE`はTealium iQプロファイル名、`TAGID`はタグの数値IDです。イベントでタグが実行された場合は`true`、実行されなかった場合は`(null)`となります。

例えば、`tags_platform_3_executed`は、`platform`プロファイルのタグ`3`がイベントで実行されたことを示します。

### データレイヤー（UDO）変数

イベントで送信されるデータレイヤー変数は、`udo_`で始まる列名を使用します。例えば、データレイヤー変数`page_name`は`udo_page_name`にマッピングされます。任意の単一値の最大文字数は255文字です。

Tealium Collectタグは、`udo_`名前空間でいくつかの組み込み変数も送信します：

| 列 | 説明 |
|---|---|
| `udo_tealium_event` | イベントの名前、例えば`view`や`link`。 |
| `udo_tealium_event_type` | トラッキングコールのタイプ、例えば`view`や`link`。 |
| `udo_tealium_library_name` | Collectライブラリ、例えば`utag.js`。 |
| `udo_tealium_library_version` | `utag.js`のバージョン番号。 |
| `udo_tealium_datasource` | Collectタグのデータソース識別子。 |
| `udo_tealium_random` | イベントのために生成されたランダムな数値。 |
| `udo_tealium_session_id` | セッションの一意の識別子。 |
| `udo_tealium_session_number` | この訪問のセッション数。 |
| `udo_tealium_session_event_number` | 現在のセッションのイベント数。 |
| `udo_tealium_timestamp_epoch` | イベントのUnixエポックタイムスタンプ。 |
| `udo_tealium_timestamp_utc` | イベントのUTCタイムスタンプ。 |
| `udo_tealium_timestamp_local` | イベントのローカルタイムスタンプ。 |
| `udo_tealium_account` | Tealiumアカウント。 |
| `udo_tealium_profile` | Tealium iQプロファイル名。 |
| `udo_tealium_environment` | 公開環境、例えば`prod`。 |
| `udo_ut_account` | Tealium iQアカウント。`udo_tealium_account`の以前の同等物。 |
| `udo_ut_profile` | Tealium iQプロファイル。`udo_tealium_profile`の以前の同等物。 |
| `udo_ut_env` | `utag.js`ファイルに関連する公開環境。`udo_tealium_environment`の以前の同等物。 |
| `udo_ut_event` | イベントタイプ、例えば`view`。`udo_tealium_event`の以前の同等物。 |
| `udo_ut_domain` | ページのトップレベルドメイン。 |
| `udo_ut_version` | `utag.js`のバージョンと公開タイムスタンプ。 |

### パフォーマンスタイミング変数

ブラウザのパフォーマンスタイミング指標は、`udo_timing_`で始まる列名として表示されます。これらの指標は、ページのロードパフォーマンスに関するリアルユーザーモニタリング（RUM）データを提供します。

| 列 | 説明 |
|---|---|
| `udo_timing_domain` | タイミングデータが収集されたドメイン。 |
| `udo_timing_timestamp` | タイミングデータが収集された日時（エポック時間）。 |
| `udo_timing_dns` | DNSルックアップ時間。 |
| `udo_timing_connect` | 接続時間。 |
| `udo_timing_time_to_first_byte` | サーバーから最初のバイトまでの時間。 |
| `udo_timing_dom_loading_to_interactive` | DOMローディングからDOMインタラクティブ状態までの時間。 |
| `udo_timing_dom_interactive_to_complete` | DOMインタラクティブからDOM完了状態までの時間。 |
| `udo_timing_load` | ページロードイベントの期間。 |
| `udo_timing_front_end` | フロントエンドのレンダリング時間。 |
| `udo_timing_fetch_to_response` | フェッチ開始からレスポンス開始までの時間。 |
| `udo_timing_fetch_to_complete` | フェッチ開始からDOM完了までの時間。 |
| `udo_timing_fetch_to_interactive` | フェッチ開始からDOMインタラクティブまでの時間。 |
| `udo_timing_pathname` | タイミングデータが収集されたパス名。 |
| `udo_timing_query_string` | タイミングデータが収集されたURLのクエリ文字列。 |
| `udo_timing_response` | サーバー応答時間。 |


<blockquote>
タイミング列の値がゼロの場合、タイミング情報はキャプチャされませんでした。報告や平均化の際にゼロ値を無視してください。
</blockquote>


## データ保持

EventDBのデータは、契約で指定された期間、Amazon Redshiftで利用可能です。イベントレコードが有効期限に達すると、自動的に削除されます。詳細については、[About AudienceDB and EventDB](https://docs.tealium.com/audiencedb-and-eventdb/)を参照してください。

## 訪問のタイムゾーンの計算

EventDBは訪問のタイムゾーンを直接保存しません。タイムゾーンを計算するには、`firstpartycookies_utag_main__ss`が`1`に等しい行で`eventtime`と`firstpartycookies_utag_main_ses_id`を比較します。これはセッションの開始を示します。`eventtime`はUTCの日時であり、`firstpartycookies_utag_main_ses_id`はエポックミリ秒値であるため、比較する前に`firstpartycookies_utag_main_ses_id`をUTCの日時に変換します。両者の差は訪問のUTCオフセットを表します。
## サンプル行

以下は、EventDBの単一行からの代表的な列のサブセットを示しています：

| 列 | サンプル値 |
|---|---|
| `visitorid` | `e9a2771b641f48009921b3a783db4c84` |
| `eventid` | `9ec23b59-2540-4a38-8ad0-2a1ec5d6016a` |
| `eventtime` | `2024-08-01 00:00:02` |
| `dom_title` | `countryroadgroup \| main` |
| `pageurl_scheme` | `https` |
| `pageurl_domain` | `my.tealiumiq.com` |
| `pageurl_path` | `/tms` |
| `pageurl_full_url` | `https://my.tealiumiq.com/tms` |
| `referrerurl_scheme` | `https` |
| `referrerurl_domain` | `my.tealiumiq.com` |
| `referrerurl_path` | `/tms` |
| `firstpartycookies_utag_main_ses_id` | `1722465600428` |
| `firstpartycookies_utag_main__pn` | `7` |
| `firstpartycookies_utag_main__sn` | `199` |
| `firstpartycookies_utag_main__ss` | `0` |
| `tags_platform_3_executed` | `true` |
| `udo_tealium_event` | `profile_publish_status` |
| `udo_tealium_library_name` | `utag.js` |
| `udo_tealium_library_version` | `4.48.0` |
| `udo_tealium_datasource` | `ujitge` |
| `udo_tealium_random` | `8550613331015047` |
| `udo_tealium_session_id` | `1722465600428` |
| `udo_tealium_session_number` | `199` |
| `udo_tealium_session_event_number` | `398` |
| `udo_tealium_environment` | `prod` |
| `udo_user_type` | `client` |


<blockquote>
このサンプルには、`udo_user_type` などのアカウント固有のデータレイヤー変数と組み込み列が含まれています。EventDBテーブルのデータレイヤー変数は、実装に依存します。
</blockquote>
