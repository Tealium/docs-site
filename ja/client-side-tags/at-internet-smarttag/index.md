---
title: AT Internet SmartTag セットアップガイド
description: この記事では、タグ管理アカウントで AT Internet SmartTag タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/at-internet-smarttag/
---
## タグに関するヒント

* クリックイベントのトラッキングを開始するには、`type` パラメータに値を構成する必要があります。
* 現在のホストバージョンは 5.18.2 です。
* バージョン 5.13.0 以降、**Log**、**LogSSL**、**Collection Domain** の各フィールドは非推奨となり、`collectDomain` および `collectDomainSSL` フィールドに置き換えられました。
* 詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#) ドキュメントを参照してください。
* AT Internet を直接呼び出す際に使用するウィンドウレベルの変数名を構成します。
* マッピングを使用して、標準の構成値を動的に上書きします。
* すべてのオプションでカスタムプロパティのマッピングを使用できます。
* 一部の E コマース変数を使用します（詳細についてはマッピングを参照してください）。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **Tag Version**
  * **Hosted** は、Tealium に直接埋め込まれた AT Internet タグです。

* **AT Internet CDN**
  * SmartTag を構成し、AT Internet CDN にデプロイする必要があります。詳細については、AT Internet アカウントにログインし、[Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。

* **Window Tracker Name**
  * タグテンプレートの外部でトラッカーを使用できるように、ウィンドウレベルの変数を構成します。

* **Site ID**
  * AT Internet のサイト ID。
  * 詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。

* **collectDomain**
  * AT Internet のデータ収集ドメイン。

* **collectDomainSSL**
  * AT Internet のセキュアなデータ収集ドメイン。

* **Log**
  * バージョン 5.13.0 以降は非推奨です。
  * このサイト ID の AT Internet ログ。
  * 詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) にあるコレクターのサブドメインに関するドキュメントを参照してください。

* **LogSSL**
  * バージョン 5.13.0 以降は非推奨です。
  * このサイト ID の AT Internet セキュアログ。
  * 詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。
  * セキュアページについては、Tag Composer のコレクター用サブドメインを参照してください。

* **Collection Domain**
  * バージョン 5.13.0 以降は非推奨です。
  * AT Internet の構成に応じて、`xiti.com `または `ati-host.net`。
  * マッピングを使用して、カスタム収集ドメインを指定できます。

* **Pixel Path**
  * AT Internet のピクセルリクエスト URL パス。
  * デフォルトは `/hit.xiti` です。

* **Cookie Domain**
  * サイトの URL。
  * 構成が正しくない場合、ユニークビジターの計算で問題が発生する可能性があります。

* **Secure**
  * 情報をセキュアな方法で送信できるようにします。

* **Cookie Secure**
  * `true` に構成すると、トラッカーCookieの書き込み（ファーストパーティー）に `secure` オプションを追加できます。
  * セキュアCookieは HTTPS ページでのみ機能することに注意してください。

* **First extension is settings**
  * AT Internet または Tealium の担当者から指示された場合にのみ有効にしてください。
  * スコープ構成された拡張機能のリストから最初の拡張機能を取得し、他の拡張機能よりも前に実行します。その後、最初の拡張機能の構成を使用してトラッカーを構築します。

* **Send Hit When OptOut**
  * ユーザーが「OPT-OUT」モード（ファーストパーティー）の場合でも、匿名ヒットを送信できるようにします。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`window_var`| <ul><li>ウィンドウトラッカー名</li><li>タグテンプレートの外部でトラッカーを使用できるように、ウィンドウレベルの変数を構成します。</li></ul> |
|`config.site`| <ul><li>AT Internet のサイト ID。</li><li>詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。</li></ul> |
|`config.collectDomain`| <ul><li>AT Internet のデータ収集ドメイン。</li></ul> |
|`config.collectDomainSSL`| <ul><li>AT Internet のセキュアなデータ収集ドメイン。</li></ul> |
|`config.log`| <ul><li>Log はバージョン 5.13.0 以降、非推奨です。</li></ul> |
|`config.logSSL`| <ul><li>バージョン 5.13.0 以降は非推奨です。</li><li>このサイト ID の AT Internet セキュアログ。</li><li>詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。</li><li>セキュアページについては、Tag Composer のコレクター用サブドメインを参照してください。</li></ul> |
|`config.domain`| <ul><li>バージョン 5.13.0 以降は非推奨です。</li><li>収集ドメイン。</li><li>AT Internet の構成に応じて、`xiti.com` または `ati-host.net`。</li><li>マッピングを使用して、カスタム収集ドメインを指定できます。</li></ul> |
|`config.pixelPath`| <ul><li>AT Internet のピクセルリクエスト URL パス。</li><li>デフォルトは `/hit.xiti` です。</li></ul> |
|`config.secure`| <ul><li>情報をセキュアな方法で送信できるようにします。</li></ul> |
|`config.cookieSecure`| <ul><li>**true** に構成すると、トラッカーCookieの書き込み（ファーストパーティー）に `secure` オプションを追加できます。</li><li>セキュアCookieは HTTPS ページでのみ機能することに注意してください。</li></ul> |
|`config.disableCookie`| <ul><li>Cookieを無効にします。</li></ul> |
|`config.cookieDomain`| <ul><li>Cookieドメイン。</li><li>サイトの URL。</li><li>構成が正しくない場合、ユニークビジターの計算で問題が発生する可能性があります。</li></ul> |
|`config.preview`| <ul><li>プレビュー。</li></ul> |
|`config.sendHitWhenOptOut`| <ul><li>ユーザーが「OPT-OUT」モード（ファーストパーティー）の場合でも、匿名ヒットを送信できるようにします。</li></ul> |

### コンテキスト

|変数|説明|
|---|---|
|`context.forcedCampaign`|強制キャンペーン。|
|`context.forcedReferer`|強制リファラー。|

### E コマース - イベント

詳細については、[カートイベント（Sales Insights）](https://developers.atinternet-solutions.com/javascript-en/ecommerce-javascript-en/sales-insights-javascript-en/cart-events-sales-insights-javascript-fr/?kw=cartdisplay#cart-display_2)を参照してください。

|変数|説明|
|---|---|
|`order`| <ul><li>注文</li></ul> |
|`cart`| <ul><li>カート</li></ul> |
|`prod`| <ul><li>商品の表示</li></ul> |
|`aisle`| <ul><li>売り場</li></ul> |
|`transactionconfirm`| <ul><li>取引の確認</li></ul> |
|`cartdisplay`| <ul><li>カートの表示</li></ul> |
|`cartupdate`| <ul><li>カートの更新</li></ul> |
|`displayshipping`| <ul><li>配送ステップの表示</li></ul> |
|`displaypayment`| <ul><li>支払いステップの表示</li></ul> |
|`cartawaitingpayment`| <ul><li>支払い待ちのカート</li></ul> |
|`productdisplay`| <ul><li>商品の表示</li></ul> |
|`productpagedisplay`| <ul><li>商品ページの表示</li></ul> |
|`productaddition`| <ul><li>商品の追加</li></ul> |
|`productremoval`| <ul><li>商品の削除</li></ul> |
### Eコマース

|変数|説明|
|---|---|
|`order_id`| <ul><li>注文ID。</li><li>`_corder`を上書きします。</li></ul> |
|`order_total`| <ul><li>注文合計。</li><li>`_ctotal`を上書きします。</li></ul> |
|`order_subtotal`| <ul><li>注文小計。</li><li>`_csubtotal`を上書きします。</li></ul> |
|`order_shipping`| <ul><li>送料。</li><li>`_cship`を上書きします。</li></ul> |
|`order_tax`| <ul><li>税額。</li><li>`_ctax`を上書きします。</li></ul> |
|`order_coupon_code`| <ul><li>プロモーションコード。</li><li>`_cpromo`を上書きします。</li></ul> |
|`product_id`| <ul><li>配列。</li><li>商品IDのリスト。</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`| <ul><li>配列。</li><li>名前のリスト。</li><li>`_cprodname`を上書きします。</li></ul> |
|`product_sku`| <ul><li>配列。</li><li>SKUのリスト。</li><li>`_csku`を上書きします。</li></ul> |
|`product_brand`| <ul><li>配列。</li><li>ブランドのリスト。</li><li>`_cbrand`を上書きします。</li></ul> |
|`product_category`| <ul><li>配列。</li><li>カテゴリーのリスト。</li><li>`_ccat`を上書きします。</li></ul> |
|`product_subcategory`| <ul><li>配列。</li><li>サブカテゴリーのリスト。</li><li>`_ccat2`を上書きします。</li></ul> |
|`product_quantity`| <ul><li>配列。</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`| <ul><li>配列。</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li></ul> |
|`product_discount`| <ul><li>配列。</li><li>割引のリスト。</li><li>`_cpdisc`を上書きします。</li></ul> |
|`customer_id`| <ul><li>顧客ID。</li><li>`_ccustid`を上書きします。</li></ul> |

### 訪問

|変数|説明|
|---|---|
|`visitor.id`| <ul><li>顧客ID。</li><li>`_ccustid`を上書きします。</li></ul> |
|`visitor.category`| <ul><li>カテゴリー。</li></ul> |
|`visitor.###`| <ul><li>カスタムプロパティ。</li></ul> |

### オンサイト広告

|変数|説明|
|---|---|
|`promo.adId`| <ul><li>作成するID。</li></ul> |
| `promo.adId` | <ul><li>広告フォーマットを示すID。</li></ul> |
|`promo.productId`| <ul><li>関連商品のID。</li></ul> |
|`promo.###`| <ul><li>カスタムマッピング。</li></ul> |

### カスタム変数

|変数|説明|
|---|---|
|`param.###`| setParamの値 |
|--カスタム変数--| カスタム変数。|
| `cv.site.###` | サイトカスタム変数。|
|`cv.page.###`| ページカスタム変数。 |
|`cv.###.###`| カスタム変数。|

### 動的ラベル

|変数|説明|
|---|---|
|`dynlabel.pageId`| <ul><li>動的ページID</li></ul> |
|`dynlabel.update`| <ul><li>名前の変更日</li></ul> |
| `dynlabel.chapter1` | <ul><li>レベル1のチャプター名。</li></ul> |
|`dynlabel.chapter2`| <ul><li>レベル2のチャプター名。</li></ul> |
|`dynlabel.chapter3`| <ul><li>レベル3のチャプター名。</li></ul> |
|`dynlabel.chapter#`| <ul><li>レベル#のチャプター名。</li></ul> |

### 内部検索

|変数|説明|
|---|---|
|`intsearch.keyword`| <ul><li>検索キーワード。</li></ul> |
|`intsearch.resultPageNumber`| <ul><li>検索結果のページ番号。</li></ul> |
| `intsearch.resultPosition` | <ul><li>検索結果の位置。</li></ul> |

### MV（多変量）テスト

|変数|説明|
|---|---|
| `mvtesting.set.test` | <ul><li>テストIDと名前。</li></ul> |
|`mvtesting.set.waveId`| <ul><li>ウェーブID。</li></ul> |
|`mvtesting.set.creation`| <ul><li>クリエイティブのIDと名前。</li></ul> |
| `mvtesting.set.###` | <ul><li>カスタムセットマッピング。</li></ul> |
|`mvtesting.add.variable`| <ul><li>CSV／配列。</li><li>テスト変数。</li></ul> |
|`mvtesting.add.version`| <ul><li>CSV／配列。</li><li>テストバージョン。</li></ul> |
| `mvtesting.add.###` | <ul><li>カスタム追加マッピング。</li></ul> |

### リッチメディア

|変数|説明|
|---|---|
|`richmedia.add.mediaType`| <ul><li>メディアタイプ。</li><li>値は次のとおりです。<ul><li>`video`</li><li>`audio`</li><li>`vpost`</li></ul> </li></ul> |
|```richmedia.add.playerId```| <ul><li>プレーヤーID。</li></ul> |
| `richmedia.add.mediaLevel2` | <ul><li>メディアレベル2。</li></ul> |
|`richmedia.add.mediaLabel`| <ul><li>メディアラベル。</li></ul> |
|`richmedia.add.isEmbedded`| <ul><li>埋め込みかどうか。</li><li>値は`int`または`ext`です。</li></ul> |
|`richmedia.add.broadcastMode`| <ul><li>配信モード。</li><li>値は`live`または`clip`です。</li></ul> |
| `richmedia.add.webdomain` | <ul><li>外部掲載先のWebドメイン</li></ul> |
| `richmedia.add.duration` | <ul><li>再生時間。</li></ul> |
|`richmedia.send.action`| <ul><li>送信アクション。</li><li>値は次のとおりです。<ul><li>`play`</li><li>`pause`</li><li>`stop`</li><li>`info`</li><li>`move`</li></ul> </li></ul> |
|`richmedia.send.playerId`| <ul><li>プレーヤーID。</li></ul> |
|`richmedia.send.mediaLabel`| <ul><li>メディアラベル。</li></ul> |
|`richmedia.send.isBuffering`| <ul><li>バッファリング中かどうか。</li><li>値は次のとおりです。<ul><li>`1` - バッファリング開始</li><li>`0` - バッファリング終了</li></ul> </li></ul> |
|`richmedia.remove`| <ul><li>プレーヤーを削除。</li></ul> |
|`richmedia.removeAll`| <ul><li>すべてのプレーヤーを削除</li><li>値は`true`または`false`です。</li></ul> |

### モバイル

|変数|説明|
|---|---|
|`mob.apvr`| <ul><li>アプリのバージョン。</li></ul> |
|`mob.ref`| <ul><li>リファラー。</li></ul> |
|`mob.stc`| <ul><li>オブジェクト。</li><li>ライフサイクル。</li></ul> |
|`mob.stc.lc`| <ul><li>オブジェクト。</li><li>ライフサイクル。</li></ul> |
|`mob.stc.lc.sessionId`| <ul><li>セッションID。</li></ul> |
|`mob.stc.lc.fl`| <ul><li>初回起動。</li><li>`lifecycle_isfirstlaunch`を上書きします。</li><li>値は`0`または`1`です。</li></ul> |
|`mob.stc.lc.flau`| <ul><li>アップデート後の初回起動。</li><li>`lifecycle_isfirstlaunchupdate`を上書きします。</li><li>値は`0`または`1`です。</li></ul> |
|`mob.stc.lc.lc`| <ul><li>数値。</li><li>起動回数。</li><li>`lifecycle_totallaunchcount`を上書きします。</li></ul> |
|`mob.stc.lc.ldc`| <ul><li>数値。</li><li>1日の起動回数。</li></ul> |
|`mob.stc.lc.lwc`| <ul><li>数値。</li><li>1週間の起動回数。</li></ul> |
|`mob.stc.lc.lmc`| <ul><li>数値。</li><li>1か月の起動回数。</li></ul> |
|`mob.stc.lc.lcsu`| <ul><li>数値。</li><li>前回のアップデート以降の起動回数。</li></ul> |
| `mob.stc.lc.fld` | <ul><li>初回起動日。</li><li>`lifecycle_firstlaunchdate`を上書きします。</li><li>日付形式は`yyyymmdd`です。</li></ul> |
|`mob.stc.lc.dsfl`| <ul><li>数値。</li><li>初回起動からの経過日数。</li><li>`lifecycle_firstlaunchdate`から計算されます。</li></ul> |
|`mob.stc.lc.uld`| <ul><li>前回のアップデート後の初回起動日。</li><li>`lifecycle_updatelaunchdate`を上書きします。</li><li>日付形式は`yyyymmdd`です。</li></ul> |
|`mob.stc.lc.dsu`| <ul><li>数値。</li><li>アップデート後の初回起動からの経過日数。</li><li>`lifecycle_dayssinceupdate`を上書きします。</li></ul> |
|`mob.stc.lc.dslu`| <ul><li>数値。</li><li>アプリが最後に使用されてからの経過日数。</li><li>`lifecycle_lastlaunchdate`から計算されます。</li></ul> |

### カスタムツリー構造

|変数|説明|
|---|---|
|`customTreeStructure.category1`| <ul><li>カテゴリーレベル1</li></ul> |
|`customTreeStructure.category2`| <ul><li>カテゴリーレベル2</li></ul> |
|`customTreeStructure.category3`| <ul><li>カテゴリーレベル3</li></ul> |

### キャンペーン

|変数|説明|
|---|---|
|`xtor`| <ul><li>キャンペーンID。</li></ul> |