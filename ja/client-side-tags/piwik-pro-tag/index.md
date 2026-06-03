---
title: Piwik PROタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでPiwik PROタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/piwik-pro-tag/
---
## タグのヒント

* 注文IDが存在する場合、Track E-commerce Order Eventが発火します。
* マッピングを使用して：
  * 標準の構成値を動的に上書き
  * イベントトリガーの構成
  * カスタムディメンションの構成
  * E-Commerce拡張の値を上書き
* 以下のE-Commerce拡張パラメータをサポートしています：
  * 注文ID (`_corder` )
  * 注文合計 (`_ctotal` )
  * 小計 (`_csubtotal` )
  * 送料 (`_cship` )
  * 税金 (`_ctax` )
  * カートまたは注文タイプ (`_ctype` )
  * 顧客ID (`_ccustid` )
  * 商品IDのリスト (`_cprod` )
  * 名前のリスト (`_cprodname` )
  * カテゴリのリスト (`_ccat` )
  * 数量のリスト (`_cquan` )
  * 価格のリスト (`_cprice` )
  * 割引のリスト (`_cpdisc` )

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Piwik PROタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **App ID**
  * PPASアプリケーション識別子（以前のウェブサイトID、サイトID、またはidSite）。

* **Base URL**
  * 末尾にスラッシュがないPPASインスタンスURL。
  * 先頭に`//`を含めます。
  * 例：`//example.com`

* **ダウンロード＆アウトリンクトラッキングを有効にする**

* **ページ内のすべてのコンテンツの印象を追跡する**  
コンテンツを追跡するには、それがdata-track-content属性または`piwikTrackContent` CSSクラスを持っている必要があります。

* **すべての表示コンテンツの印象を追跡する**  
コンテンツを追跡するには、それがdata-track-content属性または`piwikTrackContent` CSSクラスを持っている必要があります。

* **スクロール時に印象をチェックする**
  * スクロールイベントで新しい表示コンテンツの印象をチェックします。
  * スクロール可能な要素に配置されたコンテンツブロックは検出しません。

* **表示コンテンツのウォッチ間隔**
  * 新しい表示コンテンツをチェックする間隔（ミリ秒）。
  * パフォーマンスの理由から、定期的なチェックを`0`に構成して無効にすることができます。

* **ハートビートタイマー**
  * 周期的なハートビートリクエストの間隔（秒）。

* **ユーザーを匿名で追跡する**
  * 訪問を匿名で追跡します（同意なし）。
  
* **ハートビートタイマーを有効にする**

* **ページビューを送信する**
  * ページビューイベントは自動的にサイトに記録されます。スニペットがページビューイベントを送信しないようにするには、このオプションを`false`に構成します。

### データマッピング

マッピングとは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

#### 標準

| 変数                             | 説明                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| `appId`                              | &lt;ul&gt;&lt;li&gt;App ID。&lt;/li&gt;&lt;/ul&gt;                                    |
| `base_url`                           | &lt;ul&gt;&lt;li&gt;PPASインスタンスアドレス。&lt;/li&gt;&lt;/ul&gt;                     |
| `tracking_url`                       | &lt;ul&gt;&lt;li&gt;Analytics Tracker URL。&lt;/li&gt;&lt;/ul&gt;                     |
| `category`                           | &lt;ul&gt;&lt;li&gt;イベントカテゴリ。&lt;/li&gt;&lt;/ul&gt;                            |
| `action`                             | &lt;ul&gt;&lt;li&gt;イベントアクション。&lt;/li&gt;&lt;/ul&gt;                              |
| `name`                               | &lt;ul&gt;&lt;li&gt;イベント名。&lt;/li&gt;&lt;/ul&gt;                                |
| `value`                              | &lt;ul&gt;&lt;li&gt;イベント値。&lt;/li&gt;&lt;/ul&gt;                               |
| `goal_name`                          | &lt;ul&gt;&lt;li&gt;ゴール名。&lt;/li&gt;&lt;/ul&gt;                                 |
| `goal_value`                         | &lt;ul&gt;&lt;li&gt;ゴール値。&lt;/li&gt;&lt;/ul&gt;                                |
| `title`                              | &lt;ul&gt;&lt;li&gt;カスタムページ名/ドキュメントタイトル。&lt;/li&gt;&lt;/ul&gt;           |
| `beat`                               | &lt;ul&gt;&lt;li&gt;ハートビートリクエスト間の時間。&lt;/li&gt;&lt;/ul&gt;           |
| `keyword`                            | &lt;ul&gt;&lt;li&gt;キーワード&lt;/li&gt;&lt;/ul&gt;                                    |
| `searchCount`                        | &lt;ul&gt;&lt;li&gt;検索数&lt;/li&gt;&lt;/ul&gt;                               |
| `isAnonymous`                        | &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;匿名トラッキングを有効にする。&lt;/li&gt;&lt;/ul&gt; |
| `CustomUrl`                          | &lt;ul&gt;&lt;li&gt;カスタムURL&lt;/li&gt;&lt;/ul&gt;                                 |
| `ReferrerUrl`                        | &lt;ul&gt;&lt;li&gt;リファラーURL。&lt;/li&gt;&lt;/ul&gt;                              |
| `cookieDomain`                       | &lt;ul&gt;&lt;li&gt;Cookieドメイン。&lt;/li&gt;&lt;/ul&gt;                             |
| `cookiePath`                         | &lt;ul&gt;&lt;li&gt;Cookieパス。&lt;/li&gt;&lt;/ul&gt;                               |
| `updateTimingDataOnPageLoadSampling` | &lt;ul&gt;&lt;li&gt;ページロードサンプリング時にタイミングデータを更新する。&lt;/li&gt;&lt;/ul&gt;  |
| `enableHeartBeatTimer`               | &lt;ul&gt;&lt;li&gt;ハートビートタイマーを有効にする。&lt;/li&gt;&lt;/ul&gt;                   |
| `sendPageView`  | &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;ページビューを送信する&lt;/li&gt;&lt;/ul&gt;  |


#### コンテンツトラッキング

|変数| 説明|
|---| ---|
|`trackAllContentImpressions`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;すべてのコンテンツの印象を追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`checkOnScroll`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;スクロール時の印象チェック。&lt;/li&gt;&lt;/ul&gt; |
| `watchInterval` |  &lt;ul&gt;&lt;li&gt;印象のウォッチ間隔。&lt;/li&gt;&lt;/ul&gt; |
| `impressionDomNode` |  &lt;ul&gt;&lt;li&gt;印象のDomノード。&lt;/li&gt;&lt;/ul&gt; |
|`domNode`|  &lt;ul&gt;&lt;li&gt;インタラクションのDomノード。&lt;/li&gt;&lt;/ul&gt; |
| `contentInteraction` |  &lt;ul&gt;&lt;li&gt;コンテンツインタラクション名。&lt;/li&gt;&lt;/ul&gt; |
|`contentName`|  &lt;ul&gt;&lt;li&gt;コンテンツ名。&lt;/li&gt;&lt;/ul&gt; |
|`contentPiece`|  &lt;ul&gt;&lt;li&gt;コンテンツピース。&lt;/li&gt;&lt;/ul&gt; |
|`contentTarget`|  &lt;ul&gt;&lt;li&gt;コンテンツターゲット。&lt;/li&gt;&lt;/ul&gt; |

#### ダウンロードとアウトリンクトラッキング

|変数| 説明|
|---| ---|
|`link_tracking`|  &lt;ul&gt;&lt;li&gt;ブール値&lt;/li&gt;&lt;li&gt;リンクトラッキングを有効にする。&lt;/li&gt;&lt;/ul&gt; |
|`domains`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;エイリアスドメインを無視する。&lt;/li&gt;&lt;/ul&gt; |
|`outLinkClassName`|  &lt;ul&gt;&lt;li&gt;アウトリンククラス名。&lt;/li&gt;&lt;/ul&gt; |
|`linkAddress`|  &lt;ul&gt;&lt;li&gt;リンクアドレス。&lt;/li&gt;&lt;/ul&gt; |
|`addDownloadExtensions`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;ダウンロード拡張子を追加する。&lt;/li&gt;&lt;/ul&gt; |
|`setDownloadExtensions`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;デフォルトの拡張子を置き換える。&lt;/li&gt;&lt;/ul&gt; |
|`setDownloadClassName`|  &lt;ul&gt;&lt;li&gt;ダウンロードクラス名を構成する。&lt;/li&gt;&lt;/ul&gt; |
|`time`|  &lt;ul&gt;&lt;li&gt;リンクトラッキング遅延。&lt;/li&gt;&lt;/ul&gt; |
|`setIgnoreClasses`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;アウトリンクトラッキングクラスを無効にする。&lt;/li&gt;&lt;/ul&gt; |

#### イベント

|変数| 説明|
|---| ---|
|`trackEvent`|  &lt;ul&gt;&lt;li&gt;カスタムイベントをトリガーする。&lt;/li&gt;&lt;/ul&gt; |
|`trackGoal`|  &lt;ul&gt;&lt;li&gt;ゴールのコンバージョンを追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`addEcommerceItem`|  &lt;ul&gt;&lt;li&gt;Eコマースアイテムを追加する。&lt;/li&gt;&lt;/ul&gt; |
|`trackEcommerceOrder`|  &lt;ul&gt;&lt;li&gt;Eコマースの注文を追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`trackEcommerceCartUpdate`|  &lt;ul&gt;&lt;li&gt;カートを更新する。&lt;/li&gt;&lt;/ul&gt; |
|`setEcommerceView`|  &lt;ul&gt;&lt;li&gt;商品/カテゴリビューを追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`trackAllContentImpressions`|  &lt;ul&gt;&lt;li&gt;ページ内のすべてのコンテンツの印象を追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`trackVisibleContentImpressions`|  &lt;ul&gt;&lt;li&gt;すべての表示コンテンツの印象を追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`trackContentImpressionsWithinNode`|  &lt;ul&gt;&lt;li&gt;特定のページ部分のみのコンテンツの印象を追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`trackContentInteractionNode`|  &lt;ul&gt;&lt;li&gt;自動検出で手動でインタラクションを追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`trackContentImpression`|  &lt;ul&gt;&lt;li&gt;手動で印象を追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`trackContentInteraction`|  &lt;ul&gt;&lt;li&gt;手動でユーザーのインタラクションを追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`trackLink`|  &lt;ul&gt;&lt;li&gt;JS関数を使用してダウンロードの強制追跡を行う。&lt;/li&gt;&lt;/ul&gt; |
|`setUserId`|  &lt;ul&gt;&lt;li&gt;UserIdを構成する。&lt;/li&gt;&lt;/ul&gt; |
|`resetUserId`|  &lt;ul&gt;&lt;li&gt;UserIdをリセットする。&lt;/li&gt;&lt;/ul&gt; |
|`setDocumentTitle`|  &lt;ul&gt;&lt;li&gt;カスタムページ名を構成する。&lt;/li&gt;&lt;/ul&gt; |
|`trackSiteSearch`|  &lt;ul&gt;&lt;li&gt;サイト検索を追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`setUserIsAnonymous`|  &lt;ul&gt;&lt;li&gt;ユーザーを匿名で追跡する。&lt;/li&gt;&lt;/ul&gt; |
|`deanonymizeUser`|  &lt;ul&gt;&lt;li&gt;匿名でのユーザー追跡を無効にする（訪問の同意後）。&lt;/li&gt;&lt;/ul&gt; |

#### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;注文合計&lt;/li&gt;&lt;li&gt;`_ctotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;送料&lt;/li&gt;&lt;li&gt;`_cship`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;税金&lt;/li&gt;&lt;li&gt;`_ctax`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品IDのリスト。&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前のリスト。&lt;/li&gt;&lt;li&gt;`_cprodname`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリのリスト&lt;/li&gt;&lt;li&gt;`_ccat`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_discount`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;割引のリスト。&lt;/li&gt;&lt;li&gt;`_cpdisc`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
