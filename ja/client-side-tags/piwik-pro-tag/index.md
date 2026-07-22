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

まず、Tealiumのタグマーケットプレイスに移動し、Piwik PROタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

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

マッピングとは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

#### 標準

| 変数                             | 説明                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| `appId`                              | <ul><li>App ID。</li></ul>                                    |
| `base_url`                           | <ul><li>PPASインスタンスアドレス。</li></ul>                     |
| `tracking_url`                       | <ul><li>Analytics Tracker URL。</li></ul>                     |
| `category`                           | <ul><li>イベントカテゴリ。</li></ul>                            |
| `action`                             | <ul><li>イベントアクション。</li></ul>                              |
| `name`                               | <ul><li>イベント名。</li></ul>                                |
| `value`                              | <ul><li>イベント値。</li></ul>                               |
| `goal_name`                          | <ul><li>ゴール名。</li></ul>                                 |
| `goal_value`                         | <ul><li>ゴール値。</li></ul>                                |
| `title`                              | <ul><li>カスタムページ名/ドキュメントタイトル。</li></ul>           |
| `beat`                               | <ul><li>ハートビートリクエスト間の時間。</li></ul>           |
| `keyword`                            | <ul><li>キーワード</li></ul>                                    |
| `searchCount`                        | <ul><li>検索数</li></ul>                               |
| `isAnonymous`                        | <ul><li>ブール値</li><li>匿名トラッキングを有効にする。</li></ul> |
| `CustomUrl`                          | <ul><li>カスタムURL</li></ul>                                 |
| `ReferrerUrl`                        | <ul><li>リファラーURL。</li></ul>                              |
| `cookieDomain`                       | <ul><li>Cookieドメイン。</li></ul>                             |
| `cookiePath`                         | <ul><li>Cookieパス。</li></ul>                               |
| `updateTimingDataOnPageLoadSampling` | <ul><li>ページロードサンプリング時にタイミングデータを更新する。</li></ul>  |
| `enableHeartBeatTimer`               | <ul><li>ハートビートタイマーを有効にする。</li></ul>                   |
| `sendPageView`  | <ul><li>ブール値</li><li>ページビューを送信する</li></ul>  |


#### コンテンツトラッキング

|変数| 説明|
|---| ---|
|`trackAllContentImpressions`|  <ul><li>ブール値</li><li>すべてのコンテンツの印象を追跡する。</li></ul> |
|`checkOnScroll`|  <ul><li>ブール値</li><li>スクロール時の印象チェック。</li></ul> |
| `watchInterval` |  <ul><li>印象のウォッチ間隔。</li></ul> |
| `impressionDomNode` |  <ul><li>印象のDomノード。</li></ul> |
|`domNode`|  <ul><li>インタラクションのDomノード。</li></ul> |
| `contentInteraction` |  <ul><li>コンテンツインタラクション名。</li></ul> |
|`contentName`|  <ul><li>コンテンツ名。</li></ul> |
|`contentPiece`|  <ul><li>コンテンツピース。</li></ul> |
|`contentTarget`|  <ul><li>コンテンツターゲット。</li></ul> |

#### ダウンロードとアウトリンクトラッキング

|変数| 説明|
|---| ---|
|`link_tracking`|  <ul><li>ブール値</li><li>リンクトラッキングを有効にする。</li></ul> |
|`domains`|  <ul><li>配列</li><li>エイリアスドメインを無視する。</li></ul> |
|`outLinkClassName`|  <ul><li>アウトリンククラス名。</li></ul> |
|`linkAddress`|  <ul><li>リンクアドレス。</li></ul> |
|`addDownloadExtensions`|  <ul><li>配列</li><li>ダウンロード拡張子を追加する。</li></ul> |
|`setDownloadExtensions`|  <ul><li>配列</li><li>デフォルトの拡張子を置き換える。</li></ul> |
|`setDownloadClassName`|  <ul><li>ダウンロードクラス名を構成する。</li></ul> |
|`time`|  <ul><li>リンクトラッキング遅延。</li></ul> |
|`setIgnoreClasses`|  <ul><li>配列</li><li>アウトリンクトラッキングクラスを無効にする。</li></ul> |

#### イベント

|変数| 説明|
|---| ---|
|`trackEvent`|  <ul><li>カスタムイベントをトリガーする。</li></ul> |
|`trackGoal`|  <ul><li>ゴールのコンバージョンを追跡する。</li></ul> |
|`addEcommerceItem`|  <ul><li>Eコマースアイテムを追加する。</li></ul> |
|`trackEcommerceOrder`|  <ul><li>Eコマースの注文を追跡する。</li></ul> |
|`trackEcommerceCartUpdate`|  <ul><li>カートを更新する。</li></ul> |
|`setEcommerceView`|  <ul><li>商品/カテゴリビューを追跡する。</li></ul> |
|`trackAllContentImpressions`|  <ul><li>ページ内のすべてのコンテンツの印象を追跡する。</li></ul> |
|`trackVisibleContentImpressions`|  <ul><li>すべての表示コンテンツの印象を追跡する。</li></ul> |
|`trackContentImpressionsWithinNode`|  <ul><li>特定のページ部分のみのコンテンツの印象を追跡する。</li></ul> |
|`trackContentInteractionNode`|  <ul><li>自動検出で手動でインタラクションを追跡する。</li></ul> |
|`trackContentImpression`|  <ul><li>手動で印象を追跡する。</li></ul> |
|`trackContentInteraction`|  <ul><li>手動でユーザーのインタラクションを追跡する。</li></ul> |
|`trackLink`|  <ul><li>JS関数を使用してダウンロードの強制追跡を行う。</li></ul> |
|`setUserId`|  <ul><li>UserIdを構成する。</li></ul> |
|`resetUserId`|  <ul><li>UserIdをリセットする。</li></ul> |
|`setDocumentTitle`|  <ul><li>カスタムページ名を構成する。</li></ul> |
|`trackSiteSearch`|  <ul><li>サイト検索を追跡する。</li></ul> |
|`setUserIsAnonymous`|  <ul><li>ユーザーを匿名で追跡する。</li></ul> |
|`deanonymizeUser`|  <ul><li>匿名でのユーザー追跡を無効にする（訪問の同意後）。</li></ul> |

#### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`order_total`|  <ul><li>注文合計</li><li>`_ctotal`を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul> |
|`order_shipping`|  <ul><li>送料</li><li>`_cship`を上書きします。</li></ul> |
|`order_tax`|  <ul><li>税金</li><li>`_ctax`を上書きします。</li></ul> |
|`customer_id`|  <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>商品IDのリスト。</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト。</li><li>`_cprodname`を上書きします。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリのリスト</li><li>`_ccat`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li></ul> |
|`product_discount`|  <ul><li>配列</li><li>割引のリスト。</li><li>`_cpdisc`を上書きします。</li></ul> |
