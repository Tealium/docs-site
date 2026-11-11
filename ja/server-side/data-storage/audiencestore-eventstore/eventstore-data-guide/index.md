---
title: EventStoreデータガイド
description: この記事では、EventStoreを通じて利用できるイベントレベルのデータポイントの概要について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/eventstore-data-guide/
---
EventStoreは、サイトからイベントレベルのデータを収集してエクスポートするための最も効率的な方法を提供します。

## 仕組み

1. [Tealium Collect](https://docs.tealium.com/tealium-collect-tag/)タグは、サイト上の[ライブイベントフィード](https://docs.tealium.com/about-event-feeds/)を取得し、イベントをEventStoreに送信します。EventStoreでは、基となるデータを表示およびダウンロードできます。
1. 取得されたデータはフラット化されたJSONファイルに圧縮され、TealiumのAmazon S3バケットからダウンロードできるようになります。ファイル内の各JSONオブジェクトには、イベントに関連付けられた名前と値のペアからなる行が1つ以上含まれる場合があります。  
      
<blockquote>
イベントデータ（イベントフィード）を独自のS3バケットやサーバーなどの別の場所に送信した場合、そのフィードはEventStoreに表示されません。
</blockquote>

1. S3バケットのサイズが100 MB（非圧縮）に達するか、1時間が経過した時点のいずれか早い方で、データが圧縮され、Redshift向けに準備されます。
1. 圧縮されたデータは、アカウントのRedshiftデータベースにコピーされ、インポートされます。

## Tealium Collectタグのデータ

Tealium Collectタグは、以下のセクションで説明するように、事前定義された複数の変数とページ上のデータを送信します。


<blockquote>
データログファイルでは、接頭辞として`_t`が付いているレガシー値を無視してください。
</blockquote>


### デフォルト変数

| 変数 | 説明 |
|---| ---|
|`visitorid`| 訪問の一意のID。|
|`eventid`| イベントに固有の英数字識別子。|
|`eventtime`| UTCタイムゾーンに基づくイベントのUNIX／エポックタイムスタンプ。|
|`useragent`| ユーザーエージェントヘッダー。|

### DOM変数

| 変数 | 説明 |
|---| ---|
|`dom_domain`| サイトのドメイン。|
|`dom_pathname`| URLのパス名。|
|`dom_query_string`| URL内の疑問符（`?`）に続くクエリ文字列部分。|
|`dom_url`| HTMLドキュメントの完全なURL。|
|`dom_title`| HTMLドキュメントのタイトル。|
|`dom_viewport_width`| デバイス画面の幅。|
|`dom_viewport_height`| デバイス画面の高さ。|

### ページURL変数

| 変数 | 説明 |
|---| ---|
|`pageurl_scheme`| `http`や`https`などのUniform Resource Identifier（URI）プロトコル。|
|`pageurl_domain`| サイトのドメイン。|
|`pageurl_path`| URLのパス名。|
|`pageurl_querystring`| URL内の疑問符（`?`）に続くクエリ文字列部分。|
|`pageurl_query_params_key`| クエリ文字列の各パラメータには、パラメータのキーと値を含むデータポイントがあります。|
|`pageurl_full_url`| クエリ文字列パラメータを除いたHTMLドキュメントのURL。|

### 参照元URL変数

| 変数 | 説明 |
|---| ---|
|`referrerurl_scheme`| `http`や`https`など、参照元URLのURIプロトコル。|
|`referrerurl_domain`| 参照元URLサイトのドメイン。|
|`referrerurl_path`| 参照元URLのパス名。|
|`referrerurl_querystring`| 参照元URL内の「?」文字に続くクエリ文字列部分。|
|`referrerurl_query_params_key`| クエリ文字列の各パラメータには、パラメータのキーと値を含むデータポイントがあります。|
|`referrerurl_full_url`| 参照元ページの完全なURL。|

### 実行されたタグ

| 変数 | 説明 |
|---| ---|
|`tags_profile_tag-uid_executed`| <ul><li>正常に実行されたプロファイルとタグ。</li><li>正常にトリガーされた各タグには、それぞれ独自のエントリが含まれます。</li></ul> |

### 環境詳細変数

| 変数 | 説明 |
|---| ---|
|`ut.account`| Tag Managementアカウント。|
|`ut.profile`| Tag Managementプロファイル。|
|`ut.env`| `utag.js`ファイルに関連付けられたパブリッシュ環境。|

### Tealium組み込み変数

Tealium組み込み変数の完全なリストについては、[組み込みデータレイヤー変数](https://docs.tealium.com/platforms/javascript/built-in-variables/)の記事を参照してください。

| 変数 | 説明 |
|---| ---|
|`ut.event`| ビューやリンクなど、トラッキング対象のイベント名。 |
|`ut.version`| `utag.js`のバージョン番号と、それに続くパブリッシュタイムスタンプ。 |
|`ut.domain`| 現在読み込まれているWebページのトップレベルドメイン。 |
|`tealium_session_number`| `cp.utag_main__sn`内の既存値の複製。 |
|`tealium_session_event_number`| 現在のセッション（訪問）におけるutag.link/view/track呼び出しの回数をカウントする、`cp.utag_main__se`内の新しいCookie値。常に「1ページ」で、そのページ上で多数のイベントが発生するシングルページアプリケーション（SPA）に役立ちます。 |

### TealiumのファーストパーティCookie

| 変数 | 説明 |
|---| ---|
|`_ses_id`| セッションの一意の識別子。`utag.js`バージョン4.27以降が必要です。 |
|`_st`| 訪問がそれ以上何もしなかった場合に、訪問セッションが期限切れになる時刻。訪問の現在時刻にセッションタイムアウト時間を加えた値です。このタイムアウト期間は、別途構成されていない限り、通常30分（1800000ミリ秒）です。`utag.cfg.session_timeout`の値は、[JavaScript拡張機能](https://docs.tealium.com/advanced-javascript-code-extension/)を使用してこの変数を変更することで上書きできます。`utag.js`バージョン4.26以降が必要です。 |
|`_v_id`| データプライバシーおよび同意に関する規則への準拠を確保するための、訪問に固有のID値。`utag.js`バージョン4.26以降が必要です。詳細については、[`utag.js`バージョン4.50](https://docs.tealium.com/platforms/javascript/version-4-50/)を参照してください。 |
|`_se`| 現在のセッション中のイベント数。 |
|`_ss`| セッションの開始を示すフラグ値。値は`0`または`1`です。`utag.js`バージョン4.26以降が必要です。 |
|`_pn`| ページ番号の値。新しいセッションごとに`1`から始まり、`utag.js`が読み込まれるたびに増加します。`utag.js`バージョン4.28以降が必要です。 |
|`_sn`| セッション数。`utag.js`バージョン4.28以降が必要です。 |
|`_dc_group`| Tealium Collectタグの**サンプルサイズ**構成とともに使用し、サンプリング対象となるイベントを決定するための乱数。 |
|`_dc_visit`| Collectタグが発火したセッションの数。最初の訪問では`1`から始まります。 |
|`_dc_event`| Collectタグが発火したイベントの数。訪問時の最初のページビューでは`1`から始まります。 |
|`_dc_region`| 訪問セッションが保存されるCustomer Data Platform（CDP）リージョン。HTTPレスポンスヘッダーから収集されます。このCookieは、[データレイヤーエンリッチメント](https://docs.tealium.com/data-layer-enrichment/)のエンドポイントを決定するために使用されます。 |
### その他の変数

タグは、以下を含むさまざまなデータをページから収集します。

* データレイヤーで定義されたデータポイント。各値の最大文字数は255文字です。
* メタデータ、Cookieパラメータ、JavaScriptページ変数などのWebページ要素。
* リアルユーザーモニタリング（RUM）データを収集するためのパフォーマンスタイミング指標。このデータを使用して、ユーザーエクスペリエンスを把握できます。たとえば、サイト上のページについて、ブラウザーがDOMインタラクティブ状態になるまでの時間を確認できます。

| パフォーマンスタイミング変数 | 説明 |
|---| ---|
|`timing.domain`| タイミングデータが収集されたドメイン。|
|`timing.pathname`| タイミングデータが収集されたパス名（Webページ）。|
|`timing.query_string`| タイミングデータが収集されたURLのクエリ文字列値。|
|`timing.timestamp`| タイミングデータが収集された日時（クライアントのWebブラウザーのエポック時間）。|
|`timing.dns`| `t.domainLookupStart`|
|`timing.connect`| `t.connectStart`|
|`timing.response`| `t.responseStart`|
|`timing.dom_loading_to_interactive`| `t.domInteractive`から` t.domLoading`を引いた値|
|`timing.dom_interactive_to_complete`| `t.domComplete`から` t.domInteractive`を引いた値|
|`timing.load`| `t.loadEventEnd`から` t.loadEventStart`を引いた値|
|`timing.time_to_first_byte`| `t.responseStart`から` t.connectEnd`を引いた値|
|`timing.front_end`| `t.loadEventStart`から` t.responseEnd`を引いた値|
|`timing.fetch_to_response`| `t.responseStart`から` t.fetchStart`を引いた値|
|`timing.fetch_to_complete`| `t.domComplete`から` t.fetchStart`を引いた値|
|`timing.fetch_to_interactive`| `t.domInteractive`から` t.fetchStart `を引いた値|


<blockquote>
データポイントの値がゼロの場合、タイミング情報は取得されていません。レポート作成時や平均値の計算時には、ゼロの値を無視できます。
</blockquote>


## 訪問のタイムゾーンの計算

訪問のタイムゾーンは、EventStoreデータでは送信されません。`_ss`が`1`であるレコードはセッションの開始を示すため、そのレコードの`EventTime`と`_ses_id`の差を確認することで、タイムゾーンを計算できます。

`utag.cfg.session_timeout`が既知の場合は、`_st`から`utag.cfg.session_timeout`を引くことでユーザーの現在のローカル時刻を計算し、その現在時刻と`EventTime`の差からタイムゾーンを計算できます。この方法は、どのレコードにも使用できます。

## utag.jsのバージョン

個々のutagバージョンの詳細については、[utag.jsリリースノート](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag/)を参照してください。

## JSONオブジェクトの例

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
    "udo_page_name": "CDP | Real-time Data Action Engine | Tealium",
    "udo_site_name": "Tealium",
    "udo_site_description": "Tag Management and Audience Segmentation",
    "udo_page_type": "page",
    "udo_post_author": "tealium",
    "udo_post_date": "2014/11/26",
}
```

## パフォーマンスタイミング指標

パフォーマンスタイミング指標の詳細については、以下を参照してください。

* [Navigation Timingの実践ガイド](http://calendar.perfplanet.com/2011/a-practical-guide-to-the-navigation-timing-api/)
* [Web API > Navigation Timing API](https://developer.mozilla.org/en-US/docs/Web/API/Navigation_timing_API)