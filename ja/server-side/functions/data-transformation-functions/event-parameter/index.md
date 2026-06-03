---
title: イベントパラメータ
description: この記事では、データ変換機能の `event` パラメータに関する情報を提供します。
url: https://docs.tealium.com/ja/server-side/functions/data-transformation-functions/event-parameter/
---
Tealium Collectからのイベント用のデータ変換機能には、`event` という名前のパラメータがあります。`event` パラメータは、イベントを記述するいくつかのプロパティとネストされたオブジェクトを含むメタデータオブジェクトです。実際のイベントデータは `event.data.udo` オブジェクトで参照されます。

詳細については、[イベントデータオブジェクト](#event-data-object)を参照してください。

 クラウドデータソースで使用される変換機能については、[データレコードオブジェクト]()を参照してください。

## イベントパラメータオブジェクト

`event` パラメータオブジェクトには以下のプロパティが含まれます：

|**プロパティ**| **タイプ**| **説明**| **書き込み可能**|
|---| ---| ---| ---|
|`account`| 文字列| アカウント情報。| いいえ|
|`client_ip`| 文字列| クライアントのIPアドレス。| いいえ|
|`data`| オブジェクト| [イベントデータオブジェクト](#event-data-object)を参照。| いいえ|
|`dataSourcePlatform`| 文字列| データソースプラットフォームの名前。| いいえ|
|`enrichmentOnly`| ブール値| ライブイベントの場合は常に `false`。`false` の場合、DataAccessにイベントを送信できます。バルクインポートイベントの場合（`event.type=&#34;BULK_IMPORT&#34;` のとき）、`true` になることがあります。この場合、イベントデータはエンリッチメントのみに使用できます。ファイルインポートイベントはデータ変換機能ではサポートされていません。| いいえ|
|`env`| 文字列| 実行環境（devまたはprod）を指定します。| いいえ|
|`event_id`| 文字列| イベントID。| いいえ|
|`new_visitor`| ブール値| このイベントがユーザーの最初の訪問である場合は `true`、それ以外の場合は `false`。| いいえ|
|`page_url`| オブジェクト| URLプロパティのオブジェクト。[URLオブジェクト](#url-object)を参照。&lt;br&gt; モバイルイベントでは省略されます。| いいえ|
|`post_time`| 数値| イベントのタイムスタンプ。| いいえ|
|`profile`| 文字列| アカウントのプロファイル。| いいえ|
|`referrer_url`| オブジェクト| URLプロパティのオブジェクト。[URLオブジェクト](#url-object)を参照。&lt;br&gt; モバイルイベントでは省略されます。| いいえ|
|`type`| 文字列| イベントがライブ訪問からのものか、バルクインポートイベントからのものかを指定します。値は `LIVE` または `BULK_IMPORT`。ファイルインポートイベントは現在データ変換機能ではサポートされていません。| いいえ|
|`useragent`| 文字列| ユーザーが使用しているソフトウェアを指定します。例えば、ウェブブラウザなど。| いいえ|
|`visitor_id`| 文字列| 訪問ID。| いいえ|
|`_forwarding_visitor_ids`| 文字列[]| このイベントを転送する訪問のIDを含みます。訪問スティッチングプロセスで使用されます。| いいえ|

### データソースプラットフォームの値

`dataSourcePlatform` プロパティの値は次のいずれかになります：`default`, `adobe_launch`, `affirm`, `android`, `braze`, `cordova`, `cSharp`, `fileImport`, `googleAMP`, `google_tag_manager`, `http_api_flattened`, `hubspot_wf`, `intercom`, `iOS`, `iterable`, `java`, `javascript`, `mailchimp`, `python`, `RES`, `roku`, `salesforce`, `sendgrid`, `slack`, `swift`, `tiqJavascript`, `tvOS`, `watchOS`, `zapier`.

ファイルインポートイベントは現在データ変換機能ではサポートされていません。

## イベントデータオブジェクト

`event.data` オブジェクトは、受信イベントを表し、変換可能な `event.data.udo` オブジェクトを含みます：

| プロパティ | タイプ | 説明 | 書き込み可能 |
|---| ---| ---| ---|
|`dom`| オブジェクト| イベントが発生したページに関する情報を含みます（ドメイン、クエリ文字列など）。モバイルイベントでは省略されます。詳細については、[データレイヤー](https://docs.tealium.com/platforms/javascript/data-layer/)を参照してください。| いいえ|
|`firstparty_tealium_cookies`| オブジェクト| データレイヤーで指定されたクッキープロパティを含むオブジェクト。&lt;br&gt; モバイルイベントでは省略されます。| いいえ|
|`js`| オブジェクト| データレイヤーで指定されたJavaScript変数プロパティを含むオブジェクト。&lt;br&gt; モバイルイベントでは省略されます。| いいえ|
|`meta`| オブジェクト| データレイヤーで指定されたメタデータプロパティを含むオブジェクト。&lt;br&gt; モバイルイベントでは省略されます。| いいえ|
|`udo`| オブジェクト| 受信イベントのプロパティを含むオブジェクト。一部のプロパティは読み取り専用です。[書き込み可能なプロパティ](#writable-properties)を参照してください。| はい|

### 書き込み可能なプロパティ

`event.data.udo` のカスタムイベント属性は書き込み可能ですが、一部の `tealium_` プロパティのみ変更可能です。

次の `tealium_` プロパティは変更可能ですが、削除はできません：

* `event.data.udo.tealium_datasource`
* `event.data.udo.tealium_environment`
* `event.data.udo.tealium_event`
* `event.data.udo.tealium_firstparty_visitor_id`
* `event.data.udo.tealium_thirdparty_visitor_id`
* `event.data.udo.tealium_library_name`
* `event.data.udo.tealium_library_version`
* `event.data.udo.tealium_random`
* `event.data.udo.tealium_timestamp_epoch`
* `event.data.udo.tealium_timestamp_local`
* `event.data.udo.tealium_timestamp_utc`
* `event.data.udo.tealium_session_number`

### 読み取り専用プロパティ

次のオブジェクトプロパティは読み取り専用で、変更できません：

* `event.data.udo.tealium_cf_ttl`
* `event.data.udo._dc_ttl_`
* `event.data.udo.platform`
* `event.data.udo.tealium_visitor_id`
* `event.data.udo.tealium_account`
* `event.data.udo.tealium_profile`
* `event.data.udo.tealium_session_id`

## URLオブジェクト

URLオブジェクトには、以下の標準URLプロパティが含まれます：

| プロパティ | タイプ | 説明 | 書き込み可能 |
|---| ---| ---| ---|
|`domain`| 文字列| URLのドメイン。| いいえ|
|`full_url`| 文字列| 完全なURL。| いいえ|
|`path`| 文字列| URLからのパス。空の場合があります。| いいえ|
|`query_params`| オブジェクト| 1つ以上のキー・値ペアを含むオブジェクト。各キー・値ペアはURLのクエリ文字列を指定します。例えば：&lt;br&gt; ```&#34;query_params&#34;: { &#34;utm_medium&#34;: &#34;PPC&#34;, &#34;utm_source&#34;: &#34;LinkedIn&#34; }```| いいえ|
|`querystring`| 文字列| URLからのクエリ文字列。| いいえ|
|`scheme`| 文字列| ウェブサイトの使用プロトコルを指定します。例えば、HTTPまたはHTTPS。| いいえ|

## イベントパラメータオブジェクトの例

以下は、`event` パラメータオブジェクトの例です：

```json
{
    &#34;account&#34;: &#34;XYZ_admin_acct&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;env&#34;: &#34;prod&#34;,
    &#34;data&#34;: {
        &#34;dom&#34;: {
            &#34;url&#34;: &#34;https://www.example.com&#34;,
            &#34;pathname&#34;: &#34;/&#34;,
            &#34;domain&#34;: &#34;example.com&#34;,
            &#34;hash&#34;: &#34;&#34;,
            &#34;query_string&#34;: &#34;&#34;,
            &#34;title&#34;: &#34;Homepage&#34;
        },
	&#34;js&#34;: {},
	&#34;meta&#34;: {},
	&#34;udo&#34;: {
            &#34;page_view&#34;: &#34;view&#34;,
            &#34;tealium_account&#34;: &#34;XYZ_admin_acct&#34;,
            &#34;tealium_profile&#34;: &#34;main&#34;,
            &#34;page_name&#34;: &#34;Homepage&#34;,
            &#34;page_type&#34;: &#34;main&#34;,
            &#34;tealium_event&#34;: &#34;page_view&#34;,
            &#34;user&#34;: {
                &#34;browser_lang&#34;: &#34;en-us&#34;,
                &#34;ipcinfo&#34;: &#34;en-us&#34;,
                &#34;signedin&#34;: false,
                &#34;city&#34;: &#34;san diego&#34;,
                &#34;country&#34;: &#34;us&#34;,
                &#34;country_name&#34;: &#34;united states&#34;,
                &#34;registry_city&#34;: &#34;san diego&#34;,
                &#34;registry_country_code&#34;: &#34;us&#34;,
                &#34;registry_state&#34;: &#34;ca&#34;,
                &#34;state&#34;: &#34;ca&#34;
            }
        },
        &#34;firstparty_tealium_cookies&#34;: {
             &#34;trace_id&#34;: &#34;&#34;
        }
    },
    &#34;type&#34;: &#34;LIVE&#34;,
    &#34;enrichmentOnly&#34;: false,
    &#34;event_id&#34;: &#34;example-event-id&#34;,
    &#34;visitor_id&#34;: &#34;example-visitor-id&#34;,
    &#34;post_time&#34;: 1655410928993,
    &#34;useragent&#34;: &#34;Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.0.0 Safari/537.36&#34;,
    &#34;client_ip&#34;: &#34;&#34;,
    &#34;new_visitor&#34;: false
}
```