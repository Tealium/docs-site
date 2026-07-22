---
title: Snowplowタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでSnowplowタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/snowplow-tag/
---
## タグのヒント

* Eコマース拡張機能をサポート
* マッピングを使用して以下を行います：
  * 標準構成値を動的に上書き
  * Eコマース拡張値を動的に上書き
  * 構造化イベントトラッキングをトリガー
  * 非構造化イベントトラッキングをトリガー

* 構造化および非構造化イベントトラッキングは、マッピングを通じて構造化/非構造化イベントアクションが定義されたときにトリガーされます。

## タグの構成

まず、タグマーケットプレイスにアクセスしてSnowplowタグを追加します（[タグの追加方法についてはこちら](https://docs.tealium.com/manage-tags/)を参照）。

タグを追加した後、以下の構成を行います：

* **コードバージョン**
  * タグバージョンを選択（**2.18.2**、**3.1.2**、または**3.23.0**）

* **タイトル**
  * 同じベンダーの複数のタグを使用する場合は、ユニークな名前を割り当てます。

* **Snowplowオブジェクト（必須）**
  * グローバルSnowplowオブジェクトのユニークな名前。
  * Snowplowオブジェクト名は`window.snowplow.name`として定義されます。

* **SnowplowベースURL（必須）**
  * Snowplowトラッカーのバージョンを表すURL。
  * 例：`//d1fc8wv8zag5ca.cloudfront.net/x.xx.x/sp.js`

* **トラッカーネームスペース（必須）**
  * Snowplowトラッカーのネームスペース。
  * この値を動的に上書きするためにデータマッピングを使用します。

* **トラッカーエンドポイント（必須）**
  * SnowplowトラッカーのコレクターエンドポイントURI。
  * この値を動的に上書きするためにデータマッピングを使用します。

* **クッキードメイン**
  * クッキーを構成するトップレベルドメイン。
  * 例：`.mysite.com`。
  * この値を動的に上書きするためにデータマッピングを使用します。

* **リンクトラッキングを有効にする**
  * リンククリックにイベントリスナーを追加します。
  * 可能な値は`True`または`False`です。
  * この値を動的に上書きするためにデータマッピングを使用します。

* **アクティビティトラッキングを有効にする**
  * ページ上のユーザーアクティビティを追跡するために「ページピング」イベントを有効にします。
  * 可能な値は`True`または`False`です。
  * この値を動的に上書きするためにデータマッピングを使用します。

* **エラートラッキングを有効にする**
  * JavaScriptコードの未処理の例外を追跡します。
  * 可能な値は`True`または`False`です。
  * この値を動的に上書きするためにデータマッピングを使用します。

* **ページビューの保存を有効にする**
  * HTMLページ全体がロードされたときのみ、ウェブページのコンテキストを再生成します。
  * 可能な値は`True`または`False`です。
  * この値を動的に上書きするためにデータマッピングを使用します。

* **公開** **場所**
  * 選択された場所にのみタグが公開されます：`Dev`、`QA`、`Prod`、または`Custom`。

* **詳細構成**
  * このタグが組織内でどのように使用されているかについての説明的なメモ。

## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)は、サイト上でこのタグのインスタンスをいつ、どこでロードするかを決定します。

推奨ロードルール：**全ページ**

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Snowplowタグの宛先変数は、その**データマッピング**タブに組み込まれています。利用可能なカテゴリは以下の通りです：

### 標準

|**宛先名**| **説明**|
|---| ---|
| `customURL` |  <ul><li>カスタムURL</li><li>ページのカスタムURLを構成します。</li></ul> |
| `referrerURL` |  <ul><li>カスタムリファラーURL。</li><li>リファラーのカスタムURLを構成します。</li></ul> |
| `pageTitle` |  <ul><li>ページタイトル</li><li>ページのタイトルを構成します。</li></ul> |
| `cookieTimeOut` |  <ul><li>クッキータイムアウト</li><li>セッションクッキーがアクティブであるべき時間（秒単位）を構成します。</li><li>デフォルトは30分（1800秒）です。</li></ul> |
| `enableAT` |  <ul><li>アクティビティトラッキングを有効にする</li><li>ページ上のユーザーアクティビティを追跡するための`page ping`イベントを有効にします。</li><li>値のオプション：`true`または`false`</li></ul> |
| `minimumVisitLength` |  <ul><li>最小訪問時間</li><li>ページロードと最初のページピングの間の時間（秒単位）を構成します。</li></ul> |
| `heartBeat` |  <ul><li>ハートビート</li><li>ページピング間の時間（秒単位）を構成します。</li></ul> |
| `enableET` |  <ul><li>エラートラッキングを有効にする</li><li>JavaScriptコードの未処理の例外を追跡します。</li><li>値のオプション：`true`または`false`</li></ul> |
| `preservePageView` |  <ul><li>ページビューの保存</li><li>HTMLページ全体がロードされたときのみ、ウェブページのコンテキストを再生成します。</li><li>値のオプション：`true`または`false`</li></ul> |
### トラッカー

|**宛先名**| **説明**|
|---| ---|
| `trk_namespace` |  <ul><li>トラッカー名前空間</li><li>あなたのSnowplowトラッカーの名前空間。</li><li>構成値を動的に上書きするために使用します。</li></ul> |
| `trk_endpoint` |  <ul><li>トラッカーエンドポイント</li><li>あなたのSnowplowトラッカーのコレクターエンドポイントURI。</li><li>構成値を動的に上書きするために使用します。</li></ul> |
| `trk_cookieDomain` |  <ul><li>クッキードメイン</li><li>クッキーを構成するトップレベルドメイン。</li><li>構成値を動的に上書きするために使用します。</li></ul> |
| `trk_cookieName` |  <ul><li>クッキー名</li><li>Snowplowのクッキーの基本名を構成します。</li><li>デフォルト値は **sp** です。</li></ul> |
| `trk_appId` |  <ul><li>アプリID</li><li>トラッカーイベントのアプリケーションIDを構成します。</li><li>異なるページから異なるIDを送信してイベントを区別することができます</li></ul> |
| `trk_platform` |  <ul><li>プラットフォーム</li><li>トラッカーのプラットフォームタイプを構成します。</li><li>デフォルト値は **web** です。</li><li>値のオプションについては、[利用可能なプラットフォーム値](https://github.com/snowplow/snowplow/wiki/SnowPlow-Tracker-Protocol#appid)を参照してください。</li></ul> |
| `trk_send` |  <ul><li>送信トラッカー</li><li>文字列/配列</li><li>同じソース（例えば広告）からの複数のアイテムを識別するための名前空間値。</li><li>構成されている場合、ページビュー、広告の印象、広告の変換、広告のクリック、リンクのクリックに添付されます。</li></ul> |
| `trk_encodeBase64` |  <ul><li>Base 64 エンコードの使用</li><li>自己記述イベントとカスタムコンテキストがbase64にエンコードされるかどうかを構成します。</li><li>デフォルトは true です。</li><li>値のオプションは `true` または `false` です。</li></ul> |
| `trk_respectDoNotTrack` |  <ul><li>Do Not Track の尊重</li><li>ブラウザの Do Not Track オプションが尊重されるかどうかを構成します。</li><li>デフォルト値は `false` です。</li><li>値のオプションは `true` または `false` です</li></ul> |
| `trk_userFingerprint` |  <ul><li>ユーザーフィンガープリント</li><li>Snowplowがブラウザの機能に基づいてユーザーフィンガープリントを生成するかどうかを構成します。</li><li>デフォルト値は `true` です。</li><li>値のオプションは `true` または `false` です</li></ul> |
| `trk_userFingerprintSeed` |  <ul><li>ユーザーフィンガープリントシード</li><li>ユーザーフィンガープリントを生成するためのハッシュシードを構成します。</li><li>デフォルトは `123412414` です</li></ul> |
| `trk_pageUnloadTimer` |  <ul><li>ページアンロードタイマー</li><li>イベント発火後にページをアンロードするまでの待機時間（ミリ秒）を構成します。</li><li>デフォルト 500 ミリ秒。</li></ul> |
| `trk_forceSecure` |  <ul><li>セキュアトラッカーの強制</li><li>現在のページがhttpであっても、トラッカーを **https** に強制するかどうかを構成します。</li><li>デフォルト値は `false` です。</li><li>値のオプションは `true` または `false` です</li></ul> |
| `trk_sendAsPost` |  <ul><li>POSTとして送信</li><li>GETリクエストの代わりにPOSTリクエストを使用してイベントを構成します。</li><li>デフォルト値は `false` です。</li><li>値のオプションは `true` または `false` です</li></ul> |
| `trk_bufferSize` |  <ul><li>バッファサイズ</li><li>POSTを使用してイベントをバッチ処理するためのバッファサイズを構成します。</li><li>デフォルト値は **1** です。</li></ul> |
| `trk_maxPostBytes` |  <ul><li>最大POSTバイト数</li><li>コレクターに送信されるPOSTリクエストの最大サイズ（バイト単位）を構成します。</li><li>デフォルト値は40,000バイトです。</li></ul> |
| `trk_storageStrategy` |  <ul><li>状態保存戦略</li><li>トラッカーの状態を保存する戦略を構成します。</li><li>デフォルトはクッキーです。</li><li>値のオプション: `cookie`, `localStorage`, または `none`</li></ul> |
|`trk_cookieLifetime`|  <ul><li>クッキーの寿命</li><li>ドメイン固有の訪問クッキーの保持時間（秒単位）を構成します。</li><li>デフォルト値は2年です。1日は86,400秒です。</li></ul> |
|`trk_contextVendor`|  <ul><li>コンテキストエディタ</li><li>配列</li><li>すべてのイベントに自動的に送信される事前定義されたコンテキストの配列を構成します。</li><li>[ベンダーオプション](https://github.com/snowplow/snowplow/wiki/1-General-parameters-for-the-Javascript-tracker#predefined-contexts)</li></ul> |

### E-コマース

SnowplowタグはE-コマース対応であり、デフォルトのE-コマース拡張マッピングを自動的に使用します。このカテゴリで手動でマッピングする必要は通常ありませんが、拡張マッピングを上書きしたい場合や、拡張で提供されていないE-コマース変数が必要な場合は必要です。

|**宛先名**| **説明**|
|---| ---|
| `order_id` |  <ul><li>注文ID</li><li>デフォルトのE-コマース値 `_corder` を上書きするために使用します。</li></ul> |
| `order_total` |  <ul><li>注文合計</li><li>デフォルトのE-コマース値 `_ctotal` を上書きするために使用します。</li></ul> |
|`order_shipping`|  <ul><li>注文配送料</li><li>デフォルトのE-コマース値 `_cship` を上書きするために使用します。</li></ul> |
| `order_tax` |  <ul><li>注文税額</li><li>デフォルトのE-コマース値 `_ctax` を上書きするために使用します。</li></ul> |
|`order_store`|  <ul><li>注文店舗</li><li>デフォルトのE-コマース値 `_cstore` を上書きするために使用します。</li></ul> |
| `order_currency` |  <ul><li>注文通貨</li><li>デフォルトのE-コマース値 `_ccurrency` を上書きするために使用します。</li></ul> |
|`customer_id`|  <ul><li>顧客ID</li><li>デフォルトのE-コマース値 `_ccustid` を上書きするために使用します。</li></ul> |
| `customer_city` |  <ul><li>顧客の市</li><li>デフォルトのE-コマース値 `_ccity` を上書きするために使用します。</li></ul> |
|`customer_state`|  <ul><li>顧客の州</li><li>デフォルトのE-コマース値 `_cstate` を上書きするために使用します。</li></ul> |
| `customer_country` |  <ul><li>顧客の国</li><li>デフォルトのE-コマース値 `_ccountry` を上書きするために使用します。</li></ul> |
|`product_name`|  <ul><li>製品名リスト</li><li>配列</li><li>デフォルトのE-コマース値 `_cprodname` を上書きするために使用します。</li></ul> |
| `product_sku` |  <ul><li>製品SKUリスト</li><li>配列</li><li>デフォルトのE-コマース値 `_csku` を上書きするために使用します。</li></ul> |
| `product_category` |  <ul><li>製品カテゴリリスト</li><li>配列</li><li>デフォルトのE-コマース値 `_ccat` を上書きするために使用します。</li></ul> |
|`product_quantity`|  <ul><li>製品数量リスト</li><li>配列</li><li>デフォルトのE-コマース値 `_cquan` を上書きするために使用します。</li></ul> |
| `product_unit_price` |  <ul><li>製品単価リスト</li><li>配列</li><li>デフォルトのE-コマース値 `_cprice` を上書きするために使用します。</li></ul> |
| `ecm_schema` |  <ul><li>トランザクションコンテキストスキーマ</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
| `ecm_context.data` |  <ul><li>トランザクションコンテキストデータ</li><li>コンテキストによって追跡されるデータ値。</li><li>マッピング時に `ecm_context.data` の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `ecm_contextObj` |  <ul><li>トランザクションユーザー定義コンテンツ</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |
### リンク追跡

|**目的地名**| **説明**|
|---| ---|
| `enableLCT` |  <ul><li>リンククリック追跡を有効にする</li><li>リンククリックにイベントリスナーを追加する。</li><li>値のオプションは `true` または `false`。</li></ul> |
| `ltr_blacklist` |  <ul><li>ブラックリスト</li><li>文字列/配列</li><li>リンククリックトラッカーによって無視されるべきCSSクラスのリスト。</li><li>他のすべてのリンクが追跡されます。</li></ul> |
| `ltr_whitelist` |  <ul><li>ホワイトリスト</li><li>文字列/配列</li><li>リンククリックトラッカーによって追跡されるべきCSSクラスのリスト。</li><li>他のすべてのリンクは無視されます。</li></ul> |
| `ltr_filter` |  <ul><li>フィルター</li><li>`true` または `false` を返すべき関数（または関数参照）。</li><li>`true` を返すすべての項目が追跡されます。</li></ul> |
| `ltr_pseudoClicks` |  <ul><li>擬似クリック</li><li>中央クリックをクリックイベントとして認識するかどうかを構成する。</li><li>デフォルト値は `false`。</li><li>値のオプションは `true` または `false`。</li></ul> |
| `ltr_clickContent` |  <ul><li>クリックコンテンツ</li><li>クリックイベントがリンクのinnerHTMLをキャプチャするかどうかを構成する。</li><li>値のオプションは `true` または `false`</li></ul> |
|`ltr_url`|  <ul><li>URL</li><li>手動で追跡されるイベント用。</li><li>ターゲットURLを構成する。</li></ul> |
| `ltr_elementId` |  <ul><li>要素ID</li><li>手動で追跡されるイベント用。</li><li>要素のリンクIDを構成する。</li></ul> |
| `ltr_elementClasses` |  <ul><li>要素クラス</li><li>配列</li><li>手動で追跡されるイベント用。</li><li>要素のリンククラスを構成する。</li></ul> |
| `ltr_elementTarget` |  <ul><li>要素ターゲット</li><li>手動で追跡されるイベント用。</li><li>要素のリンクターゲットを構成する。</li></ul> |
|`ltr_elementClickContent`|  <ul><li>要素クリックコンテンツ</li><li>配列</li><li>手動で追跡されるイベント用。</li><li>要素のリンクコンテンツを構成する。</li></ul> |
| `ltr_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
| `ltr_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによって追跡されるデータ値。</li><li>マッピング時に `ltr_context.data` の `data` を関連する値の名前に置き換えてください。</li></ul> |
| `ltr_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |

### 広告追跡

|**目的地名**| **説明**|
|---| ---|
|`adtracking`|  <ul><li>広告追跡</li><li>追跡される広告のタイプを構成する。</li><li>これが入力されている場合のみ、広告イベントが発生します。</li><li>値のオプションは `impression`, `click`, `conversion`。</li></ul> |
| `ad_impressionId` |  <ul><li>インプレッションID</li><li>現在のインプレッションインスタンスの識別子を構成する。</li></ul> |
| `ad_costModel` |  <ul><li>コストモデル</li><li>キャンペーンのコストモデルを構成する。</li><li>値のオプション: `cpc`, `cpm`, `cpa`</li></ul> |
| `ad_cost` |  <ul><li>コスト</li><li>広告のコストを構成する。</li></ul> |
|`ad_targetUrl`|  <ul><li>ターゲットURL</li><li>広告の目的地URLを構成する。</li></ul> |
|`ad_bannerId`|  <ul><li>バナーID</li><li>広告の `adserver` 識別子を構成する。</li></ul> |
| `ad_zoneId` |  <ul><li>ゾーンID</li><li>広告が配置されているゾーンの `adserver` 識別子を構成する。</li></ul> |
| `ad_advertiserId` |  <ul><li>広告主ID</li><li>配列</li><li>キャンペーンが属する広告主の `adserver` 識別子を構成する。</li></ul> |
| `ad_campaignId` |  <ul><li>キャンペーンID</li><li>バナーが属するキャンペーンの `adserver` 識別子を構成する。</li></ul> |
| `ad_clickId` |  <ul><li>クリックID</li><li>現在のクリックインスタンスの識別子を構成する。</li></ul> |
| `ad_conversionId` |  <ul><li>コンバージョンID</li><li>現在のコンバージョンインスタンスの識別子を構成する。</li></ul> |
| `ad_category` |  <ul><li>カテゴリ</li><li>コンバージョンのカテゴリを構成する。</li></ul> |
| `ad_action` |  <ul><li>アクション</li><li>コンバージョンのユーザーインタラクションのタイプを構成する。</li></ul> |
| `ad_property` |  <ul><li>プロパティ</li><li>コンバージョンのオブジェクト説明を構成する。</li></ul> |
| `ad_initialValue` |  <ul><li>初期値</li><li>コンバージョンの初期価値を構成する。</li></ul> |
| `ad_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
| `ad_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによって追跡されるデータ値。</li><li>マッピング時に `ad_context.data` の `data` を関連する値の名前に置き換えてください。</li></ul> |
| `ad_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |

### ページビューカスタムコンテキスト

|**目的地名**| **説明**|
|---| ---|
| `cc_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
|`cc_context.data`|  <ul><li>コンテキストデータ</li><li>コンテキストによって追跡されるデータ値。</li><li>マッピング時に `cc_context.data` の `data` を関連する値の名前に置き換えてください。</li></ul> |
| `cc_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |

### ソーシャル追跡

|**目的地名**| **説明**|
|---| ---|
| `sot_action` |  <ul><li>アクション</li><li>ユーザーによって実行されたアクション。</li></ul> |
| `sot_network` |  <ul><li>ソーシャルネットワーク</li><li>ユーザーが対話したネットワーク。</li></ul> |
| `sot_target` |  <ul><li>ターゲット</li><li>実行されたアクションの対象オブジェクト。</li></ul> |
| `sot_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
| `sot_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによって追跡されるデータ値。</li><li>マッピング時に `sot_context.data` の `data` を関連する値の名前に置き換えてください。</li></ul> |
| `sot_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |

### フォーム追跡

|**目的地名**| **説明**|
|---| ---|
| `enableFormTracking` |  <ul><li>フォーム追跡を有効にする</li><li>フォームの変更と送信が追跡されるかどうかを構成する。</li><li>値のオプションは `true` または `false`。</li></ul> |
| `ftr_formBlacklist` |  <ul><li>フォームカスタムブラックリスト</li><li>配列</li><li>フォームトラッカーによって無視されるべきフォームCSSクラスのリスト。</li><li>他のすべてのリンクが追跡されます。</li><li>例: ログインフォーム、リクエストフォーム</li></ul> |
| `ftr_formWhitelist` |  <ul><li>フォームカスタムホワイトリスト</li><li>配列</li><li>フォームトラッカーによって追跡されるべきフォームCSSクラスのリスト。</li><li>他のすべてのリンクは無視されます。</li><li>例: ログインフォーム、リクエストフォーム</li></ul> |
| `ftr_fieldBlacklist` |  <ul><li>フィールドカスタムブラックリスト</li><li>配列</li><li>フォームトラッカーによって無視されるべきフィールドCSSクラスのリスト。</li><li>他のすべてのリンクが追跡されます。</li><li>例: パスワードフィールド、メールフィールド</li></ul> |
| `ftr_fieldWhitelist` |  <ul><li>フィールドカスタムホワイトリスト</li><li>配列</li><li>フォームトラッカーによって追跡されるべきフィールドCSSクラスのリスト。</li><li>他のすべてのリンクは無視されます。</li><li>例: パスワードフィールド、メールフィールド</li></ul> |
| `ftr_filterForm` |  <ul><li>カスタムフォームフィルター関数</li><li>`true` または `false` を返すべき関数（または関数参照）。</li><li>`true` を返すすべての項目が追跡されます。</li></ul> |
| `ftr_filterField` |  <ul><li>カスタムフィールドフィルター関数</li><li>`true` または `false` を返すべき関数（または関数参照）。</li><li>`true` を返すすべての項目が追跡されます。</li></ul> |
| `ftr_ctmConfig` |  <ul><li>ユーザー定義構成</li><li>上記のプロパティを持つカスタム構成オブジェクト。</li><li>個々のプロパティの代わりに使用します。</li></ul> |
### カート追跡

|**宛先名**| **説明**|
|---| ---|
| `cartTracking` |  <ul><li>カート追跡</li><li>追跡されるカートイベントのタイプを構成します。</li><li>これが入力されている場合のみカートイベントが発火します。</li><li>値のオプションは `cart_add` または `cart_remove` です。</li></ul> |
| `cart_sku` |  <ul><li>カートアイテムSKU</li><li>カート内で移動されるアイテムのSKUです。</li></ul> |
| `cart_name` |  <ul><li>カートアイテム名</li><li>カート内で移動されるアイテムの名前です。</li></ul> |
| `cart_category` |  <ul><li>カートアイテムカテゴリ</li><li>カート内で移動されるアイテムのカテゴリです。</li></ul> |
| `cart_price` |  <ul><li>カートアイテム単価</li><li>カート内で移動されるアイテムの価格です。</li></ul> |
| `cart_quantity` |  <ul><li>カートアイテム数量</li><li>カート内で移動されるアイテムの数量です。</li></ul> |
| `cart_currency` |  <ul><li>カートアイテム通貨</li><li>カート内で移動されるアイテムの通貨です。</li></ul> |
| `cart_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマです。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
| `cart_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによって追跡されるデータ値です。</li><li>マッピング時に `cart_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。</li></ul> |
| `cart_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。</li></ul> |

### サイト検索追跡

|**宛先名**| **説明**|
|---| ---|
| `sst_terms` |  <ul><li>検索用語</li><li>配列</li><li>サイト検索で使用される用語のリストです。</li><li>これが入力されている場合のみ検索イベントが発火します。</li></ul> |
|`sst_filters`|  <ul><li>検索フィルター</li><li>フィルタータイプと用語を定義するJSONオブジェクトです。</li></ul> |
| `sst_totalResults` |  <ul><li>検索結果の総数</li><li>検索で見つかった結果の総数です</li></ul> |
| `sst_pageResults` |  <ul><li>最初のページの結果</li><li>最初のページに表示される結果の数です。</li></ul> |
| `sst_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマです。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
| `sst_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによって追跡されるデータ値です。</li><li>マッピング時に `sst_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。</li></ul> |
| `sst_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。</li></ul> |

### 構造化イベント

|**宛先名**| **説明**|
|---| ---|
| `stctCat` |  <ul><li>カテゴリ</li><li>追跡しているオブジェクトのグループ名です。</li></ul> |
| `stctActn` |  <ul><li>アクション名</li><li>追跡しているオブジェクトのユーザーインタラクションの名前です。</li></ul> |
| `stctLabel` |  <ul><li>ラベル</li><li>追跡している特定のオブジェクトを識別する追加の名前です。</li></ul> |
| `stctProp` |  <ul><li>プロパティ</li><li>オブジェクトまたはそれに対して行われたアクションを説明する追加の項目です。</li></ul> |
| `stctVal` |  <ul><li>値</li><li>ユーザーインタラクションを説明する追加の小数点数です。</li></ul> |
| `stc_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマです。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
|`stc_context.data`|  <ul><li>コンテキストデータ</li><li>コンテキストによって追跡されるデータ値です。</li><li>マッピング時に `stc_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。</li></ul> |
| `stc_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。</li></ul> |

### 非構造化イベント

|**宛先名**| **説明**|
|---| ---|
| `unstctDataSchema` |  <ul><li>スキーマ</li><li>イベントを記述するJSONスキーマです。Igluライブラリに存在する必要があります。</li></ul> |
| `unstctData.data` |  <ul><li>ユーザー定義データ</li><li>イベントによって追跡されるデータ値です。</li><li>マッピング時に `unstctData.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。</li></ul> |
| `unstctDataObj` |  <ul><li>ユーザー定義データオブジェクト</li><li>上記のプロパティを持つカスタム構成オブジェクトです。</li><li>個々のプロパティの代わりに使用してください。</li></ul> |
| `stc_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマです。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
| `nstc_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによって追跡されるデータ値です。</li><li>マッピング時に `unstc_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。</li></ul> |
| `unstc_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。</li></ul> |

### 同意追跡

|**宛先名**| **説明**|
|---| ---|
| `consentGranted` |  <ul><li>ユーザーが同意を許可</li><li>ユーザーがデータ収集に同意することを追跡するために使用されます。</li><li>少なくとも `id` と `version` の引数が提供されている場合、同意文書コンテキストがイベントに添付されます。</li></ul> |
| `consentWithdrawn` |  <ul><li>ユーザーが一部の同意を撤回</li><li>ユーザーがデータ収集の同意を撤回することを追跡するために使用されます。</li><li>少なくとも `id` と `version` の引数が提供されている場合、同意文書コンテキストがイベントに添付されます。</li></ul> |
| `allConsentWithdrawn` |  <ul><li>ユーザーがすべての同意を撤回</li><li>すべての同意が撤回されるべきかどうかを指定します。</li></ul> |
| `con_documentId` |  <ul><li>同意文書ID</li><li>同意文書は、メソッドに提供された引数（許可および撤回イベントの両方でこれは：`id`、`version`、`name`、および `description`）を格納するカスタムコンテキストです。</li><li>いずれかの同意方法で、コンテキスト引数に同意文書の自己記述JSONの配列を渡すことによって、追加の文書がイベントに追加されることができます。</li></ul> |
| `con_documentVer` |  <ul><li>同意文書バージョン</li><li>必須</li><li>同意を与える文書のバージョンです</li></ul> |
| `con_documentName` |  <ul><li>同意文書名</li><li>同意文書の名前です。</li></ul> |
| `con_documentDesc` |  <ul><li>同意文書の説明</li><li>同意文書の説明です。</li></ul> |
| `con_documentExpiry` |  <ul><li>同意文書の有効期限</li><li>提供された日時までユーザーが添付された文書に同意し、その後は同意が無効になることを指定します。</li></ul> |
| `unstc_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマです。</li><li>Igluライブラリに存在する必要があります。</li></ul> |
| `nstc_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによって追跡されるデータ値です。</li><li>マッピング時に `unstc_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。</li></ul> |
| `con_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。</li></ul> |

## ベンダー文書

* [SnowPlow Javascript トラッカーのドキュメント](https://docs.snowplowanalytics.com/docs/collecting-data/collecting-from-own-applications/javascript-trackers/)
