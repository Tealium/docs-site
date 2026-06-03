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

まず、Tealium のタグマーケットプレイスにアクセスし、AT Internet SmartTag タグを追加します（[タグの追加方法]()について詳しくはこちら）。

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

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`window_var`|  &lt;ul&gt;&lt;li&gt;ウィンドウトラッカー名&lt;/li&gt;&lt;li&gt;タグテンプレートの外でトラッカーを使用できるように、ウィンドウレベルの変数を構成します。&lt;/li&gt;&lt;/ul&gt; |
|`config.site`|  &lt;ul&gt;&lt;li&gt;AT Internet サイトID。&lt;/li&gt;&lt;li&gt;詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。&lt;/li&gt;&lt;/ul&gt; |
|`config.collectDomain`|  &lt;ul&gt;&lt;li&gt;AT Internet データ収集ドメイン。&lt;/li&gt;&lt;/ul&gt; |
|`config.collectDomainSSL`|  &lt;ul&gt;&lt;li&gt;AT Internet セキュアデータ収集ドメイン。&lt;/li&gt;&lt;/ul&gt; |
|`config.log`|  &lt;ul&gt;&lt;li&gt;バージョン 5.13.0 以降、Log は廃止されました。&lt;/li&gt;&lt;/ul&gt; |
|`config.logSSL`|  &lt;ul&gt;&lt;li&gt;バージョン 5.13.0 以降、廃止されました。&lt;/li&gt;&lt;li&gt;このサイトIDの AT Internet セキュアログ。&lt;/li&gt;&lt;li&gt;詳細については、AT Internet の [Tag Composer](https://apps.atinternet-solutions.com/TagComposer/#/) ドキュメントを参照してください。&lt;/li&gt;&lt;li&gt;セキュアページ用のコレクターサブドメインの Tag Composer を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|`config.domain`|  &lt;ul&gt;&lt;li&gt;バージョン 5.13.0 以降、廃止されました。&lt;/li&gt;&lt;li&gt;コレクションドメイン。&lt;/li&gt;&lt;li&gt;`xiti.com` または `ati-host.net`、AT Internet の構成に応じて。&lt;/li&gt;&lt;li&gt;マッピングを使用してカスタムコレクションドメインを指定できます。&lt;/li&gt;&lt;/ul&gt; |
|`config.pixelPath`|  &lt;ul&gt;&lt;li&gt;AT Internet ピクセルリクエストの URL パス。&lt;/li&gt;&lt;li&gt;デフォルトは `/hit.xiti` です。&lt;/li&gt;&lt;/ul&gt; |
|`config.secure`|  &lt;ul&gt;&lt;li&gt;情報を安全に送信するために有効にします。&lt;/li&gt;&lt;/ul&gt; |
|`config.cookieSecure`|  &lt;ul&gt;&lt;li&gt;**true** に構成すると、トラッカークッキーの書き込みに `secure` オプションを追加することができます（最初に）。&lt;/li&gt;&lt;li&gt;セキュアクッキーは HTTPS ページでのみ機能することに注意してください。&lt;/li&gt;&lt;/ul&gt; |
|`config.disableCookie`|  &lt;ul&gt;&lt;li&gt;Cookie を無効にします。&lt;/li&gt;&lt;/ul&gt; |
|`config.cookieDomain`|  &lt;ul&gt;&lt;li&gt;Cookie ドメイン。&lt;/li&gt;&lt;li&gt;あなたのサイトの URL。&lt;/li&gt;&lt;li&gt;構成が正しくない場合、ユニークビジターの計算に問題が生じる可能性があります。&lt;/li&gt;&lt;/ul&gt; |
|`config.preview`|  &lt;ul&gt;&lt;li&gt;プレビュー。&lt;/li&gt;&lt;/ul&gt; |
|`config.sendHitWhenOptOut`|  &lt;ul&gt;&lt;li&gt;ユーザーが「OPT-OUT」モードの場合に匿名ヒットを送信することができます（ファーストパーティ）。&lt;/li&gt;&lt;/ul&gt; |

### コンテキスト

|変数| 説明|
|---| ---|
|`context.forcedCampaign`| 強制キャンペーン。|
|`context.forcedReferer`| 強制リファラー。|

### Eコマース - イベント

追加情報については、[カートイベント（セールスインサイト）](https://developers.atinternet-solutions.com/javascript-en/ecommerce-javascript-en/sales-insights-javascript-en/cart-events-sales-insights-javascript-fr/?kw=cartdisplay#cart-display_2)を参照してください。

|変数| 説明|
|---| ---|
|`order`|  &lt;ul&gt;&lt;li&gt;注文&lt;/li&gt;&lt;/ul&gt; |
|`cart`|  &lt;ul&gt;&lt;li&gt;カート&lt;/li&gt;&lt;/ul&gt; |
|`prod`|  &lt;ul&gt;&lt;li&gt;商品表示&lt;/li&gt;&lt;/ul&gt; |
|`aisle`|  &lt;ul&gt;&lt;li&gt;通路&lt;/li&gt;&lt;/ul&gt; |
|`transactionconfirm`|  &lt;ul&gt;&lt;li&gt;取引確認&lt;/li&gt;&lt;/ul&gt; |
|`cartdisplay`|  &lt;ul&gt;&lt;li&gt;カート表示&lt;/li&gt;&lt;/ul&gt; |
|`cartupdate`|  &lt;ul&gt;&lt;li&gt;カート更新&lt;/li&gt;&lt;/ul&gt; |
|`displayshipping`|  &lt;ul&gt;&lt;li&gt;配送ステップの表示&lt;/li&gt;&lt;/ul&gt; |
|`displaypayment`|  &lt;ul&gt;&lt;li&gt;支払いステップの表示&lt;/li&gt;&lt;/ul&gt; |
|`cartawaitingpayment`|  &lt;ul&gt;&lt;li&gt;支払い待ちのカート&lt;/li&gt;&lt;/ul&gt; |
|`productdisplay`|  &lt;ul&gt;&lt;li&gt;商品表示&lt;/li&gt;&lt;/ul&gt; |
|`productpagedisplay`|  &lt;ul&gt;&lt;li&gt;商品ページ表示&lt;/li&gt;&lt;/ul&gt; |
|`productaddition`| &lt;ul&gt;&lt;li&gt;商品追加&lt;/li&gt;&lt;/ul&gt; |
|`productremoval`|  &lt;ul&gt;&lt;li&gt;商品削除&lt;/li&gt;&lt;/ul&gt; |
### E-コマース

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;`_corder`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;注文合計。&lt;/li&gt;&lt;li&gt;`_ctotal`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;注文小計。&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;送料。&lt;/li&gt;&lt;li&gt;`_cship`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;税金。&lt;/li&gt;&lt;li&gt;`_ctax`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;プロモーションコード。&lt;/li&gt;&lt;li&gt;`_cpromo`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;商品IDのリスト。&lt;/li&gt;&lt;li&gt;`_cprod`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;商品名のリスト。&lt;/li&gt;&lt;li&gt;`_cprodname`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_sku`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;SKUのリスト。&lt;/li&gt;&lt;li&gt;`_csku`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;ブランドのリスト。&lt;/li&gt;&lt;li&gt;`_cbrand`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;カテゴリのリスト。&lt;/li&gt;&lt;li&gt;`_ccat`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_subcategory`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;サブカテゴリのリスト。&lt;/li&gt;&lt;li&gt;`_ccat2`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;`_cprice`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_discount`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;割引のリスト。&lt;/li&gt;&lt;li&gt;`_cpdisc`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;顧客ID。&lt;/li&gt;&lt;li&gt;`_ccustid`を上書き。&lt;/li&gt;&lt;/ul&gt; |

### 訪問

|変数| 説明|
|---| ---|
|`visitor.id`|  &lt;ul&gt;&lt;li&gt;顧客ID。&lt;/li&gt;&lt;li&gt;`_ccustid`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`visitor.category`|  &lt;ul&gt;&lt;li&gt;カテゴリ。&lt;/li&gt;&lt;/ul&gt; |
|`visitor.###`|  &lt;ul&gt;&lt;li&gt;カスタムプロパティ。&lt;/li&gt;&lt;/ul&gt; |

### サイト内広告

|変数| 説明|
|---| ---|
|`promo.adId`|  &lt;ul&gt;&lt;li&gt;作成されるID。&lt;/li&gt;&lt;/ul&gt; |
| `promo.adId` |  &lt;ul&gt;&lt;li&gt;広告形式を示すID。&lt;/li&gt;&lt;/ul&gt; |
|`promo.productId`|  &lt;ul&gt;&lt;li&gt;関連商品のID。&lt;/li&gt;&lt;/ul&gt; |
|`promo.###`|  &lt;ul&gt;&lt;li&gt;カスタムマッピング。&lt;/li&gt;&lt;/ul&gt; |

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
|`dynlabel.pageId`|  &lt;ul&gt;&lt;li&gt;動的ページID&lt;/li&gt;&lt;/ul&gt; |
|`dynlabel.update`|  &lt;ul&gt;&lt;li&gt;名前変更の日付&lt;/li&gt;&lt;/ul&gt; |
| `dynlabel.chapter1` |  &lt;ul&gt;&lt;li&gt;レベル1の章の名前。&lt;/li&gt;&lt;/ul&gt; |
|`dynlabel.chapter2`|  &lt;ul&gt;&lt;li&gt;レベル2の章の名前。&lt;/li&gt;&lt;/ul&gt; |
|`dynlabel.chapter3`|  &lt;ul&gt;&lt;li&gt;レベル3の章の名前。&lt;/li&gt;&lt;/ul&gt; |
|`dynlabel.chapter#`|  &lt;ul&gt;&lt;li&gt;レベル#の章の名前。&lt;/li&gt;&lt;/ul&gt; |

### サイト内検索

|変数| 説明|
|---| ---|
|`intsearch.keyword`|  &lt;ul&gt;&lt;li&gt;検索キーワード。&lt;/li&gt;&lt;/ul&gt; |
|`intsearch.resultPageNumber`|  &lt;ul&gt;&lt;li&gt;検索結果ページ番号。&lt;/li&gt;&lt;/ul&gt; |
| `intsearch.resultPosition` |  &lt;ul&gt;&lt;li&gt;検索結果の位置。&lt;/li&gt;&lt;/ul&gt; |

### MV (多変量) テスト

|変数| 説明|
|---| ---|
| `mvtesting.set.test` |  &lt;ul&gt;&lt;li&gt;テストIDと名前。&lt;/li&gt;&lt;/ul&gt; |
|`mvtesting.set.waveId`|  &lt;ul&gt;&lt;li&gt;ウェーブID。&lt;/li&gt;&lt;/ul&gt; |
|`mvtesting.set.creation`|  &lt;ul&gt;&lt;li&gt;作成IDと名前。&lt;/li&gt;&lt;/ul&gt; |
| `mvtesting.set.###` |  &lt;ul&gt;&lt;li&gt;カスタムセットマッピング。&lt;/li&gt;&lt;/ul&gt; |
|`mvtesting.add.variable`|  &lt;ul&gt;&lt;li&gt;CSV/配列。&lt;/li&gt;&lt;li&gt;テスト変数。&lt;/li&gt;&lt;/ul&gt; |
|`mvtesting.add.version`|  &lt;ul&gt;&lt;li&gt;CSV/配列。&lt;/li&gt;&lt;li&gt;テストバージョン。&lt;/li&gt;&lt;/ul&gt; |
| `mvtesting.add.###` |  &lt;ul&gt;&lt;li&gt;カスタム追加マッピング。&lt;/li&gt;&lt;/ul&gt; |

### リッチメディア

|変数| 説明|
|---| ---|
|`richmedia.add.mediaType`|  &lt;ul&gt;&lt;li&gt;メディアタイプ。&lt;/li&gt;&lt;li&gt;値は:  &lt;ul&gt;&lt;li&gt;`video`&lt;/li&gt;&lt;li&gt;`audio`&lt;/li&gt;&lt;li&gt;`vpost`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|```richmedia.add.playerId```|  &lt;ul&gt;&lt;li&gt;プレイヤーID。&lt;/li&gt;&lt;/ul&gt; |
| `richmedia.add.mediaLevel2` |  &lt;ul&gt;&lt;li&gt;メディアレベル2。&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.add.mediaLabel`|  &lt;ul&gt;&lt;li&gt;メディアラベル。&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.add.isEmbedded`|  &lt;ul&gt;&lt;li&gt;埋め込みかどうか。&lt;/li&gt;&lt;li&gt;値は `int` または `ext`。&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.add.broadcastMode`|  &lt;ul&gt;&lt;li&gt;放送モード。&lt;/li&gt;&lt;li&gt;値は `live` または `clip`。&lt;/li&gt;&lt;/ul&gt; |
| `richmedia.add.webdomain` |  &lt;ul&gt;&lt;li&gt;外部配置のウェブドメイン&lt;/li&gt;&lt;/ul&gt; |
| `richmedia.add.duration` |  &lt;ul&gt;&lt;li&gt;持続時間。&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.send.action`|  &lt;ul&gt;&lt;li&gt;送信アクション。&lt;/li&gt;&lt;li&gt;値は:  &lt;ul&gt;&lt;li&gt;`play`&lt;/li&gt;&lt;li&gt;`pause`&lt;/li&gt;&lt;li&gt;`stop`&lt;/li&gt;&lt;li&gt;`info`&lt;/li&gt;&lt;li&gt;`move`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`richmedia.send.playerId`|  &lt;ul&gt;&lt;li&gt;プレイヤーID。&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.send.mediaLabel`|  &lt;ul&gt;&lt;li&gt;メディアラベル。&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.send.isBuffering`|  &lt;ul&gt;&lt;li&gt;バッファリング中かどうか。&lt;/li&gt;&lt;li&gt;値は:  &lt;ul&gt;&lt;li&gt;`1` - バッファリング開始&lt;/li&gt;&lt;li&gt;`0` - バッファリング終了&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`richmedia.remove`|  &lt;ul&gt;&lt;li&gt;プレイヤーを削除。&lt;/li&gt;&lt;/ul&gt; |
|`richmedia.removeAll`|  &lt;ul&gt;&lt;li&gt;すべてのプレイヤーを削除&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |

### モバイル

|変数| 説明|
|---| ---|
|`mob.apvr`|  &lt;ul&gt;&lt;li&gt;アプリバージョン。&lt;/li&gt;&lt;/ul&gt; |
|`mob.ref`|  &lt;ul&gt;&lt;li&gt;リファラー。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc`|  &lt;ul&gt;&lt;li&gt;オブジェクト。&lt;/li&gt;&lt;li&gt;ライフサイクル。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc`|  &lt;ul&gt;&lt;li&gt;オブジェクト。&lt;/li&gt;&lt;li&gt;ライフサイクル。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.sessionId`|  &lt;ul&gt;&lt;li&gt;セッションID。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.fl`|  &lt;ul&gt;&lt;li&gt;初回起動。&lt;/li&gt;&lt;li&gt;`lifecycle_isfirstlaunch`を上書き。&lt;/li&gt;&lt;li&gt;値は `0` または `1`。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.flau`|  &lt;ul&gt;&lt;li&gt;アップデート以降の初回起動。&lt;/li&gt;&lt;li&gt;`lifecycle_isfirstlaunchupdate`を上書き。&lt;/li&gt;&lt;li&gt;値は `0` または `1`。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.lc`|  &lt;ul&gt;&lt;li&gt;数値。&lt;/li&gt;&lt;li&gt;起動回数。&lt;/li&gt;&lt;li&gt;`lifecycle_totallaunchcount`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.ldc`|  &lt;ul&gt;&lt;li&gt;数値。&lt;/li&gt;&lt;li&gt;その日の起動回数。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.lwc`|  &lt;ul&gt;&lt;li&gt;数値。&lt;/li&gt;&lt;li&gt;その週の起動回数。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.lmc`|  &lt;ul&gt;&lt;li&gt;数値。&lt;/li&gt;&lt;li&gt;その月の起動回数。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.lcsu`|  &lt;ul&gt;&lt;li&gt;数値。&lt;/li&gt;&lt;li&gt;最後のアップデート以降の起動回数。&lt;/li&gt;&lt;/ul&gt; |
| `mob.stc.lc.fld` |  &lt;ul&gt;&lt;li&gt;初回起動日。&lt;/li&gt;&lt;li&gt;`lifecycle_firstlaunchdate`を上書き。&lt;/li&gt;&lt;li&gt;日付形式は `yyyymmdd`。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.dsfl`|  &lt;ul&gt;&lt;li&gt;数値。&lt;/li&gt;&lt;li&gt;初回起動からの日数。&lt;/li&gt;&lt;li&gt;`lifecycle_firstlaunchdate`から計算。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.uld`|  &lt;ul&gt;&lt;li&gt;最後のアップデート以降の初回起動日。&lt;/li&gt;&lt;li&gt;`lifecycle_updatelaunchdate`を上書き。&lt;/li&gt;&lt;li&gt;日付形式は `yyyymmdd`。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.dsu`|  &lt;ul&gt;&lt;li&gt;数値。&lt;/li&gt;&lt;li&gt;アップデート以降の初回起動からの日数。&lt;/li&gt;&lt;li&gt;`lifecycle_dayssinceupdate`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`mob.stc.lc.dslu`|  &lt;ul&gt;&lt;li&gt;数値。&lt;/li&gt;&lt;li&gt;最後の使用からの日数。&lt;/li&gt;&lt;li&gt;`lifecycle_lastlaunchdate`から計算。&lt;/li&gt;&lt;/ul&gt; |

### カスタムツリー構造

|変数| 説明|
|---| ---|
|`customTreeStructure.category1`|  &lt;ul&gt;&lt;li&gt;カテゴリーレベル1&lt;/li&gt;&lt;/ul&gt; |
|`customTreeStructure.category2`|  &lt;ul&gt;&lt;li&gt;カテゴリーレベル2&lt;/li&gt;&lt;/ul&gt; |
|`customTreeStructure.category3`|  &lt;ul&gt;&lt;li&gt;カテゴリーレベル3&lt;/li&gt;&lt;/ul&gt; |

### キャンペーン

|変数| 説明|
|---| ---|
|`xtor`|  &lt;ul&gt;&lt;li&gt;キャンペーンID。&lt;/li&gt;&lt;/ul&gt; |