---
title: イベントパラメータ
description: この記事では、データ変換機能の `event` パラメータに関する情報を提供します。
url: https://docs.tealium.com/ja/server-side/functions/data-transformation-functions/event-parameter/
---
Tealium Collectからのイベント用のデータ変換機能には、`event` という名前のパラメータがあります。`event` パラメータは、イベントを記述するいくつかのプロパティとネストされたオブジェクトを含むメタデータオブジェクトです。実際のイベントデータは `event.data.udo` オブジェクトで参照されます。

詳細については、[イベントデータオブジェクト](#event-data-object)を参照してください。


<blockquote>
クラウドデータソースで使用される変換機能については、[データレコードオブジェクト](https://docs.tealium.com/about-data-record-functions/#data-record-object)を参照してください。
</blockquote>


## イベントパラメータオブジェクト

`event` パラメータオブジェクトには以下のプロパティが含まれます：

|**プロパティ**| **タイプ**| **説明**| **書き込み可能**|
|---| ---| ---| ---|
|`account`| 文字列| アカウント情報。| いいえ|
|`client_ip`| 文字列| クライアントのIPアドレス。| いいえ|
|`data`| オブジェクト| [イベントデータオブジェクト](#event-data-object)を参照。| いいえ|
|`dataSourcePlatform`| 文字列| データソースプラットフォームの名前。| いいえ|
|`enrichmentOnly`| ブール値| ライブイベントの場合は常に `false`。`false` の場合、DataAccessにイベントを送信できます。バルクインポートイベントの場合（`event.type="BULK_IMPORT"` のとき）、`true` になることがあります。この場合、イベントデータはエンリッチメントのみに使用できます。ファイルインポートイベントはデータ変換機能ではサポートされていません。| いいえ|
|`env`| 文字列| 実行環境（devまたはprod）を指定します。| いいえ|
|`event_id`| 文字列| イベントID。| いいえ|
|`new_visitor`| ブール値| このイベントがユーザーの最初の訪問である場合は `true`、それ以外の場合は `false`。| いいえ|
|`page_url`| オブジェクト| URLプロパティのオブジェクト。[URLオブジェクト](#url-object)を参照。<br> モバイルイベントでは省略されます。| いいえ|
|`post_time`| 数値| イベントのタイムスタンプ。| いいえ|
|`profile`| 文字列| アカウントのプロファイル。| いいえ|
|`referrer_url`| オブジェクト| URLプロパティのオブジェクト。[URLオブジェクト](#url-object)を参照。<br> モバイルイベントでは省略されます。| いいえ|
|`type`| 文字列| イベントがライブ訪問からのものか、バルクインポートイベントからのものかを指定します。値は `LIVE` または `BULK_IMPORT`。ファイルインポートイベントは現在データ変換機能ではサポートされていません。| いいえ|
|`useragent`| 文字列| ユーザーが使用しているソフトウェアを指定します。例えば、ウェブブラウザなど。| いいえ|
|`visitor_id`| 文字列| 訪問ID。| いいえ|
|`_forwarding_visitor_ids`| 文字列[]| このイベントを転送する訪問のIDを含みます。訪問スティッチングプロセスで使用されます。| いいえ|

### データソースプラットフォームの値

`dataSourcePlatform` プロパティの値は次のいずれかになります：`default`, `adobe_launch`, `affirm`, `android`, `braze`, `cordova`, `cSharp`, `fileImport`, `googleAMP`, `google_tag_manager`, `http_api_flattened`, `hubspot_wf`, `intercom`, `iOS`, `iterable`, `java`, `javascript`, `mailchimp`, `python`, `RES`, `roku`, `salesforce`, `sendgrid`, `slack`, `swift`, `tiqJavascript`, `tvOS`, `watchOS`, `zapier`.


<blockquote>
ファイルインポートイベントは現在データ変換機能ではサポートされていません。
</blockquote>


## イベントデータオブジェクト

`event.data` オブジェクトは、受信イベントを表し、変換可能な `event.data.udo` オブジェクトを含みます：

| プロパティ | タイプ | 説明 | 書き込み可能 |
|---| ---| ---| ---|
|`dom`| オブジェクト| イベントが発生したページに関する情報を含みます（ドメイン、クエリ文字列など）。モバイルイベントでは省略されます。詳細については、[データレイヤー](https://docs.tealium.com/platforms/javascript/data-layer/)を参照してください。| いいえ|
|`firstparty_tealium_cookies`| オブジェクト| データレイヤーで指定されたクッキープロパティを含むオブジェクト。<br> モバイルイベントでは省略されます。| いいえ|
|`js`| オブジェクト| データレイヤーで指定されたJavaScript変数プロパティを含むオブジェクト。<br> モバイルイベントでは省略されます。| いいえ|
|`meta`| オブジェクト| データレイヤーで指定されたメタデータプロパティを含むオブジェクト。<br> モバイルイベントでは省略されます。| いいえ|
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
|`query_params`| オブジェクト| 1つ以上のキー・値ペアを含むオブジェクト。各キー・値ペアはURLのクエリ文字列を指定します。例えば：<br> ```"query_params": { "utm_medium": "PPC", "utm_source": "LinkedIn" }```| いいえ|
|`querystring`| 文字列| URLからのクエリ文字列。| いいえ|
|`scheme`| 文字列| ウェブサイトの使用プロトコルを指定します。例えば、HTTPまたはHTTPS。| いいえ|

## イベントパラメータオブジェクトの例

以下は、`event` パラメータオブジェクトの例です：

```json
{
    "account": "XYZ_admin_acct",
    "profile": "main",
    "env": "prod",
    "data": {
        "dom": {
            "url": "https://www.example.com",
            "pathname": "/",
            "domain": "example.com",
            "hash": "",
            "query_string": "",
            "title": "Homepage"
        },
	"js": {},
	"meta": {},
	"udo": {
            "page_view": "view",
            "tealium_account": "XYZ_admin_acct",
            "tealium_profile": "main",
            "page_name": "Homepage",
            "page_type": "main",
            "tealium_event": "page_view",
            "user": {
                "browser_lang": "en-us",
                "ipcinfo": "en-us",
                "signedin": false,
                "city": "san diego",
                "country": "us",
                "country_name": "united states",
                "registry_city": "san diego",
                "registry_country_code": "us",
                "registry_state": "ca",
                "state": "ca"
            }
        },
        "firstparty_tealium_cookies": {
             "trace_id": ""
        }
    },
    "type": "LIVE",
    "enrichmentOnly": false,
    "event_id": "example-event-id",
    "visitor_id": "example-visitor-id",
    "post_time": 1655410928993,
    "useragent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.0.0 Safari/537.36",
    "client_ip": "",
    "new_visitor": false
}
```