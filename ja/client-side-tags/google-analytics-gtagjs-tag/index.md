---
title: Google Analytics (gtag.js) タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Google Analytics (gtag.js) タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-analytics-gtagjs-tag/
---
Google Analyticsは、オンラインコンテンツとのユーザーインタラクションを収集、構成、報告するためのAPIを提供します。gtag.jsを使用することで、最新のトラッキング機能や統合が利用可能になると同時に、それらを利用することができます。

## タグのヒント

* マッピングを使用して：
  * Eコマース拡張値を動的に上書きします。
  * イベントトリガーを構成します。
  * カスタムメトリクス、ディメンション、コンテンツグループを追加します。
* カスタムイベント変数の `cst` を、使用したいイベント名に置き換えます。
* 次のEコマース拡張値をサポートします：
  * 注文ID
  * 注文合計
  * 配送料
  * 税額
  * 店舗
  * プロモーションコード
  * 顧客ID
  * 製品IDリスト
  * 名前リスト
  * ブランドリスト
  * カテゴリリスト
  * 価格リスト
  * 数量リスト
  * 割引リスト

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグを追加する一般的な手順については、[タグ概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を構成します：

* **トラッキングID**
  * データを送信したいGoogle AnalyticsプロパティのトラッキングID
  * 例：`UA-XXXXXX-13`
  * 複数のプロパティにデータを送信する場合は、カンマ区切りのリストを使用します。

<blockquote>
[App + Web](https://developers.google.com/analytics/devguides/collection/app-web/basic-tag)を有効にするには、トラッキングID値に測定IDを含めます。例：`UA-XXXXXX-13,G-XXXXXXXXXX`
</blockquote>

* **グローバルオブジェクト**
  * イベントキューに使用されるグローバルオブジェクトの名前。
  * 指定されていない場合は「gtag」が使用されます。
  * ほとんどの実装では必要ありません。
* **クロストラッキングドメイン**
  * クロスドメイントラッキングに使用するドメインのカンマ区切りリスト（`setAllowLinker`）。
  * このリストを使用するには、クロスドメイントラッキングを**true**に構成する必要があります。
  * トップレベルドメイン、例えば**tealiumiq.com**であるべきです。
* **クロスドメイントラッキング**
  * `setAllowLinker`の値を構成し、クロスドメイントラッキングプラグインを有効にします。
  * この機能を使用するには、「クロストラッキングドメイン」フィールドに1つ以上のドメインを指定するか、`crossDomainTrack`にマッピングする必要があります。
* **トランスポートタイプ**
  * ヒットが送信されるトランスポートメカニズムを指定します。
* **広告機能を許可する**
  * Google Ad Manager（DoubleClick）クッキーを通じて、標準のGoogle Analytics実装を通じて収集されたデータに加えて、トラフィックに関するデータをGoogle Analyticsが収集することを可能にします。
  * これを**オフ**に構成すると、すべての広告、レポート、リマーケティング機能が無効になり、Google Analyticsユーザーインターフェースで構成されたプロパティ構成が上書きされます。
* **リンク属性のエンリッチメント**
  * 確信が持てない場合は、デフォルト値（**false**）を使用します。
  * Google Analyticsは、リンク属性のエンリッチメントを提供して、単一ページ上の同じURLへの複数のリンクを自動的に区別し、リンク要素IDを使用してレポートデータの精度を向上させます。
* **スクリーンビューのトラッキング**
  * アプリ/スクリーンのトラッキングを有効にします。
  * 有効にすると、初期ページビューの後に別のスクリーンビューリクエストが送信されます。
* **IPの匿名化**
  * Google Analyticsにトラッカーオブジェクトによって送信される情報を匿名化するよう指示します。これは、IPアドレスの最後のオクテットを保存に保存する前に削除することによって行われます。
  * 地理的レポートの精度がわずかに低下します。
* **クリアバーズ**
  * 各トラッキングリクエスト後にトラッカーの寿命に構成された項目をクリアします。
* **オプティマイズコンテナID**
  * `optimize_id`を構成し、Google Optimizeプラグインを有効にします。
  * このIDはOptimizeアカウントページで見つかります。
  * 例：**GTM-XXXXXX**
* **AMPクライアントIDの使用**
  * Google AMPクライアントIDを使用して、AMPおよび非AMPページでコンテンツに関与するユーザーを一意に識別します。
  * オプトインすると、Google AnalyticsはAMPクライアントIDを使用して、そのユーザーがGoogle AMP閲覧者を介してAMPページを訪れる際に、複数のサイトイベントが同じユーザーに属することを判断します。
* **データレイヤー名**
  * デフォルトでは、グローバルサイトタグによって初期化および参照されるデータレイヤーは `dataLayer` という名前です。
  * プロジェクトが別の名前を必要とする場合のみ、データレイヤーの名前を変更します。
* **アンカーを許可する**
  * trueの場合、`_ga`パラメータはURLのアンカー部分（「#」）ではなく、クエリ部分に追加されます。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tracking_id`|  <ul><li>トラッキングID</li><li>データを送信したいGoogle AnalyticsプロパティのトラッキングID</li><li>例：`UA-XXXXXX-13`</li><li>複数のプロパティにデータを送信する場合は、カンマ区切りのリストを使用します。</li></ul> |
|`transport_type`|  <ul><li>トランスポートタイプ</li></ul> |
|`page_title`|  <ul><li>ページタイトル</li></ul> |
|`page_location`|  <ul><li>ページ位置</li></ul> |
| `page_path` |  <ul><li>ページパス</li></ul> |
|`cookie_name`|  <ul><li>クッキー名</li></ul> |
| `cookie_domain` |  <ul><li>クッキードメイン</li></ul> |
| `cookie_expires` |  <ul><li>クッキーの有効期限</li></ul> |
|`cookie_prefix`|  <ul><li>クッキープレフィックス</li></ul> |
|`cookie_update`|  <ul><li>クッキー更新</li></ul> |
|`config.allow_google_signals`|  <ul><li>ブール値</li><li>広告機能を許可する。</li></ul> |
|`allow_ad_personalization_signals`|  <ul><li>ブール値</li><li>広告パーソナライゼーションシグナルを許可する。</li><li>Google Ad Manager（DoubleClick）クッキーを通じて、標準のGoogle Analytics実装を通じて収集されたデータに加えて、トラフィックに関するデータをGoogle Analyticsが収集することを可能にします。</li></ul> |
|`config.link_attribution.cookie_name`|  <ul><li>リンク属性クッキー名</li></ul> |
|`config.link_attribution.cookie_expires`|  <ul><li>リンク属性クッキーの有効期限</li></ul> |
|`config.link_attribution.levels`|  <ul><li>リンク属性レベル</li></ul> |
|`config.campaign.id`|  <ul><li>キャンペーンID</li></ul> |
|`config.campaign.name`|  <ul><li>キャンペーン名</li></ul> |
|`config.campaign.source`|  <ul><li>キャンペーンソース</li></ul> |
|`config.campaign.medium`|  <ul><li>キャンペーンメディア</li></ul> |
|`config.campaign.content`|  <ul><li>キャンペーンコンテンツ</li></ul> |
|`config.campaign.term`|  <ul><li>キャンペーン用語/キーワード</li></ul> |
|`config.anonymize_ip`|  <ul><li>ブール値</li><li>IPの匿名化</li><li>Google Analyticsにトラッカーオブジェクトによって送信される情報を匿名化するよう指示します。これは、IPアドレスの最後のオクテットを保存に保存する前に削除することによって行われます。</li><li>地理的レポートの精度がわずかに低下します。</li></ul> |
|`clear_global_vars`|  <ul><li>ブール値</li><li>クリアバーズ</li><li>各トラッキングリクエスト後にトラッカーの寿命に構成された項目をクリアします。</li></ul> |
|`config.optimize_id`|  <ul><li>オプティマイズコンテナID</li><li>`optimize_id`を構成し、Google Optimizeプラグインを有効にします。</li><li>このIDはOptimizeアカウントページで見つかります。</li><li>例：**GTM-XXXXXX**</li></ul> |
|`config.use_amp_client_id`|  <ul><li>ブール値</li><li>AMPクライアントIDの使用</li><li>Google AMPクライアントIDを使用して、AMPおよび非AMPページでコンテンツに関与するユーザーを一意に識別します。</li><li>オプトインすると、Google AnalyticsはAMPクライアントIDを使用して、そのユーザーがGoogle AMP閲覧者を介してAMPページを訪れる際に、複数のサイトイベントが同じユーザーに属することを判断します。</li></ul> |
| `config.sample_rate` |  <ul><li>サンプルレート</li></ul> |
|`config.site_speed_sample_rate`|  <ul><li>サイトスピードサンプルレート</li></ul> |
|`customer_id`|  <ul><li>ユーザーID</li><li>`_ccustid`を上書きします</li></ul> |
|`config.client_id`|  <ul><li>クライアントID</li></ul> |


### イベント

|変数| 説明|
|---| ---|
| `event_name` |  <ul><li>イベントアクション</li></ul> |
| `event.event_category` |  <ul><li>イベントカテゴリ</li></ul> |
| `event.event_label` |  <ul><li>イベントラベル</li></ul> |
| `event.value` |  <ul><li>イベント/タイミング値</li></ul> |
| `event.name` |  <ul><li>タイミング変数名</li></ul> |
| `event.description` |  <ul><li>例外説明</li></ul> |
| `event.non_interaction` |  <ul><li>非インタラクション</li></ul> |
|`event.fatal`|  <ul><li>ブール値</li><li>致命的エラー</li></ul> |
| `event.search_term` |  <ul><li>検索語</li></ul> |
| `event.method` |  <ul><li>メソッド</li></ul> |
| `event.content_type` |  <ul><li>コンテンツタイプ</li></ul> |
| `event.content_id` |  <ul><li>コンテンツID</li></ul> |
| `event.destination` |  <ul><li>目的地</li></ul> |
|`event.start_date`|  <ul><li>開始日</li><li>日付形式はYYYYMMDDです。</li></ul> |
|`event.end_date`|  <ul><li>終了日</li><li>日付形式はYYYYMMDDです。</li></ul> |
| `event.custom` |  <ul><li>カスタムイベントデータ</li></ul> |
|`event.anonymize_ip`|  <ul><li>ブール値</li><li>IP匿名化</li><li>トラッカーオブジェクトによって送信される情報からIPアドレスの最後のオクテットを削除することでGoogle Analyticsに匿名化を指示します。</li><li>地理的レポートの精度がわずかに低下します。</li></ul> |
| `event.send_to` |  <ul><li>デフォルトルーティングの上書き</li></ul> |
| `event.event_callback` |  <ul><li>イベントコールバック</li></ul> |

### アプリ/スクリーントラッキング

|変数| 説明|
|---| ---|
|`screen_view`|  <ul><li>ブール値。</li><li>有効化に受け入れられる値: "true", "on"</li><li>スクリーンビューの追跡</li><li>アプリ/スクリーン追跡を有効にします。</li><li>有効にすると、初期ページビューの後に別のスクリーンビューリクエストが送信されます。</li></ul> |
| `event.screen_name` |  <ul><li>スクリーン名</li></ul> |
| `config.app_name` |  <ul><li>アプリケーション名</li></ul> |
| `config.app_id` |  <ul><li>アプリケーションID</li></ul> |
| `config.app_version` |  <ul><li>アプリケーションバージョン</li></ul> |
|`IDconfig.app_installer_id`|  <ul><li>アプリケーションインストーラ</li></ul> |

### コンテンツグループ

|変数| 説明|
|---| ---|
|`content_group1`| コンテンツグループ1|
|`content_group2`| コンテンツグループ2|
|`content_group3`| コンテンツグループ3|
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
|`dimension21` - `dimension200`| ディメンション21からディメンション200まで|

### メトリック

|変数| 説明|
|---| ---|
|`metric1`| メトリック1|
|`metric2`| メトリック2|
|`metric3`| メトリック3|
|`metric4`| メトリック4|
|`metric5`| メトリック5|
|`metric6`| メトリック6|
|`metric7`| メトリック7|
|`metric8`| メトリック8|
|`metric9`| メトリック9|
|`metric10`| メトリック10|
|`metric11`| メトリック11|
|`metric12`| メトリック12|
|`metric13`| メトリック13|
|`metric14`| メトリック14|
|`metric15`| メトリック15|
|`metric16`| メトリック16|
|`metric17`| メトリック17|
|`metric18`| メトリック18|
|`metric19`| メトリック19|
|`metric20`| メトリック20|
|-- プレミアムメトリック--|
|`metric21` - `metric200`| メトリック21からメトリック200まで|

### エンリッチメントEコマース

|変数| 説明|
|---| ---|
|`checkout_step`|  <ul><li>数値</li><li>チェックアウトステップ。</li></ul> |
| `checkout_option` |  <ul><li>チェックアウトオプション。</li></ul> |
|`order_currency`|  <ul><li>通貨</li><li>`_ccurrency`を上書きします。</li></ul> |
|`order_id`|  <ul><li>トランザクションID</li><li>`_corder`を上書きします。</li></ul> |
|`order_total`|  <ul><li>値/注文合計</li><li>`_ctotal`を上書きします。</li></ul> |
| `order_shipping` |  <ul><li>送料金額</li><li>`_cship`を上書きします。</li></ul> |
|`order_tax`|  <ul><li>税金額</li><li>`_ctax`を上書きします。</li></ul> |
|`order_store`|  <ul><li>提携/店舗</li><li>`_cstore`を上書きします。</li></ul> |
| `order_coupon_code` |  <ul><li>プロモーションコード/クーポン</li><li>`_cpromo`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>ユーザーID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト</li><li>`_cprodname`を上書きします。</li></ul> |
|`product_brand`|  <ul><li>配列</li><li>ブランドのリスト</li><li>`_cbrand`を上書きします。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリのリスト</li><li>`_ccat`を上書きします。</li></ul> |
|`product_variant`|  <ul><li>配列</li><li>バリアントのリスト</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_discount`|  <ul><li>配列</li><li>割引のリスト</li><li>`_cdisc`を上書きします。</li></ul> |
|`product_promo_code`|  <ul><li>配列</li><li>プロモーションコード/クーポンのリスト</li></ul> |
|`product_action_list`|  <ul><li>配列</li><li>製品アクションリスト</li></ul> |
|`product_list_name`|  <ul><li>配列</li><li>製品名</li></ul> |
|`product_list_id`|  <ul><li>配列</li><li>製品リストID</li></ul> |
|`product_list_position`|  <ul><li>配列</li><li>製品位置</li></ul> |
|`product_location_id`|  <ul><li>製品位置ID</li></ul> |

### エンリッチメントEコマースエンゲージメント

|変数| 説明|
|---| ---|
|`impression_id`|  <ul><li>配列</li><li>製品印象ID</li></ul> |
|`impression_name`|  <ul><li>配列</li><li>製品印象名</li></ul> |
| `impression_category` |  <ul><li>配列</li><li>製品印象カテゴリ</li></ul> |
|`impression_brand`|  <ul><li>配列</li><li>製品印象ブランド</li></ul> |
|`impression_variant`|  <ul><li>配列</li><li>製品印象バリアント</li></ul> |
|`impression_price`|  <ul><li>配列</li><li>製品印象価格</li></ul> |
|`impression_list_name`|  <ul><li>配列</li><li>製品印象リスト</li></ul> |
|`impression_item_list_id`|  <ul><li>製品印象リストID</li></ul> |
|`impression_list_position`|  <ul><li>配列</li><li>製品印象位置</li></ul> |
|```promo_id```|  <ul><li>配列</li><li>プロモーションID</li></ul> |
|`promo_name`|  <ul><li>配列</li><li>プロモーション名</li></ul> |
|`promo_creative_name`|  <ul><li>配列</li><li>プロモーションクリエイティブ</li></ul> |
| `promo_creative_slot` |  <ul><li>配列</li><li>プロモーション位置</li></ul> |
| `promo_location_id` |  <ul><li>配列</li><li>プロモーション位置</li></ul> |

### アプリ+ウェブ旅行

|変数| 説明|
|---| ---|
|`event.trip_type`|  <ul><li>旅行タイプ</li></ul> |
|`start_date`|  <ul><li>配列</li><li>開始日</li></ul> |
|`end_date`|  <ul><li>配列</li><li>終了日</li></ul> |
|`origin`|  <ul><li>配列</li><li>出発地</li></ul> |
|`destination`|  <ul><li>配列</li><li>目的地</li></ul> |
|`flight_number`|  <ul><li>配列</li><li>フライト番号</li></ul> |
|`travel_class`|  <ul><li>配列</li><li>旅行クラス</li></ul> |
|`fare_product`|  <ul><li>配列</li><li>運賃商品</li></ul> |
|`booking_code`|  <ul><li>配列</li><li>予約コード</li></ul> |
|`event.passengers.total`|  <ul><li>総乗客数</li></ul> |
|`event.passengers.adult`|  <ul><li>大人の乗客数</li></ul> |
|`event.passengers.child`|  <ul><li>子供の乗客数</li></ul> |
|`event.passengers.infant_in_lap`|  <ul><li>膝の上の乳児の乗客数</li></ul> |
|`event.passengers.infant_in_seat`|  <ul><li>座席の乳児の乗客数</li></ul> |
### App+Web ゲーム

|変数| 説明|
|---| ---|
|`event.achievement_id`|  <ul><li>実績ID</li></ul> |
|`event.character`|  <ul><li>キャラクター</li></ul> |
|`event.group_id`|  <ul><li>グループID</li></ul> |
|`event.item_name`|  <ul><li>アイテム名</li></ul> |
|`event.level`|  <ul><li>レベル</li></ul> |
|`event.level_name`|  <ul><li>レベル名</li></ul> |
|`event.score`|  <ul><li>スコア</li></ul> |
|`event.success`|  <ul><li>成功</li></ul> |
|`event.virtual_currency_name`|  <ul><li>仮想通貨名</li></ul> |

### IAB 透明性と同意フレームワーク v2

|変数| 説明|
|---| ---|
|`gtag_enable_tcf_support`|  <ul><li>TCF サポートを有効にする</li><li>値は **true** または **false**。</li></ul> |

## Google Analytics 4 のサポート

Google Analytics 4 (GA4) は、このタグの App と Web のマッピングを通じて現在サポートされています。

