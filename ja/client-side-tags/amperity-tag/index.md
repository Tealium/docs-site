---
title: Amperity タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Amperity タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amperity-tag/
---
## タグのヒント

* マッピングを使用して、標準の構成値を動的にオーバーライドします。
* このタグは以下の [E-Commerce extension](https://docs.tealium.com/e-commerce-extension/) パラメータをサポートしています:
    * 注文ID
    * 製品ID

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグを追加する方法についての詳細は、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します:

* **Write Token**: 期限のない公開書き込みトークン
* **Stream ID**: 書き込まれるストリームを識別します
* **Tenant Name**: 書き込まれるAmperityテナントの名前
* **Hosted JavaScript Endpoint**: JavaScriptが埋め込まれているURL

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです:

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `writeToken`  | 文字列 | 書き込みトークン |
|  `streamID`  | 文字列 | ストリームID |
|  `tenantName`  | 文字列 | テナント名 |
|  `hostedJavaScriptEndpoint`  | 文字列 | ホストされているJavaScriptエンドポイント |
| `tenantUrl`  | 真偽値 | テナントURL  |
|  `is-mobile`  | 真偽値 | ユーザーがモバイルデバイスまたはブラウザでサイトにアクセスしているかどうか。 |
|  `session-id`  | 文字列 | イベントが発生したウェブセッションのID。 |
|  `property`  | 文字列 | 複数ブランドまたは複数サイトの場合、特定のプロパティ。 |
| `brand`  | 文字列 | 複数ブランドの場合、ページに関連するブランド。 |
|  `page-url`  | 文字列 | イベントが発生したURL。 |
|  `page-name`  | 文字列 | イベントが発生したページ名。 |
|  `referral-url`  | 文字列 | ユーザーをサイトに誘導したURL。 |
|  `referral-source`  | 文字列 | サイトへの参照元/ソース（ダイレクト、オーガニック検索など）。 |
|  `search-value`  | 文字列 | サイトのクエリが実行された際に入力された検索値。 |

### 識別子

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `first-party-web-id`  | 文字列 | セッションに保存されている第一者の顧客識別子。|
|  `first-party-cookie`  | 文字列 | ソースから渡された第一者のクッキー/ハッシュ化されたID。 |
|  `visitor-id`  | 文字列 | プロバイダーによって割り当てられた訪問ID。このフィールドはセッションの保存に使用できますが、一意ではない場合があります。 |
|  `device-id`  | 文字列 | イベントに関連するデバイスID。データソースのプライバシー制限により表示されない場合があります。 |
|  `mobile-ad-id`  | 文字列 | イベントに関連するモバイル広告IDまたはMAID。信頼性の低い顧客識別子ですが、キャプチャする価値があります。 |
|  `captured-email`  | 文字列 | 注文状況の確認、再入荷アラート、サブスクリプションの登録、クレジットカードの登録、またはロイヤリティの登録のために入力されたメール。 |
|  `identifiers.custom`  | 文字列 | その他のキャプチャ可能な顧客識別子。 |

### キャンペーン/広告情報

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `campaign-id`  | 文字列 | メール、デジタル広告、またはその他のキャンペーンからの参照/追跡されたキャンペーンID。 |
|  `campaign-name`  | 文字列 | メール、デジタル広告、またはその他のキャンペーンからの参照/追跡されたキャンペーン名。 |
|  `adword-group`  | 文字列 | ユーザーを参照したアドワードグループ。 | 
|  `adword-keyword`  | 文字列 | ユーザーを参照した広告/検索キーワードリスト。 |

### E-Commerce

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `order-id` (Overrides `_corder`)  | [数値, 文字列] | 注文ID  |
| `product-id` (Overrides `_cprod`)  | 配列 | 製品ID |

### イベントパラメータ

| 変数 | タイプ |説明 |
|:---------|:------------|:------------|
|  `event-datetime`  | DATETIME | イベントが発生した時間と日 |

### イベントトリガー
イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `purchase` | 購入 |
| `productDetailPageBrowse` | 製品詳細ページ閲覧 |
| `viewProduct` | 製品表示 |
| `categoryPageBrowse` | カテゴリページ閲覧 |
| `viewCartAbandon` | カート放棄表示 | 
| `storeLocatorSearch` | ストアロケータ検索  |
| `highValuePageView` | 高価値ページ表示 |
| `productFilterSelections` | 製品フィルタ選択 |
| `accountCreation` | アカウント作成 |
| `emailListServ` | メールリストサービス |
| `promoCodeSignup` | プロモーションコード登録 |
| `creditCardBrowse` | クレジットカード閲覧 |
| `creditCardSignup` | クレジットカード登録 |
| `checkOrderStatus` | 注文状況確認 |
| `leaveReview` | レビュー投稿 |
| `siteSearch` | サイト検索 |
| `supportContact` | サポート/連絡 |
| `productRestockAlert` | 製品再入荷アラート |
| `addToWishlist` |  ウィッシュリストに追加  |

### イベント固有のパラメータ

利用可能なマッピングは、このオプションを選択することでイベントトリガーに固有のものに構成できます。