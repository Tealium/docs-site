---
title: Google Universal Analytics (analytics.js) タグ構成ガイド
description: この記事では、iQタグ管理アカウントでGoogle Universal Analyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-analyticsjs-tag/
---
 2023年7月1日以降、Google Universal Analyticsのプロパティはヒットの処理を停止しました。このタグは廃止され、タグマーケットプレイスではもう利用できません。現在のタグについては、[Google Analytics 4]()をご覧ください。 

Google Analytics (analytics.js)は、Google Analyticsアカウントでデータが収集・整理される方法を変える一連の機能を導入します。

## タグのヒント

* Google Analytics (analytics.js)についての詳細は、[About Universal Analytics](http://support.google.com/analytics/bin/answer.py?hl=en&amp;answer=2790010&amp;topic=2790009)をご覧ください。
* このタグのTealium実装を使用する場合は、Google API関数の代わりにマッピングを使用してください。
* ディスプレイ広告のサポート情報については、[About Advertising Features](http://support.google.com/analytics/answer/3450482)をご覧ください。
* 自動生成されたトラッカー名は、定義されたアカウント数に対して`tealium_X`の形式を取ります。

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[Tag Overview]()の記事を読んでください。

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
  * 共有サブドメイン間での追跡を有効にする場合は、ドメインの&#39;www.&#39;プレフィックスを省略します。例えば、[www.tealium.com](http://www.tealium.com)は**tealium.com**になります。特定のサブドメインを個別に追跡したい場合は、ドメインアドレス全体を入力します。例：`www.tealium.com`。
* **グローバルオブジェクト**
  * ほとんどの実装では必要ありません。
  * イベントキューに使用されるグローバルオブジェクトの名前。
  * 指定されていない場合は&#34;**ga**&#34;が使用されます。
* **クロスドメイン追跡**
  * 任意。
  * クロスドメイン追跡を有効にするには**true**に構成する必要があります。
  * クロスドメイン追跡（setAllowLinker）で使用するドメインのカンマ区切りのリスト。
  * トップレベルドメインの&#34;tealiumiq.com&#34;ではなく、完全修飾ドメイン名、例えば&#34;my.tealiumiq.com&#34;を使用する必要があります。
* **クロスドメイン追跡**
  * 任意。
  * クロスドメイン追跡を有効にするには**On**を選択します。
  * クロスドメイン追跡（setAllowLinker）で使用するドメインのカンマ区切りのリスト。
  * &#34;setAllowLinker&#34;の値を構成し、クロスドメイン追跡プラグインを有効にします。
  * この機能を使用するには、&#34;Cross-Tracking Domains&#34;フィールドに1つ以上のドメインを指定するか、&#34;crossDomainTrack&#34;にマッピングする必要があります。
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
  * Tealium iQタグ管理を通じてエンハンストEコマースアクションを構成する方法についての詳細は、[Google Universal Analytics Tag: Enhanced E-Commerce](/ja/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/)をご覧ください。
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
  * 拡張子が実行される前にGAの&#34;create&#34;メソッドを使用してトラッキングIDを初期化することを有効にするには、**On**を選択します。
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

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[Load Rules]()のドキュメンテーションをご覧ください。
Google Universal Analyticsなどの分析タグはすべてのページで読み込むことを目的としているため、デフォルトの**すべてのページ**読み込みルールを選択するべきです。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

* 電子商取引のデータを追跡している場合、[E-Commerce Extension]()を追加し、構成することをお勧めします。マッピングツールボックス内の電子商取引の宛先へのマッピングは、電子商取引の拡張のマッピングを上書きします。
* Google Analyticsでは、基本的なページ追跡には追加のマッピングは必要ありません。タグは自動的に基本的なページデータを追跡します。イベント追跡、キャンペーン追跡、ソーシャルインタラクション測定、コンテンツグループ、カスタム変数は自動的に送信されません。これらは手動でマッピングする必要があります。

Google Universal Analyticsへのマッピングに関する詳細情報は、[Google Universal Analytics Tag: Advanced Mapping](/ja/client-side-tags/google-universal-analytics-tag-advanced-mapping/)の記事を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`tid`|  &lt;ul&gt;&lt;li&gt;トラッキングID&lt;/li&gt;&lt;li&gt;データを送信したいGoogle AnalyticsプロパティのトラッキングID&lt;/li&gt;&lt;li&gt;例： **UA-12345678-1**&lt;/li&gt;&lt;li&gt;複数のプロパティにデータを送信するには、カンマ区切りのリストを使用します。&lt;/li&gt;&lt;li&gt;デフォルトを上書き。&lt;/li&gt;&lt;/ul&gt; |
|`name`|  &lt;ul&gt;&lt;li&gt;トラッカー名。&lt;/li&gt;&lt;li&gt;デフォルトを上書き。&lt;/li&gt;&lt;/ul&gt; |
|`page`|  &lt;ul&gt;&lt;li&gt;ページ&lt;/li&gt;&lt;/ul&gt; |
|`title`|  &lt;ul&gt;&lt;li&gt;タイトル&lt;/li&gt;&lt;/ul&gt; |
|`location`|  &lt;ul&gt;&lt;li&gt;ロケーション&lt;/li&gt;&lt;/ul&gt; |
|`uid`|  &lt;ul&gt;&lt;li&gt;UID&lt;/li&gt;&lt;/ul&gt; |
|`transport`|  &lt;ul&gt;&lt;li&gt;トランスポート&lt;/li&gt;&lt;/ul&gt; |
|`cookieDomain`|  &lt;ul&gt;&lt;li&gt;Cookieドメイン&lt;/li&gt;&lt;li&gt;デフォルトを上書き。&lt;/li&gt;&lt;/ul&gt; |
|`cookieExpires`|  &lt;ul&gt;&lt;li&gt;Cookieの有効期限&lt;/li&gt;&lt;/ul&gt; |
|`legacyCookieDomain`|  &lt;ul&gt;&lt;li&gt;レガシーCookieドメイン&lt;/li&gt;&lt;/ul&gt; |
|`legacyHistoryImport`|  &lt;ul&gt;&lt;li&gt;レガシーヒストリーインポート&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |
|`nonInteraction`|  &lt;ul&gt;&lt;li&gt;非インタラクション&lt;/li&gt;&lt;/ul&gt; |
|`enhancedLinkAttribution`|  &lt;ul&gt;&lt;li&gt;リンク属性のエンリッチメント&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |
|`allowLinker`|  &lt;ul&gt;&lt;li&gt;リンカーの構成&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |
|`crossDomainTrack`|  &lt;ul&gt;&lt;li&gt;ブーリアン&lt;/li&gt;&lt;li&gt;クロスドメイン追跡&lt;/li&gt;&lt;li&gt;自動リンクドメイン&lt;/li&gt;&lt;li&gt;`setAllowLinker`の値を構成し、クロスドメイン追跡プラグインを有効にします。&lt;/li&gt;&lt;li&gt;この機能を使用するには、&#34;クロストラッキングドメイン&#34;フィールドに1つ以上のドメインを指定するか、`crossDomainTrack`にマッピングする必要があります。&lt;/li&gt;&lt;li&gt;複数のドメインに対しては、カンマ区切りのリストを使用します。&lt;/li&gt;&lt;/ul&gt; |
|`siteSpeedSampleRate`|  &lt;ul&gt;&lt;li&gt;サイトスピードサンプルレート&lt;/li&gt;&lt;/ul&gt; |
|`sampleRate`|  &lt;ul&gt;&lt;li&gt;サンプルレート&lt;/li&gt;&lt;/ul&gt; |
|`autofill_params`|  &lt;ul&gt;&lt;li&gt;自動入力E-Commerceパラメータ&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |
|`optimizely`|  &lt;ul&gt;&lt;li&gt;Optimizely統合&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |
|`init_before_extensions`|  &lt;ul&gt;&lt;li&gt;拡張機能の前にトラッカーを初期化&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |
|`sessionControl`|  &lt;ul&gt;&lt;li&gt;セッション制御&lt;/li&gt;&lt;li&gt;値は **start** または **end**。&lt;/li&gt;&lt;/ul&gt; |
|`anonymizeIp`|  &lt;ul&gt;&lt;li&gt;IPの匿名化&lt;/li&gt;&lt;li&gt;トラッカーオブジェクトによって送信される情報を匿名化するようGoogle Analyticsに指示します。これは、IPアドレスの最後のオクテットを保存する前に削除します。&lt;/li&gt;&lt;li&gt;地理的な報告の精度をわずかに低下させます。&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |
|`dataSource`|  &lt;ul&gt;&lt;li&gt;データソース&lt;/li&gt;&lt;li&gt;例：ウェブ、モバイル。&lt;/li&gt;&lt;/ul&gt; |
|`clear_global_vars`|  &lt;ul&gt;&lt;li&gt;変数のクリア&lt;/li&gt;&lt;li&gt;各トラッキングリクエスト後に、トラッカーの寿命の間に通常構成される項目をクリアします。&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |
|`clientId`|  &lt;ul&gt;&lt;li&gt;クライアントID&lt;/li&gt;&lt;/ul&gt; |
|`useAmpClientId`|  &lt;ul&gt;&lt;li&gt;AMPクライアントIDの使用&lt;/li&gt;&lt;li&gt;値は **true** または **false**。&lt;/li&gt;&lt;/ul&gt; |
|`set.###`|  &lt;ul&gt;&lt;li&gt;カスタムセットコマンド&lt;/li&gt;&lt;/ul&gt; |

### イベント

|変数| 説明|
|---| ---|
|`eventCategory`|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;イベントカテゴリ。&lt;/li&gt;&lt;/ul&gt; |
|`eventAction`|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;イベントアクション。&lt;/li&gt;&lt;/ul&gt; |
|`eventLabel`|  &lt;ul&gt;&lt;li&gt;イベントラベル&lt;/li&gt;&lt;/ul&gt; |
|`eventValue`|  &lt;ul&gt;&lt;li&gt;イベント値&lt;/li&gt;&lt;/ul&gt; |
|`ga_events`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;GAイベント配列&lt;/li&gt;&lt;/ul&gt; |
|`global_event_cb`|  &lt;ul&gt;&lt;li&gt;グローバルビューコールバック&lt;/li&gt;&lt;/ul&gt; |
|`standard_event_cb`|  &lt;ul&gt;&lt;li&gt;スタンダードイベントコールバック&lt;/li&gt;&lt;/ul&gt; |

### キャンペーン

|変数| 説明|
|---| ---|
|`campaignId`|  &lt;ul&gt;&lt;li&gt;キャンペーンID&lt;/li&gt;&lt;/ul&gt; |
|`campaignName`|  &lt;ul&gt;&lt;li&gt;キャンペーン名&lt;/li&gt;&lt;/ul&gt; |
|`campaignSource`|  &lt;ul&gt;&lt;li&gt;キャンペーンソース&lt;/li&gt;&lt;/ul&gt; |
|`campaignMedium`|  &lt;ul&gt;&lt;li&gt;キャンペーン媒体&lt;/li&gt;&lt;/ul&gt; |
|`campaignContent`|  &lt;ul&gt;&lt;li&gt;キャンペーンコンテンツ&lt;/li&gt;&lt;/ul&gt; |
|`campaignKeyword`|  &lt;ul&gt;&lt;li&gt;キャンペーンキーワード&lt;/li&gt;&lt;/ul&gt; |

### ソーシャル

|変数| 説明|
|---| ---|
|`socialNetwork`|  &lt;ul&gt;&lt;li&gt;ソーシャルネットワーク&lt;/li&gt;&lt;/ul&gt; |
|`socialAction`|  &lt;ul&gt;&lt;li&gt;ソーシャルアクション&lt;/li&gt;&lt;/ul&gt; |
|`socialTarget`|  &lt;ul&gt;&lt;li&gt;ソーシャルターゲット&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;トランザクションID&lt;/li&gt;&lt;/ul&gt; |
|`affiliation`|  &lt;ul&gt;&lt;li&gt;ストア名/ID&lt;/li&gt;&lt;/ul&gt; |
|`revenue`|  &lt;ul&gt;&lt;li&gt;総合計&lt;/li&gt;&lt;/ul&gt; |
|`shipping`|  &lt;ul&gt;&lt;li&gt;送料&lt;/li&gt;&lt;/ul&gt; |
|`tax`|  &lt;ul&gt;&lt;li&gt;税金&lt;/li&gt;&lt;/ul&gt; |

### アプリ / スクリーントラッキング

|変数| 説明|
|---| ---|
|`screenView`|  &lt;ul&gt;&lt;li&gt;スクリーンビューの追跡&lt;/li&gt;&lt;li&gt;アプリ/スクリーン追跡を有効にします。&lt;/li&gt;&lt;li&gt;有効にすると、初期のページビュー後に別のスクリーンビューリクエストが送信されます。&lt;/li&gt;&lt;/ul&gt; |
| `appName` |  &lt;ul&gt;&lt;li&gt;アプリケーション名&lt;/li&gt;&lt;/ul&gt; |
| `appId` |  &lt;ul&gt;&lt;li&gt;アプリケーションID&lt;/li&gt;&lt;/ul&gt; |
| `appVersion` |  &lt;ul&gt;&lt;li&gt;アプリケーションバージョン&lt;/li&gt;&lt;/ul&gt; |
|`appInstallerId`|  &lt;ul&gt;&lt;li&gt;アプリケーションインストーラーID&lt;/li&gt;&lt;/ul&gt; |
|`screenName`|  &lt;ul&gt;&lt;li&gt;スクリーン名&lt;/li&gt;&lt;/ul&gt; |
|`exception_reason`|  &lt;ul&gt;&lt;li&gt;例外の説明&lt;/li&gt;&lt;/ul&gt; |

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
|`enh_action`|  &lt;ul&gt;&lt;li&gt;E-Commerceアクション&lt;/li&gt;&lt;/ul&gt; |
| `enh_event_cb` |  &lt;ul&gt;&lt;li&gt;E-Commerceイベントコールバック&lt;/li&gt;&lt;/ul&gt; |
| `enh_checkout_step` |  &lt;ul&gt;&lt;li&gt;チェックアウトステップ&lt;/li&gt;&lt;/ul&gt; |
| `enh_checkout_option` |  &lt;ul&gt;&lt;li&gt;チェックアウトオプション&lt;/li&gt;&lt;/ul&gt; |
| `order_id` |  &lt;ul&gt;&lt;li&gt;トランザクションID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `affiliation` |  &lt;ul&gt;&lt;li&gt;ストア名/ID&lt;/li&gt;&lt;li&gt;`_cstore`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `revenue` |  &lt;ul&gt;&lt;li&gt;総合計&lt;/li&gt;&lt;li&gt;`_ctotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `shipping` |  &lt;ul&gt;&lt;li&gt;配送&lt;/li&gt;&lt;li&gt;`_cship`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `tax` |  &lt;ul&gt;&lt;li&gt;税金&lt;/li&gt;&lt;li&gt;`_ctax`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `coupon` |  &lt;ul&gt;&lt;li&gt;クーポン&lt;/li&gt;&lt;li&gt;`_cpromo`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `product_id` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;IDのリスト&lt;/li&gt;&lt;/ul&gt; |
| `product_name` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前のリスト&lt;/li&gt;&lt;/ul&gt; |
| `product_category` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリのリスト&lt;/li&gt;&lt;/ul&gt; |
| `product_brand` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;ブランドのリスト&lt;/li&gt;&lt;/ul&gt; |
| `product_variant` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;バリアントのリスト&lt;/li&gt;&lt;/ul&gt; |
| `product_unit_price` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト&lt;/li&gt;&lt;/ul&gt; |
| `product_quantity` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト&lt;/li&gt;&lt;/ul&gt; |
| `product_discount` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;割引のリスト&lt;/li&gt;&lt;/ul&gt; |
| `product_action_list` |  &lt;ul&gt;&lt;li&gt;商品アクションリスト&lt;/li&gt;&lt;/ul&gt; |
| `product_position` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品位置&lt;/li&gt;&lt;/ul&gt; |

### Enh E-Comm: インプレッション/プロモ

|変数| 説明|
|---| ---|
|`enh_impression_id`|  &lt;ul&gt;&lt;/ul&gt; |
|`enh_impression_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品インプレッション名&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_category`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品インプレッションカテゴリ&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_brand`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品インプレッションブランド&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_variant`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品インプレッションバリアント&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品インプレッション価格&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_list`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品インプレッションリスト&lt;/li&gt;&lt;/ul&gt; |
|`enh_impression_position`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品インプレッション位置&lt;/li&gt;&lt;/ul&gt; |
|`enh_promo_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーションID&lt;/li&gt;&lt;/ul&gt; |
|`enh_promo_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーション名&lt;/li&gt;&lt;/ul&gt; |
|`enh_promo_creative`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーションクリエイティブ&lt;/li&gt;&lt;/ul&gt; |
|`enh_promo_position`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーション位置&lt;/li&gt;&lt;/ul&gt; |

## ベンダーのドキュメンテーション

* [あなたのサイトにanalytics.jsを追加する (**Google Analytics** &amp;gt; **トラッキング**)](https://developers.google.com/analytics/devguides/collection/analyticsjs/)



