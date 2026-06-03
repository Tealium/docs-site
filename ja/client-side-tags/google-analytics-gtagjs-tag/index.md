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

タグマーケットプレイスに移動して新しいタグを追加します。タグを追加する一般的な手順については、[タグ概要]()の記事を読んでください。

タグを追加する際には、以下の構成を構成します：

* **トラッキングID**
  * データを送信したいGoogle AnalyticsプロパティのトラッキングID
  * 例：`UA-XXXXXX-13`
  * 複数のプロパティにデータを送信する場合は、カンマ区切りのリストを使用します。
[App &#43; Web](https://developers.google.com/analytics/devguides/collection/app-web/basic-tag)を有効にするには、トラッキングID値に測定IDを含めます。例：`UA-XXXXXX-13,G-XXXXXXXXXX`
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

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tracking_id`|  &lt;ul&gt;&lt;li&gt;トラッキングID&lt;/li&gt;&lt;li&gt;データを送信したいGoogle AnalyticsプロパティのトラッキングID&lt;/li&gt;&lt;li&gt;例：`UA-XXXXXX-13`&lt;/li&gt;&lt;li&gt;複数のプロパティにデータを送信する場合は、カンマ区切りのリストを使用します。&lt;/li&gt;&lt;/ul&gt; |
|`transport_type`|  &lt;ul&gt;&lt;li&gt;トランスポートタイプ&lt;/li&gt;&lt;/ul&gt; |
|`page_title`|  &lt;ul&gt;&lt;li&gt;ページタイトル&lt;/li&gt;&lt;/ul&gt; |
|`page_location`|  &lt;ul&gt;&lt;li&gt;ページ位置&lt;/li&gt;&lt;/ul&gt; |
| `page_path` |  &lt;ul&gt;&lt;li&gt;ページパス&lt;/li&gt;&lt;/ul&gt; |
|`cookie_name`|  &lt;ul&gt;&lt;li&gt;クッキー名&lt;/li&gt;&lt;/ul&gt; |
| `cookie_domain` |  &lt;ul&gt;&lt;li&gt;クッキードメイン&lt;/li&gt;&lt;/ul&gt; |
| `cookie_expires` |  &lt;ul&gt;&lt;li&gt;クッキーの有効期限&lt;/li&gt;&lt;/ul&gt; |
|`cookie_prefix`|  &lt;ul&gt;&lt;li&gt;クッキープレフィックス&lt;/li&gt;&lt;/ul&gt; |
|`cookie_update`|  &lt;ul&gt;&lt;li&gt;クッキー更新&lt;/li&gt;&lt;/ul&gt; |
|`config.allow_google_signals`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;広告機能を許可する。&lt;/li&gt;&lt;/ul&gt; |
|`allow_ad_personalization_signals`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;広告パーソナライゼーションシグナルを許可する。&lt;/li&gt;&lt;li&gt;Google Ad Manager（DoubleClick）クッキーを通じて、標準のGoogle Analytics実装を通じて収集されたデータに加えて、トラフィックに関するデータをGoogle Analyticsが収集することを可能にします。&lt;/li&gt;&lt;/ul&gt; |
|`config.link_attribution.cookie_name`|  &lt;ul&gt;&lt;li&gt;リンク属性クッキー名&lt;/li&gt;&lt;/ul&gt; |
|`config.link_attribution.cookie_expires`|  &lt;ul&gt;&lt;li&gt;リンク属性クッキーの有効期限&lt;/li&gt;&lt;/ul&gt; |
|`config.link_attribution.levels`|  &lt;ul&gt;&lt;li&gt;リンク属性レベル&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.id`|  &lt;ul&gt;&lt;li&gt;キャンペーンID&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.name`|  &lt;ul&gt;&lt;li&gt;キャンペーン名&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.source`|  &lt;ul&gt;&lt;li&gt;キャンペーンソース&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.medium`|  &lt;ul&gt;&lt;li&gt;キャンペーンメディア&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.content`|  &lt;ul&gt;&lt;li&gt;キャンペーンコンテンツ&lt;/li&gt;&lt;/ul&gt; |
|`config.campaign.term`|  &lt;ul&gt;&lt;li&gt;キャンペーン用語/キーワード&lt;/li&gt;&lt;/ul&gt; |
|`config.anonymize_ip`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;IPの匿名化&lt;/li&gt;&lt;li&gt;Google Analyticsにトラッカーオブジェクトによって送信される情報を匿名化するよう指示します。これは、IPアドレスの最後のオクテットを保存に保存する前に削除することによって行われます。&lt;/li&gt;&lt;li&gt;地理的レポートの精度がわずかに低下します。&lt;/li&gt;&lt;/ul&gt; |
|`clear_global_vars`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;クリアバーズ&lt;/li&gt;&lt;li&gt;各トラッキングリクエスト後にトラッカーの寿命に構成された項目をクリアします。&lt;/li&gt;&lt;/ul&gt; |
|`config.optimize_id`|  &lt;ul&gt;&lt;li&gt;オプティマイズコンテナID&lt;/li&gt;&lt;li&gt;`optimize_id`を構成し、Google Optimizeプラグインを有効にします。&lt;/li&gt;&lt;li&gt;このIDはOptimizeアカウントページで見つかります。&lt;/li&gt;&lt;li&gt;例：**GTM-XXXXXX**&lt;/li&gt;&lt;/ul&gt; |
|`config.use_amp_client_id`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;AMPクライアントIDの使用&lt;/li&gt;&lt;li&gt;Google AMPクライアントIDを使用して、AMPおよび非AMPページでコンテンツに関与するユーザーを一意に識別します。&lt;/li&gt;&lt;li&gt;オプトインすると、Google AnalyticsはAMPクライアントIDを使用して、そのユーザーがGoogle AMP閲覧者を介してAMPページを訪れる際に、複数のサイトイベントが同じユーザーに属することを判断します。&lt;/li&gt;&lt;/ul&gt; |
| `config.sample_rate` |  &lt;ul&gt;&lt;li&gt;サンプルレート&lt;/li&gt;&lt;/ul&gt; |
|`config.site_speed_sample_rate`|  &lt;ul&gt;&lt;li&gt;サイトスピードサンプルレート&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;ユーザーID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書きします&lt;/li&gt;&lt;/ul&gt; |
|`config.client_id`|  &lt;ul&gt;&lt;li&gt;クライアントID&lt;/li&gt;&lt;/ul&gt; |


### イベント

|変数| 説明|
|---| ---|
| `event_name` |  &lt;ul&gt;&lt;li&gt;イベントアクション&lt;/li&gt;&lt;/ul&gt; |
| `event.event_category` |  &lt;ul&gt;&lt;li&gt;イベントカテゴリ&lt;/li&gt;&lt;/ul&gt; |
| `event.event_label` |  &lt;ul&gt;&lt;li&gt;イベントラベル&lt;/li&gt;&lt;/ul&gt; |
| `event.value` |  &lt;ul&gt;&lt;li&gt;イベント/タイミング値&lt;/li&gt;&lt;/ul&gt; |
| `event.name` |  &lt;ul&gt;&lt;li&gt;タイミング変数名&lt;/li&gt;&lt;/ul&gt; |
| `event.description` |  &lt;ul&gt;&lt;li&gt;例外説明&lt;/li&gt;&lt;/ul&gt; |
| `event.non_interaction` |  &lt;ul&gt;&lt;li&gt;非インタラクション&lt;/li&gt;&lt;/ul&gt; |
|`event.fatal`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;致命的エラー&lt;/li&gt;&lt;/ul&gt; |
| `event.search_term` |  &lt;ul&gt;&lt;li&gt;検索語&lt;/li&gt;&lt;/ul&gt; |
| `event.method` |  &lt;ul&gt;&lt;li&gt;メソッド&lt;/li&gt;&lt;/ul&gt; |
| `event.content_type` |  &lt;ul&gt;&lt;li&gt;コンテンツタイプ&lt;/li&gt;&lt;/ul&gt; |
| `event.content_id` |  &lt;ul&gt;&lt;li&gt;コンテンツID&lt;/li&gt;&lt;/ul&gt; |
| `event.destination` |  &lt;ul&gt;&lt;li&gt;目的地&lt;/li&gt;&lt;/ul&gt; |
|`event.start_date`|  &lt;ul&gt;&lt;li&gt;開始日&lt;/li&gt;&lt;li&gt;日付形式はYYYYMMDDです。&lt;/li&gt;&lt;/ul&gt; |
|`event.end_date`|  &lt;ul&gt;&lt;li&gt;終了日&lt;/li&gt;&lt;li&gt;日付形式はYYYYMMDDです。&lt;/li&gt;&lt;/ul&gt; |
| `event.custom` |  &lt;ul&gt;&lt;li&gt;カスタムイベントデータ&lt;/li&gt;&lt;/ul&gt; |
|`event.anonymize_ip`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;IP匿名化&lt;/li&gt;&lt;li&gt;トラッカーオブジェクトによって送信される情報からIPアドレスの最後のオクテットを削除することでGoogle Analyticsに匿名化を指示します。&lt;/li&gt;&lt;li&gt;地理的レポートの精度がわずかに低下します。&lt;/li&gt;&lt;/ul&gt; |
| `event.send_to` |  &lt;ul&gt;&lt;li&gt;デフォルトルーティングの上書き&lt;/li&gt;&lt;/ul&gt; |
| `event.event_callback` |  &lt;ul&gt;&lt;li&gt;イベントコールバック&lt;/li&gt;&lt;/ul&gt; |

### アプリ/スクリーントラッキング

|変数| 説明|
|---| ---|
|`screen_view`|  &lt;ul&gt;&lt;li&gt;ブール値。&lt;/li&gt;&lt;li&gt;有効化に受け入れられる値: &#34;true&#34;, &#34;on&#34;&lt;/li&gt;&lt;li&gt;スクリーンビューの追跡&lt;/li&gt;&lt;li&gt;アプリ/スクリーン追跡を有効にします。&lt;/li&gt;&lt;li&gt;有効にすると、初期ページビューの後に別のスクリーンビューリクエストが送信されます。&lt;/li&gt;&lt;/ul&gt; |
| `event.screen_name` |  &lt;ul&gt;&lt;li&gt;スクリーン名&lt;/li&gt;&lt;/ul&gt; |
| `config.app_name` |  &lt;ul&gt;&lt;li&gt;アプリケーション名&lt;/li&gt;&lt;/ul&gt; |
| `config.app_id` |  &lt;ul&gt;&lt;li&gt;アプリケーションID&lt;/li&gt;&lt;/ul&gt; |
| `config.app_version` |  &lt;ul&gt;&lt;li&gt;アプリケーションバージョン&lt;/li&gt;&lt;/ul&gt; |
|`IDconfig.app_installer_id`|  &lt;ul&gt;&lt;li&gt;アプリケーションインストーラ&lt;/li&gt;&lt;/ul&gt; |

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
|`checkout_step`|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;li&gt;チェックアウトステップ。&lt;/li&gt;&lt;/ul&gt; |
| `checkout_option` |  &lt;ul&gt;&lt;li&gt;チェックアウトオプション。&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;通貨&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_id`|  &lt;ul&gt;&lt;li&gt;トランザクションID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;値/注文合計&lt;/li&gt;&lt;li&gt;`_ctotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `order_shipping` |  &lt;ul&gt;&lt;li&gt;送料金額&lt;/li&gt;&lt;li&gt;`_cship`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;税金額&lt;/li&gt;&lt;li&gt;`_ctax`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_store`|  &lt;ul&gt;&lt;li&gt;提携/店舗&lt;/li&gt;&lt;li&gt;`_cstore`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `order_coupon_code` |  &lt;ul&gt;&lt;li&gt;プロモーションコード/クーポン&lt;/li&gt;&lt;li&gt;`_cpromo`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;ユーザーID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;IDのリスト&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前のリスト&lt;/li&gt;&lt;li&gt;`_cprodname`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;ブランドのリスト&lt;/li&gt;&lt;li&gt;`_cbrand`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリのリスト&lt;/li&gt;&lt;li&gt;`_ccat`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_variant`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;バリアントのリスト&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_discount`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;割引のリスト&lt;/li&gt;&lt;li&gt;`_cdisc`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_promo_code`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーションコード/クーポンのリスト&lt;/li&gt;&lt;/ul&gt; |
|`product_action_list`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品アクションリスト&lt;/li&gt;&lt;/ul&gt; |
|`product_list_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品名&lt;/li&gt;&lt;/ul&gt; |
|`product_list_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品リストID&lt;/li&gt;&lt;/ul&gt; |
|`product_list_position`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品位置&lt;/li&gt;&lt;/ul&gt; |
|`product_location_id`|  &lt;ul&gt;&lt;li&gt;製品位置ID&lt;/li&gt;&lt;/ul&gt; |

### エンリッチメントEコマースエンゲージメント

|変数| 説明|
|---| ---|
|`impression_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品印象ID&lt;/li&gt;&lt;/ul&gt; |
|`impression_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品印象名&lt;/li&gt;&lt;/ul&gt; |
| `impression_category` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品印象カテゴリ&lt;/li&gt;&lt;/ul&gt; |
|`impression_brand`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品印象ブランド&lt;/li&gt;&lt;/ul&gt; |
|`impression_variant`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品印象バリアント&lt;/li&gt;&lt;/ul&gt; |
|`impression_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品印象価格&lt;/li&gt;&lt;/ul&gt; |
|`impression_list_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品印象リスト&lt;/li&gt;&lt;/ul&gt; |
|`impression_item_list_id`|  &lt;ul&gt;&lt;li&gt;製品印象リストID&lt;/li&gt;&lt;/ul&gt; |
|`impression_list_position`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品印象位置&lt;/li&gt;&lt;/ul&gt; |
|```promo_id```|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーションID&lt;/li&gt;&lt;/ul&gt; |
|`promo_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーション名&lt;/li&gt;&lt;/ul&gt; |
|`promo_creative_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーションクリエイティブ&lt;/li&gt;&lt;/ul&gt; |
| `promo_creative_slot` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーション位置&lt;/li&gt;&lt;/ul&gt; |
| `promo_location_id` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーション位置&lt;/li&gt;&lt;/ul&gt; |

### アプリ&#43;ウェブ旅行

|変数| 説明|
|---| ---|
|`event.trip_type`|  &lt;ul&gt;&lt;li&gt;旅行タイプ&lt;/li&gt;&lt;/ul&gt; |
|`start_date`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;開始日&lt;/li&gt;&lt;/ul&gt; |
|`end_date`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;終了日&lt;/li&gt;&lt;/ul&gt; |
|`origin`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;出発地&lt;/li&gt;&lt;/ul&gt; |
|`destination`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;目的地&lt;/li&gt;&lt;/ul&gt; |
|`flight_number`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;フライト番号&lt;/li&gt;&lt;/ul&gt; |
|`travel_class`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;旅行クラス&lt;/li&gt;&lt;/ul&gt; |
|`fare_product`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;運賃商品&lt;/li&gt;&lt;/ul&gt; |
|`booking_code`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;予約コード&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.total`|  &lt;ul&gt;&lt;li&gt;総乗客数&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.adult`|  &lt;ul&gt;&lt;li&gt;大人の乗客数&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.child`|  &lt;ul&gt;&lt;li&gt;子供の乗客数&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.infant_in_lap`|  &lt;ul&gt;&lt;li&gt;膝の上の乳児の乗客数&lt;/li&gt;&lt;/ul&gt; |
|`event.passengers.infant_in_seat`|  &lt;ul&gt;&lt;li&gt;座席の乳児の乗客数&lt;/li&gt;&lt;/ul&gt; |
### App&#43;Web ゲーム

|変数| 説明|
|---| ---|
|`event.achievement_id`|  &lt;ul&gt;&lt;li&gt;実績ID&lt;/li&gt;&lt;/ul&gt; |
|`event.character`|  &lt;ul&gt;&lt;li&gt;キャラクター&lt;/li&gt;&lt;/ul&gt; |
|`event.group_id`|  &lt;ul&gt;&lt;li&gt;グループID&lt;/li&gt;&lt;/ul&gt; |
|`event.item_name`|  &lt;ul&gt;&lt;li&gt;アイテム名&lt;/li&gt;&lt;/ul&gt; |
|`event.level`|  &lt;ul&gt;&lt;li&gt;レベル&lt;/li&gt;&lt;/ul&gt; |
|`event.level_name`|  &lt;ul&gt;&lt;li&gt;レベル名&lt;/li&gt;&lt;/ul&gt; |
|`event.score`|  &lt;ul&gt;&lt;li&gt;スコア&lt;/li&gt;&lt;/ul&gt; |
|`event.success`|  &lt;ul&gt;&lt;li&gt;成功&lt;/li&gt;&lt;/ul&gt; |
|`event.virtual_currency_name`|  &lt;ul&gt;&lt;li&gt;仮想通貨名&lt;/li&gt;&lt;/ul&gt; |

### IAB 透明性と同意フレームワーク v2

|変数| 説明|
|---| ---|
|`gtag_enable_tcf_support`|  &lt;ul&gt;&lt;li&gt;TCF サポートを有効にする&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |

## Google Analytics 4 のサポート

Google Analytics 4 (GA4) は、このタグの App と Web のマッピングを通じて現在サポートされています。

