---
title: Google広告のコンバージョントラッキングとリマーケティング（gtag.js）タグ構成ガイド
description: この記事では、Google広告のコンバージョントラッキング＆リマーケティング（gtag.js）タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-ads-conversion-tracking-and-remarketing-gtagjs-tag/
---
## タグのヒント

* Eコマース拡張機能をサポートしています：
  * 小計/コンバージョン値。
  * 注文通貨/コンバージョン通貨。
  * 注文ID/トランザクションID。
  * 製品IDのリスト。
  * カテゴリのリスト。
  * 数量のリスト。
  * 価格のリスト。
* タグとコネクタを使用したハイブリッド構成を推奨します。この構成は、最大限のデータ耐久性を保証し、サーバーサイドのシグナルとのイベントマッチングを改善し、リアルタイムのクライアントサイドシグナルを保持しながらデータフローの連続性を維持します。詳細については、[Google広告のウェブ用拡張コンバージョンコネクタ]()を参照してください。
* 標準構成値とEコマース拡張値を動的に上書きするためにマッピングを使用します。
* カスタムコンバージョン変数をマッピングして、`myvar`をカスタム変数名に置き換えて渡します。
* [Google: ダイナミックリマーケティングのドキュメント](https://support.google.com/google-ads/answer/7305793)。
* [Google: Google広告のドキュメント](https://developers.google.com/adwords-remarketing-tag/)。
* [Crypto Extension]()を使用して、**ハッシュ化されたメール**と**電話番号**の値を暗号化して入力します。

## 拡張コンバージョン

Googleのウェブ用拡張コンバージョン機能は、コンバージョン測定の精度を向上させることができます。これは、プライバシーを保護する方法でウェブサイトからハッシュ化された第一者のコンバージョンデータを既存のコンバージョンタグに送信することによって補完します。

* 拡張コンバージョンを有効にする前に、Google広告アカウントで拡張コンバージョンを有効にする必要があります。詳細については、[Google: Googleタグを使用してウェブ用拡張コンバージョンを構成する](https://support.google.com/google-ads/answer/13258081?sjid=1600196321043643540-NC)を参照してください。
* このクライアントサイドタグを補完するためにサーバーサイドのウェブ用拡張コンバージョンコネクタを使用している場合、Googleがイベントを重複排除できるように、非購入コンバージョンの**トランザクションID**に`tealium_random`のようなユニークな値をマッピングします。さらに、コンバージョンのGoogle広告構成で**実装タイプ**を`API`に構成します。

 拡張コンバージョンのサポートは2022年6月に追加されました。古いバージョンのタグを使用していてこの機能を使用したい場合は、タグテンプレートを更新する必要があります。詳細については、[タグテンプレートの管理]()を参照してください。 

## 重複排除

Googleは、クライアントサイドとサーバーサイドのコンバージョンから同じコンバージョンイベントが送信された場合にトランザクションIDを使用して重複排除します。トランザクションIDは各コンバージョンイベントに固有であるべきです。このIDのサーバーサイドの値は、対応するクライアントサイドのイベントIDと一致するべきです。購入イベントには`order_ID`を、その他のイベントには`tealium_random`を使用することを推奨します。

## ダイナミックリマーケティング

Google広告のコンバージョントラッキングとリマーケティングタグは、ウェブサイトでの以前の訪問の活動に基づいて広告をパーソナライズするダイナミックリマーケティングをサポートしています。このタグでリマーケティング機能を使用するには、タグ構成で**リマーケティングを有効にする**を**オン**に構成します。

リマーケティングを有効にすると、このタグは自動的に[Eコマース拡張機能]()からデータを引き出してGoogle広告**小売**パラメータを入力します。リマーケティングイベントで値を渡すには、**データマッピング &gt; イベント固有のパラメータ**に移動し、関連するデータレイヤー属性をリマーケティングイベント属性にマッピングします。

Googleは、リマーケティングカテゴリの少なくとも1つの属性（例えば、小売、教育、フライト、ホテルとレンタル、求人、ローカル、不動産、旅行など）をリマーケティングイベントにマッピングすることを常に推奨しています。ユーザーがウェブサイトで複数のアイテムと対話する場合、たとえばショッピングカートのチェックアウトや旅行の行程の検索など、複数の属性をマッピングすることができます。

ダイナミックリマーケティングイベントとアイテムパラメータについての詳細は、[Google: ダイナミックリマーケティングイベントとパラメータ](https://support.google.com/google-ads/answer/7305793)を参照してください。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、次の構成を構成します：

* **コンバージョンID**：コンバージョンのユニークID。このIDはGoogle広告のコントロールパネルで見つけることができます（例：`AW-123456789`）。
    * この値を動的に上書きするためにマッピングを使用します。
    * 複数のプロパティのデータを送信するためにカンマ区切りのリストを使用します。
* **コンバージョンラベル**：ここにデフォルトのラベルを構成し、マッピングを使用してこの値を動的に上書きします。
    * 複数のラベルのデータを送信するためにカンマ区切りのリストを使用します。このリストは、**コンバージョンID**の数に合わせて**コンバージョンラベル**を使用するか、すべての**コンバージョンID**に対して単一のラベルを使用することができます。
* **コンバージョン値**：ここにデフォルト値を構成するか、Eコマース拡張機能からの小計値を使用するためにこの欄を空白にします。
    * この値とEコマース拡張値を動的に上書きするためにマッピングを使用します。
* **グローバルオブジェクト**：この値はイベントキューに使用される**グローバルオブジェクト**の名前です。指定されていない場合、`gtag`が使用されます。
    * ほとんどの実装では必要ありません。
* **データレイヤー名**：デフォルトでは、グローバルサイトタグによって開始され参照されるデータレイヤーは**dataLayer**という名前です。プロジェクトが別の名前を必要とする場合のみ、データレイヤーの名前を変更します。
* **リマーケティングを有効にする**：リマーケティングが有効になっている場合、このタグは自動的にEコマース拡張機能からデータを引き出してGoogle広告**小売**パラメータを入力します。
    * ツールボックスの**小売**タブに直接マッピングすると、Eコマース拡張機能を通じて引き出されたデータを上書きします。
* **ページタイプ**：ここでデフォルトのページタイプを選択し、マッピングを使用してこの値を動的に上書きします。
* **クロストラッキングドメイン**：クロスドメイントラッキング（`setAllowLinker`）で使用するドメインのカンマ区切りリストです。
    * このリストは、`tealiumiq.com`のようなトップレベルドメインで構成されるべきです。
* **拡張コンバージョンを有効にする**
  * このオプションは、タグを通じてPII（個人識別情報）を送信している場合のみ有効にします。
  * このクライアントサイドタグを補完するためにサーバーサイドの**ウェブ用拡張コンバージョン**コネクタを使用している場合、非購入コンバージョンの**トランザクションID**に`tealium_random`のようなユニークな値をマッピングし、Googleがイベントを重複排除できるようにします。さらに、コンバージョンのGoogle広告構成で**実装タイプ**を`API`に構成します。
  * EventStreamでGoogle広告拡張コンバージョンコネクタを使用してこのタグを構成する方法については、[Tealium &#43; Google拡張コンバージョン統合ガイド]()を参照してください。
* **サーバーサイド拡張コンバージョンのイベントマッチングを有効にする**
  * [Google広告ウェブ用拡張コンバージョンコネクタ]()で自動トランザクションIDを使用するためにイベントマッチングを有効にします。

## 読み込みルール

すべてのページでタグを読み込むか、タグの読み込み条件を構成します。詳細については、[読み込みルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは次のとおりです：


### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `conversion_id` | 文字列 | 変換 ID。  |
| `conversion_label` | 文字列 | 変換ラベル。  | 
|  `conversion_value` | 文字列 | 変換値。  |
|  `conversion_currency` | 文字列 | 変換通貨。  |
|  `user_id` | 文字列 | ユーザー ID。  |
|  `pagetype` | 文字列 | ページタイプ。  |
| `aw_merchant_id` | 文字列 | マーチャントセンター ID。  | 
| `aw_feed_country` | 文字列 | フィード国。  | 
|  `aw_feed_language` | 文字列 | フィード言語。  |
|  `config.send_page_view`  | ブール値 | ページビューを送信。 |
| `conversion_cookie_prefix` | 文字列 | 変換クッキープレフィックス。  | 
| `custom.myvar` | 文字列 | カスタム変換変数。  | 
|  `cross_track_domains` | カンマ区切り文字列 | クロストラッキングドメイン。  |
| `config.enable_event_matching_conversions` | ブール値 | サーバーサイドエンリッチメント変換のイベントマッチングを有効にする。 |

### 小売

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `rmkt.retail.id`  | 配列 | ユニークな商品 ID（`_cprod`を上書き）。  | 

### 教育

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `rmkt.education.id`  | 配列 | ユニーク ID。|
|  `rmkt.education.location_id`  | 配列 | ロケーション ID。|

### フライト

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `rmkt.flights.origin`  | 配列 | 出発地 ID。|
|  `rmkt.flights.destination`  | 配列 | 目的地 ID。|
|  `rmkt.flights.start_date`  | 配列 | 開始日。|
| `rmkt.flights.end_date`  | 配列 | 終了日。  |

### ホテルとレンタル

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `rmkt.hotel_rental.id`  | 配列 | 物件 ID。 |
|  `rmkt.hotel_rental.start_date`  | 配列 | 開始日。|
|  `rmkt.hotel_rental.end_date`  | 配列 | 終了日。|

### ジョブ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `rmkt.jobs.id`  | 配列 | ジョブ ID。 |
|  `rmkt.jobs.location_id`  | 配列 | ロケーション ID。|

### ローカル

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `rmkt.local.id`  | 配列 | ディール ID。|

### 不動産

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `rmkt.real_estate.id`  | 配列 |リスティング ID。 |

### 旅行

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `rmkt.travel.origin`  | 配列 | 出発地 ID。|
|  `rmkt.travel.destination`  | 配列 | 目的地 ID。 |
|  `rmkt.travel.start_date`  | 配列 |開始日。|
|  `rmkt.travel.end_date`  | 配列 | 終了日。 |

### カスタム / レガシー

| 変数 |  説明 |
|:---------|:------------|
| `rmkt.custom.id`  | 配列。カスタム ID。  |
|  `rmkt.custom.location_id`  | 配列。カスタムロケーション ID/ID2 |
|   `ecomm.prodid` |  ecomm.prodid  (`_cprod`を上書き) |
|     `ecomm.totalvalue` | ecomm.totalvalue |
|   `ecomm.category` |  ecomm.category (`_ccat`を上書き) |
|  `ecomm.pvalue`  | ecomm.pvalue (`_cprice`を上書き) |
|  `ecomm.quantity`  | ecomm.quantity (`_cquan`を上書き) |
| `edu.pid` |  edu.pid  | 
|  `edu.plocid` |  edu.plocid  |
| `flight.originid` | flight.originid  | 
| `flight.destid` | flight.destid  | 
|  `flight.totalvalue` | flight.totalvalue  |
| `flight.startdate` | flight.startdate  | 
|  `flight.enddate` | flight.enddate  |
| `hrental.id` | hrental.id  | 
| `hrental.startdate` | hrental.startdate  | 
| `hrental.enddate` | hrental.enddate  | 
| `hrental.totalvalue` |hrental.totalvalue  | 
| `job.id` |  job.id  | 
| `job.locid`  | job.locid  | 
| `job.totalvalue` |  job.totalvalue  | 
| `local.id` |  local.id  | 
|  `local.totalvalue` | local.totalvalue  |
|  `listing.id` |  listing.id  |
|  `listing.totalvalue` |  listing.totalvalue  |
|  `travel.destid` |  travel.destid  |
|  `travel.originid` |  travel.originid  |
| `travel.startdate` |  travel.startdate  | 
|  `travel.enddate` |  travel.enddate  |
| `travel.totalvalue` |  travel.totalvalue  | 
|  `dynx.itemid` |  dynx.itemid  |
|  `dynx.itemid2` |  dynx.itemid2  |
| `dynx.totalvalue` |  dynx.totalvalue  | 

### 上級

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `custom.ecomm_rec_prodid`| 配列  |推奨される商品 ID。  | 
|`custom.a` |  数値 |訪問の年齢。  |
| `custom.g`| 文字列 |訪問の性別。  |
|`custom.hasaccount`| ブール値  |訪問がアカウントを持っているか。  | 
| `custom.cqs`| 数値 |顧客品質スコア。  | 
| `custom.rp`| ブール値  |リピート購入者。  | 
| `custom.ly` | 数値 |訪問のロイヤルティスコア。 | 
| `custom.hs`| 数値 |訪問のハイスペンダースコア。 | 
| `custom.myvar`| 文字列  |カスタム。  | 

### 電話変換

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `config.phone_conversion_number` | 文字列 | 電話変換番号。  | 
|  `config.phone_conversion_callback`  | 関数 | 電話変換コールバック。 |
|  `config.phone_conversion_css_class`  | 文字列 | 電話変換 CSS クラス名。 |
|  `config.phone_conversion_options.timeout`  | 数値 | 電話変換タイムアウト。 |
| `config.phone_conversion_options.cache`  | ブール値 | 電話変換キャッシュ。  |

### Eコマース

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|   `order_id` (`_corder`を上書き) | 文字列 | 注文 ID。 |
|  `order_subtotal` (`_csubtotal`を上書き) | 数値 | 小計。  | 
|   `order_currency` (`_ccurrency`を上書き) | 文字列 | 通貨。 |
|  `product_id` (`_cprod`を上書き)  | 配列 | 商品 ID のリスト |
| `product_category` (`_ccat`を上書き)  | 配列 | カテゴリのリスト。  |
|  `product_quantity` (`_cquan`を上書き)  | 配列 | 数量のリスト。 |
| `product_unit_price` (`_cprice`を上書き)  | 配列 | 価格のリスト。  |
|  `product_discount` (`_cdisc`を上書き)  | 配列 | 割引のリスト。 |

### イベント固有のパラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `gtag_enable_tcf_support` (true/false) | ブール値 | TCFサポートを有効にする  |
| `user_provided_data` | 文字列 | `user_data`オブジェクトで渡される任意のマップされたイベント固有のパラメータ。 |
| `customer_type` | 文字列 | `purchase`イベントでの顧客が新規顧客かどうか。 &lt;ul&gt;&lt;li&gt;`New`: 540日以内に購入がない新規顧客。&lt;/li&gt;&lt;li&gt;`Returning`: 540日以内に購入があるリターニング顧客。&lt;/li&gt;&lt;/ul&gt; |
### IAB透明性と同意フレームワーク v2

イベントのマッピングについては、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `exception` | アプリの実行の通常の流れが中断されたときに、例外イベントが記録されます。 |
| `generate_lead` | リードが生成されました。この変数は、再エンゲージメントキャンペーンの効果を理解するのに役立ちます。 |
| `login` | ユーザーがログインしました。 |
| `page_view` | ユーザーがページを閲覧しました。 |
| `screen_view` | ユーザーが新しい画面に移動しました。 |
| `search` | ユーザーが検索を実行しました。このイベントを使用して、検索操作をコンテキスト化し、ユーザーがウェブサイトやアプリで何を検索しているかを特定できます。例えば、検索を実行した後にユーザーがページを閲覧したときにこのイベントを送信できます。 |
| `share` | ユーザーがコンテンツを共有したときにこのイベントを使用します。 |
| `sign_up` | ユーザーがサイトやサービスに登録しました。 |
| `timing_complete` | ユーザーがプロセスを完了しました。 |
| `view_search_results` | ユーザーに検索結果が表示されました。Google Analyticsの拡張イベント測定で`view_search_results`イベントを自動収集するように構成できることに注意してください。 |
| `cst` | カスタムイベント。 |
| `add_payment_info` | ユーザーが支払い情報を提出しました。 |
| `add_to_cart` | アイテムが購入用カートに追加されました。 |
| `add_to_wishlist` | アイテムがウィッシュリストに追加されました。このイベントを使用して、アプリ内で人気のギフトアイテムを特定します。 |
| `begin_checkout` | ユーザーがチェックアウトを開始しました。 |
| `checkout_progress` | ユーザーがチェックアウトの途中です。 |
| `purchase` | 一つ以上のアイテムがユーザーによって購入されました。 |
| `refund` | 一つ以上のアイテムがユーザーに返金されました。 |
| `remove_from_cart` | アイテムがカートから削除されました。 |
| `product_click` | リストからアイテムが選択されました。 |
| `promotion_click` | リストからプロモーションが選択されました。 |
| `set_checkout_option` | ユーザーがチェックアウトオプションを選択しました。例えば、配送方法などです。 |
| `view_item` | ユーザーにコンテンツが表示されました。このイベントを使用して、最も人気のある閲覧アイテムを発見します。 |
| `view_item_list` | ユーザーに特定のカテゴリのアイテムリストが表示されました。 |
| `view_promotion` | リストからプロモーションが表示されました。 |

### エンリッチメントされたコンバージョン

| 変数  | タイプ | 説明 |
|:---------|:------------|:------------|
|  `config.allow_enhanced_conversions`  | Boolean | エンリッチメントされたコンバージョンを許可します。 |
|  `user_data.email` | String |メールアドレス。  |
|  `user_data.sha256_email_address` | String |ハッシュ化されたメールアドレス。  |
|  `user_data.phone_number` | String |電話番号。  |
| `user_data.sha256_phone_number` | String |ハッシュ化された電話番号。  | 
|  `user_data.address.first_name` | String |名前。  |
| `user_data.address.sha256_first_name` |String | ハッシュ化された名前。  | 
|  `user_data.address.last_name` |String |姓。  | 
| `user_data.address.sha256_last_name` | String |ハッシュ化された姓。  | 
| `user_data.address.street` | String |住所。  | 
|  `user_data.address.city` |String |市区町村。  |
|  `user_data.address.region` | String |地域。  |
| `user_data.address.postal_code` | String |郵便番号。  | 
|  `user_data.address.country` | String |国。  |
|  `transaction_id` |String | (必須) トランザクションID。  |
