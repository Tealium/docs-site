---
title: Google Analytics（gtag.js）タグ構成ガイド
description: この記事では、タグ管理アカウントで Google Analytics（gtag.js）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-analytics-gtagjs-tag/
---
Google Analytics は、オンラインコンテンツに対するユーザー操作を収集、構成、レポートするための API を提供します。gtag.js を使用すると、最新のトラッキング機能や統合機能が利用可能になった時点で活用できます。

## タグに関するヒント

* マッピングを使用して、以下を行います。
  * E コマース拡張機能の値を動的に上書きする。
  * イベントトリガーを構成する。
  * カスタムの指標、ディメンション、コンテンツグループを追加する。
* カスタムイベント変数内の `cst` を、使用するイベント名に置き換えます。
* 次の E コマース拡張機能の値をサポートします。
  * 注文 ID
  * 注文合計
  * 配送料
  * 税額
  * ストア
  * プロモーションコード
  * 顧客 ID
  * 商品 ID のリスト
  * 名前のリスト
  * ブランドのリスト
  * カテゴリのリスト
  * 価格のリスト
  * 数量のリスト
  * 割引のリスト

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を行います。

* **トラッキング ID**
  * データの送信先となる Google Analytics プロパティのトラッキング ID  
  * 例：`UA-XXXXXX-13`  
  * 複数のプロパティにデータを送信するには、カンマ区切りのリストを使用します。

<blockquote>
測定 ID をトラッキング ID の値に含めて、[アプリ + ウェブ](https://developers.google.com/analytics/devguides/collection/app-web/basic-tag)を有効にします。例：`UA-XXXXXX-13,G-XXXXXXXXXX`
</blockquote>

* **グローバルオブジェクト**
  * イベントキューに使用するグローバルオブジェクトの名前です。
  * 指定しない場合は、"gtag" が使用されます。
  * ほとんどの実装では指定する必要はありません。
* **クロストラッキングドメイン**
  * クロスドメイントラッキング（`setAllowLinker`）で使用するドメインのカンマ区切りリストです。
  * このリストを使用するには、クロスドメイントラッキングを **true** に構成する必要があります。
  * **tealiumiq.com** などのトップレベルドメインを指定してください。
* **クロスドメイントラッキング**
  * `setAllowLinker` の値を構成し、クロスドメイントラッキングプラグインを有効にします。
  * この機能を使用するには、1 つ以上のドメインを「クロストラッキングドメイン」フィールドで指定するか、`crossDomainTrack` にマッピングする必要があります。
* **トランスポートタイプ**
  * ヒットの送信に使用するトランスポートメカニズムを指定します。
* **広告機能を許可**
  * 標準の Google Analytics 実装で収集されるデータに加えて、Google Ad Manager（DoubleClick）Cookie を通じてトラフィックに関するデータを Google Analytics が収集できるようにします。
  * これを **オフ** に構成すると、すべての広告、レポート、リマーケティング機能が無効になり、Google Analytics のユーザーインターフェイスで構成されたプロパティ構成が上書きされます。
* **拡張リンクアトリビューション**
  * 不明な場合は、デフォルト値（**false**）を使用してください。
  * Google Analytics の拡張リンクアトリビューションは、1 つのページ上にある同じ URL への複数のリンクを自動的に区別し、リンク要素 ID を使用することで、レポートデータの精度を向上させます。
* **スクリーンビューをトラッキング**
  * アプリ／スクリーンのトラッキングを有効にします。
  * 有効にすると、最初のページビューの後に別のスクリーンビューリクエストが送信されます。
* **IP の匿名化**
  * IP アドレスを保存する前に最後のオクテットを削除することで、トラッカーオブジェクトから送信される情報を匿名化するよう Google Analytics に指示します。
  * 地域レポートの精度がわずかに低下します。
* **変数をクリア**
  * 各トラッキングリクエストの後に、通常はトラッカーの有効期間中にわたって構成される項目をクリアします。
* **Optimize コンテナ ID**
  * `optimize_id` を構成し、Google Optimize プラグインを有効にします。
  * この ID は、Optimize アカウントページで確認できます。
  * 例：**GTM-XXXXXX**
* **AMP クライアント ID を使用**
  * Google AMP クライアント ID を使用すると、AMP ページと非 AMP ページのコンテンツを利用するユーザーを一意に識別できます。
  * オプトインすると、ユーザーが Google AMP 閲覧者ーを通じて AMP ページにアクセスした際に、Google Analytics は AMP クライアント ID を使用して、複数のサイトイベントが同じユーザーによるものかどうかを判断します。
* **データレイヤー名**
  * デフォルトでは、グローバルサイトタグによって初期化および参照されるデータレイヤーの名前は `dataLayer` です。
  * プロジェクトで別の名前が必要な場合にのみ、データレイヤーの名前を変更してください。
* **アンカーを許可**
  * true の場合、`_ga` パラメータは URL のアンカー部分（"#"）ではなく、クエリ部分に追加されます。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは以下のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`tracking_id`|  <ul><li>トラッキング ID</li><li>データの送信先となる Google Analytics プロパティのトラッキング ID</li><li>例：`UA-XXXXXX-13`</li><li>複数のプロパティにデータを送信するには、カンマ区切りのリストを使用します。</li></ul> |
|`transport_type`|  <ul><li>トランスポートタイプ</li></ul> |
|`page_title`|  <ul><li>ページタイトル</li></ul> |
|`page_location`|  <ul><li>ページの場所</li></ul> |
| `page_path` |  <ul><li>ページパス</li></ul> |
|`cookie_name`|  <ul><li>Cookie 名</li></ul> |
| `cookie_domain` |  <ul><li>Cookie ドメイン</li></ul> |
| `cookie_expires` |  <ul><li>Cookie の有効期限</li></ul> |
|`cookie_prefix`|  <ul><li>Cookie プレフィックス</li></ul> |
|`cookie_update`|  <ul><li>Cookie の更新</li></ul> |
|`config.allow_google_signals`|  <ul><li>ブール値</li><li>広告機能を許可します。</li></ul> |
|`allow_ad_personalization_signals`|  <ul><li>ブール値</li><li>広告パーソナライズシグナルを許可します。</li><li>標準の Google Analytics 実装で収集されるデータに加えて、Google Ad Manager（DoubleClick）Cookie を通じてトラフィックに関するデータを Google Analytics が収集できるようにします。</li></ul> |
|`config.link_attribution.cookie_name`|  <ul><li>リンクアトリビューションの Cookie 名</li></ul> |
|`config.link_attribution.cookie_expires`|  <ul><li>リンクアトリビューション Cookie の有効期限</li></ul> |
|`config.link_attribution.levels`|  <ul><li>リンクアトリビューションのレベル</li></ul> |
|`config.campaign.id`|  <ul><li>キャンペーン ID</li></ul> |
|`config.campaign.name`|  <ul><li>キャンペーン名</li></ul> |
|`config.campaign.source`|  <ul><li>キャンペーンソース</li></ul> |
|`config.campaign.medium`|  <ul><li>キャンペーンメディア</li></ul> |
|`config.campaign.content`|  <ul><li>キャンペーンコンテンツ</li></ul> |
|`config.campaign.term`|  <ul><li>キャンペーンのキーワード</li></ul> |
|`config.anonymize_ip`|  <ul><li>ブール値</li><li>IP の匿名化</li><li>IP アドレスを保存する前に最後のオクテットを削除することで、トラッカーオブジェクトから送信される情報を匿名化するよう Google Analytics に指示します。</li><li>地域レポートの精度がわずかに低下します。</li></ul> |
|`clear_global_vars`|  <ul><li>ブール値</li><li>変数をクリア</li><li>各トラッキングリクエストの後に、通常はトラッカーの有効期間中にわたって構成される項目をクリアします。</li></ul> |
|`config.optimize_id`|  <ul><li>Optimize コンテナ ID</li><li>`optimize_id` を構成し、Google Optimize プラグインを有効にします。</li><li>この ID は、Optimize アカウントページで確認できます。</li><li>例：**GTM-XXXXXX**</li></ul> |
|`config.use_amp_client_id`|  <ul><li>ブール値</li><li>AMP クライアント ID を使用</li><li>Google AMP クライアント ID を使用すると、AMP ページと非 AMP ページのコンテンツを利用するユーザーを一意に識別できます。</li><li>オプトインすると、ユーザーが Google AMP 閲覧者ーを通じて AMP ページにアクセスした際に、Google Analytics は AMP クライアント ID を使用して、複数のサイトイベントが同じユーザーによるものかどうかを判断します。</li></ul> |
| `config.sample_rate` |  <ul><li>サンプルレート</li></ul> |
|`config.site_speed_sample_rate`|  <ul><li>サイト速度のサンプルレート</li></ul> |
|`customer_id`|  <ul><li>ユーザー ID</li><li>`_ccustid` を上書きします</li></ul> |
|`config.client_id`|  <ul><li>クライアント ID</li></ul> |
### イベント

|変数| 説明|
|---| ---|
| `event_name` |  <ul><li>イベントアクション</li></ul> |
| `event.event_category` |  <ul><li>イベントカテゴリ</li></ul> |
| `event.event_label` |  <ul><li>イベントラベル</li></ul> |
| `event.value` |  <ul><li>イベント／タイミング値</li></ul> |
| `event.name` |  <ul><li>タイミング変数名</li></ul> |
| `event.description` |  <ul><li>例外の説明</li></ul> |
| `event.non_interaction` |  <ul><li>非インタラクション</li></ul> |
|`event.fatal`|  <ul><li>ブール値</li><li>致命的エラー</li></ul> |
| `event.search_term` |  <ul><li>検索語句</li></ul> |
| `event.method` |  <ul><li>メソッド</li></ul> |
| `event.content_type` |  <ul><li>コンテンツタイプ</li></ul> |
| `event.content_id` |  <ul><li>コンテンツID</li></ul> |
| `event.destination` |  <ul><li>目的地</li></ul> |
|`event.start_date`|  <ul><li>開始日</li><li>日付形式はYYYYMMDDです。</li></ul> |
|`event.end_date`|  <ul><li>終了日</li><li>日付形式はYYYYMMDDです。</li></ul> |
| `event.custom` |  <ul><li>カスタムイベントデータ</li></ul> |
|`event.anonymize_ip`|  <ul><li>ブール値</li><li>IPの匿名化</li><li>保存前にIPアドレスの最後のオクテットを削除し、トラッカーオブジェクトから送信される情報を匿名化するようGoogle Analyticsに指示します。</li><li>地域レポートの精度がわずかに低下します。</li></ul> |
| `event.send_to` |  <ul><li>デフォルトルーティングの上書き</li></ul> |
| `event.event_callback` |  <ul><li>イベントコールバック</li></ul> |

### アプリ／スクリーンのトラッキング

|変数| 説明|
|---| ---|
|`screen_view`|  <ul><li>ブール値。</li><li>有効化に使用できる値: "true"、"on"</li><li>スクリーンビューをトラッキング</li><li>アプリ／スクリーンのトラッキングを有効にします。</li><li>有効にすると、最初のページビューの後に別個のスクリーンビューリクエストが送信されます。</li></ul> |
| `event.screen_name` |  <ul><li>スクリーン名</li></ul> |
| `config.app_name` |  <ul><li>アプリケーション名</li></ul> |
| `config.app_id` |  <ul><li>アプリケーションID</li></ul> |
| `config.app_version` |  <ul><li>アプリケーションのバージョン</li></ul> |
|`IDconfig.app_installer_id`|  <ul><li>アプリケーションのインストーラー</li></ul> |

### コンテンツグループ

|変数| 説明|
|---| ---|
|`content_group1`| コンテンツグループ1|
|`content_group2`| コンテンツグループ2|
|`content_group3`| コンテンツグループ4|
|`content_group4`| コンテンツグループ4|
|`content_group5`| コンテンツグループ5|

### ディメンション

|変数| 説明|
|---| ---|
|`dimension1`| ディメンション1|
|`dimension2`| ディメンション2|
|`dimension3`| ディメンション3|
|`dimension4`| ディメンション4|
|`dimension5`| ディメンション5|
|`dimension6`| ディメンション6|
|`dimension7`| ディメンション7|
|`dimension8`| ディメンション8|
|`dimension9`| ディメンション9|
|`dimension10`| ディメンション10|
|`dimension11`| ディメンション11|
|`dimension12`| ディメンション12|
|`dimension13`| ディメンション13|
|`dimension14`| ディメンション14|
|`dimension15`| ディメンション15|
|`dimension16`| ディメンション16|
|`dimension17`| ディメンション17|
|`dimension18`| ディメンション18|
|`dimension19`| ディメンション19|
|`dimension20`| ディメンション20|
|-- プレミアムディメンション--|
|`dimension21` - `dimension200`| ディメンション21からディメンション100まで|

### 指標

|変数| 説明|
|---| ---|
|`metric1`| 指標1|
|`metric2`| 指標2|
|`metric3`| 指標3|
|`metric4`| 指標4|
|`metric5`| 指標5|
|`metric6`| 指標6|
|`metric7`| 指標7|
|`metric8`| 指標8|
|`metric9`| 指標9|
|`metric10`| 指標10|
|`metric11`| 指標11|
|`metric12`| 指標12|
|`metric13`| 指標13|
|`metric14`| 指標14|
|`metric15`| 指標15|
|`metric16`| 指標16|
|`metric17`| 指標17|
|`metric18`| 指標18|
|`metric19`| 指標19|
|`metric20`| 指標20|
|-- プレミアム指標--|
|`metric21` - `metric200`| 指標21から指標200まで|

### 拡張eコマース

|変数| 説明|
|---| ---|
|`checkout_step`|  <ul><li>数値</li><li>チェックアウトのステップ。</li></ul> |
| `checkout_option` |  <ul><li>チェックアウトオプション。</li></ul> |
|`order_currency`|  <ul><li>通貨</li><li>`_ccurrency`を上書きします。</li></ul> |
|`order_id`|  <ul><li>トランザクションID</li><li>`_corder`を上書きします。</li></ul> |
|`order_total`|  <ul><li>値／注文合計</li><li>`_ctotal`を上書きします。</li></ul> |
| `order_shipping` |  <ul><li>送料</li><li>`_cship`を上書きします。</li></ul> |
|`order_tax`|  <ul><li>税額</li><li>`_ctax`を上書きします。</li></ul> |
|`order_store`|  <ul><li>提携先／店舗</li><li>`_cstore`を上書きします。</li></ul> |
| `order_coupon_code` |  <ul><li>プロモーションコード／クーポン</li><li>`_cpromo`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>ユーザーID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト</li><li>`Overrides _cprodname`。</li></ul> |
|`product_brand`|  <ul><li>配列</li><li>ブランドのリスト</li><li>`_cbrand`を上書きします。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリのリスト</li><li>`_ccat`を上書きします。</li></ul> |
|`product_variant`|  <ul><li>配列</li><li>バリエーションのリスト</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_discount`|  <ul><li>配列</li><li>割引のリスト</li><li>`_cdisc`を上書きします。</li></ul> |
|`product_promo_code`|  <ul><li>配列</li><li>プロモーションコード／クーポンのリスト</li></ul> |
|`product_action_list`|  <ul><li>配列</li><li>商品アクションリスト</li></ul> |
|`product_list_name`|  <ul><li>配列</li><li>商品名</li></ul> |
|`product_list_id`|  <ul><li>配列</li><li>商品リストID</li></ul> |
|`product_list_position`|  <ul><li>配列</li><li>商品の位置</li></ul> |
|`product_location_id`|  <ul><li>商品のロケーションID</li></ul> |

### 拡張eコマースのエンゲージメント

|変数| 説明|
|---| ---|
|`impression_id`|  <ul><li>配列</li><li>商品インプレッションID</li></ul> |
|`impression_name`|  <ul><li>配列</li><li>商品インプレッション名</li></ul> |
| `impression_category` |  <ul><li>配列</li><li>商品インプレッションカテゴリ</li></ul> |
|`impression_brand`|  <ul><li>配列</li><li>商品インプレッションブランド</li></ul> |
|`impression_variant`|  <ul><li>配列</li><li>商品インプレッションのバリエーション</li></ul> |
|`impression_price`|  <ul><li>配列</li><li>商品インプレッション価格</li></ul> |
|`impression_list_name`|  <ul><li>配列</li><li>商品インプレッションリスト</li></ul> |
|`impression_item_list_id`|  <ul><li>商品インプレッションリストID</li></ul> |
|`impression_list_position`|  <ul><li>配列</li><li>商品インプレッションの位置</li></ul> |
|```promo_id```|  <ul><li>配列</li><li>プロモーションID</li></ul> |
|`promo_name`|  <ul><li>配列</li><li>プロモーション名</li></ul> |
|`promo_creative_name`|  <ul><li>配列</li><li>プロモーションクリエイティブ</li></ul> |
| `promo_creative_slot` |  <ul><li>配列</li><li>プロモーションの位置</li></ul> |
| `promo_location_id` |  <ul><li>配列</li><li>プロモーションのロケーション</li></ul> |

### アプリ＋ウェブの旅行

|変数| 説明|
|---| ---|
|`event.trip_type`|  <ul><li>旅行タイプ</li></ul> |
|`start_date`|  <ul><li>配列</li><li>開始日</li></ul> |
|`end_date`|  <ul><li>配列</li><li>終了日</li></ul> |
|`origin`|  <ul><li>配列</li><li>出発地</li></ul> |
|`destination`|  <ul><li>配列</li><li>目的地</li></ul> |
|`flight_number`|  <ul><li>配列</li><li>便名</li></ul> |
|`travel_class`|  <ul><li>配列</li><li>搭乗クラス</li></ul> |
|`fare_product`|  <ul><li>配列</li><li>運賃商品</li></ul> |
|`booking_code`|  <ul><li>配列</li><li>予約コード</li></ul> |
|`event.passengers.total`|  <ul><li>乗客の合計人数</li></ul> |
|`event.passengers.adult`|  <ul><li>大人の乗客数</li></ul> |
|`event.passengers.child`|  <ul><li>子どもの乗客数</li></ul> |
|`event.passengers.infant_in_lap`|  <ul><li>膝上に乗せる乳幼児の乗客数</li></ul> |
|`event.passengers.infant_in_seat`|  <ul><li>座席を使用する乳幼児の乗客数</li></ul> |
### App+Web ゲーム

|変数|説明|
|---|---|
|`event.achievement_id`| <ul><li>実績 ID</li></ul> |
|`event.character`| <ul><li>キャラクター</li></ul> |
|`event.group_id`| <ul><li>グループ ID</li></ul> |
|`event.item_name`| <ul><li>アイテム名</li></ul> |
|`event.level`| <ul><li>レベル</li></ul> |
|`event.level_name`| <ul><li>レベル名</li></ul> |
|`event.score`| <ul><li>スコア</li></ul> |
|`event.success`| <ul><li>成功</li></ul> |
|`event.virtual_currency_name`| <ul><li>仮想通貨名</li></ul> |

### IAB Transparency and Consent Framework v2

|変数|説明|
|---|---|
|`gtag_enable_tcf_support`| <ul><li>TCF サポートを有効にする</li><li>値は **true** または **false** です。</li></ul> |

## Google Analytics 4 のサポート

現在、Google Analytics 4（GA4）は、このタグの App and Web マッピングを通じてサポートされています。