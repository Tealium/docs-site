---
title: Google Universal Analytics（analytics.js）タグ構成ガイド
description: この記事では、タグ管理アカウントで Google Universal Analytics タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-analyticsjs-tag/
---

<blockquote>
2023 年 7 月 1 日以降、Google Universal Analytics プロパティではヒットの処理が停止されています。このタグは非推奨となり、タグマーケットプレイスでは利用できなくなりました。現在のタグについては、[Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/)を参照してください。
</blockquote>


Google Analytics（analytics.js）では、Google Analytics アカウントでデータを収集および整理する方法を変更する一連の機能が導入されています。

## タグに関するヒント

* Google Analytics（analytics.js）の詳細については、[Universal Analytics について](http://support.google.com/analytics/bin/answer.py?hl=en&answer=2790010&topic=2790009)を参照してください。
* このタグに Tealium の実装を使用するには、Google API 関数ではなくマッピングを使用します。
* ディスプレイ広告のサポート情報については、[広告向け機能について](http://support.google.com/analytics/answer/3450482)を参照してください。
* 自動生成されるトラッカー名は、定義されたアカウント数に応じて `tealium_X` という形式になります。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を行います。

* **タイトル**
  * （必須）タグインスタンスを識別するためのわかりやすいタイトルを入力します。
* **トラッキング ID**
  * （必須）Google Universal Analytics（GUA）アカウントのトラッキング ID を入力します。
  * Google Analytics で追跡する各プロパティには、一意のプロパティトラッキング ID があります。
  * 例：**UA-12345678-1**
  * 複数のプロパティにデータを送信するには、カンマ区切りのリストを使用します。
* **トラッカー名**
  * （任意）複数のトラッカーを使用している場合、または使用する予定がある場合は、この構成を使用します。
  * データの送信先となる各アカウント ID または GUA プロパティには、関連付けられたトラッカー名が必要です。
  * ページごとにこのタグの複数のコピーを実行する場合は必須です。
  * 複数のトラッカー名（複数アカウントのトラッキング）にはカンマ区切りのリストを使用します。このリストの長さは、上記で入力したトラッキング ID のリストと同じである必要があります。
  * トラッカー名ではハイフン（-）はサポートされていません。
* **ドメイン**
  * （任意）特定のドメインのみでトラッキングを許可するには、この値を構成します。
  * サイトのドメイン名を入力します。
  * Google Analytics でドメインを自動検出するには、このフィールドを空白のままにします。
  * この構成により、GUA がサイト訪問の識別に使用する Cookie のドメインが構成されます。
  * 共有サブドメイン間のトラッキングを有効にする場合は、ドメインの「www.」プレフィックスを省略します。たとえば、[www.tealium.com](http://www.tealium.com) は **tealium.com** になります。サブドメインを個別に追跡する場合は、ドメインアドレス全体を入力します。例：`www.tealium.com`
* **グローバルオブジェクト**
  * ほとんどの実装では必要ありません。
  * イベントキューに使用するグローバルオブジェクトの名前です。
  * 指定しない場合は「**ga**」が使用されます。
* **クロストラッキングドメイン**
  * （任意）このリストを使用するには、クロスドメイントラッキングを **true** に構成する必要があります。
  * クロスドメイントラッキング（setAllowLinker）で使用するドメインのカンマ区切りリストです。
  * トップレベルドメイン「tealiumiq.com」ではなく、「my.tealiumiq.com」のような完全修飾ドメイン名を使用する必要があります。
* **クロスドメイントラッキング**
  * （任意）クロスドメイントラッキングを有効にするには、**On** を選択します。
  * クロスドメイントラッキング（setAllowLinker）で使用するドメインのカンマ区切りリストです。
  * 「setAllowLinker」の値を構成し、クロスドメイントラッキングプラグインを有効にします。
  * この機能を使用するには、「クロストラッキングドメイン」フィールドで 1 つ以上のドメインを指定するか、「crossDomainTrack」にマッピングする必要があります。
* **トランスポート**
  * ヒットの送信に使用する転送メカニズムを指定します。
* **拡張 e コマース**
  * （任意）不明な場合は、デフォルト値（**false**）を使用します。
  * **true** に構成すると、拡張 e コマース機能が有効になります。
  * 以下のアクションには、e コマースアクションのマッピングが必要です。
    * `product_click`
    * `detail`
    * `add`
    * `remove`
    * `checkout`
    * `checkout_option`
    * `promo_click`
    * `refund`
  * 詳細については、Google の[拡張 e コマース](http://developers.google.com/analytics/devguides/collection/analyticsjs/enhanced-ecommerce)ドキュメントを参照してください。
  * タグ管理を通じて拡張 e コマースアクションを構成する方法の詳細については、[Google Universal Analytics タグ：拡張 e コマース](https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-tag-enhanced-e-commerce/)を参照してください。
* **拡張リンク属性**
  * （任意）有効にすると、各ページで `linkid.js` に対するリクエストが行われます。
  * 不明な場合は、デフォルト（**false**）を使用します。
  * **true** に構成すると、[拡張リンク](https://developers.google.com/analytics/devguides/collection/analyticsjs/advanced#enhancedlink)のリンクトラッキング機能が有効になります。
* **ディスプレイ広告向け機能**
  * （任意）標準の Google Analytics 実装で収集されるデータに加えて、DoubleClick Cookie を通じてトラフィックに関するデータを Google Analytics が収集できるようにします。
  * 標準の GUA 実装で収集されるデータに加えて、DoubleClick Cookie を通じてトラフィックに関するデータを GUA が収集できるようにするには、**On** を選択します。
* **スクリーンビューの追跡**
  * （任意）GUA の[アプリ／スクリーントラッキング](https://developers.google.com/analytics/devguides/collection/analyticsjs/screens)機能を有効にするには、**On** を選択します。
  * 有効にすると、最初のページビューの後に、別のスクリーンビューリクエストが送信されます。
  * 有効にすることで、訪問がアプリを使用して閲覧したコンテンツをこのタグで追跡できます。
* **IP の匿名化**
  * （任意）GUA データ収集ネットワークに送信する前に訪問の IP アドレスの末尾部分をゼロに構成し、プライバシーポリシーに準拠できるようにするには、**On** を選択します。
  * 保存前に IP アドレスの最終オクテットを削除することで、トラッカーオブジェクトから送信される情報を匿名化するよう Google Analytics に指示します。
  * これにより、地域レポートの精度がわずかに低下します。
* **拡張機能より前に create を有効化**
  * 任意です。
  * 拡張機能が実行される前に、GA の「create」メソッドを使用してトラッキング ID を初期化するには、**On** を選択します。
  * トラッキング ID がマッピングで構成されている場合は適用されません。
* **e コマース値の自動入力**
  * （任意）商品名、単価、数量が定義されていない場合に、それらの値を入力します。
  * e コマースのマッピングを変更しない場合は、この構成を **Off** にできます。
* **イベントの自動送信**
  * （任意）有効にすると、以下の拡張 e コマースアクションに対してデフォルトのカスタムイベントが生成されます。
    * `product_click`
    * `add`
    * `remove`
    * `checkout_option`
    * `promo_click`
* **Optimizely 連携を有効化**
  * （任意）Optimizely の実験に対する GA の自動トラッキングを有効にします。
  * Optimizely の実験をタグで追跡する場合は、**On** を選択します。
* **変数をクリア**
  * 通常はトラッカーの存続期間中に構成される項目を、各トラッキングリクエストの後にクリアします。
  * シングルページアプリケーションにのみ適用されます。
  * デフォルト値は **Off** です。
* **AMP クライアント ID を使用**
  * Google AMP クライアント ID を使用すると、AMP ページと非 AMP ページのコンテンツを利用するユーザーを一意に識別できます。
  * 有効にするには、**On** を選択します。
  * オプトインすると、ユーザーが Google AMP 閲覧者ーで AMP ページにアクセスした際に、Google Analytics は AMP クライアント ID を使用して、複数のサイトイベントが同じユーザーに属することを判定します。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。ロードルールの詳細については、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。


<blockquote>
Google Universal Analytics などの分析タグはすべてのページで読み込むことを想定しているため、デフォルトの **All Pages** ロードルールを選択してください。
</blockquote>

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

* Eコマースデータをトラッキングする場合は、[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を追加して構成することをお勧めします。マッピングツールボックスでEコマース送信先に構成したマッピングは、Eコマース拡張機能のマッピングを上書きします。
* Google Analyticsでは、基本的なページトラッキングに追加のマッピングは必要ありません。タグによって基本的なページデータが自動的にトラッキングされます。イベントトラッキング、キャンペーントラッキング、ソーシャルインタラクションの測定、コンテンツグループ、カスタム変数は自動的には送信されないため、手動でマッピングする必要があります。

Google Universal Analyticsへのマッピングの詳細については、[Google Universal Analyticsタグ：高度なマッピング](https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-tag-advanced-mapping/)の記事を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`tid`| <ul><li>トラッキングID</li><li>データの送信先となるGoogle AnalyticsプロパティのトラッキングID</li><li>例：**UA-12345678-1**</li><li>複数のプロパティにデータを送信するには、カンマ区切りのリストを使用します。</li><li>デフォルト値を上書きします。</li></ul> |
|`name`| <ul><li>トラッカー名。</li><li>デフォルト値を上書きします。</li></ul> |
|`page`| <ul><li>ページ</li></ul> |
|`title`| <ul><li>タイトル</li></ul> |
|`location`| <ul><li>場所</li></ul> |
|`uid`| <ul><li>UID</li></ul> |
|`transport`| <ul><li>トランスポート</li></ul> |
|`cookieDomain`| <ul><li>Cookieドメイン</li><li>デフォルト値を上書きします。</li></ul> |
|`cookieExpires`| <ul><li>Cookieの有効期限</li></ul> |
|`legacyCookieDomain`| <ul><li>レガシーCookieドメイン</li></ul> |
|`legacyHistoryImport`| <ul><li>レガシー履歴のインポート</li><li>値は**true**または**false**です。</li></ul> |
|`nonInteraction`| <ul><li>非インタラクション</li></ul> |
|`enhancedLinkAttribution`| <ul><li>拡張リンクアトリビューション</li><li>値は**true**または**false**です。</li></ul> |
|`allowLinker`| <ul><li>Allow Linkerの構成</li><li>値は**true**または**false**です。</li></ul> |
|`crossDomainTrack`| <ul><li>ブール値</li><li>クロスドメイントラッキング</li><li>ドメインの自動リンク</li><li>`setAllowLinker`の値を構成し、クロスドメイントラッキングプラグインを有効にします。</li><li>この機能を使用するには、1つ以上のドメインを「Cross-Tracking Domains」フィールドで指定するか、`crossDomainTrack`にマッピングする必要があります。</li><li>複数のドメインには、カンマ区切りのリストを使用します。</li></ul> |
|`siteSpeedSampleRate`| <ul><li>サイト速度のサンプルレート</li></ul> |
|`sampleRate`| <ul><li>サンプルレート</li></ul> |
|`autofill_params`| <ul><li>Eコマースパラメータの自動入力</li><li>値は**true**または**false**です。</li></ul> |
|`optimizely`| <ul><li>Optimizely連携</li><li>値は**true**または**false**です。</li></ul> |
|`init_before_extensions`| <ul><li>拡張機能より前にトラッカーを初期化</li><li>値は**true**または**false**です。</li></ul> |
|`sessionControl`| <ul><li>セッション制御</li><li>値は**start**または**end**です。</li></ul> |
|`anonymizeIp`| <ul><li>IPの匿名化</li><li>保存前にIPアドレスの最後のオクテットを削除することで、トラッカーオブジェクトから送信される情報を匿名化するようGoogle Analyticsに指示します。</li><li>地域レポートの精度がわずかに低下します。</li><li>値は**true**または**false**です。</li></ul> |
|`dataSource`| <ul><li>データソース</li><li>例：Web、モバイル。</li></ul> |
|`clear_global_vars`| <ul><li>変数のクリア</li><li>通常はトラッカーの存続期間を通じて構成される項目を、各トラッキングリクエスト後にクリアします。</li><li>値は**true**または**false**です。</li></ul> |
|`clientId`| <ul><li>クライアントID</li></ul> |
|`useAmpClientId`| <ul><li>AMPクライアントIDを使用</li><li>値は**true**または**false**です。</li></ul> |
|`set.###`| <ul><li>カスタム構成コマンド</li></ul> |

### イベント

|変数|説明|
|---|---|
|`eventCategory`| <ul><li>（必須）イベントカテゴリー。</li></ul> |
|`eventAction`| <ul><li>（必須）イベントアクション。</li></ul> |
|`eventLabel`| <ul><li>イベントラベル</li></ul> |
|`eventValue`| <ul><li>イベント値</li></ul> |
|`ga_events`| <ul><li>配列</li><li>GAイベント配列</li></ul> |
|`global_event_cb`| <ul><li>グローバルビューコールバック</li></ul> |
|`standard_event_cb`| <ul><li>標準イベントコールバック</li></ul> |

### キャンペーン

|変数|説明|
|---|---|
|`campaignId`| <ul><li>キャンペーンID</li></ul> |
|`campaignName`| <ul><li>キャンペーン名</li></ul> |
|`campaignSource`| <ul><li>キャンペーンソース</li></ul> |
|`campaignMedium`| <ul><li>キャンペーンメディア</li></ul> |
|`campaignContent`| <ul><li>キャンペーンコンテンツ</li></ul> |
|`campaignKeyword`| <ul><li>キャンペーンキーワード</li></ul> |

### ソーシャル

|変数|説明|
|---|---|
|`socialNetwork`| <ul><li>ソーシャルネットワーク</li></ul> |
|`socialAction`| <ul><li>ソーシャルアクション</li></ul> |
|`socialTarget`| <ul><li>ソーシャルターゲット</li></ul> |

### Eコマース

|変数|説明|
|---|---|
|`order_id`| <ul><li>トランザクションID</li></ul> |
|`affiliation`| <ul><li>店舗名／ID</li></ul> |
|`revenue`| <ul><li>総合計</li></ul> |
|`shipping`| <ul><li>送料</li></ul> |
|`tax`| <ul><li>税金</li></ul> |

### アプリ／スクリーントラッキング

|変数|説明|
|---|---|
|`screenView`| <ul><li>スクリーンビューのトラッキング</li><li>アプリ／スクリーントラッキングを有効にします。</li><li>有効にすると、最初のページビューの後に別のスクリーンビューリクエストが送信されます。</li></ul> |
| `appName` | <ul><li>アプリケーション名</li></ul> |
| `appId` | <ul><li>アプリケーションID</li></ul> |
| `appVersion` | <ul><li>アプリケーションバージョン</li></ul> |
|`appInstallerId`| <ul><li>アプリケーションインストーラーID</li></ul> |
|`screenName`| <ul><li>スクリーン名</li></ul> |
|`exception_reason`| <ul><li>例外の説明</li></ul> |

### コンテンツグループ

|変数|説明|
|---|---|
|`content_group1`|コンテンツグループ1|
|`content_group2`|コンテンツグループ2|
|`content_group3`|コンテンツグループ4|
|`content_group4`|コンテンツグループ4|
|`content_group5`|コンテンツグループ5|

### ディメンション

|変数|説明|
|---|---|
|`dimension1`|ディメンション1|
|`dimension2`|ディメンション2|
|`dimension3`|ディメンション3|
|`dimension4`|ディメンション4|
|`dimension5`|ディメンション5|
|`dimension6`|ディメンション6|
|`dimension7`|ディメンション7|
|`dimension8`|ディメンション8|
|`dimension9`|ディメンション9|
|`dimension10`|ディメンション10|
|`dimension11`|ディメンション11|
|`dimension12`|ディメンション12|
|`dimension13`|ディメンション13|
|`dimension14`|ディメンション14|
|`dimension15`|ディメンション15|
|`dimension16`|ディメンション16|
|`dimension17`|ディメンション17|
|`dimension18`|ディメンション18|
|`dimension19`|ディメンション19|
|`dimension20`|ディメンション20|
|-- プレミアムディメンション--|
|`dimension21` - `dimension200`|ディメンション21からディメンション100まで|

### 指標

|変数|説明|
|---|---|
|`metric1`|指標1|
|`metric2`|指標2|
|`metric3`|指標3|
|`metric4`|指標4|
|`metric5`|指標5|
|`metric6`|指標6|
|`metric7`|指標7|
|`metric8`|指標8|
|`metric9`|指標9|
|`metric10`|指標10|
|`metric11`|指標11|
|`metric12`|指標12|
|`metric13`|指標13|
|`metric14`|指標14|
|`metric15`|指標15|
|`metric16`|指標16|
|`metric17`|指標17|
|`metric18`|指標18|
|`metric19`|指標19|
|`metric20`|指標20|
|-- プレミアム指標--|
|`metric21` - `metric200`|指標21から指標200まで|
### 拡張 E コマース

|変数|説明|
|---|---|
|`enh_action`| <ul><li>E コマースアクション</li></ul> |
| `enh_event_cb` | <ul><li>E コマースイベントのコールバック</li></ul> |
| `enh_checkout_step` | <ul><li>チェックアウトステップ</li></ul> |
| `enh_checkout_option` | <ul><li>チェックアウトオプション</li></ul> |
| `order_id` | <ul><li>トランザクション ID</li><li> `_corder` を上書きします。</li></ul> |
| `affiliation` | <ul><li>ストア名/ID</li><li> `_cstore` を上書きします。</li></ul> |
| `revenue` | <ul><li>総合計</li><li> `_ctotal` を上書きします。</li></ul> |
| `shipping` | <ul><li>送料</li><li> `_cship` を上書きします。</li></ul> |
| `tax` | <ul><li>税額</li><li> `_ctax` を上書きします。</li></ul> |
| `coupon` | <ul><li>クーポン</li><li> `_cpromo` を上書きします。</li></ul> |
| `product_id` | <ul><li>配列</li><li>ID のリスト</li></ul> |
| `product_name` | <ul><li>配列</li><li>名前のリスト</li></ul> |
| `product_category` | <ul><li>配列</li><li>カテゴリーのリスト</li></ul> |
| `product_brand` | <ul><li>配列</li><li>ブランドのリスト</li></ul> |
| `product_variant` | <ul><li>配列</li><li>バリエーションのリスト</li></ul> |
| `product_unit_price` | <ul><li>配列</li><li>価格のリスト</li></ul> |
| `product_quantity` | <ul><li>配列</li><li>数量のリスト</li></ul> |
| `product_discount` | <ul><li>配列</li><li>割引のリスト</li></ul> |
| `product_action_list` | <ul><li>商品アクションリスト</li></ul> |
| `product_position` | <ul><li>配列</li><li>商品の位置</li></ul> |

### 拡張 E コマース：インプレッション/プロモーション

|変数|説明|
|---|---|
|`enh_impression_id`| <ul></ul> |
|`enh_impression_name`| <ul><li>配列</li><li>商品インプレッション名</li></ul> |
|`enh_impression_category`| <ul><li>配列</li><li>商品インプレッションのカテゴリー</li></ul> |
|`enh_impression_brand`| <ul><li>配列</li><li>商品インプレッションのブランド</li></ul> |
|`enh_impression_variant`| <ul><li>配列</li><li>商品インプレッションのバリエーション</li></ul> |
|`enh_impression_price`| <ul><li>配列</li><li>商品インプレッションの価格</li></ul> |
|`enh_impression_list`| <ul><li>配列</li><li>商品インプレッションのリスト</li></ul> |
|`enh_impression_position`| <ul><li>配列</li><li>商品インプレッションの位置</li></ul> |
|`enh_promo_id`| <ul><li>配列</li><li>プロモーション ID</li></ul> |
|`enh_promo_name`| <ul><li>配列</li><li>プロモーション名</li></ul> |
|`enh_promo_creative`| <ul><li>配列</li><li>プロモーションのクリエイティブ</li></ul> |
|`enh_promo_position`| <ul><li>配列</li><li>プロモーションの位置</li></ul> |

## ベンダーのドキュメント

* [サイトへの analytics.js の追加（**Google Analytics** &gt; **トラッキング**）](https://developers.google.com/analytics/devguides/collection/analyticsjs/)