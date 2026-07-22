---
title: データレイヤー
description: ユニバーサルデータオブジェクトの組み込み変数について学びます。
url: https://docs.tealium.com/ja/platforms/javascript/data-layer/
---ユニバーサルデータオブジェクト（UDO）には、読み込まれたページに関する基本情報を収集する組み込み変数が含まれています。これらの変数には、`utag.js`によって作成されたクッキー、ページの標準DOM変数、および読み込まれた構成に関するTealium固有の変数が含まれます。

[詳細はこちら](https://docs.tealium.com/data-layer-variables/)でデータレイヤー変数の種類について学びましょう。

## 標準ページデータ

以下の変数は、ウェブページで利用可能な標準JavaScriptプロパティから生成されます。これらの変数は、ロードルール、拡張機能、データマッピング、および条件を使用するためにiQインターフェース内で自動的に表示されます。

これらの値はページのURLを前提としています：

```
http://www.example.com/path/file.html?param1=value1#hash=fragment
```

| 変数 | 説明 | 例 |
| --- | --- | --- |
| `dom.domain`| URLの完全なドメイン。出典: `location.hostname` | `www.example.com` |
| `dom.hash` | URLのハッシュフラグメント（#文字を除く）。出典: `location.hash` | `hash=fragment` |
| `dom.pathname` | URLのパス、クエリパラメータとドメインを除く。出典: `location.pathname` | `"/path/file.html"` |
| `dom.query_string`| URLの完全なクエリ文字列。出典: `location.search` |  `param1=value1` |
| `dom.referrer` | 前のページのURL。出典: `document.referrer` |   |
| `dom.title` | `<title>`タグの間に含まれるテキスト。出典: `document.title`| `"Test Page Name"`|
| `dom.url` | ページの完全なURL。出典: `document.URL` | `http://www.example.com/` `PATH/FILE.html?param1=VALUE#hash=FRAGMENT` |
| `dom.viewport_height` | ブラウザビューポートの高さ。出典: `window.innerHeight` または `document.documentElement. clientHeight` | `1320` |
| `dom.viewport_width` | ブラウザビューポートの幅。出典: `window.innerWidth` または `document.documentElement. clientWidth` | `1278` |

## クッキー

以下の変数は、`utag_main`という単一のクッキーに格納および維持されるか、バージョン4.50からは`utag_main_`クッキー名前空間のスタンドアロンクッキーとして存在します。すべての変数は、`cp.utag_main_`で接頭辞が付けられた別々の変数としてデータオブジェクトに表示されます。

これらの変数をiQ構成に追加するには、**Data Layer**タブから`Tealium Built-in Data`という名前の[データバンドルを使用](https://docs.tealium.com/data-bundles/)します。

| 変数 | 説明 | 例 |
| --- | --- | --- |
| `cp.utag_main__pn` | **セッションページビューカウント** - 現在のセッションで表示されたページ数 | `2` |
| `cp.utag_main__se` | **セッションイベントカウント** - 現在のセッションで追跡されたイベント数 | `2` |
| `cp.utag_main__sn` | **セッションカウント** - このユニーク訪問のセッション数 | `1` |
| `cp.utag_main__ss` | **セッションの開始かどうか** - ページビューがセッションの開始かどうかを示すフラグ（1=はい、0=いいえ） | `0` |
| `cp.utag_main__st` | **タイムスタンプ** - ミリ秒単位のUnix/Epochタイムスタンプ | `1522968400449` |
| `cp.utag_main_ses_id` | **セッションID** - セッションのユニーク識別子 | `1522965346545` |
| `cp.utag_main_v_id` | **訪問ID** - 各訪問のユニーク識別子 | `016297481...` (45文字) |

## Tealiumデータ

以下の変数は、ページに読み込まれた`utag.js`に関する情報と、内部で使用される他の値を含みます。

`ut.*`変数をiQ構成に追加するには、**Data Layer**タブから`Tealium Built-in Data`という名前の[データバンドルを使用](https://docs.tealium.com/data-bundles/)します。

| 変数 | 名前 | 例 |
| --- | --- | --- |
| `tealium_account` | アカウント名 | `sandbox` |
| `tealium_datasource` | データソースキー | `"abc123"` |
| `tealium_environment` | 公開環境 | `prod` |
| `tealium_event` | Tealiumイベント名（直接構成されていない場合はデフォルトで"view"または"link"） | `view` |
| `tealium_library_name` | ライブラリ名 | `utag.js` |
| `tealium_library_version` | ライブラリバージョン | `4.44.0` |
| `tealium_profile` | アカウントプロファイル | `main` |
| `tealium_random` | ランダム数 | `7782219635308327` |
| `tealium_session_id` | `utag_main_ses_id`のコピー | `1522965346545` |
| `tealium_timestamp_epoch` | 現在のUnixタイムスタンプ（秒単位） | `1522956509` |
| `tealium_timestamp_local` | ローカルタイムスタンプ | `2018-04-05T12:28:29.019` |
| `tealium_timestamp_utc` | UTCタイムスタンプ | `2018-04-05T19:28:29.019Z` |
| `tealium_visitor_id` | `utag_main_v_id`のコピー | `016297481...` (45文字) |
| `ut.account` | tealium_accountのコピー | `sandbox` |
| `ut.domain` | クッキー構成用のトップレベルドメイン | `example.com` |
| `ut.env` | `tealium_environment`のコピー | `prod` |
| `ut.event` | `tealium_event`のコピー | `view` |
| `ut.profile` | `tealium_profile`のコピー | `main` |
| `ut.session_id` | `tealium_session_id`のコピー | `1522956509018` |
| `ut.version` | 公開バージョン（`utag.js`バージョン + タイムスタンプ） | `ut4.44.201710171745` |
| `ut.visitor_id` | `tealium_visitor_id`のコピー |`016297481...` (45文字) |

## ローカルおよびセッション保存

ローカルおよびセッション保存キーは、`localStorage`および`sessionStorage`変数を使用してデータレイヤーに自動的に表示されます。

これらの保存変数を使用するには、**Tag Management > Data Layer > +Add Variable**に移動します。**UDO Variable**を選択し、ソース変数名を入力します。ローカル保存の場合は`ls.variable_name`を、セッション保存の場合は`ss.variable_name`を使用します。

ローカルおよびセッション保存変数についての詳細は、[Data Layer Variables](https://docs.tealium.com/data-layer-variables/)を参照してください。

## サンプル

以下は、`utag.data`内に見つかる組み込みデータのサンプルです。

```json
{  
    "cp.utag_main_v_id"       : "015da2e1daf10020914ce74dfaf00207900780700093c",
    "cp.utag_main__sn"        : "389",
    "cp.utag_main__ss"        : "0",
    "cp.utag_main__st"        : "1522970376944",
    "cp.utag_main__se"        : "2",
    "cp.utag_main_ses_id"     : "1522915346545",
    "cp.utag_main__pn"        : "8",
    "qp.param1"               : "value1",
    "qp.hash1"                : "val1",
    "dom.referrer"            : "",
    "dom.title"               : "Test Page",
    "dom.domain"              : "www.example.com",
    "dom.query_string"        : "param1=value1",
    "dom.hash"                : "hash=fragment",
    "dom.url"                 : "http://www.example.com/path/file.html?param1=value1#hash=fragment",
    "dom.pathname"            : "/path/file.html",
    "dom.viewport_height"     : 780,
    "dom.viewport_width"      : 1436,
    "ut.domain"               : "example.com",
    "ut.version"              : "ut4.44.201710171745",
    "ut.event"                : "view",
    "ut.visitor_id"           : "015da2e1daf10020914ce74dfaf00207900780700093c",
    "ut.session_id"           : "1522965346545",
    "ut.account"              : "sandbox",
    "ut.profile"              : "main",
    "ut.env"                  : "prod",
    "tealium_event"           : "view",
    "tealium_visitor_id"      : "015da2e1daf10020914ce74dfaf00207900780700093c",
    "tealium_session_id"      : "1522915346545",
    "tealium_datasource"      : "abc123",
    "tealium_account"         : "sandbox",
    "tealium_profile"         : "main",
    "tealium_environment"     : "prod",
    "tealium_random"          : "7421526627003796",
    "tealium_library_name"    : "utag.js",
    "tealium_library_version" : "4.44.0",
    "tealium_timestamp_epoch" : 1522968576,
    "tealium_timestamp_utc"   : "2018-04-05T22:49:36.945Z",
    "tealium_timestamp_local" : "2018-04-05T15:49:36.945"
}
```