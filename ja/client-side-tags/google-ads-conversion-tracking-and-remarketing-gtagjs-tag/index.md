---
title: Google 広告コンバージョン トラッキングおよびリマーケティング（gtag.js）タグ構成ガイド
description: この記事では、Google 広告コンバージョン トラッキングおよびリマーケティング（gtag.js）タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-ads-conversion-tracking-and-remarketing-gtagjs-tag/
---
## タグに関するヒント

* E-Commerce 拡張機能の以下の項目をサポートします。
  * 小計／コンバージョン値。
  * 注文通貨／コンバージョン通貨。
  * 注文 ID／トランザクション ID。
  * 商品 ID のリスト。
  * カテゴリのリスト。
  * 数量のリスト。
  * 価格のリスト。
* タグとコネクタの両方を使用するハイブリッド構成を推奨します。この構成により、データの耐障害性を最大限に高め、サーバーサイドのシグナルとのイベントマッチングを改善し、リアルタイムのクライアントサイドシグナルを維持しながらデータフローの継続性を確保できます。詳細については、[Google Ads Enhanced Conversions for Web コネクタ](https://docs.tealium.com/google-ads-enhanced-conversions-for-web-connector/)を参照してください。
* マッピングを使用して、標準の構成値と E-Commerce 拡張機能の値を動的に上書きします。
* **カスタム コンバージョン変数**にマッピングし、`myvar` をカスタム変数名に置き換えることで、カスタム コンバージョン変数を渡します。
* [Google：動的リマーケティングのドキュメント](https://support.google.com/google-ads/answer/7305793)。
* [Google：Google 広告のドキュメント](https://developers.google.com/adwords-remarketing-tag/)。
* [Crypto 拡張機能](https://docs.tealium.com/crypto-extension/)を使用して、**ハッシュ化されたメールアドレス**と**電話番号**の値を暗号化して入力します。

## 拡張コンバージョン

Google のウェブ向け拡張コンバージョン機能を使用すると、コンバージョン測定の精度を向上できます。この機能は、ウェブサイトからハッシュ化されたファーストパーティのコンバージョンデータをプライバシーに配慮した方法で送信することで、既存のコンバージョンタグを補完します。

* 拡張コンバージョンを有効にする前に、Google 広告アカウントで拡張コンバージョンを有効にする必要があります。詳細については、[Google：Google タグを使用してウェブ向け拡張コンバージョンを構成する](https://support.google.com/google-ads/answer/13258081?sjid=1600196321043643540-NC)を参照してください。
* このクライアントサイドタグを補完するために、サーバーサイドのウェブ向け拡張コンバージョンコネクタを使用している場合は、購入以外のコンバージョンについて、`tealium_random` などの一意の値を**トランザクション ID**にマッピングし、Google がイベントを重複排除できるようにします。また、コンバージョンの Google 広告構成で、**実装タイプ**を `API` に構成します。


<blockquote>
拡張コンバージョンのサポートは 2022 年 6 月に追加されました。古いバージョンのタグを実行しており、この機能を使用する場合は、タグテンプレートを更新する必要があります。詳細については、[タグテンプレートの管理](https://docs.tealium.com/manage-templates/)を参照してください。
</blockquote>


## 重複排除

同じコンバージョンイベントがクライアントサイドとサーバーサイドの両方から送信された場合、Google はトランザクション ID を使用して重複を排除します。トランザクション ID は、コンバージョンイベントごとに一意である必要があります。この ID のサーバーサイドの値は、対応するクライアントサイドのイベント ID と同じである必要があります。購入には `order_ID`、その他のイベントには `tealium_random` を使用することを推奨します。

## 動的リマーケティング

Google 広告コンバージョン トラッキングおよびリマーケティングタグは、ウェブサイト上での訪問の過去のアクティビティに基づいて広告をパーソナライズできる動的リマーケティングをサポートしています。このタグでリマーケティング機能を使用するには、タグ構成で**リマーケティングを有効化**を**オン**に構成します。

リマーケティングを有効にすると、このタグは [E-Commerce 拡張機能](https://docs.tealium.com/e-commerce-extension/)からデータを自動的に取得し、Google 広告の**小売**パラメータに値を構成します。リマーケティングイベントで値を渡すには、**データマッピング > イベント固有のパラメータ**に移動し、関連するデータレイヤー属性をリマーケティングイベント属性にマッピングします。

Google は、リマーケティングカテゴリ（小売、教育、航空便、ホテルと賃貸、求人、地域、不動産、旅行など）のいずれかから、少なくとも 1 つの属性をリマーケティングイベントに必ずマッピングすることを推奨しています。ショッピングカートの確認や旅行日程の検索など、ユーザーがウェブサイト上で複数の項目を操作する場合は、複数の属性をマッピングできます。

動的リマーケティングイベントと商品パラメータの詳細については、[Google：動的リマーケティングのイベントとパラメータ](https://support.google.com/google-ads/answer/7305793)を参照してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、以下の構成を構成します。

* **コンバージョン ID**：コンバージョンの一意の ID。Google 広告の管理画面でこの ID を確認できます（例：`AW-123456789`）。
    * マッピングを使用して、この値を動的に上書きします。
    * 複数のプロパティにデータを送信するには、カンマ区切りのリストを使用します。
* **コンバージョン ラベル**：ここでデフォルトのラベルを構成し、マッピングを使用してこの値を動的に上書きします。
    * 複数のラベルにデータを送信するには、カンマ区切りのリストを使用します。このリストでは、**コンバージョン ID**と同じ数の**コンバージョン ラベル**を使用するか、すべての**コンバージョン ID**に対して単一のラベルを使用できます。
* **コンバージョン値**：ここでデフォルト値を構成するか、空欄のままにして E-Commerce 拡張機能の小計値を使用します。
    * マッピングを使用して、この値と E-Commerce 拡張機能の値を動的に上書きします。
* **グローバルオブジェクト**：イベントキューに使用される**グローバルオブジェクト**の名前です。指定しない場合は、`gtag` が使用されます。
    * ほとんどの実装では必要ありません。
* **データレイヤー名**：デフォルトでは、グローバルサイトタグによって初期化および参照されるデータレイヤーの名前は **dataLayer** です。プロジェクトで別の名前が必要な場合にのみ、データレイヤーの名前を変更してください。
* **リマーケティングを有効化**：リマーケティングを有効にすると、このタグは E-Commerce 拡張機能からデータを自動的に取得し、Google 広告の**小売**パラメータに値を構成します。
    * ツールボックスの**小売**タブに直接マッピングすると、E-Commerce 拡張機能から取得されたデータが上書きされます。
* **ページタイプ**：ここでデフォルトのページタイプを選択し、マッピングを使用してこの値を動的に上書きします。
* **クロストラッキングドメイン**：クロスドメイントラッキング（`setAllowLinker`）で使用するドメインのカンマ区切りリストです。
    * このリストには、`tealiumiq.com` などのトップレベルドメインを指定します。
* **拡張コンバージョンを有効化**
  * タグを通じて PII（個人を特定できる情報）を送信する場合にのみ、このオプションを有効にしてください。
  * このクライアントサイドタグを補完するために、サーバーサイドの**ウェブ向け拡張コンバージョン**コネクタを使用している場合は、購入以外のコンバージョンについて、`tealium_random` などの一意の値を**トランザクション ID**にマッピングし、Google がイベントを重複排除できるようにします。また、コンバージョンの Google 広告構成で、**実装タイプ**を `API` に構成します。
  * Event Streaming で Google 広告拡張コンバージョンコネクタと連携するようにこのタグを構成する方法については、[Tealium + Google 拡張コンバージョン統合ガイド](https://docs.tealium.com/tealium-google-enhanced-conversions-integration-guide/)を参照してください。
* **サーバーサイド拡張コンバージョンのイベントマッチングを有効化**
  * [Google Ads Enhanced Conversions for Web コネクタ](https://docs.tealium.com/google-ads-enhanced-conversions-for-web-connector/)で自動トランザクション ID を使用するには、イベントマッチングを有効にします。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは以下のとおりです。
### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `conversion_id` | 文字列 | コンバージョン ID。 |
| `conversion_label` | 文字列 | コンバージョン ラベル。 | 
| `conversion_value` | 文字列 | コンバージョン値。 |
| `conversion_currency` | 文字列 | コンバージョン通貨。 |
| `user_id` | 文字列 | ユーザー ID。 |
| `pagetype` | 文字列 | ページタイプ。 |
| `aw_merchant_id` | 文字列 | Merchant Center ID。 | 
| `aw_feed_country` | 文字列 | フィードの国。 | 
| `aw_feed_language` | 文字列 | フィードの言語。 |
| `config.send_page_view` | ブール値 | ページビューを送信します。 |
| `conversion_cookie_prefix` | 文字列 | コンバージョン Cookie のプレフィックス。 | 
| `custom.myvar` | 文字列 | カスタム コンバージョン変数。 | 
| `cross_track_domains` | カンマ区切りの文字列 | クロストラッキング対象のドメイン。 |
| `config.enable_event_matching_conversions` | ブール値 | サーバーサイドの拡張コンバージョンでイベント マッチングを有効にします。 |

### 小売

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `rmkt.retail.id` | 配列 | 一意の商品 ID（`_cprod` を上書き）。 | 

### 教育

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `rmkt.education.id` | 配列 | 一意の ID。|
| `rmkt.education.location_id` | 配列 | ロケーション ID。|

### 航空便

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `rmkt.flights.origin` | 配列 | 出発地 ID。|
| `rmkt.flights.destination` | 配列 | 目的地 ID。|
| `rmkt.flights.start_date` | 配列 | 開始日。|
| `rmkt.flights.end_date` | 配列 | 終了日。 |

### ホテルとレンタル

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `rmkt.hotel_rental.id` | 配列 | 施設 ID。 |
| `rmkt.hotel_rental.start_date` | 配列 | 開始日。|
| `rmkt.hotel_rental.end_date` | 配列 | 終了日。|

### 求人

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `rmkt.jobs.id` | 配列 | 求人 ID。 |
| `rmkt.jobs.location_id` | 配列 | ロケーション ID。|

### ローカル

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `rmkt.local.id` | 配列 | 特典 ID。|

### 不動産

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `rmkt.real_estate.id` | 配列 | リスティング ID。 |

### 旅行

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `rmkt.travel.origin` | 配列 | 出発地 ID。|
| `rmkt.travel.destination` | 配列 | 目的地 ID。 |
| `rmkt.travel.start_date` | 配列 | 開始日。|
| `rmkt.travel.end_date` | 配列 | 終了日。 |

### カスタム／レガシー

| 変数 | 説明 |
|:---------|:------------|
| `rmkt.custom.id` | 配列。カスタム ID。 |
| `rmkt.custom.location_id` | 配列。カスタム ロケーション ID／ID2 |
| `ecomm.prodid` | ecomm.prodid（`_cprod` を上書き） |
| `ecomm.totalvalue` | ecomm.totalvalue |
| `ecomm.category` | ecomm.category（`_ccat` を上書き） |
| `ecomm.pvalue` | ecomm.pvalue（`_cprice` を上書き） |
| `ecomm.quantity` | ecomm.quantity（`_cquan` を上書き） |
| `edu.pid` | edu.pid | 
| `edu.plocid` | edu.plocid |
| `flight.originid` | flight.originid | 
| `flight.destid` | flight.destid | 
| `flight.totalvalue` | flight.totalvalue |
| `flight.startdate` | flight.startdate | 
| `flight.enddate` | flight.enddate |
| `hrental.id` | hrental.id | 
| `hrental.startdate` | hrental.startdate | 
| `hrental.enddate` | hrental.enddate | 
| `hrental.totalvalue` | hrental.totalvalue | 
| `job.id` | job.id | 
| `job.locid` | job.locid | 
| `job.totalvalue` | job.totalvalue | 
| `local.id` | local.id | 
| `local.totalvalue` | local.totalvalue |
| `listing.id` | listing.id |
| `listing.totalvalue` | listing.totalvalue |
| `travel.destid` | travel.destid |
| `travel.originid` | travel.originid |
| `travel.startdate` | travel.startdate | 
| `travel.enddate` | travel.enddate |
| `travel.totalvalue` | travel.totalvalue | 
| `dynx.itemid` | dynx.itemid |
| `dynx.itemid2` | dynx.itemid2 |
| `dynx.totalvalue` | dynx.totalvalue | 

### 詳細構成

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `custom.ecomm_rec_prodid` | 配列 | おすすめ商品の ID。 | 
| `custom.a` | 数値 | 訪問の年齢。 |
| `custom.g` | 文字列 | 訪問の性別。 |
| `custom.hasaccount` | ブール値 | 訪問がアカウントを所有しているかどうか。 | 
| `custom.cqs` | 数値 | 顧客品質スコア。 | 
| `custom.rp` | ブール値 | リピーター購入者かどうか。 | 
| `custom.ly` | 数値 | 訪問のロイヤルティ スコア。 | 
| `custom.hs` | 数値 | 訪問の高額購入者スコア。 | 
| `custom.myvar` | 文字列 | カスタム。 | 

### 電話コンバージョン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `config.phone_conversion_number` | 文字列 | 電話コンバージョン番号。 | 
| `config.phone_conversion_callback` | 関数 | 電話コンバージョンのコールバック。 |
| `config.phone_conversion_css_class` | 文字列 | 電話コンバージョンの CSS クラス名。 |
| `config.phone_conversion_options.timeout` | 数値 | 電話コンバージョンのタイムアウト。 |
| `config.phone_conversion_options.cache` | ブール値 | 電話コンバージョンのキャッシュ。 |

### E コマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `order_id`（`_corder` を上書き） | 文字列 | 注文 ID。 |
| `order_subtotal`（`_csubtotal` を上書き） | 数値 | 小計。 | 
| `order_currency`（`_ccurrency` を上書き） | 文字列 | 通貨。 |
| `product_id`（`_cprod` を上書き） | 配列 | 商品 ID のリスト。 |
| `product_category`（`_ccat` を上書き） | 配列 | カテゴリのリスト。 |
| `product_quantity`（`_cquan` を上書き） | 配列 | 数量のリスト。 |
| `product_unit_price`（`_cprice` を上書き） | 配列 | 価格のリスト。 |
| `product_discount`（`_cdisc` を上書き） | 配列 | 割引のリスト。 |

### イベント固有のパラメータ

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `gtag_enable_tcf_support`（true/false） | ブール値 | TCF サポートを有効にします。 |
| `user_provided_data` | 文字列 | `user_data` オブジェクトで渡される、マッピング済みの任意のイベント固有パラメータ。 |
| `customer_type` | 文字列 | `purchase` イベントの顧客が新規顧客かどうか。<ul><li>`New`：過去 540 日以内に購入していない新規顧客。</li><li>`Returning`：過去 540 日以内に購入したことがあるリピーター顧客。</li></ul> |
### IAB透明性・同意フレームワーク v2

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `exception` | アプリの通常の実行フローが中断された場合に、例外イベントが記録されます。 |
| `generate_lead` | リードが生成されました。この変数は、再エンゲージメントキャンペーンの効果を把握するのに役立ちます。 |
| `login` | ユーザーがログインしました。 |
| `page_view` | ユーザーがページを閲覧しました。 |
| `screen_view` | ユーザーが新しい画面に移動しました。 |
| `search` | ユーザーが検索を実行しました。このイベントを使用して検索操作にコンテキストを与えることで、ユーザーがウェブサイトやアプリで検索しているコンテンツを特定できます。たとえば、ユーザーが検索後にページを閲覧したときに、このイベントを送信できます。 |
| `share` | ユーザーがコンテンツを共有したときに、このイベントを使用します。 |
| `sign_up` | ユーザーがサイトまたはサービスに登録しました。 |
| `timing_complete` | ユーザーがプロセスを完了しました。 |
| `view_search_results` | 検索結果がユーザーに表示されました。Google アナリティクスの拡張イベント計測を使用すると、`view_search_results`イベントの自動収集を有効にできます。 |
| `cst` | カスタムイベント。 |
| `add_payment_info` | ユーザーが支払い情報を送信しました。 |
| `add_to_cart` | 購入する商品がカートに追加されました。 |
| `add_to_wishlist` | 商品がウィッシュリストに追加されました。このイベントを使用すると、アプリ内で人気のギフト商品を特定できます。 |
| `begin_checkout` | ユーザーが購入手続きを開始しました。 |
| `checkout_progress` | ユーザーが購入手続きを進めています。 |
| `purchase` | ユーザーが1つ以上の商品を購入しました。 |
| `refund` | 1つ以上の商品についてユーザーへの返金が行われました。 |
| `remove_from_cart` | 商品がカートから削除されました。 |
| `product_click` | リストから商品が選択されました。 |
| `promotion_click` | リストからプロモーションが選択されました。 |
| `set_checkout_option` | ユーザーが配送方法などの購入手続きオプションを選択しました。 |
| `view_item` | コンテンツがユーザーに表示されました。このイベントを使用すると、最も多く閲覧されている商品を確認できます。 |
| `view_item_list` | 特定のカテゴリーに属する商品のリストがユーザーに表示されました。 |
| `view_promotion` | リスト内のプロモーションが閲覧されました。 |

### 拡張コンバージョン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `config.allow_enhanced_conversions` | ブール値 | 拡張コンバージョンを許可します。 |
| `user_data.email` | 文字列 | メールアドレス。 |
| `user_data.sha256_email_address` | 文字列 | ハッシュ化されたメールアドレス。 |
| `user_data.phone_number` | 文字列 | 電話番号。 |
| `user_data.sha256_phone_number` | 文字列 | ハッシュ化された電話番号。 |
| `user_data.address.first_name` | 文字列 | 名。 |
| `user_data.address.sha256_first_name` | 文字列 | ハッシュ化された名。 |
| `user_data.address.last_name` | 文字列 | 姓。 |
| `user_data.address.sha256_last_name` | 文字列 | ハッシュ化された姓。 |
| `user_data.address.street` | 文字列 | 番地。 |
| `user_data.address.city` | 文字列 | 市区町村。 |
| `user_data.address.region` | 文字列 | 都道府県または地域。 |
| `user_data.address.postal_code` | 文字列 | 郵便番号。 |
| `user_data.address.country` | 文字列 | 国。 |
| `transaction_id` | 文字列 | （必須）トランザクションID。 |