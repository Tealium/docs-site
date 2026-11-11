---
title: Piwik PROタグ構成ガイド
description: この記事では、タグ管理アカウントでPiwik PROタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/piwik-pro-tag/
---
## タグに関するヒント

* 注文IDが存在する場合、Eコマース注文追跡イベントが発生します。
* マッピングを使用すると、次のことができます。
  * 標準構成値を動的に上書きする
  * イベントトリガーを構成する
  * カスタムディメンションを構成する
  * Eコマース拡張機能の値を上書きする
* 次のEコマース拡張機能パラメーターをサポートしています。
  * 注文ID（`_corder`）
  * 注文合計（`_ctotal`）
  * 小計（`_csubtotal`）
  * 配送料（`_cship`）
  * 税額（`_ctax`）
  * カートまたは注文タイプ（`_ctype`）
  * 顧客ID（`_ccustid`）
  * 商品IDのリスト（`_cprod`）
  * 名前のリスト（`_cprodname`）
  * カテゴリーのリスト（`_ccat`）
  * 数量のリスト（`_cquan`）
  * 価格のリスト（`_cprice`）
  * 割引のリスト（`_cpdisc`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **アプリID**
  * PPASアプリケーション識別子（旧称：WebサイトID、サイトID、またはidSite）。

* **ベースURL**
  * 末尾にスラッシュを付けないPPASインスタンスURL。
  * 先頭に`//`を含めます。
  * 例：`//example.com`

* **ダウンロードおよび外部リンクのトラッキングを有効にする**

* **ページ内のすべてのコンテンツインプレッションをトラッキングする**  
コンテンツをトラッキングするには、data-track-content属性または`piwikTrackContent` CSSクラスが付与されている必要があります。

* **表示されているすべてのコンテンツインプレッションをトラッキングする**  
コンテンツをトラッキングするには、data-track-content属性または`piwikTrackContent` CSSクラスが付与されている必要があります。

* **スクロール時にインプレッションを確認**
  * スクロールイベント時に、新しく表示されたコンテンツのインプレッションを確認します。
  * スクロール可能な要素内に配置されたコンテンツブロックは検出されません。

* **表示コンテンツの監視間隔**
  * 新しく表示されたコンテンツを確認する間隔（ミリ秒）。
  * パフォーマンス上の理由から、`0`に構成すると定期的な確認を無効にできます。

* **ハートビートタイマー**
  * 定期的なハートビートリクエストの間隔（秒）。

* **ユーザーを匿名でトラッキング**
  * 訪問を匿名でトラッキングします（同意なし）。
  
* **ハートビートタイマーを有効にする**

* **ページビューを送信**
  * ページビューイベントはサイトで自動的に記録されます。スニペットからページビューイベントを送信しない場合は、このオプションを`false`に構成します。

### データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

#### 標準

| 変数                                 | 説明                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| `appId`                              | <ul><li>アプリID。</li></ul>                                 |
| `base_url`                           | <ul><li>PPASインスタンスのアドレス。</li></ul>               |
| `tracking_url`                       | <ul><li>アナリティクストラッカーのURL。</li></ul>             |
| `category`                           | <ul><li>イベントカテゴリー。</li></ul>                        |
| `action`                             | <ul><li>イベントアクション。</li></ul>                        |
| `name`                               | <ul><li>イベント名。</li></ul>                                |
| `value`                              | <ul><li>イベント値。</li></ul>                                |
| `goal_name`                          | <ul><li>ゴール名。</li></ul>                                  |
| `goal_value`                         | <ul><li>ゴール値。</li></ul>                                  |
| `title`                              | <ul><li>カスタムページ名／ドキュメントタイトル。</li></ul>    |
| `beat`                               | <ul><li>ハートビートリクエストの間隔。</li></ul>              |
| `keyword`                            | <ul><li>キーワード</li></ul>                                 |
| `searchCount`                        | <ul><li>検索件数</li></ul>                                   |
| `isAnonymous`                        | <ul><li>ブール値</li><li>匿名トラッキングを有効にします。</li></ul> |
| `CustomUrl`                          | <ul><li>カスタムURL</li></ul>                                |
| `ReferrerUrl`                        | <ul><li>参照元URL。</li></ul>                                |
| `cookieDomain`                       | <ul><li>Cookieドメイン。</li></ul>                            |
| `cookiePath`                         | <ul><li>Cookieパス。</li></ul>                                |
| `updateTimingDataOnPageLoadSampling` | <ul><li>ページ読み込み時のサンプリングでタイミングデータを更新します。</li></ul> |
| `enableHeartBeatTimer`               | <ul><li>ハートビートタイマーを有効にします。</li></ul>        |
| `sendPageView`                       | <ul><li>ブール値</li><li>ページビューを送信します。</li></ul> |

#### コンテンツトラッキング

|変数| 説明|
|---| ---|
|`trackAllContentImpressions`| <ul><li>ブール値</li><li>すべてのコンテンツインプレッションをトラッキングします。</li></ul> |
|`checkOnScroll`| <ul><li>ブール値</li><li>スクロール時にインプレッションを確認します。</li></ul> |
| `watchInterval` | <ul><li>インプレッションの監視間隔。</li></ul> |
| `impressionDomNode` | <ul><li>インプレッションのDOMノード。</li></ul> |
|`domNode`| <ul><li>インタラクションのDOMノード。</li></ul> |
| `contentInteraction` | <ul><li>コンテンツインタラクション名。</li></ul> |
|`contentName`| <ul><li>コンテンツ名。</li></ul> |
|`contentPiece`| <ul><li>コンテンツ要素。</li></ul> |
|`contentTarget`| <ul><li>コンテンツターゲット。</li></ul> |

#### ダウンロードおよび外部リンクのトラッキング

|変数| 説明|
|---| ---|
|`link_tracking`| <ul><li>ブール値</li><li>リンクトラッキングを有効にします。</li></ul> |
|`domains`| <ul><li>配列</li><li>エイリアスドメインを無視します。</li></ul> |
|`outLinkClassName`| <ul><li>外部リンクのクラス名。</li></ul> |
|`linkAddress`| <ul><li>リンクアドレス。</li></ul> |
|`addDownloadExtensions`| <ul><li>配列</li><li>ダウンロード拡張子を追加します。</li></ul> |
|`setDownloadExtensions`| <ul><li>配列</li><li>デフォルトの拡張子を置き換えます。</li></ul> |
|`setDownloadClassName`| <ul><li>ダウンロードのクラス名を構成します。</li></ul> |
|`time`| <ul><li>リンクトラッキングの遅延。</li></ul> |
|`setIgnoreClasses`| <ul><li>配列</li><li>外部リンクトラッキングを無効にするクラス。</li></ul> |

#### イベント

|変数| 説明|
|---| ---|
|`trackEvent`| <ul><li>カスタムイベントをトリガーします。</li></ul> |
|`trackGoal`| <ul><li>ゴールコンバージョンをトラッキングします。</li></ul> |
|`addEcommerceItem`| <ul><li>Eコマース商品を追加します。</li></ul> |
|`trackEcommerceOrder`| <ul><li>Eコマース注文をトラッキングします。</li></ul> |
|`trackEcommerceCartUpdate`| <ul><li>カートを更新します。</li></ul> |
|`setEcommerceView`| <ul><li>商品／カテゴリーの閲覧をトラッキングします。</li></ul> |
|`trackAllContentImpressions`| <ul><li>ページ内のすべてのコンテンツインプレッションをトラッキングします。</li></ul> |
|`trackVisibleContentImpressions`| <ul><li>表示されているすべてのコンテンツインプレッションをトラッキングします。</li></ul> |
|`trackContentImpressionsWithinNode`| <ul><li>ページの特定部分にあるコンテンツのインプレッションのみをトラッキングします。</li></ul> |
|`trackContentInteractionNode`| <ul><li>自動検出を使用してインタラクションを手動でトラッキングします。</li></ul> |
|`trackContentImpression`| <ul><li>インプレッションを手動でトラッキングします。</li></ul> |
|`trackContentInteraction`| <ul><li>ユーザーインタラクションを手動でトラッキングします。</li></ul> |
|`trackLink`| <ul><li>JS関数を使用してダウンロードを強制的にトラッキングします。</li></ul> |
|`setUserId`| <ul><li>ユーザーIDを構成します。</li></ul> |
|`resetUserId`| <ul><li>ユーザーIDをリセットします。</li></ul> |
|`setDocumentTitle`| <ul><li>カスタムページ名を構成します。</li></ul> |
|`trackSiteSearch`| <ul><li>サイト内検索をトラッキングします。</li></ul> |
|`setUserIsAnonymous`| <ul><li>ユーザーを匿名でトラッキングします。</li></ul> |
|`deanonymizeUser`| <ul><li>ユーザーの匿名トラッキングを無効にします（訪問の同意取得後）。</li></ul> |
#### Eコマース

|変数|説明|
|---|---|
|`order_id`| <ul><li>注文ID</li><li>`_corder`をオーバーライドします。</li></ul> |
|`order_total`| <ul><li>注文合計額</li><li>`_ctotal`をオーバーライドします。</li></ul> |
|`order_subtotal`| <ul><li>小計</li><li>`_csubtotal`をオーバーライドします。</li></ul> |
|`order_shipping`| <ul><li>配送料</li><li>`_cship`をオーバーライドします。</li></ul> |
|`order_tax`| <ul><li>税額</li><li>`_ctax`をオーバーライドします。</li></ul> |
|`customer_id`| <ul><li>顧客ID</li><li>`_ccustid`をオーバーライドします。</li></ul> |
|`product_id`| <ul><li>配列</li><li>商品IDのリスト。</li><li>`_cprod`をオーバーライドします。</li></ul> |
|`product_name`| <ul><li>配列</li><li>商品名のリスト。</li><li>`_cprodname`をオーバーライドします。</li></ul> |
|`product_category`| <ul><li>配列</li><li>カテゴリーのリスト</li><li>`_ccat`をオーバーライドします。</li></ul> |
|`product_quantity`| <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`をオーバーライドします。</li></ul> |
|`product_unit_price`| <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`をオーバーライドします。</li></ul> |
|`product_discount`| <ul><li>配列</li><li>割引のリスト。</li><li>`_cpdisc`をオーバーライドします。</li></ul> |