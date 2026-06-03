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

まず、タグマーケットプレイスにアクセスしてSnowplowタグを追加します（[タグの追加方法についてはこちら]()を参照）。

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

[ロードルール]()は、サイト上でこのタグのインスタンスをいつ、どこでロードするかを決定します。

推奨ロードルール：**全ページ**

## データマッピング

マッピングは、[データレイヤー変数](/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Snowplowタグの宛先変数は、その**データマッピング**タブに組み込まれています。利用可能なカテゴリは以下の通りです：

### 標準

|**宛先名**| **説明**|
|---| ---|
| `customURL` |  &lt;ul&gt;&lt;li&gt;カスタムURL&lt;/li&gt;&lt;li&gt;ページのカスタムURLを構成します。&lt;/li&gt;&lt;/ul&gt; |
| `referrerURL` |  &lt;ul&gt;&lt;li&gt;カスタムリファラーURL。&lt;/li&gt;&lt;li&gt;リファラーのカスタムURLを構成します。&lt;/li&gt;&lt;/ul&gt; |
| `pageTitle` |  &lt;ul&gt;&lt;li&gt;ページタイトル&lt;/li&gt;&lt;li&gt;ページのタイトルを構成します。&lt;/li&gt;&lt;/ul&gt; |
| `cookieTimeOut` |  &lt;ul&gt;&lt;li&gt;クッキータイムアウト&lt;/li&gt;&lt;li&gt;セッションクッキーがアクティブであるべき時間（秒単位）を構成します。&lt;/li&gt;&lt;li&gt;デフォルトは30分（1800秒）です。&lt;/li&gt;&lt;/ul&gt; |
| `enableAT` |  &lt;ul&gt;&lt;li&gt;アクティビティトラッキングを有効にする&lt;/li&gt;&lt;li&gt;ページ上のユーザーアクティビティを追跡するための`page ping`イベントを有効にします。&lt;/li&gt;&lt;li&gt;値のオプション：`true`または`false`&lt;/li&gt;&lt;/ul&gt; |
| `minimumVisitLength` |  &lt;ul&gt;&lt;li&gt;最小訪問時間&lt;/li&gt;&lt;li&gt;ページロードと最初のページピングの間の時間（秒単位）を構成します。&lt;/li&gt;&lt;/ul&gt; |
| `heartBeat` |  &lt;ul&gt;&lt;li&gt;ハートビート&lt;/li&gt;&lt;li&gt;ページピング間の時間（秒単位）を構成します。&lt;/li&gt;&lt;/ul&gt; |
| `enableET` |  &lt;ul&gt;&lt;li&gt;エラートラッキングを有効にする&lt;/li&gt;&lt;li&gt;JavaScriptコードの未処理の例外を追跡します。&lt;/li&gt;&lt;li&gt;値のオプション：`true`または`false`&lt;/li&gt;&lt;/ul&gt; |
| `preservePageView` |  &lt;ul&gt;&lt;li&gt;ページビューの保存&lt;/li&gt;&lt;li&gt;HTMLページ全体がロードされたときのみ、ウェブページのコンテキストを再生成します。&lt;/li&gt;&lt;li&gt;値のオプション：`true`または`false`&lt;/li&gt;&lt;/ul&gt; |
### トラッカー

|**宛先名**| **説明**|
|---| ---|
| `trk_namespace` |  &lt;ul&gt;&lt;li&gt;トラッカー名前空間&lt;/li&gt;&lt;li&gt;あなたのSnowplowトラッカーの名前空間。&lt;/li&gt;&lt;li&gt;構成値を動的に上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `trk_endpoint` |  &lt;ul&gt;&lt;li&gt;トラッカーエンドポイント&lt;/li&gt;&lt;li&gt;あなたのSnowplowトラッカーのコレクターエンドポイントURI。&lt;/li&gt;&lt;li&gt;構成値を動的に上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `trk_cookieDomain` |  &lt;ul&gt;&lt;li&gt;クッキードメイン&lt;/li&gt;&lt;li&gt;クッキーを構成するトップレベルドメイン。&lt;/li&gt;&lt;li&gt;構成値を動的に上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `trk_cookieName` |  &lt;ul&gt;&lt;li&gt;クッキー名&lt;/li&gt;&lt;li&gt;Snowplowのクッキーの基本名を構成します。&lt;/li&gt;&lt;li&gt;デフォルト値は **sp** です。&lt;/li&gt;&lt;/ul&gt; |
| `trk_appId` |  &lt;ul&gt;&lt;li&gt;アプリID&lt;/li&gt;&lt;li&gt;トラッカーイベントのアプリケーションIDを構成します。&lt;/li&gt;&lt;li&gt;異なるページから異なるIDを送信してイベントを区別することができます&lt;/li&gt;&lt;/ul&gt; |
| `trk_platform` |  &lt;ul&gt;&lt;li&gt;プラットフォーム&lt;/li&gt;&lt;li&gt;トラッカーのプラットフォームタイプを構成します。&lt;/li&gt;&lt;li&gt;デフォルト値は **web** です。&lt;/li&gt;&lt;li&gt;値のオプションについては、[利用可能なプラットフォーム値](https://github.com/snowplow/snowplow/wiki/SnowPlow-Tracker-Protocol#appid)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| `trk_send` |  &lt;ul&gt;&lt;li&gt;送信トラッカー&lt;/li&gt;&lt;li&gt;文字列/配列&lt;/li&gt;&lt;li&gt;同じソース（例えば広告）からの複数のアイテムを識別するための名前空間値。&lt;/li&gt;&lt;li&gt;構成されている場合、ページビュー、広告の印象、広告の変換、広告のクリック、リンクのクリックに添付されます。&lt;/li&gt;&lt;/ul&gt; |
| `trk_encodeBase64` |  &lt;ul&gt;&lt;li&gt;Base 64 エンコードの使用&lt;/li&gt;&lt;li&gt;自己記述イベントとカスタムコンテキストがbase64にエンコードされるかどうかを構成します。&lt;/li&gt;&lt;li&gt;デフォルトは true です。&lt;/li&gt;&lt;li&gt;値のオプションは `true` または `false` です。&lt;/li&gt;&lt;/ul&gt; |
| `trk_respectDoNotTrack` |  &lt;ul&gt;&lt;li&gt;Do Not Track の尊重&lt;/li&gt;&lt;li&gt;ブラウザの Do Not Track オプションが尊重されるかどうかを構成します。&lt;/li&gt;&lt;li&gt;デフォルト値は `false` です。&lt;/li&gt;&lt;li&gt;値のオプションは `true` または `false` です&lt;/li&gt;&lt;/ul&gt; |
| `trk_userFingerprint` |  &lt;ul&gt;&lt;li&gt;ユーザーフィンガープリント&lt;/li&gt;&lt;li&gt;Snowplowがブラウザの機能に基づいてユーザーフィンガープリントを生成するかどうかを構成します。&lt;/li&gt;&lt;li&gt;デフォルト値は `true` です。&lt;/li&gt;&lt;li&gt;値のオプションは `true` または `false` です&lt;/li&gt;&lt;/ul&gt; |
| `trk_userFingerprintSeed` |  &lt;ul&gt;&lt;li&gt;ユーザーフィンガープリントシード&lt;/li&gt;&lt;li&gt;ユーザーフィンガープリントを生成するためのハッシュシードを構成します。&lt;/li&gt;&lt;li&gt;デフォルトは `123412414` です&lt;/li&gt;&lt;/ul&gt; |
| `trk_pageUnloadTimer` |  &lt;ul&gt;&lt;li&gt;ページアンロードタイマー&lt;/li&gt;&lt;li&gt;イベント発火後にページをアンロードするまでの待機時間（ミリ秒）を構成します。&lt;/li&gt;&lt;li&gt;デフォルト 500 ミリ秒。&lt;/li&gt;&lt;/ul&gt; |
| `trk_forceSecure` |  &lt;ul&gt;&lt;li&gt;セキュアトラッカーの強制&lt;/li&gt;&lt;li&gt;現在のページがhttpであっても、トラッカーを **https** に強制するかどうかを構成します。&lt;/li&gt;&lt;li&gt;デフォルト値は `false` です。&lt;/li&gt;&lt;li&gt;値のオプションは `true` または `false` です&lt;/li&gt;&lt;/ul&gt; |
| `trk_sendAsPost` |  &lt;ul&gt;&lt;li&gt;POSTとして送信&lt;/li&gt;&lt;li&gt;GETリクエストの代わりにPOSTリクエストを使用してイベントを構成します。&lt;/li&gt;&lt;li&gt;デフォルト値は `false` です。&lt;/li&gt;&lt;li&gt;値のオプションは `true` または `false` です&lt;/li&gt;&lt;/ul&gt; |
| `trk_bufferSize` |  &lt;ul&gt;&lt;li&gt;バッファサイズ&lt;/li&gt;&lt;li&gt;POSTを使用してイベントをバッチ処理するためのバッファサイズを構成します。&lt;/li&gt;&lt;li&gt;デフォルト値は **1** です。&lt;/li&gt;&lt;/ul&gt; |
| `trk_maxPostBytes` |  &lt;ul&gt;&lt;li&gt;最大POSTバイト数&lt;/li&gt;&lt;li&gt;コレクターに送信されるPOSTリクエストの最大サイズ（バイト単位）を構成します。&lt;/li&gt;&lt;li&gt;デフォルト値は40,000バイトです。&lt;/li&gt;&lt;/ul&gt; |
| `trk_storageStrategy` |  &lt;ul&gt;&lt;li&gt;状態保存戦略&lt;/li&gt;&lt;li&gt;トラッカーの状態を保存する戦略を構成します。&lt;/li&gt;&lt;li&gt;デフォルトはクッキーです。&lt;/li&gt;&lt;li&gt;値のオプション: `cookie`, `localStorage`, または `none`&lt;/li&gt;&lt;/ul&gt; |
|`trk_cookieLifetime`|  &lt;ul&gt;&lt;li&gt;クッキーの寿命&lt;/li&gt;&lt;li&gt;ドメイン固有の訪問クッキーの保持時間（秒単位）を構成します。&lt;/li&gt;&lt;li&gt;デフォルト値は2年です。1日は86,400秒です。&lt;/li&gt;&lt;/ul&gt; |
|`trk_contextVendor`|  &lt;ul&gt;&lt;li&gt;コンテキストエディタ&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;すべてのイベントに自動的に送信される事前定義されたコンテキストの配列を構成します。&lt;/li&gt;&lt;li&gt;[ベンダーオプション](https://github.com/snowplow/snowplow/wiki/1-General-parameters-for-the-Javascript-tracker#predefined-contexts)&lt;/li&gt;&lt;/ul&gt; |

### E-コマース

SnowplowタグはE-コマース対応であり、デフォルトのE-コマース拡張マッピングを自動的に使用します。このカテゴリで手動でマッピングする必要は通常ありませんが、拡張マッピングを上書きしたい場合や、拡張で提供されていないE-コマース変数が必要な場合は必要です。

|**宛先名**| **説明**|
|---| ---|
| `order_id` |  &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_corder` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `order_total` |  &lt;ul&gt;&lt;li&gt;注文合計&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_ctotal` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;注文配送料&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_cship` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `order_tax` |  &lt;ul&gt;&lt;li&gt;注文税額&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_ctax` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_store`|  &lt;ul&gt;&lt;li&gt;注文店舗&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_cstore` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `order_currency` |  &lt;ul&gt;&lt;li&gt;注文通貨&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_ccurrency` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_ccustid` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `customer_city` |  &lt;ul&gt;&lt;li&gt;顧客の市&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_ccity` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`customer_state`|  &lt;ul&gt;&lt;li&gt;顧客の州&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_cstate` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `customer_country` |  &lt;ul&gt;&lt;li&gt;顧客の国&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_ccountry` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;製品名リスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_cprodname` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `product_sku` |  &lt;ul&gt;&lt;li&gt;製品SKUリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_csku` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `product_category` |  &lt;ul&gt;&lt;li&gt;製品カテゴリリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_ccat` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;製品数量リスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_cquan` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `product_unit_price` |  &lt;ul&gt;&lt;li&gt;製品単価リスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;デフォルトのE-コマース値 `_cprice` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| `ecm_schema` |  &lt;ul&gt;&lt;li&gt;トランザクションコンテキストスキーマ&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマ。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `ecm_context.data` |  &lt;ul&gt;&lt;li&gt;トランザクションコンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値。&lt;/li&gt;&lt;li&gt;マッピング時に `ecm_context.data` の `data` を値に関連付けられた名前に置き換えます。&lt;/li&gt;&lt;/ul&gt; |
| `ecm_contextObj` |  &lt;ul&gt;&lt;li&gt;トランザクションユーザー定義コンテンツ&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。&lt;/li&gt;&lt;/ul&gt; |
### リンク追跡

|**目的地名**| **説明**|
|---| ---|
| `enableLCT` |  &lt;ul&gt;&lt;li&gt;リンククリック追跡を有効にする&lt;/li&gt;&lt;li&gt;リンククリックにイベントリスナーを追加する。&lt;/li&gt;&lt;li&gt;値のオプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_blacklist` |  &lt;ul&gt;&lt;li&gt;ブラックリスト&lt;/li&gt;&lt;li&gt;文字列/配列&lt;/li&gt;&lt;li&gt;リンククリックトラッカーによって無視されるべきCSSクラスのリスト。&lt;/li&gt;&lt;li&gt;他のすべてのリンクが追跡されます。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_whitelist` |  &lt;ul&gt;&lt;li&gt;ホワイトリスト&lt;/li&gt;&lt;li&gt;文字列/配列&lt;/li&gt;&lt;li&gt;リンククリックトラッカーによって追跡されるべきCSSクラスのリスト。&lt;/li&gt;&lt;li&gt;他のすべてのリンクは無視されます。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_filter` |  &lt;ul&gt;&lt;li&gt;フィルター&lt;/li&gt;&lt;li&gt;`true` または `false` を返すべき関数（または関数参照）。&lt;/li&gt;&lt;li&gt;`true` を返すすべての項目が追跡されます。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_pseudoClicks` |  &lt;ul&gt;&lt;li&gt;擬似クリック&lt;/li&gt;&lt;li&gt;中央クリックをクリックイベントとして認識するかどうかを構成する。&lt;/li&gt;&lt;li&gt;デフォルト値は `false`。&lt;/li&gt;&lt;li&gt;値のオプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_clickContent` |  &lt;ul&gt;&lt;li&gt;クリックコンテンツ&lt;/li&gt;&lt;li&gt;クリックイベントがリンクのinnerHTMLをキャプチャするかどうかを構成する。&lt;/li&gt;&lt;li&gt;値のオプションは `true` または `false`&lt;/li&gt;&lt;/ul&gt; |
|`ltr_url`|  &lt;ul&gt;&lt;li&gt;URL&lt;/li&gt;&lt;li&gt;手動で追跡されるイベント用。&lt;/li&gt;&lt;li&gt;ターゲットURLを構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_elementId` |  &lt;ul&gt;&lt;li&gt;要素ID&lt;/li&gt;&lt;li&gt;手動で追跡されるイベント用。&lt;/li&gt;&lt;li&gt;要素のリンクIDを構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_elementClasses` |  &lt;ul&gt;&lt;li&gt;要素クラス&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;手動で追跡されるイベント用。&lt;/li&gt;&lt;li&gt;要素のリンククラスを構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_elementTarget` |  &lt;ul&gt;&lt;li&gt;要素ターゲット&lt;/li&gt;&lt;li&gt;手動で追跡されるイベント用。&lt;/li&gt;&lt;li&gt;要素のリンクターゲットを構成する。&lt;/li&gt;&lt;/ul&gt; |
|`ltr_elementClickContent`|  &lt;ul&gt;&lt;li&gt;要素クリックコンテンツ&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;手動で追跡されるイベント用。&lt;/li&gt;&lt;li&gt;要素のリンクコンテンツを構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_schema` |  &lt;ul&gt;&lt;li&gt;コンテキストスキーマ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマ。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_context.data` |  &lt;ul&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値。&lt;/li&gt;&lt;li&gt;マッピング時に `ltr_context.data` の `data` を関連する値の名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `ltr_contextObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義コンテキスト&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。&lt;/li&gt;&lt;/ul&gt; |

### 広告追跡

|**目的地名**| **説明**|
|---| ---|
|`adtracking`|  &lt;ul&gt;&lt;li&gt;広告追跡&lt;/li&gt;&lt;li&gt;追跡される広告のタイプを構成する。&lt;/li&gt;&lt;li&gt;これが入力されている場合のみ、広告イベントが発生します。&lt;/li&gt;&lt;li&gt;値のオプションは `impression`, `click`, `conversion`。&lt;/li&gt;&lt;/ul&gt; |
| `ad_impressionId` |  &lt;ul&gt;&lt;li&gt;インプレッションID&lt;/li&gt;&lt;li&gt;現在のインプレッションインスタンスの識別子を構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_costModel` |  &lt;ul&gt;&lt;li&gt;コストモデル&lt;/li&gt;&lt;li&gt;キャンペーンのコストモデルを構成する。&lt;/li&gt;&lt;li&gt;値のオプション: `cpc`, `cpm`, `cpa`&lt;/li&gt;&lt;/ul&gt; |
| `ad_cost` |  &lt;ul&gt;&lt;li&gt;コスト&lt;/li&gt;&lt;li&gt;広告のコストを構成する。&lt;/li&gt;&lt;/ul&gt; |
|`ad_targetUrl`|  &lt;ul&gt;&lt;li&gt;ターゲットURL&lt;/li&gt;&lt;li&gt;広告の目的地URLを構成する。&lt;/li&gt;&lt;/ul&gt; |
|`ad_bannerId`|  &lt;ul&gt;&lt;li&gt;バナーID&lt;/li&gt;&lt;li&gt;広告の `adserver` 識別子を構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_zoneId` |  &lt;ul&gt;&lt;li&gt;ゾーンID&lt;/li&gt;&lt;li&gt;広告が配置されているゾーンの `adserver` 識別子を構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_advertiserId` |  &lt;ul&gt;&lt;li&gt;広告主ID&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;キャンペーンが属する広告主の `adserver` 識別子を構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_campaignId` |  &lt;ul&gt;&lt;li&gt;キャンペーンID&lt;/li&gt;&lt;li&gt;バナーが属するキャンペーンの `adserver` 識別子を構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_clickId` |  &lt;ul&gt;&lt;li&gt;クリックID&lt;/li&gt;&lt;li&gt;現在のクリックインスタンスの識別子を構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_conversionId` |  &lt;ul&gt;&lt;li&gt;コンバージョンID&lt;/li&gt;&lt;li&gt;現在のコンバージョンインスタンスの識別子を構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_category` |  &lt;ul&gt;&lt;li&gt;カテゴリ&lt;/li&gt;&lt;li&gt;コンバージョンのカテゴリを構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_action` |  &lt;ul&gt;&lt;li&gt;アクション&lt;/li&gt;&lt;li&gt;コンバージョンのユーザーインタラクションのタイプを構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_property` |  &lt;ul&gt;&lt;li&gt;プロパティ&lt;/li&gt;&lt;li&gt;コンバージョンのオブジェクト説明を構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_initialValue` |  &lt;ul&gt;&lt;li&gt;初期値&lt;/li&gt;&lt;li&gt;コンバージョンの初期価値を構成する。&lt;/li&gt;&lt;/ul&gt; |
| `ad_schema` |  &lt;ul&gt;&lt;li&gt;コンテキストスキーマ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマ。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `ad_context.data` |  &lt;ul&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値。&lt;/li&gt;&lt;li&gt;マッピング時に `ad_context.data` の `data` を関連する値の名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `ad_contextObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義コンテキスト&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。&lt;/li&gt;&lt;/ul&gt; |

### ページビューカスタムコンテキスト

|**目的地名**| **説明**|
|---| ---|
| `cc_schema` |  &lt;ul&gt;&lt;li&gt;コンテキストスキーマ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマ。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`cc_context.data`|  &lt;ul&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値。&lt;/li&gt;&lt;li&gt;マッピング時に `cc_context.data` の `data` を関連する値の名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `cc_contextObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義コンテキスト&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。&lt;/li&gt;&lt;/ul&gt; |

### ソーシャル追跡

|**目的地名**| **説明**|
|---| ---|
| `sot_action` |  &lt;ul&gt;&lt;li&gt;アクション&lt;/li&gt;&lt;li&gt;ユーザーによって実行されたアクション。&lt;/li&gt;&lt;/ul&gt; |
| `sot_network` |  &lt;ul&gt;&lt;li&gt;ソーシャルネットワーク&lt;/li&gt;&lt;li&gt;ユーザーが対話したネットワーク。&lt;/li&gt;&lt;/ul&gt; |
| `sot_target` |  &lt;ul&gt;&lt;li&gt;ターゲット&lt;/li&gt;&lt;li&gt;実行されたアクションの対象オブジェクト。&lt;/li&gt;&lt;/ul&gt; |
| `sot_schema` |  &lt;ul&gt;&lt;li&gt;コンテキストスキーマ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマ。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `sot_context.data` |  &lt;ul&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値。&lt;/li&gt;&lt;li&gt;マッピング時に `sot_context.data` の `data` を関連する値の名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `sot_contextObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義コンテキスト&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクト。&lt;/li&gt;&lt;/ul&gt; |

### フォーム追跡

|**目的地名**| **説明**|
|---| ---|
| `enableFormTracking` |  &lt;ul&gt;&lt;li&gt;フォーム追跡を有効にする&lt;/li&gt;&lt;li&gt;フォームの変更と送信が追跡されるかどうかを構成する。&lt;/li&gt;&lt;li&gt;値のオプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
| `ftr_formBlacklist` |  &lt;ul&gt;&lt;li&gt;フォームカスタムブラックリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;フォームトラッカーによって無視されるべきフォームCSSクラスのリスト。&lt;/li&gt;&lt;li&gt;他のすべてのリンクが追跡されます。&lt;/li&gt;&lt;li&gt;例: ログインフォーム、リクエストフォーム&lt;/li&gt;&lt;/ul&gt; |
| `ftr_formWhitelist` |  &lt;ul&gt;&lt;li&gt;フォームカスタムホワイトリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;フォームトラッカーによって追跡されるべきフォームCSSクラスのリスト。&lt;/li&gt;&lt;li&gt;他のすべてのリンクは無視されます。&lt;/li&gt;&lt;li&gt;例: ログインフォーム、リクエストフォーム&lt;/li&gt;&lt;/ul&gt; |
| `ftr_fieldBlacklist` |  &lt;ul&gt;&lt;li&gt;フィールドカスタムブラックリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;フォームトラッカーによって無視されるべきフィールドCSSクラスのリスト。&lt;/li&gt;&lt;li&gt;他のすべてのリンクが追跡されます。&lt;/li&gt;&lt;li&gt;例: パスワードフィールド、メールフィールド&lt;/li&gt;&lt;/ul&gt; |
| `ftr_fieldWhitelist` |  &lt;ul&gt;&lt;li&gt;フィールドカスタムホワイトリスト&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;フォームトラッカーによって追跡されるべきフィールドCSSクラスのリスト。&lt;/li&gt;&lt;li&gt;他のすべてのリンクは無視されます。&lt;/li&gt;&lt;li&gt;例: パスワードフィールド、メールフィールド&lt;/li&gt;&lt;/ul&gt; |
| `ftr_filterForm` |  &lt;ul&gt;&lt;li&gt;カスタムフォームフィルター関数&lt;/li&gt;&lt;li&gt;`true` または `false` を返すべき関数（または関数参照）。&lt;/li&gt;&lt;li&gt;`true` を返すすべての項目が追跡されます。&lt;/li&gt;&lt;/ul&gt; |
| `ftr_filterField` |  &lt;ul&gt;&lt;li&gt;カスタムフィールドフィルター関数&lt;/li&gt;&lt;li&gt;`true` または `false` を返すべき関数（または関数参照）。&lt;/li&gt;&lt;li&gt;`true` を返すすべての項目が追跡されます。&lt;/li&gt;&lt;/ul&gt; |
| `ftr_ctmConfig` |  &lt;ul&gt;&lt;li&gt;ユーザー定義構成&lt;/li&gt;&lt;li&gt;上記のプロパティを持つカスタム構成オブジェクト。&lt;/li&gt;&lt;li&gt;個々のプロパティの代わりに使用します。&lt;/li&gt;&lt;/ul&gt; |
### カート追跡

|**宛先名**| **説明**|
|---| ---|
| `cartTracking` |  &lt;ul&gt;&lt;li&gt;カート追跡&lt;/li&gt;&lt;li&gt;追跡されるカートイベントのタイプを構成します。&lt;/li&gt;&lt;li&gt;これが入力されている場合のみカートイベントが発火します。&lt;/li&gt;&lt;li&gt;値のオプションは `cart_add` または `cart_remove` です。&lt;/li&gt;&lt;/ul&gt; |
| `cart_sku` |  &lt;ul&gt;&lt;li&gt;カートアイテムSKU&lt;/li&gt;&lt;li&gt;カート内で移動されるアイテムのSKUです。&lt;/li&gt;&lt;/ul&gt; |
| `cart_name` |  &lt;ul&gt;&lt;li&gt;カートアイテム名&lt;/li&gt;&lt;li&gt;カート内で移動されるアイテムの名前です。&lt;/li&gt;&lt;/ul&gt; |
| `cart_category` |  &lt;ul&gt;&lt;li&gt;カートアイテムカテゴリ&lt;/li&gt;&lt;li&gt;カート内で移動されるアイテムのカテゴリです。&lt;/li&gt;&lt;/ul&gt; |
| `cart_price` |  &lt;ul&gt;&lt;li&gt;カートアイテム単価&lt;/li&gt;&lt;li&gt;カート内で移動されるアイテムの価格です。&lt;/li&gt;&lt;/ul&gt; |
| `cart_quantity` |  &lt;ul&gt;&lt;li&gt;カートアイテム数量&lt;/li&gt;&lt;li&gt;カート内で移動されるアイテムの数量です。&lt;/li&gt;&lt;/ul&gt; |
| `cart_currency` |  &lt;ul&gt;&lt;li&gt;カートアイテム通貨&lt;/li&gt;&lt;li&gt;カート内で移動されるアイテムの通貨です。&lt;/li&gt;&lt;/ul&gt; |
| `cart_schema` |  &lt;ul&gt;&lt;li&gt;コンテキストスキーマ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマです。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `cart_context.data` |  &lt;ul&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値です。&lt;/li&gt;&lt;li&gt;マッピング時に `cart_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `cart_contextObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義コンテキスト&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。&lt;/li&gt;&lt;/ul&gt; |

### サイト検索追跡

|**宛先名**| **説明**|
|---| ---|
| `sst_terms` |  &lt;ul&gt;&lt;li&gt;検索用語&lt;/li&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;サイト検索で使用される用語のリストです。&lt;/li&gt;&lt;li&gt;これが入力されている場合のみ検索イベントが発火します。&lt;/li&gt;&lt;/ul&gt; |
|`sst_filters`|  &lt;ul&gt;&lt;li&gt;検索フィルター&lt;/li&gt;&lt;li&gt;フィルタータイプと用語を定義するJSONオブジェクトです。&lt;/li&gt;&lt;/ul&gt; |
| `sst_totalResults` |  &lt;ul&gt;&lt;li&gt;検索結果の総数&lt;/li&gt;&lt;li&gt;検索で見つかった結果の総数です&lt;/li&gt;&lt;/ul&gt; |
| `sst_pageResults` |  &lt;ul&gt;&lt;li&gt;最初のページの結果&lt;/li&gt;&lt;li&gt;最初のページに表示される結果の数です。&lt;/li&gt;&lt;/ul&gt; |
| `sst_schema` |  &lt;ul&gt;&lt;li&gt;コンテキストスキーマ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマです。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `sst_context.data` |  &lt;ul&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値です。&lt;/li&gt;&lt;li&gt;マッピング時に `sst_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `sst_contextObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義コンテキスト&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。&lt;/li&gt;&lt;/ul&gt; |

### 構造化イベント

|**宛先名**| **説明**|
|---| ---|
| `stctCat` |  &lt;ul&gt;&lt;li&gt;カテゴリ&lt;/li&gt;&lt;li&gt;追跡しているオブジェクトのグループ名です。&lt;/li&gt;&lt;/ul&gt; |
| `stctActn` |  &lt;ul&gt;&lt;li&gt;アクション名&lt;/li&gt;&lt;li&gt;追跡しているオブジェクトのユーザーインタラクションの名前です。&lt;/li&gt;&lt;/ul&gt; |
| `stctLabel` |  &lt;ul&gt;&lt;li&gt;ラベル&lt;/li&gt;&lt;li&gt;追跡している特定のオブジェクトを識別する追加の名前です。&lt;/li&gt;&lt;/ul&gt; |
| `stctProp` |  &lt;ul&gt;&lt;li&gt;プロパティ&lt;/li&gt;&lt;li&gt;オブジェクトまたはそれに対して行われたアクションを説明する追加の項目です。&lt;/li&gt;&lt;/ul&gt; |
| `stctVal` |  &lt;ul&gt;&lt;li&gt;値&lt;/li&gt;&lt;li&gt;ユーザーインタラクションを説明する追加の小数点数です。&lt;/li&gt;&lt;/ul&gt; |
| `stc_schema` |  &lt;ul&gt;&lt;li&gt;コンテキストスキーマ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマです。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`stc_context.data`|  &lt;ul&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値です。&lt;/li&gt;&lt;li&gt;マッピング時に `stc_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `stc_contextObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義コンテキスト&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。&lt;/li&gt;&lt;/ul&gt; |

### 非構造化イベント

|**宛先名**| **説明**|
|---| ---|
| `unstctDataSchema` |  &lt;ul&gt;&lt;li&gt;スキーマ&lt;/li&gt;&lt;li&gt;イベントを記述するJSONスキーマです。Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `unstctData.data` |  &lt;ul&gt;&lt;li&gt;ユーザー定義データ&lt;/li&gt;&lt;li&gt;イベントによって追跡されるデータ値です。&lt;/li&gt;&lt;li&gt;マッピング時に `unstctData.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `unstctDataObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義データオブジェクト&lt;/li&gt;&lt;li&gt;上記のプロパティを持つカスタム構成オブジェクトです。&lt;/li&gt;&lt;li&gt;個々のプロパティの代わりに使用してください。&lt;/li&gt;&lt;/ul&gt; |
| `stc_schema` |  &lt;ul&gt;&lt;li&gt;コンテキストスキーマ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマです。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `nstc_context.data` |  &lt;ul&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値です。&lt;/li&gt;&lt;li&gt;マッピング時に `unstc_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `unstc_contextObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義コンテキスト&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。&lt;/li&gt;&lt;/ul&gt; |

### 同意追跡

|**宛先名**| **説明**|
|---| ---|
| `consentGranted` |  &lt;ul&gt;&lt;li&gt;ユーザーが同意を許可&lt;/li&gt;&lt;li&gt;ユーザーがデータ収集に同意することを追跡するために使用されます。&lt;/li&gt;&lt;li&gt;少なくとも `id` と `version` の引数が提供されている場合、同意文書コンテキストがイベントに添付されます。&lt;/li&gt;&lt;/ul&gt; |
| `consentWithdrawn` |  &lt;ul&gt;&lt;li&gt;ユーザーが一部の同意を撤回&lt;/li&gt;&lt;li&gt;ユーザーがデータ収集の同意を撤回することを追跡するために使用されます。&lt;/li&gt;&lt;li&gt;少なくとも `id` と `version` の引数が提供されている場合、同意文書コンテキストがイベントに添付されます。&lt;/li&gt;&lt;/ul&gt; |
| `allConsentWithdrawn` |  &lt;ul&gt;&lt;li&gt;ユーザーがすべての同意を撤回&lt;/li&gt;&lt;li&gt;すべての同意が撤回されるべきかどうかを指定します。&lt;/li&gt;&lt;/ul&gt; |
| `con_documentId` |  &lt;ul&gt;&lt;li&gt;同意文書ID&lt;/li&gt;&lt;li&gt;同意文書は、メソッドに提供された引数（許可および撤回イベントの両方でこれは：`id`、`version`、`name`、および `description`）を格納するカスタムコンテキストです。&lt;/li&gt;&lt;li&gt;いずれかの同意方法で、コンテキスト引数に同意文書の自己記述JSONの配列を渡すことによって、追加の文書がイベントに追加されることができます。&lt;/li&gt;&lt;/ul&gt; |
| `con_documentVer` |  &lt;ul&gt;&lt;li&gt;同意文書バージョン&lt;/li&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;同意を与える文書のバージョンです&lt;/li&gt;&lt;/ul&gt; |
| `con_documentName` |  &lt;ul&gt;&lt;li&gt;同意文書名&lt;/li&gt;&lt;li&gt;同意文書の名前です。&lt;/li&gt;&lt;/ul&gt; |
| `con_documentDesc` |  &lt;ul&gt;&lt;li&gt;同意文書の説明&lt;/li&gt;&lt;li&gt;同意文書の説明です。&lt;/li&gt;&lt;/ul&gt; |
| `con_documentExpiry` |  &lt;ul&gt;&lt;li&gt;同意文書の有効期限&lt;/li&gt;&lt;li&gt;提供された日時までユーザーが添付された文書に同意し、その後は同意が無効になることを指定します。&lt;/li&gt;&lt;/ul&gt; |
| `unstc_schema` |  &lt;ul&gt;&lt;li&gt;コンテキストスキーマ&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;コンテキストを記述するJSONスキーマです。&lt;/li&gt;&lt;li&gt;Igluライブラリに存在する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `nstc_context.data` |  &lt;ul&gt;&lt;li&gt;コンテキストデータ&lt;/li&gt;&lt;li&gt;コンテキストによって追跡されるデータ値です。&lt;/li&gt;&lt;li&gt;マッピング時に `unstc_context.data` の `data` をあなたの値に関連付けられた名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `con_contextObj` |  &lt;ul&gt;&lt;li&gt;ユーザー定義コンテキスト&lt;/li&gt;&lt;li&gt;スキーマとデータプロパティを持つカスタムコンテキストオブジェクトです。&lt;/li&gt;&lt;/ul&gt; |

## ベンダー文書

* [SnowPlow Javascript トラッカーのドキュメント](https://docs.snowplowanalytics.com/docs/collecting-data/collecting-from-own-applications/javascript-trackers/)
