---
title: データレイヤー
description: ユニバーサル データ オブジェクトの組み込み変数について学習します。
url: https://docs.tealium.com/ja/platforms/javascript/data-layer/
---ユニバーサルデータオブジェクト（UDO）には、読み込まれたページに関する基本情報を収集する組み込み変数が含まれています。これらの変数には、`utag.js`によって作成されたクッキー、ページからの標準DOM変数、読み込まれた構成に関するTealium固有の変数が含まれます。

利用可能なデータレイヤー変数の種類について[詳しく学ぶ]()。

## 標準ページデータ

以下の変数は、ウェブページで利用可能な標準的なJavaScriptプロパティから生成されます。これらの変数は、ロードルール、拡張機能、データマッピング、条件とともにiQインターフェース内に自動的に表示されます。

これらの値は、ページのURLを前提としています：

```
http://www.example.com/path/file.html?param1=value1#hash=fragment
```

| 変数 | 説明 | 例 |
| --- | --- | --- |
| `dom.domain`| URLの完全なドメイン。ソース: `location.hostname` | `www.example.com` |
| `dom.hash` | URLのハッシュフラグメント（#文字を除く）。ソース: `location.hash` | `hash=fragment` |
| `dom.pathname` | URLのパス、クエリパラメータとドメインを除く。ソース: `location.pathname` | `&#34;/path/file.html&#34;` |
| `dom.query_string`| URLの完全なクエリストリング。ソース: `location.search` |  `param1=value1` |
| `dom.referrer` | 前のページのURL。ソース: `document.referrer` |   |
| `dom.title` | `&lt;title&gt;`タグ間のテキスト。ソース: `document.title`| `&#34;Test Page Name&#34;`|
| `dom.url` | ページの完全なURL。ソース: `document.URL` | `http://www.example.com/` `PATH/FILE.html?param1=VALUE#hash=FRAGMENT` |
| `dom.viewport_height` | ブラウザビューポートの高さ。ソース: `window.innerHeight` または `document.documentElement. clientHeight` | `1320` |
| `dom.viewport_width` | ブラウザビューポートの幅。ソース: `window.innerWidth` または `document.documentElement. clientWidth` | `1278` |

## クッキー

以下の変数は、`utag_main`という名前の単一のクッキーに保存され、維持されます。または、`utag_main_`クッキーネームスペース（バージョン4.50から）のスタンドアロンクッキーとして保存されます。すべての変数は、データオブジェクト内に別々の変数として表示され、すべて`cp.utag_main_`でプレフィックスされます。

これらの変数をiQ構成に追加するには、**Data Layer**タブから`Tealium Built-in Data`という名前の[データバンドルを使用]()します。

| 変数 | 説明 | 例 |
| --- | --- | --- |
| `cp.utag_main__pn` | **セッションページビューカウント** - 現在のセッションで表示されたページの数 | `2` |
| `cp.utag_main__se` | **セッションイベントカウント** - 現在のセッションで追跡されたイベントの数 | `2` |
| `cp.utag_main__sn` | **セッションカウント** - このユニークな訪問のセッション数 | `1` |
| `cp.utag_main__ss` | **セッションの開始かどうか** - ページビューがセッションの開始かどうかを示すフラグ（1=はい、0=いいえ） | `0` |
| `cp.utag_main__st` | **タイムスタンプ** - ミリ秒単位のUnix/Epochタイムスタンプ | `1522968400449` |
| `cp.utag_main_ses_id` | **セッションID** - セッションの一意の識別子 | `1522965346545` |
| `cp.utag_main_v_id` | **訪問ID** - 各訪問の一意の識別子 | `016297481...` (45文字) |

## Tealiumデータ

以下の変数には、ページに読み込まれた`utag.js`に関する情報と、内部で使用される他の値が含まれています。

`ut.*`変数をiQ構成に追加するには、**Data Layer**タブから`Tealium Built-in Data`という名前の[データバンドルを使用]()します。

| 変数 | 名前 | 例 |
| --- | --- | --- |
| `tealium_account` | アカウント名 | `sandbox` |
| `tealium_datasource` | データソースキー | `&#34;abc123&#34;` |
| `tealium_environment` | 公開環境 | `prod` |
| `tealium_event` | Tealiumイベント名（直接構成されていない場合は&#34;view&#34;または&#34;link&#34;にデフォルト構成） | `view` |
| `tealium_library_name` | ライブラリ名 | `utag.js` |
| `tealium_library_version` | ライブラリバージョン | `4.44.0` |
| `tealium_profile` | アカウントプロファイル | `main` |
| `tealium_random` | ランダム数 | `7782219635308327` |
| `tealium_session_id` | `utag_main_ses_id`のコピー | `1522965346545` |
| `tealium_timestamp_epoch` | 現在のUnixタイムスタンプ（秒） | `1522956509` |
| `tealium_timestamp_local` | ローカルタイムスタンプ | `2018-04-05T12:28:29.019` |
| `tealium_timestamp_utc` | UTCタイムスタンプ  | `2018-04-05T19:28:29.019Z` |
| `tealium_visitor_id` | `utag_main_v_id`のコピー | `016297481...` (45文字) |
| `ut.account` | tealium_accountのコピー | `sandbox` |
| `ut.domain` | クッキーを構成するためのトップレベルドメイン。 | `example.com` |
| `ut.env` | `tealium_environment`のコピー | `prod` |
| `ut.event` | `tealium_event`のコピー | `view` |
| `ut.profile` | `tealium_profile`のコピー | `main` |
| `ut.session_id` | `tealium_session_id`のコピー | `1522956509018` |
| `ut.version` | 公開バージョン（`utag.js`バージョン &#43; タイムスタンプ） | `ut4.44.201710171745` |
| `ut.visitor_id` | `tealium_visitor_id`のコピー |`016297481...` (45文字) |

## ローカル保存とセッション保存

ローカル保存とセッション保存のキーは、`localStorage`と`sessionStorage`変数を使用してデータレイヤーに自動的に表示されます。

これらの保存変数を使用するには、**iQタグ管理 &gt; データレイヤー &gt; &#43;変数を追加**に移動します。**UDO変数**を選択し、ソース変数名を入力します。ローカル保存の場合は`ls.variable_name`、セッション保存の場合は`ss.variable_name`を使用します。

ローカル保存とセッション保存変数についての詳細は、[データレイヤー変数]()を参照してください。

## サンプル

以下は、`utag.data`内の組み込みデータのサンプルです。

```json
{  
    &#34;cp.utag_main_v_id&#34;       : &#34;015da2e1daf10020914ce74dfaf00207900780700093c&#34;,
    &#34;cp.utag_main__sn&#34;        : &#34;389&#34;,
    &#34;cp.utag_main__ss&#34;        : &#34;0&#34;,
    &#34;cp.utag_main__st&#34;        : &#34;1522970376944&#34;,
    &#34;cp.utag_main__se&#34;        : &#34;2&#34;,
    &#34;cp.utag_main_ses_id&#34;     : &#34;1522915346545&#34;,
    &#34;cp.utag_main__pn&#34;        : &#34;8&#34;,
    &#34;qp.param1&#34;               : &#34;value1&#34;,
    &#34;qp.hash1&#34;                : &#34;val1&#34;,
    &#34;dom.referrer&#34;            : &#34;&#34;,
    &#34;dom.title&#34;               : &#34;Test Page&#34;,
    &#34;dom.domain&#34;              : &#34;www.example.com&#34;,
    &#34;dom.query_string&#34;        : &#34;param1=value1&#34;,
    &#34;dom.hash&#34;                : &#34;hash=fragment&#34;,
    &#34;dom.url&#34;                 : &#34;http://www.example.com/path/file.html?param1=value1#hash=fragment&#34;,
    &#34;dom.pathname&#34;            : &#34;/path/file.html&#34;,
    &#34;dom.viewport_height&#34;     : 780,
    &#34;dom.viewport_width&#34;      : 1436,
    &#34;ut.domain&#34;               : &#34;example.com&#34;,
    &#34;ut.version&#34;              : &#34;ut4.44.201710171745&#34;,
    &#34;ut.event&#34;                : &#34;view&#34;,
    &#34;ut.visitor_id&#34;           : &#34;015da2e1daf10020914ce74dfaf00207900780700093c&#34;,
    &#34;ut.session_id&#34;           : &#34;1522965346545&#34;,
    &#34;ut.account&#34;              : &#34;sandbox&#34;,
    &#34;ut.profile&#34;              : &#34;main&#34;,
    &#34;ut.env&#34;                  : &#34;prod&#34;,
    &#34;tealium_event&#34;           : &#34;view&#34;,
    &#34;tealium_visitor_id&#34;      : &#34;015da2e1daf10020914ce74dfaf00207900780700093c&#34;,
    &#34;tealium_session_id&#34;      : &#34;1522915346545&#34;,
    &#34;tealium_datasource&#34;      : &#34;abc123&#34;,
    &#34;tealium_account&#34;         : &#34;sandbox&#34;,
    &#34;tealium_profile&#34;         : &#34;main&#34;,
    &#34;tealium_environment&#34;     : &#34;prod&#34;,
    &#34;tealium_random&#34;          : &#34;7421526627003796&#34;,
    &#34;tealium_library_name&#34;    : &#34;utag.js&#34;,
    &#34;tealium_library_version&#34; : &#34;4.44.0&#34;,
    &#34;tealium_timestamp_epoch&#34; : 1522968576,
    &#34;tealium_timestamp_utc&#34;   : &#34;2018-04-05T22:49:36.945Z&#34;,
    &#34;tealium_timestamp_local&#34; : &#34;2018-04-05T15:49:36.945&#34;
}
```