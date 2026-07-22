---
title: AT Internet SmartTag 構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで AT Internet SmartTag タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/at-internet-smarttag/
---
## タグのヒント

* `type` パラメータは、クリックイベントトラッキングをトリガーするために入力する必要があります。
* 現在のホストバージョンは 5.18.2 です。
* バージョン 5.13.0 以降、**Log**、**LogSSL**、および **Collection Domain** フィールドは廃止され、`collectDomain` および `collectDomainSSL` フィールドに置き換えられました。
* 詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#) ドキュメントを参照してください。
* AT Internet への直接呼び出しに使用するウィンドウレベルの変数名を構成します。
* マッピングを使用して標準構成値を動的に上書きします。
* すべてのオプションはカスタムプロパティのマッピングを受け入れます。
* Eコマース変数の一部を使用します（詳細はマッピングを参照）。

## タグの構成

まず、Tealium のタグマーケットプレイスにアクセスし、AT Internet SmartTag タグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を構成します：

* **タグバージョン**
  * **ホスト** は Tealium に直接埋め込まれた AT Internet タグです。

* **AT Internet CDN**
  * SmartTag を構成し、AT Internet CDN にデプロイする必要があります。詳細については、AT Internet アカウントにログインし、[Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。

* **ウィンドウトラッカー名**
  * タグテンプレートの外でトラッカーを使用できるように、ウィンドウレベルの変数を構成します。

* **サイトID**
  * AT Internet サイトID。
  * 詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。

* **collectDomain**
  * AT Internet データ収集ドメイン。

* **collectDomainSSL**
  * AT Internet セキュアデータ収集ドメイン。

* **Log**
  * バージョン 5.13.0 以降、廃止されました。
  * このサイトIDの AT Internet ログ。
  * 詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) コレクター用サブドメインのドキュメントを参照してください。

* **LogSSL**
  * バージョン 5.13.0 以降、廃止されました。
  * このサイトIDの AT Internet セキュアログ。
  * 詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。
  * セキュアページ用のコレクターサブドメインの Tag Composer を参照してください。

* **Collection Domain**
  * バージョン 5.13.0 以降、廃止されました。
  * `xiti.com` または `ati-host.net`、AT Internet の構成に応じて。
  * マッピングを使用してカスタムコレクションドメインを指定できます。

* **Pixel Path**
  * AT Internet ピクセルリクエストの URL パス。
  * デフォルトは `/hit.xiti` です。

* **Cookie Domain**
  * あなたのサイトの URL。
  * 構成が正しくない場合、ユニークビジターの計算に問題が生じる可能性があります。

* **Secure**
  * 情報を安全に送信するために有効にします。

* **Cookie Secure**
  * `true` に構成すると、トラッカークッキーの書き込みに `secure` オプションを追加することができます（最初に）。
  * セキュアクッキーは HTTPS ページでのみ機能することに注意してください。

* **最初の拡張機能は構成です**
  * AT Internet または Tealium の担当者から指示があった場合にのみ有効にします。
  * スコープ付き拡張機能リストから最初の拡張機能を取り、他の拡張機能の前に実行し、最初の拡張機能からの構成を使用してトラッカーを構築します。

* **OptOut時にヒットを送信**
  * ユーザーが「OPT-OUT」モードの場合に匿名ヒットを送信することができます（ファーストパーティ）。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`window_var`|  <ul><li>ウィンドウトラッカー名</li><li>タグテンプレートの外でトラッカーを使用できるように、ウィンドウレベルの変数を構成します。</li></ul> |
|`config.site`|  <ul><li>AT Internet サイトID。</li><li>詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。</li></ul> |
|`config.collectDomain`|  <ul><li>AT Internet データ収集ドメイン。</li></ul> |
|`config.collectDomainSSL`|  <ul><li>AT Internet セキュアデータ収集ドメイン。</li></ul> |
|`config.log`|  <ul><li>バージョン 5.13.0 以降、Log は廃止されました。</li></ul> |
|`config.logSSL`|  <ul><li>バージョン 5.13.0 以降、廃止されました。</li><li>このサイトIDの AT Internet セキュアログ。</li><li>詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。</li><li>セキュアページ用のコレクターサブドメインの Tag Composer を参照してください。</li></ul> |
|`config.domain`|  <ul><li>バージョン 5.13.0 以降、廃止されました。</li><li>コレクションドメイン。</li><li>`xiti.com` または `ati-host.net`、AT Internet の構成に応じて。</li><li>マッピングを使用してカスタムコレクションドメインを指定できます。</li></ul> |
|`config.pixelPath`|  <ul><li>AT Internet ピクセルリクエストの URL パス。</li><li>デフォルトは `/hit.xiti` です。</li></ul> |
|`config.secure`|  <ul><li>情報を安全に送信するために有効にします。</li></ul> |
|`config.cookieSecure`|  <ul><li>**true** に構成すると、トラッカークッキーの書き込みに `secure` オプションを追加することができます（最初に）。</li><li>セキュアクッキーは HTTPS ページでのみ機能することに注意してください。</li></ul> |
|`config.disableCookie`|  <ul><li>Cookie を無効にします。</li></ul> |
|`config.cookieDomain`|  <ul><li>Cookie ドメイン。</li><li>あなたのサイトの URL。</li><li>構成が正しくない場合、ユニークビジターの計算に問題が生じる可能性があります。</li></ul> |
|`config.preview`|  <ul><li>プレビュー。</li></ul> |
|`config.sendHitWhenOptOut`|  <ul><li>ユーザーが「OPT-OUT」モードの場合に匿名ヒットを送信することができます（ファーストパーティ）。</li></ul> |

### コンテキスト

|変数| 説明|
|---| ---|
|`context.forcedCampaign`| 強制キャンペーン。|
|`context.forcedReferer`| 強制リファラー。|

### Eコマース - イベント

追加情報については、[カートイベント（セールスインサイト）](https://developers.atinternet-solutions.com/javascript-en/ecommerce-javascript-en/sales-insights-javascript-en/cart-events-sales-insights-javascript-fr/?kw=cartdisplay#cart-display_2)を参照してください。

|変数| 説明|
|---| ---|
|`order`|  <ul><li>注文</li></ul> |
|`cart`|  <ul><li>カート</li></ul> |
|`prod`|  <ul><li>商品表示</li></ul> |
|`aisle`|  <ul><li>通路</li></ul> |
|`transactionconfirm`|  <ul><li>取引確認</li></ul> |
|`cartdisplay`|  <ul><li>カート表示</li></ul> |
|`cartupdate`|  <ul><li>カート更新</li></ul> |
|`displayshipping`|  <ul><li>配送ステップの表示</li></ul> |
|`displaypayment`|  <ul><li>支払いステップの表示</li></ul> |
|`cartawaitingpayment`|  <ul><li>支払い待ちのカート</li></ul> |
|`productdisplay`|  <ul><li>商品表示</li></ul> |
|`productpagedisplay`|  <ul><li>商品ページ表示</li></ul> |
|`productaddition`| <ul><li>商品追加</li></ul> |
|`productremoval`|  <ul><li>商品削除</li></ul> |
### E-コマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID。</li><li>`_corder`を上書き。</li></ul> |
|`order_total`|  <ul><li>注文合計。</li><li>`_ctotal`を上書き。</li></ul> |
|`order_subtotal`|  <ul><li>注文小計。</li><li>`_csubtotal`を上書き。</li></ul> |
|`order_shipping`|  <ul><li>送料。</li><li>`_cship`を上書き。</li></ul> |
|`order_tax`|  <ul><li>税金。</li><li>`_ctax`を上書き。</li></ul> |
|`order_coupon_code`|  <ul><li>プロモーションコード。</li><li>`_cpromo`を上書き。</li></ul> |
|`product_id`|  <ul><li>配列。</li><li>商品IDのリスト。</li><li>`_cprod`を上書き。</li></ul> |
|`product_name`|  <ul><li>配列。</li><li>商品名のリスト。</li><li>`_cprodname`を上書き。</li></ul> |
|`product_sku`|  <ul><li>配列。</li><li>SKUのリスト。</li><li>`_csku`を上書き。</li></ul> |
|`product_brand`|  <ul><li>配列。</li><li>ブランドのリスト。</li><li>`_cbrand`を上書き。</li></ul> |
|`product_category`|  <ul><li>配列。</li><li>カテゴリのリスト。</li><li>`_ccat`を上書き。</li></ul> |
|`product_subcategory`|  <ul><li>配列。</li><li>サブカテゴリのリスト。</li><li>`_ccat2`を上書き。</li></ul> |
|`product_quantity`|  <ul><li>配列。</li><li>数量のリスト。</li><li>`_cquan`を上書き。</li></ul> |
|`product_unit_price`|  <ul><li>配列。</li><li>価格のリスト。</li><li>`_cprice`を上書き。</li></ul> |
|`product_discount`|  <ul><li>配列。</li><li>割引のリスト。</li><li>`_cpdisc`を上書き。</li></ul> |
|`customer_id`|  <ul><li>顧客ID。</li><li>`_ccustid`を上書き。</li></ul> |

### 訪問

|変数| 説明|
|---| ---|
|`visitor.id`|  <ul><li>顧客ID。</li><li>`_ccustid`を上書き。</li></ul> |
|`visitor.category`|  <ul><li>カテゴリ。</li></ul> |
|`visitor.###`|  <ul><li>カスタムプロパティ。</li></ul> |

### サイト内広告

|変数| 説明|
|---| ---|
|`promo.adId`|  <ul><li>作成されるID。</li></ul> |
| `promo.adId` |  <ul><li>広告形式を示すID。</li></ul> |
|`promo.productId`|  <ul><li>関連商品のID。</li></ul> |
|`promo.###`|  <ul><li>カスタムマッピング。</li></ul> |

### カスタム変数

|変数| 説明|
|---| ---|
|`param.###`|  setParamの値 |
|--カスタム変数--| カスタム変数。|
| `cv.site.###` | サイトのカスタム変数。|
|`cv.page.###`|  ページのカスタム変数。 |
|`cv.###.###`| カスタム変数。|

### 動的ラベル

|変数| 説明|
|---| ---|
|`dynlabel.pageId`|  <ul><li>動的ページID</li></ul> |
|`dynlabel.update`|  <ul><li>名前変更の日付</li></ul> |
| `dynlabel.chapter1` |  <ul><li>レベル1の章の名前。</li></ul> |
|`dynlabel.chapter2`|  <ul><li>レベル2の章の名前。</li></ul> |
|`dynlabel.chapter3`|  <ul><li>レベル3の章の名前。</li></ul> |
|`dynlabel.chapter#`|  <ul><li>レベル#の章の名前。</li></ul> |

### サイト内検索

|変数| 説明|
|---| ---|
|`intsearch.keyword`|  <ul><li>検索キーワード。</li></ul> |
|`intsearch.resultPageNumber`|  <ul><li>検索結果ページ番号。</li></ul> |
| `intsearch.resultPosition` |  <ul><li>検索結果の位置。</li></ul> |

### MV (多変量) テスト

|変数| 説明|
|---| ---|
| `mvtesting.set.test` |  <ul><li>テストIDと名前。</li></ul> |
|`mvtesting.set.waveId`|  <ul><li>ウェーブID。</li></ul> |
|`mvtesting.set.creation`|  <ul><li>作成IDと名前。</li></ul> |
| `mvtesting.set.###` |  <ul><li>カスタムセットマッピング。</li></ul> |
|`mvtesting.add.variable`|  <ul><li>CSV/配列。</li><li>テスト変数。</li></ul> |
|`mvtesting.add.version`|  <ul><li>CSV/配列。</li><li>テストバージョン。</li></ul> |
| `mvtesting.add.###` |  <ul><li>カスタム追加マッピング。</li></ul> |

### リッチメディア

|変数| 説明|
|---| ---|
|`richmedia.add.mediaType`|  <ul><li>メディアタイプ。</li><li>値は:  <ul><li>`video`</li><li>`audio`</li><li>`vpost`</li></ul> </li></ul> |
|```richmedia.add.playerId```|  <ul><li>プレイヤーID。</li></ul> |
| `richmedia.add.mediaLevel2` |  <ul><li>メディアレベル2。</li></ul> |
|`richmedia.add.mediaLabel`|  <ul><li>メディアラベル。</li></ul> |
|`richmedia.add.isEmbedded`|  <ul><li>埋め込みかどうか。</li><li>値は `int` または `ext`。</li></ul> |
|`richmedia.add.broadcastMode`|  <ul><li>放送モード。</li><li>値は `live` または `clip`。</li></ul> |
| `richmedia.add.webdomain` |  <ul><li>外部配置のウェブドメイン</li></ul> |
| `richmedia.add.duration` |  <ul><li>持続時間。</li></ul> |
|`richmedia.send.action`|  <ul><li>送信アクション。</li><li>値は:  <ul><li>`play`</li><li>`pause`</li><li>`stop`</li><li>`info`</li><li>`move`</li></ul> </li></ul> |
|`richmedia.send.playerId`|  <ul><li>プレイヤーID。</li></ul> |
|`richmedia.send.mediaLabel`|  <ul><li>メディアラベル。</li></ul> |
|`richmedia.send.isBuffering`|  <ul><li>バッファリング中かどうか。</li><li>値は:  <ul><li>`1` - バッファリング開始</li><li>`0` - バッファリング終了</li></ul> </li></ul> |
|`richmedia.remove`|  <ul><li>プレイヤーを削除。</li></ul> |
|`richmedia.removeAll`|  <ul><li>すべてのプレイヤーを削除</li><li>値は `true` または `false`。</li></ul> |

### モバイル

|変数| 説明|
|---| ---|
|`mob.apvr`|  <ul><li>アプリバージョン。</li></ul> |
|`mob.ref`|  <ul><li>リファラー。</li></ul> |
|`mob.stc`|  <ul><li>オブジェクト。</li><li>ライフサイクル。</li></ul> |
|`mob.stc.lc`|  <ul><li>オブジェクト。</li><li>ライフサイクル。</li></ul> |
|`mob.stc.lc.sessionId`|  <ul><li>セッションID。</li></ul> |
|`mob.stc.lc.fl`|  <ul><li>初回起動。</li><li>`lifecycle_isfirstlaunch`を上書き。</li><li>値は `0` または `1`。</li></ul> |
|`mob.stc.lc.flau`|  <ul><li>アップデート以降の初回起動。</li><li>`lifecycle_isfirstlaunchupdate`を上書き。</li><li>値は `0` または `1`。</li></ul> |
|`mob.stc.lc.lc`|  <ul><li>数値。</li><li>起動回数。</li><li>`lifecycle_totallaunchcount`を上書き。</li></ul> |
|`mob.stc.lc.ldc`|  <ul><li>数値。</li><li>その日の起動回数。</li></ul> |
|`mob.stc.lc.lwc`|  <ul><li>数値。</li><li>その週の起動回数。</li></ul> |
|`mob.stc.lc.lmc`|  <ul><li>数値。</li><li>その月の起動回数。</li></ul> |
|`mob.stc.lc.lcsu`|  <ul><li>数値。</li><li>最後のアップデート以降の起動回数。</li></ul> |
| `mob.stc.lc.fld` |  <ul><li>初回起動日。</li><li>`lifecycle_firstlaunchdate`を上書き。</li><li>日付形式は `yyyymmdd`。</li></ul> |
|`mob.stc.lc.dsfl`|  <ul><li>数値。</li><li>初回起動からの日数。</li><li>`lifecycle_firstlaunchdate`から計算。</li></ul> |
|`mob.stc.lc.uld`|  <ul><li>最後のアップデート以降の初回起動日。</li><li>`lifecycle_updatelaunchdate`を上書き。</li><li>日付形式は `yyyymmdd`。</li></ul> |
|`mob.stc.lc.dsu`|  <ul><li>数値。</li><li>アップデート以降の初回起動からの日数。</li><li>`lifecycle_dayssinceupdate`を上書き。</li></ul> |
|`mob.stc.lc.dslu`|  <ul><li>数値。</li><li>最後の使用からの日数。</li><li>`lifecycle_lastlaunchdate`から計算。</li></ul> |

### カスタムツリー構造

|変数| 説明|
|---| ---|
|`customTreeStructure.category1`|  <ul><li>カテゴリーレベル1</li></ul> |
|`customTreeStructure.category2`|  <ul><li>カテゴリーレベル2</li></ul> |
|`customTreeStructure.category3`|  <ul><li>カテゴリーレベル3</li></ul> |

### キャンペーン

|変数| 説明|
|---| ---|
|`xtor`|  <ul><li>キャンペーンID。</li></ul> |