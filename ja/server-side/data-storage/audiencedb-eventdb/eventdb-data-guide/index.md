---
title: EventDB データガイド
description: このガイドでは、組み込み列、Cookie 変数、タグ実行データ、パフォーマンスタイミング指標など、EventDB で利用可能なデータについて説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencedb-eventdb/eventdb-data-guide/
---

<blockquote>
アカウント内の該当するプロファイルで EventDB を有効にするには、アカウントマネージャーにお問い合わせください。EventDB に保存する属性の構成については、[AudienceDB と EventDB の構成]()を参照してください。
</blockquote>


EventDB は、[Tealium Collect タグ](https://docs.tealium.com/tealium-collect-tag/)またはその他の Collect ライブラリによって収集されたイベントレベルのデータを保存します。EventDB はデータソースとして [EventStore](https://docs.tealium.com/audiencestore-and-eventstore/) を使用し、そのデータを Amazon Redshift に読み込んで、SQL ベースのクエリを実行できるようにします。

## 仕組み

EventDB は、以下の手順で EventStore からデータを読み込みます。

1. Tealium Collect タグがイベントデータを EventStore に送信します。データは、フラット化された JSON として Amazon S3 バケットに保存されます。
1. S3 バケットの非圧縮時のサイズが 100 MB に達するか、1 時間が経過すると、いずれか早い時点で、システムがデータを圧縮して Redshift に読み込む準備をします。
1. 圧縮後、システムはデータをアカウントの Redshift データベースにコピーしてインポートします。

新しいデータは、Redshift クラスターの負荷に応じて 30～90 分以内に EventDB に保存されます。

## イベントフィードとテーブル

各イベントフィードは、Redshift スキーマ `ACCOUNT__PROFILE` に保存されます。`ACCOUNT__PROFILE` は、Tealium のアカウントとプロファイルを二重アンダースコアで区切ったものです（例：`mycompany__main`）。このスキーマ内で、各[イベントフィード](https://docs.tealium.com/about-event-feeds/)には以下が含まれます。

* `events__{event-feed-id}` という名前のベーステーブル
* 説明的な列名を持つビュー：`events_view__{feed-name}__{event-feed-id}`

イベントフィード ID は、Event Streaming 内でフィードを識別するための ID です。フィード ID を確認するには、**ライブイベント**に移動してフィードをクリックし、URL を確認します。

![](https://docs.tealium.com/images/server-side/eventstore-id-in-url-highlighted.png)

たとえば、スキーマ `mycompany__main` 内にある、ID が `7f78639b-34c2-4f8e-a575-d132c1008c80` の「Conversions」という名前のフィードの場合は、以下のようになります。

| テーブルタイプ | 完全なテーブル参照 |
|---|---|
| ベーステーブル | `mycompany__main.events__7f78639b_34c2_4f8e_a575_d132c1008c80` |
| ビュー | `mycompany__main.events_view__conversions__7f78639b_34c2_4f8e_a575_d132c1008c80` |

すべてのイベントフィードでは、フィード ID の代わりに固定名を使用します。

| テーブルタイプ | 完全なテーブル参照 |
|---|---|
| ベーステーブル | `mycompany__main.events__all_events` |
| ビュー | `mycompany__main.events_view__all_events__all_events` |

## 列の命名規則

EventDB では、同じデータにアクセスする方法が 2 つあります。ベーステーブルでは、`pageurl_full_url` や `firstpartycookies_utag_main_ses_id` など、プレフィックス付きの短い列名を使用します。ビューでは、`event - page url - full_url` や `event - first party cookies - utag_main_ses_id` など、説明的な列名を使用します。

このガイドでは、ベーステーブルの列名について説明します。以下のプレフィックスは、データのカテゴリを示します。

| プレフィックス | データカテゴリ |
|---|---|
| *（なし）* | 組み込み列 |
| `dom_` | ページから取得された DOM 変数 |
| `firstpartycookies_` | ファーストパーティ Cookie の値 |
| `js_` | ページの JavaScript 変数 |
| `meta_` | ページのメタデータ |
| `pageurl_` | ページ URL の構成要素 |
| `referrerurl_` | 参照元 URL の構成要素 |
| `tags_` | タグ実行データ |
| `udo_` | データレイヤー変数 |

すべての EventDB テーブルに、すべてのプレフィックスが表示されるわけではありません。以下の列は常に含まれます。

* DOM 属性（`dom_`）
* 事前に読み込まれた Tealium イベント属性（`udo_tealium_*`、`udo_ut_*`）
* タグ実行データ（`tags_`）
* ファーストパーティ Cookie の値（`firstpartycookies_`）
* ページ URL と参照元 URL の構成要素（`pageurl_`、`referrerurl_`）

以下の列は、対応するイベント属性が EventDB に対して有効になっている場合にのみ表示されます。

* JavaScript 変数（`js_`）
* ページのメタデータ（`meta_`）
* カスタムデータレイヤー変数（`udo_`）— データレイヤーに変数が存在する場合にのみ含まれます

詳細については、[AudienceDB と EventDB の構成]()を参照してください。

## 組み込み列

Tealium Collect タグは、以下のセクションで説明する複数の定義済み変数をイベントデータとともに送信します。

### デフォルト列

| 列 | 説明 |
|---|---|
| `visitorid` | 訪問の一意の ID。 |
| `eventid` | イベントに固有の英数字の識別子。 |
| `eventtime` | Amazon Redshift に UTC 日時として保存されるイベントのタイムスタンプ（例：`2024-08-01 00:00:02`）。これは、EventStore で使用されるエポックミリ秒表現とは異なります。 |
| `useragent` | クライアントのユーザーエージェントヘッダー。 |
| `clientip` | クライアントの IP アドレス。[サーバーサイドのアカウント構成](https://docs.tealium.com/server-side-account-settings/#general-settings)で、**訪問 IP 属性を有効化**構成を有効にする必要があります。 |

### DOM 変数

ページから取得された DOM データは、`dom_` プレフィックスが付いた列として表示されます。DOM 属性は常に EventDB に送信され、除外することはできません。詳細については、[AudienceDB と EventDB の構成]()を参照してください。

| 列 | 説明 |
|---|---|
| `dom_domain` | サイトのドメイン。 |
| `dom_pathname` | URL のパス名。 |
| `dom_query_string` | DOM から直接取得された URL のクエリ文字列部分（`document.location.search`）。 |
| `dom_url` | HTML ドキュメントの完全な URL。 |
| `dom_title` | HTML ドキュメントのタイトル。 |
| `dom_viewport_width` | デバイスの画面幅。 |
| `dom_viewport_height` | デバイスの画面の高さ。 |

### ページ URL 変数

| 列 | 説明 |
|---|---|
| `pageurl_scheme` | `http` や `https` などの URI プロトコル。 |
| `pageurl_domain` | サイトのドメイン。 |
| `pageurl_path` | URL のパス名。 |
| `pageurl_querystring` | 完全なページ URL から解析された、URL のクエリ文字列部分。 |
| `pageurl_query_params_KEY` | 各クエリ文字列パラメータについて、そのパラメータ値を含む列。`KEY` はパラメータ名です。 |
| `pageurl_full_url` | ページの完全な URL。 |

### 参照元 URL 変数

| 列 | 説明 |
|---|---|
| `referrerurl_scheme` | 参照元 URL の URI プロトコル。 |
| `referrerurl_domain` | 参照元サイトのドメイン。 |
| `referrerurl_path` | 参照元 URL のパス名。 |
| `referrerurl_querystring` | 参照元 URL の `?` 文字に続くクエリ文字列部分。 |
| `referrerurl_query_params_KEY` | 参照元 URL の各クエリ文字列パラメータについて、そのパラメータ値を含む列。`KEY` はパラメータ名です。 |
| `referrerurl_full_url` | 参照元ページの完全な URL。 |
### ファーストパーティ Cookie 変数

ファーストパーティ Cookie の値には、`firstpartycookies_` というプレフィックスが付いた列が使用されます。EventDB は、`utag_main` だけでなく、すべてのブラウザー Cookie から値を取得します。列名は Cookie 名とキーを反映します。たとえば、`firstpartycookies_utag_main_ses_id` は `utag_main` Cookie の `ses_id` キーに対応します。

| 列 | 説明 |
|---|---|
| `firstpartycookies_utag_main_ses_id` | セッションの一意の識別子。 |
| `firstpartycookies_utag_main__st` | 現在の訪問セッションが期限切れになる時刻（ミリ秒単位）。 |
| `firstpartycookies_utag_main_v_id` | 訪問 ID。 |
| `firstpartycookies_utag_main__ss` | セッションの開始を示すフラグ。値は `0` または `1` です。 |
| `firstpartycookies_utag_main__pn` | 現在のセッション内のページ番号。ページが読み込まれるたびに増加します。 |
| `firstpartycookies_utag_main__sn` | この訪問のセッション数。 |
| `firstpartycookies_utag_main__se` | 現在のセッション中のイベント数。 |
| `firstpartycookies_utag_main_dc_region` | 訪問セッションデータが保存される Customer Data Platform（CDP）リージョン。HTTP レスポンスヘッダーから収集されます。 |
| `firstpartycookies_utag_main_dc_group` | Tealium Collect タグの **Sample Size** 構成と併用され、サンプリングするイベントを決定するための乱数。 |
| `firstpartycookies_utag_main_dc_visit` | （レガシー）Collect タグが実行されたセッション数。最初の訪問では `1` から始まります。 |
| `firstpartycookies_utag_main_dc_event` | （レガシー）Collect タグが実行されたイベント数。訪問の最初のページビューでは `1` から始まります。 |
| `firstpartycookies_COOKIENAME` | Cookie の値。`COOKIENAME` は Cookie 名です。たとえば、`_ga` Cookie は `firstpartycookies__ga` として表示されます。 |

### JavaScript 変数

ページの JavaScript 変数は、`js_` というプレフィックスが付いた列として表示されます。実際の列名は、サイトで利用可能な変数によって異なります。命名を確認するには、EventDB スキーマまたは [Live Events](https://docs.tealium.com/about-live-events/) を確認してください。

| 列 | 説明 |
|---|---|
| `js_VARIABLE` | ページの JavaScript 変数。 |

たとえば、`js_screen_availheight` は利用可能な画面の高さを取得し、`js__tealplc_libraryversion` は Tealium Private Label Cloud ライブラリのバージョンを取得します。

### メタ変数

ページの HTML メタデータは、`meta_` というプレフィックスが付いた列として表示されます。

| 列 | 説明 |
|---|---|
| `meta_VARIABLE` | HTML メタタグの値。`VARIABLE` はメタタグ名です。 |

たとえば、`meta_description` はページのメタディスクリプションを取得し、`meta_og_title` は Open Graph タイトルを取得します。

### 実行されたタグ

イベントで発火した各タグによって、次の形式の列が生成されます。

```
tags_PROFILE_TAGID_executed
```

`PROFILE` は Tag Management のプロファイル名、`TAGID` はタグの数値 ID です。イベントでタグが実行された場合、値は `true` になり、実行されなかった場合は `(null)` になります。

たとえば、`tags_platform_3_executed` は、`platform` プロファイルのタグ `3` がイベントで実行されたことを示します。

### データレイヤー（UDO）変数

イベントとともに送信されたデータレイヤー変数には、`udo_` というプレフィックスが付いた列が使用されます。たとえば、`page_name` という名前のデータレイヤー変数は `udo_page_name` にマッピングされます。各値の最大文字数は 255 文字です。

Tealium Collect タグは、`udo_` 名前空間で複数の組み込み変数も送信します。

| 列 | 説明 |
|---|---|
| `udo_tealium_event` | `view` や `link` などのイベント名。 |
| `udo_tealium_event_type` | `view` や `link` などのトラッキング呼び出しの種類。 |
| `udo_tealium_library_name` | `utag.js` などの Collect ライブラリ。 |
| `udo_tealium_library_version` | `utag.js` のバージョン番号。 |
| `udo_tealium_datasource` | Collect タグのデータソース識別子。 |
| `udo_tealium_random` | イベント用に生成された乱数。 |
| `udo_tealium_session_id` | セッションの一意の識別子。 |
| `udo_tealium_session_number` | この訪問のセッション数。 |
| `udo_tealium_session_event_number` | 現在のセッション内のイベント数。 |
| `udo_tealium_timestamp_epoch` | イベントの Unix エポックタイムスタンプ。 |
| `udo_tealium_timestamp_utc` | イベントの UTC タイムスタンプ。 |
| `udo_tealium_timestamp_local` | イベントのローカルタイムスタンプ。 |
| `udo_tealium_account` | Tealium アカウント。 |
| `udo_tealium_profile` | Tag Management のプロファイル名。 |
| `udo_tealium_environment` | `prod` などのパブリッシュ環境。 |
| `udo_ut_account` | Tag Management アカウント。`udo_tealium_account` の以前の同等変数です。 |
| `udo_ut_profile` | Tag Management プロファイル。`udo_tealium_profile` の以前の同等変数です。 |
| `udo_ut_env` | `utag.js` ファイルに関連付けられたパブリッシュ環境。`udo_tealium_environment` の以前の同等変数です。 |
| `udo_ut_event` | `view` などのイベントタイプ。`udo_tealium_event` の以前の同等変数です。 |
| `udo_ut_domain` | ページのトップレベルドメイン。 |
| `udo_ut_version` | `utag.js` のバージョンとパブリッシュタイムスタンプ。 |

### パフォーマンスタイミング変数

ブラウザーのパフォーマンスタイミング指標は、`udo_timing_` というプレフィックスが付いた列として表示されます。これらの指標は、ページ読み込みパフォーマンスに関するリアルユーザーモニタリング（RUM）データを提供します。

| 列 | 説明 |
|---|---|
| `udo_timing_domain` | タイミングデータが収集されたドメイン。 |
| `udo_timing_timestamp` | タイミングデータが収集された日時（エポック時間）。 |
| `udo_timing_dns` | DNS ルックアップ時間。 |
| `udo_timing_connect` | 接続時間。 |
| `udo_timing_time_to_first_byte` | サーバーから最初のバイトを受信するまでの時間。 |
| `udo_timing_dom_loading_to_interactive` | DOM の読み込み開始から DOM が操作可能な状態になるまでの時間。 |
| `udo_timing_dom_interactive_to_complete` | DOM が操作可能な状態になってから DOM が完了状態になるまでの時間。 |
| `udo_timing_load` | ページ読み込みイベントの所要時間。 |
| `udo_timing_front_end` | フロントエンドのレンダリング時間。 |
| `udo_timing_fetch_to_response` | フェッチの開始からレスポンスの開始までの時間。 |
| `udo_timing_fetch_to_complete` | フェッチの開始から DOM が完了するまでの時間。 |
| `udo_timing_fetch_to_interactive` | フェッチの開始から DOM が操作可能になるまでの時間。 |
| `udo_timing_pathname` | タイミングデータが収集されたパス名。 |
| `udo_timing_query_string` | タイミングデータが収集された URL のクエリ文字列。 |
| `udo_timing_response` | サーバーのレスポンス時間。 |


<blockquote>
タイミング列の値がゼロの場合、タイミング情報は取得されていません。レポート作成時や平均値の計算時にはゼロの値を無視してください。
</blockquote>


## データ保持

EventDB のデータは、契約で指定された期間、Amazon Redshift で利用できます。イベントレコードが有効期限に達すると、自動的に消去されます。詳細については、[AudienceDB と EventDB について](https://docs.tealium.com/audiencedb-and-eventdb/)を参照してください。

## 訪問のタイムゾーンの計算

EventDB は、訪問のタイムゾーンを直接保存しません。タイムゾーンを計算するには、セッションの開始を示す `firstpartycookies_utag_main__ss` が `1` の行で、`eventtime` と `firstpartycookies_utag_main_ses_id` を比較します。`eventtime` は UTC 日時であり、`firstpartycookies_utag_main_ses_id` はエポックミリ秒値であるため、比較する前に `firstpartycookies_utag_main_ses_id` を UTC 日時に変換します。2 つの値の差が、訪問の UTC オフセットを表します。
## サンプル行

以下は、EventDB の単一行に含まれる列の代表的なサブセットです。

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
このサンプルには、組み込み列に加えて、`udo_user_type` などのアカウント固有のデータレイヤー変数が含まれています。EventDB テーブル内のデータレイヤー変数は、実装内容によって異なります。
</blockquote>
