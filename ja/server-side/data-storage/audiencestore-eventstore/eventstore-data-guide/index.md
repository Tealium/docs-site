---
title: EventStoreデータガイド
description: この記事では、EventStoreを通じて提供されるイベントレベルのデータポイントの概要を提供します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/eventstore-data-guide/
---
EventStoreは、サイトからのイベントレベルのデータを収集し、エクスポートする最も効率的な方法を提供します。

## 仕組み

1. [Tealium Collect](https://docs.tealium.com/tealium-collect-tag/)タグは、サイト上の[ライブイベントフィード](https://docs.tealium.com/about-event-feeds/)をキャプチャし、イベントをEventStoreにフィードします。これにより、基礎となるデータを表示し、ダウンロードすることができます。
1. キャプチャしたデータは、フラット化されたJSONファイルに圧縮され、TealiumのAmazon S3バケットからダウンロードできるようになります。ファイル内の各JSONオブジェクトには、イベントに関連する名前-値のペアの1行または複数行が含まれる場合があります。  
      
<blockquote>
イベントデータ（イベントフィード）を別の場所（例えば、自分のS3バケットやサーバー）に送信する場合、フィードはEventStoreに表示されません。
</blockquote>

1. S3バケットが100MB（非圧縮）のサイズに達するか、1時間が経過すると、いずれか早い方が来た時点で、データは圧縮され、Redshiftの準備が整います。
1. 圧縮されたデータはコピーされ、あなたのアカウントのRedshiftデータベースにインポートされます。

## Tealium Collectタグデータ

Tealium Collectタグは、以下のセクションで説明するように、いくつかの事前定義された変数とページからのデータを送信します。


<blockquote>
データログファイル内の`_t`で始まるレガシー値は無視してください。
</blockquote>


### デフォルト変数

| 変数 | 説明 |
|---| ---|
|`visitorid`| 訪問の一意のID。|
|`eventid`| イベントに固有の英数字識別子。|
|`eventtime`| イベントのUNIX/エポックタイムスタンプ、UTCタイムゾーンに基づいています。|
|`useragent`| ユーザーエージェントヘッダー。|

### DOM変数

| 変数 | 説明 |
|---| ---|
|`dom_domain`| サイトのドメイン。|
|`dom_pathname`| URLのパス名。|
|`dom_query_string`| URLのクエリストリング部分（`?`文字の後）。|
|`dom_url`| HTMLドキュメントの全URL。|
|`dom_title`| HTMLドキュメントのタイトル。|
|`dom_viewport_width`| デバイスの画面幅。|
|`dom_viewport_height`| デバイスの画面高さ。|

### ページURL変数

| 変数 | 説明 |
|---| ---|
|`pageurl_scheme`| URIプロトコル（`http`や`https`など）。|
|`pageurl_domain`| サイトのドメイン。|
|`pageurl_path`| URLのパス名。|
|`pageurl_querystring`| URLのクエリストリング部分（`?`文字の後）。|
|`pageurl_query_params_key`| 各クエリストリングパラメータには、パラメータキーと値を含むデータポイントがあります。|
|`pageurl_full_url`| クエリストリングパラメータなしのHTMLドキュメントのURL。|

### リファラーURL変数

| 変数 | 説明 |
|---| ---|
|`referrerurl_scheme`| リファラーURLのURIプロトコル（`http`や`https`など）。|
|`referrerurl_domain`| リファラーURLサイトのドメイン。|
|`referrerurl_path`| リファラーURLのパス名。|
|`referrerurl_querystring`| リファラーURLのクエリストリング部分（`?`文字の後）。|
|`referrerurl_query_params_key`| 各クエリストリングパラメータには、パラメータキーと値を含むデータポイントがあります。|
|`referrerurl_full_url`| リファラーページの全URL。|

### 実行されたタグ

| 変数 | 説明 |
|---| ---|
|`tags_profile_tag-uid_executed`|  <ul><li>成功したプロファイルとタグ。</li><li>各成功したタグトリガーには独自のエントリが含まれます。</li></ul> |

### 環境詳細変数

| 変数 | 説明 |
|---| ---|
|`ut.account`| Tealium iQアカウント。|
|`ut.profile`| Tealium iQプロファイル。|
|`ut.env`| `utag.js`ファイルに関連する公開環境。|

### Tealium組み込み変数

Tealium組み込み変数の完全なリストは、[Built-In Data Layer Variables](https://docs.tealium.com/platforms/javascript/built-in-variables/)記事で提供されています。

| 変数 | 説明 |
|---| ---|
|`ut.event`| トラッキングされているイベントの名前、例えばビューやリンク。 |
|`ut.version`| `utag.js`のバージョン番号、公開タイムスタンプが続きます。 |
|`ut.domain`| 現在読み込まれているウェブページのトップレベルドメイン。 |
|`tealium_session_number`| `cp.utag_main__sn`の既存の値の複製。 |
|`tealium_session_event_number`| 現在のセッション（訪問）でのutag.link/view/track呼び出しの数をカウントする`cp.utag_main__se`の新しいクッキー値。常に'1ページ'があり、そのページ上で多くのイベントが発生するシングルページアプリ（SPA）に便利です |

### ファーストパーティTealiumクッキー

| 変数 | 説明 |
|---| ---|
|`_ses_id`| セッションの一意の識別子。`utag.js`バージョン4.27以降が必要です。 |
|`_st`| 訪問が何もしない場合に訪問セッションが期限切れになる時間。これは訪問の現在の時間にセッションタイムアウト時間を加えたものです。このタイムアウト期間は通常30分（1800000ミリ秒）ですが、構成により異なる場合があります。`utag.cfg.session_timeout`の値は、[JavaScript Extension](https://docs.tealium.com/advanced-javascript-code-extension/)を使用してこの変数を変更することで上書きできます。`utag.js`バージョン4.26以降が必要です。 |
|`_v_id`| データプライバシーと同意ルールを遵守するための訪問に固有のID値。`utag.js`バージョン4.26以降が必要です。詳細については、[`utag.js`バージョン4.50](https://docs.tealium.com/platforms/javascript/version-4-50/)を参照してください。 |
|`_se`| 現在のセッション中のイベント数。 |
|`_ss`| セッション開始を示すフラグ値。値は`0`または`1`です。`utag.js`バージョン4.26以降が必要です。 |
|`_pn`| ページ番号値。新しいセッションごとに`1`から始まり、`utag.js`がロードされるたびに増加します。`utag.js`バージョン4.28以降が必要です。 |
|`_sn`| セッション数。`utag.js`バージョン4.28以降が必要です。 |
|`_dc_group`| **Sample Size**構成と一緒に使用するランダムな数値。Tealium Collectタグがどのイベントをサンプリングするかを決定します。 |
|`_dc_visit`| Collectタグが発火したセッション数。最初の訪問では`1`から始まります。 |
|`_dc_event`| Collectタグが発火したイベント数。訪問の最初のページビューでは`1`から始まります。 |
|`_dc_region`| 訪問セッションが保存されているAudienceStream地域、HTTPレスポンスヘッダーから収集されます。このクッキーは、[データレイヤーのエンリッチメント](https://docs.tealium.com/data-layer-enrichment/)のエンドポイントを決定するために使用されます。 |

### 追加変数

タグは、以下を含むページからの他のデータを収集します：

* データレイヤーで定義されたデータポイント。任意の値の最大文字長は255文字です。
* ウェブページの要素、例えばメタデータ、クッキーパラメータ、JavaScriptページ変数。
* リアルユーザーモニタリング（RUM）データを収集するためのパフォーマンスタイミングメトリクス。このデータは、ユーザーの体験を理解するために使用できます。例えば、あなたのサイトのページでのブラウザーのDOMインタラクティブ状態までの時間など。  

| パフォーマンスタイミング変数 | 説明 |
|---| ---|
|`timing.domain`| タイミングデータが収集されたドメイン。|
|`timing.pathname`| タイミングデータが収集されたパス名（ウェブページ）。|
|`timing.query_string`| タイミングデータが収集されたURLのクエリストリング値。|
|`timing.timestamp`| タイミングデータが収集された日時（クライアントのウェブブラウザのエポック時間）。|
|`timing.dns`| `t.domainLookupStart`|
|`timing.connect`| `t.connectStart`|
|`timing.response`| `t.responseStart`|
|`timing.dom_loading_to_interactive`| `t.domInteractive`から`t.domLoading`を引いた値|
|`timing.dom_interactive_to_complete`| `t.domComplete`から`t.domInteractive`を引いた値|
|`timing.load`| `t.loadEventEnd`から`t.loadEventStart`を引いた値|
|`timing.time_to_first_byte`| `t.responseStart`から`t.connectEnd`を引いた値|
|`timing.front_end`| `t.loadEventStart`から`t.responseEnd`を引いた値|
|`timing.fetch_to_response`| `t.responseStart`から`t.fetchStart`を引いた値|
|`timing.fetch_to_complete`| `t.domComplete`から`t.fetchStart`を引いた値|
|`timing.fetch_to_interactive`| `t.domInteractive` から `t.fetchStart `を引いたもの|


<blockquote>
データポイントの値がゼロの場合、タイミング情報は取得されません。報告や平均を出す際にはゼロの値は無視できます。
</blockquote>


## 訪問のタイムゾーンの計算

訪問のタイムゾーンはEventStoreデータには送信されません。`_ss`が`1`のレコードで`EventTime`と`_ses_id`の差を見ることでタイムゾーンを計算できます。そのレコードはセッションの開始を示しています。

`utag.cfg.session_timeout`がわかっている場合、`_st`から`utag.cfg.session_timeout`を引くことでユーザーの現地時間を計算できます。その後、現在の時間と`EventTime`の差を見ることでタイムゾーンを計算できます。このアプローチは任意のレコードに使用できます。

## utag.jsのバージョン

個々のutagバージョンについての詳細情報は、[utag.jsリリースノート](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag/)をご覧ください。

## サンプルJSONオブジェクト

```json
{
    "visitorid": "014fb34a718e001ad754191d58ff1c074003a06c00c48",
    "eventid": "65f61a4b-54ca-4adf-b757-657e1711f6e7",
    "eventtime": 1441822083000,
    "useragent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5) AppleWebKit/600.8.9 (KHTML, like Gecko) Version/8.0.8 Safari/600.8.9",
    "dom_domain": "tealium.com",
    "dom_pathname": "/products/audiencestream/",
    "dom_query_string": "",
    "dom_url": "http://tealium.com/products/audiencestream/",
    "dom_title": "AudienceStream | Real-time Data Action Engine | Tealium",
    "dom_viewport_width": "1670",
    "dom_viewport_height": "1059",
    "pageurl_scheme": "http",
    "pageurl_domain": "tealium.com",
    "pageurl_path": "/products/audiencestream/",
    "pageurl_querystring": "",
    "pageurl_full_url": "http://tealium.com/products/audiencestream/",
    "referrerurl_scheme": "https",
    "referrerurl_domain": "google.com",
    "referrerurl_path": "",
    "referrerurl_querystring": "",
    "referrerurl_full_url": "https://www.google.com/",
    "tags_tiq_as_3_executed": true,
    "tags_tiq_as_1_executed": true,
    "udo_ut_account": "tealium",
    "udo_ut_profile": "main",
    "udo_ut_env": "prod",
    "udo_ut_event": "view",
    "udo_ut_version": "ut4.39.201509091709",
    "udo_ut_domain": "tealium.com",
    "firstpartycookies_utag_main_ses_id": "1441822044558",
    "firstpartycookies_utag_main__st": "1441823881730",
    "firstpartycookies_utag_main_v_id": "014fb34a718e001ad754191d58ff1c074003a06c00c48",
    "firstpartycookies_utag_main__ss": "0",
    "firstpartycookies_utag_main__pn": "2",
    "firstpartycookies_utag_main__sn": "1",
    "firstpartycookies_utag_main_dc_visit": "1",
    "firstpartycookies_utag_main_dc_event": "2",
    "firstpartycookies_utag_main_dc_region": "us-west-1",
    "firstpartycookies__gat": "1",
    "firstpartycookies__ga": "GA1.2.2095105468.1441822080",
    "js_page.is_mobile": "false",
    "js_page.is_tablet": "false",
    "device_type": "desktop",
    "udo_page_name": "AudienceStream | Real-time Data Action Engine | Tealium",
    "udo_site_name": "Tealium",
    "udo_site_description": "Tag Management and Audience Segmentation",
    "udo_page_type": "page",
    "udo_post_author": "tealium",
    "udo_post_date": "2014/11/26",
}
```

## パフォーマンスタイミングメトリクス

パフォーマンスタイミングメトリクスについての追加情報は、以下を参照してください：

* [Navigation Timingの実用ガイド](http://calendar.perfplanet.com/2011/a-practical-guide-to-the-navigation-timing-api/)
* [Web APIs > Navigation Timing API](https://developer.mozilla.org/en-US/docs/Web/API/Navigation_timing_API)
