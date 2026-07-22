---
title: Google Universal Analytics (analytics.js) タグ構成ガイド
description: この記事では、iQタグ管理アカウントでGoogle Universal Analyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-analyticsjs-tag/
---

<blockquote>
2023年7月1日以降、Google Universal Analyticsのプロパティはヒットの処理を停止しました。このタグは廃止され、タグマーケットプレイスではもう利用できません。現在のタグについては、[Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/)をご覧ください。
</blockquote>


Google Analytics (analytics.js)は、Google Analyticsアカウントでデータが収集・整理される方法を変える一連の機能を導入します。

## タグのヒント

* Google Analytics (analytics.js)についての詳細は、[About Universal Analytics](http://support.google.com/analytics/bin/answer.py?hl=en&answer=2790010&topic=2790009)をご覧ください。
* このタグのTealium実装を使用する場合は、Google API関数の代わりにマッピングを使用してください。
* ディスプレイ広告のサポート情報については、[About Advertising Features](http://support.google.com/analytics/answer/3450482)をご覧ください。
* 自動生成されたトラッカー名は、定義されたアカウント数に対して`tealium_X`の形式を取ります。

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[Tag Overview](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **タイトル**
  * 必須。
  * タグインスタンスを識別するための記述的なタイトルを入力します。
* **トラッキングID**
  * 必須。
  * Google Universal Analytics (GUA)アカウントのトラッキングIDを入力します。
  * Google Analyticsで追跡する各プロパティには、一意のプロパティトラッキングIDがあります。
  * 例：**UA-12345678-1**
  * 複数のプロパティにデータを送信するためには、カンマ区切りのリストを使用します。
* **トラッカー名**
  * 任意。
  * 複数のトラッカーを持っている、または持つ予定がある場合にこの構成を使用します。
  * データを送信したい各アカウントIDまたはGUAプロパティには、関連するトラッカー名が必要です。
  * このタグのコピーがページごとに複数存在する場合は必須です。
  * 複数のトラッカー名（複数のアカウント追跡用）には、カンマ区切りのリストを使用します。これは、上記のトラッキングIDのリストと同じ長さであるべきです。
  * トラッカー名ではダッシュ(-)はサポートされていません。
* **ドメイン**
  * 任意。
  * 特定のドメインのみでの追跡を許可するためにこの値を構成します。
  * サイトのドメイン名を入力します。
  * Google Analyticsにドメインを自動検出させるためには、このフィールドを空白にします。
  * この構成は、GUAがサイト訪問を識別するために使用するクッキーのドメインを構成します。
  * 共有サブドメイン間での追跡を有効にする場合は、ドメインの'www.'プレフィックスを省略します。例えば、[www.tealium.com](http://www.tealium.com)は**tealium.com**になります。特定のサブドメインを個別に追跡したい場合は、ドメインアドレス全体を入力します。例：`www.tealium.com`。
* **グローバルオブジェクト**
  * ほとんどの実装では必要ありません。
  * イベントキューに使用されるグローバルオブジェクトの名前。
  * 指定されていない場合は"**ga**"が使用されます。
* **クロスドメイン追跡**
  * 任意。
  * クロスドメイン追跡を有効にするには**true**に構成する必要があります。
  * クロスドメイン追跡（setAllowLinker）で使用するドメインのカンマ区切りのリスト。
  * トップレベルドメインの"tealiumiq.com"ではなく、完全修飾ドメイン名、例えば"my.tealiumiq.com"を使用する必要があります。
* **クロスドメイン追跡**
  * 任意。
  * クロスドメイン追跡を有効にするには**On**を選択します。
  * クロスドメイン追跡（setAllowLinker）で使用するドメインのカンマ区切りのリスト。
  * "setAllowLinker"の値を構成し、クロスドメイン追跡プラグインを有効にします。
  * この機能を使用するには、"Cross-Tracking Domains"フィールドに1つ以上のドメインを指定するか、"crossDomainTrack"にマッピングする必要があります。
* **トランスポート**
  * ヒットが送信されるトランスポートメカニズムを指定します。
* **エンハンストEコマース**
  * 任意。
  * 確認できない場合はデフォルト値（**false**）を使用します。
  * **true**に構成すると、エンハンストEコマース機能が有効になります。
  * 次のアクションにはEコマースアクションのマッピングが必要です：
    * `product_click`
    * `detail`
    * `add`
    * `remove`
    * `checkout`
    * `checkout_option`
    * `promo_click`
    * `refund`
  * 詳細については、Googleの[Enhanced E-Commerce](http://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce)ドキュメンテーションをご覧ください。
  * Tealium iQタグ管理を通じてエンハンストEコマースアクションを構成する方法についての詳細は、[Google Universal Analytics Tag: Enhanced E-Commerce](https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/)をご覧ください。
* **エンハンストリンク属性**
  * 任意。
  * 有効にすると、各ページで`linkid.js`のリクエストが行われます。
  * 確認できない場合はデフォルト（**false**）を使用します。
  * **true**に構成すると、[enhanced link](https://developers.google.com/analytics/devguides/collection/analyticsjs/advanced#enhancedlink)リンク追跡機能が有効になります。
* **ディスプレイ広告機能**
  * 任意。
  * Google AnalyticsがDoubleClickクッキーを介してあなたのトラフィックに関するデータを収集することを可能にします。これは、標準のGoogle Analytics実装を通じて収集されたデータに加えて行われます。
  * GUAがDoubleClickクッキーを介してあなたのトラフィックに関するデータを収集することを可能にするには、**On**を選択します。これは、標準のGUA実装を通じて収集されたデータに加えて行われます。
* **スクリーンビューの追跡**
  * 任意。
  * GUAの[App/Screen tracking](https://developers.google.com/analytics/devguides/collection/analyticsjs/screens)機能を有効にするには、**On**を選択します。
  * 有効にすると、初期のページビュー後に別のスクリーンビューリクエストが送信されます。
  * 有効にすると、このタグは訪問がアプリを使用して表示したコンテンツを追跡することができます。
* **IPの匿名化**
  * 任意。
  * プライバシーポリシーを遵守するために、訪問のIPアドレスの最後の部分をゼロに構成してから、それをGUAデータ収集ネットワークに送信するには、**On**を選択します。
  * Google Analyticsにトラッカーオブジェクトによって送信される情報を匿名化するよう指示します。これは、IPアドレスの最後のオクテットをその保存前に削除します。
  * これにより、地理的な報告の精度がわずかに低下します。
* **拡張子実行前の作成を有効にする**
  * 任意。
  * 拡張子が実行される前にGAの"create"メソッドを使用してトラッキングIDを初期化することを有効にするには、**On**を選択します。
  * トラッキングIDがマッピングで構成されている場合は適用されません。
* **Eコマース値の自動入力**
  * 任意。
  * 商品名、単価、数量が定義されていない場合に自動的に入力します。
  * Eコマースのマッピングを変更したくない場合は、この構成をOFFにすることができます。
* **自動送信イベント**
  * 任意。
  * 有効にすると、次のエンハンストEコマースアクションに対してデフォルトのカスタムイベントが生成されます：
    * `product_click`
    * `add`
    * `remove`
    * `checkout_option`
    * `promo_click`
* **Optimizely統合を有効にする**
  * 任意。
  * Optimizelyの実験に対する自動GA追跡を有効にします。
  * タグがOptimizelyの実験を追跡するようにしたい場合は、**On**を選択します。
* **Clear Vars**
  * 通常、トラッカーの寿命に構成されているアイテムを、各トラッキングリクエスト後にクリアします。
  * シングルページアプリケーションにのみ適用されます。
  * デフォルト値は**Off**です。
* **AMPクライアントIDを使用する**
  * Google AMPクライアントIDを使用すると、AMPと非AMPページでコンテンツを閲覧するユーザーを一意に識別することができます。
  * 有効にするには**On**を選択します。
  * オプトインすると、Google AnalyticsはAMPクライアントIDを使用して、ユーザーがGoogle AMP閲覧者を介してAMPページを訪れたときに、複数のサイトイベントが同じユーザーに属することを判断します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[Load Rules](https://docs.tealium.com/about-load-rules/)のドキュメンテーションをご覧ください。

<blockquote>
Google Universal Analyticsなどの分析タグはすべてのページで読み込むことを目的としているため、デフォルトの**すべてのページ**読み込みルールを選択するべきです。
</blockquote>


## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

* 電子商取引のデータを追跡している場合、[E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/)を追加し、構成することをお勧めします。マッピングツールボックス内の電子商取引の宛先へのマッピングは、電子商取引の拡張のマッピングを上書きします。
* Google Analyticsでは、基本的なページ追跡には追加のマッピングは必要ありません。タグは自動的に基本的なページデータを追跡します。イベント追跡、キャンペーン追跡、ソーシャルインタラクション測定、コンテンツグループ、カスタム変数は自動的に送信されません。これらは手動でマッピングする必要があります。

Google Universal Analyticsへのマッピングに関する詳細情報は、[Google Universal Analytics Tag: Advanced Mapping](https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-tag-advanced-mapping/)の記事を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`tid`|  <ul><li>トラッキングID</li><li>データを送信したいGoogle AnalyticsプロパティのトラッキングID</li><li>例： **UA-12345678-1**</li><li>複数のプロパティにデータを送信するには、カンマ区切りのリストを使用します。</li><li>デフォルトを上書き。</li></ul> |
|`name`|  <ul><li>トラッカー名。</li><li>デフォルトを上書き。</li></ul> |
|`page`|  <ul><li>ページ</li></ul> |
|`title`|  <ul><li>タイトル</li></ul> |
|`location`|  <ul><li>ロケーション</li></ul> |
|`uid`|  <ul><li>UID</li></ul> |
|`transport`|  <ul><li>トランスポート</li></ul> |
|`cookieDomain`|  <ul><li>Cookieドメイン</li><li>デフォルトを上書き。</li></ul> |
|`cookieExpires`|  <ul><li>Cookieの有効期限</li></ul> |
|`legacyCookieDomain`|  <ul><li>レガシーCookieドメイン</li></ul> |
|`legacyHistoryImport`|  <ul><li>レガシーヒストリーインポート</li><li>値は **true** または **false**。</li></ul> |
|`nonInteraction`|  <ul><li>非インタラクション</li></ul> |
|`enhancedLinkAttribution`|  <ul><li>リンク属性のエンリッチメント</li><li>値は **true** または **false**。</li></ul> |
|`allowLinker`|  <ul><li>リンカーの構成</li><li>値は **true** または **false**。</li></ul> |
|`crossDomainTrack`|  <ul><li>ブーリアン</li><li>クロスドメイン追跡</li><li>自動リンクドメイン</li><li>`setAllowLinker`の値を構成し、クロスドメイン追跡プラグインを有効にします。</li><li>この機能を使用するには、"クロストラッキングドメイン"フィールドに1つ以上のドメインを指定するか、`crossDomainTrack`にマッピングする必要があります。</li><li>複数のドメインに対しては、カンマ区切りのリストを使用します。</li></ul> |
|`siteSpeedSampleRate`|  <ul><li>サイトスピードサンプルレート</li></ul> |
|`sampleRate`|  <ul><li>サンプルレート</li></ul> |
|`autofill_params`|  <ul><li>自動入力E-Commerceパラメータ</li><li>値は **true** または **false**。</li></ul> |
|`optimizely`|  <ul><li>Optimizely統合</li><li>値は **true** または **false**。</li></ul> |
|`init_before_extensions`|  <ul><li>拡張機能の前にトラッカーを初期化</li><li>値は **true** または **false**。</li></ul> |
|`sessionControl`|  <ul><li>セッション制御</li><li>値は **start** または **end**。</li></ul> |
|`anonymizeIp`|  <ul><li>IPの匿名化</li><li>トラッカーオブジェクトによって送信される情報を匿名化するようGoogle Analyticsに指示します。これは、IPアドレスの最後のオクテットを保存する前に削除します。</li><li>地理的な報告の精度をわずかに低下させます。</li><li>値は **true** または **false**。</li></ul> |
|`dataSource`|  <ul><li>データソース</li><li>例：ウェブ、モバイル。</li></ul> |
|`clear_global_vars`|  <ul><li>変数のクリア</li><li>各トラッキングリクエスト後に、トラッカーの寿命の間に通常構成される項目をクリアします。</li><li>値は **true** または **false**。</li></ul> |
|`clientId`|  <ul><li>クライアントID</li></ul> |
|`useAmpClientId`|  <ul><li>AMPクライアントIDの使用</li><li>値は **true** または **false**。</li></ul> |
|`set.###`|  <ul><li>カスタムセットコマンド</li></ul> |

### イベント

|変数| 説明|
|---| ---|
|`eventCategory`|  <ul><li>必須</li><li>イベントカテゴリ。</li></ul> |
|`eventAction`|  <ul><li>必須</li><li>イベントアクション。</li></ul> |
|`eventLabel`|  <ul><li>イベントラベル</li></ul> |
|`eventValue`|  <ul><li>イベント値</li></ul> |
|`ga_events`|  <ul><li>配列</li><li>GAイベント配列</li></ul> |
|`global_event_cb`|  <ul><li>グローバルビューコールバック</li></ul> |
|`standard_event_cb`|  <ul><li>スタンダードイベントコールバック</li></ul> |

### キャンペーン

|変数| 説明|
|---| ---|
|`campaignId`|  <ul><li>キャンペーンID</li></ul> |
|`campaignName`|  <ul><li>キャンペーン名</li></ul> |
|`campaignSource`|  <ul><li>キャンペーンソース</li></ul> |
|`campaignMedium`|  <ul><li>キャンペーン媒体</li></ul> |
|`campaignContent`|  <ul><li>キャンペーンコンテンツ</li></ul> |
|`campaignKeyword`|  <ul><li>キャンペーンキーワード</li></ul> |

### ソーシャル

|変数| 説明|
|---| ---|
|`socialNetwork`|  <ul><li>ソーシャルネットワーク</li></ul> |
|`socialAction`|  <ul><li>ソーシャルアクション</li></ul> |
|`socialTarget`|  <ul><li>ソーシャルターゲット</li></ul> |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>トランザクションID</li></ul> |
|`affiliation`|  <ul><li>ストア名/ID</li></ul> |
|`revenue`|  <ul><li>総合計</li></ul> |
|`shipping`|  <ul><li>送料</li></ul> |
|`tax`|  <ul><li>税金</li></ul> |

### アプリ / スクリーントラッキング

|変数| 説明|
|---| ---|
|`screenView`|  <ul><li>スクリーンビューの追跡</li><li>アプリ/スクリーン追跡を有効にします。</li><li>有効にすると、初期のページビュー後に別のスクリーンビューリクエストが送信されます。</li></ul> |
| `appName` |  <ul><li>アプリケーション名</li></ul> |
| `appId` |  <ul><li>アプリケーションID</li></ul> |
| `appVersion` |  <ul><li>アプリケーションバージョン</li></ul> |
|`appInstallerId`|  <ul><li>アプリケーションインストーラーID</li></ul> |
|`screenName`|  <ul><li>スクリーン名</li></ul> |
|`exception_reason`|  <ul><li>例外の説明</li></ul> |

### コンテンツグループ

|変数| 説明|
|---| ---|
|`content_group1`| コンテンツグループ 1|
|`content_group2`| コンテンツグループ 2|
|`content_group3`| コンテンツグループ 3|
|`content_group4`| コンテンツグループ 4|
|`content_group5`| コンテンツグループ 5|

### ディメンション

|変数| 説明|
|---| ---|
|`dimension1`| ディメンション 1|
|`dimension2`| ディメンション 2|
|`dimension3`| ディメンション 3|
|`dimension4`| ディメンション 4|
|`dimension5`| ディメンション 5|
|`dimension6`| ディメンション 6|
|`dimension7`| ディメンション 7|
|`dimension8`| ディメンション 8|
|`dimension9`| ディメンション 9|
|`dimension10`| ディメンション 10|
|`dimension11`| ディメンション 11|
|`dimension12`| ディメンション 12|
|`dimension13`| ディメンション 13|
|`dimension14`| ディメンション 14|
|`dimension15`| ディメンション 15|
|`dimension16`| ディメンション 16|
|`dimension17`| ディメンション 17|
|`dimension18`| ディメンション 18|
|`dimension19`| ディメンション 19|
|`dimension20`| ディメンション 20|
|-- プレミアムディメンション--|
|`dimension21` - `dimension200`| ディメンション 21 から ディメンション 100まで|

### メトリクス

|変数| 説明|
|---| ---|
|`metric1`| メトリクス 1|
|`metric2`| メトリクス 2|
|`metric3`| メトリクス 3|
|`metric4`| メトリクス 4|
|`metric5`| メトリクス 5|
|`metric6`| メトリクス 6|
|`metric7`| メトリクス 7|
|`metric8`| メトリクス 8|
|`metric9`| メトリクス 9|
|`metric10`| メトリクス 10|
|`metric11`| メトリクス 11|
|`metric12`| メトリクス 12|
|`metric13`| メトリクス 13|
|`metric14`| メトリクス 14|
|`metric15`| メトリクス 15|
|`metric16`| メトリクス 16|
|`metric17`| メトリクス 17|
|`metric18`| メトリクス 18|
|`metric19`| メトリクス 19|
|`metric20`| メトリクス 20|
|-- プレミアムメトリクス--|
|`metric21` - `metric200`| メトリクス 21 から メトリクス 200まで|

### エンリッチメントE-Commerce

|変数| 説明|
|---| ---|
|`enh_action`|  <ul><li>E-Commerceアクション</li></ul> |
| `enh_event_cb` |  <ul><li>E-Commerceイベントコールバック</li></ul> |
| `enh_checkout_step` |  <ul><li>チェックアウトステップ</li></ul> |
| `enh_checkout_option` |  <ul><li>チェックアウトオプション</li></ul> |
| `order_id` |  <ul><li>トランザクションID</li><li>`_corder`を上書きします。</li></ul> |
| `affiliation` |  <ul><li>ストア名/ID</li><li>`_cstore`を上書きします。</li></ul> |
| `revenue` |  <ul><li>総合計</li><li>`_ctotal`を上書きします。</li></ul> |
| `shipping` |  <ul><li>配送</li><li>`_cship`を上書きします。</li></ul> |
| `tax` |  <ul><li>税金</li><li>`_ctax`を上書きします。</li></ul> |
| `coupon` |  <ul><li>クーポン</li><li>`_cpromo`を上書きします。</li></ul> |
| `product_id` |  <ul><li>配列</li><li>IDのリスト</li></ul> |
| `product_name` |  <ul><li>配列</li><li>名前のリスト</li></ul> |
| `product_category` |  <ul><li>配列</li><li>カテゴリのリスト</li></ul> |
| `product_brand` |  <ul><li>配列</li><li>ブランドのリスト</li></ul> |
| `product_variant` |  <ul><li>配列</li><li>バリアントのリスト</li></ul> |
| `product_unit_price` |  <ul><li>配列</li><li>価格のリスト</li></ul> |
| `product_quantity` |  <ul><li>配列</li><li>数量のリスト</li></ul> |
| `product_discount` |  <ul><li>配列</li><li>割引のリスト</li></ul> |
| `product_action_list` |  <ul><li>商品アクションリスト</li></ul> |
| `product_position` |  <ul><li>配列</li><li>商品位置</li></ul> |

### Enh E-Comm: インプレッション/プロモ

|変数| 説明|
|---| ---|
|`enh_impression_id`|  <ul></ul> |
|`enh_impression_name`|  <ul><li>配列</li><li>商品インプレッション名</li></ul> |
|`enh_impression_category`|  <ul><li>配列</li><li>商品インプレッションカテゴリ</li></ul> |
|`enh_impression_brand`|  <ul><li>配列</li><li>商品インプレッションブランド</li></ul> |
|`enh_impression_variant`|  <ul><li>配列</li><li>商品インプレッションバリアント</li></ul> |
|`enh_impression_price`|  <ul><li>配列</li><li>商品インプレッション価格</li></ul> |
|`enh_impression_list`|  <ul><li>配列</li><li>商品インプレッションリスト</li></ul> |
|`enh_impression_position`|  <ul><li>配列</li><li>商品インプレッション位置</li></ul> |
|`enh_promo_id`|  <ul><li>配列</li><li>プロモーションID</li></ul> |
|`enh_promo_name`|  <ul><li>配列</li><li>プロモーション名</li></ul> |
|`enh_promo_creative`|  <ul><li>配列</li><li>プロモーションクリエイティブ</li></ul> |
|`enh_promo_position`|  <ul><li>配列</li><li>プロモーション位置</li></ul> |

## ベンダーのドキュメンテーション

* [あなたのサイトにanalytics.jsを追加する (**Google Analytics** &gt; **トラッキング**)](https://developers.google.com/analytics/devguides/collection/analyticsjs/)



