---
title: Amperityタグ構成ガイド
description: この記事では、タグ管理アカウントでAmperityタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amperity-tag/
---
## タグに関するヒント

* マッピングを使用すると、標準構成値を動的に上書きできます。
* このタグは、以下の[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)パラメータをサポートしています。
    * 注文ID
    * 商品ID

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の項目を構成します。

* **書き込みトークン**：有効期限のない公開書き込みトークン
* **ストリームID**：書き込み先のストリームを識別します
* **テナント名**：書き込み先となるAmperityテナントの名前
* **ホスト型JavaScriptエンドポイント**：埋め込まれるJavaScriptをホストするURL

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `writeToken`  | 文字列 | 書き込みトークン |
|  `streamID`  | 文字列 | ストリームID |
|  `tenantName`  | 文字列 | テナント名 |
|  `hostedJavaScriptEndpoint`  | 文字列 | ホスト型JavaScriptエンドポイント |
| `tenantUrl`  | ブール値 | テナントURL |
|  `is-mobile`  | ブール値 | ユーザーがモバイルデバイスまたはブラウザーでサイトにアクセスしているかどうか。 |
|  `session-id`  | 文字列 | イベントが発生したWebセッションのID。 |
|  `property`  | 文字列 | 複数ブランドまたは複数サイトの場合の、特定のプロパティ。 |
| `brand`  | 文字列 | 複数ブランドの場合の、ページに関連付けられたブランド。 |
|  `page-url`  | 文字列 | イベントが発生したURL。 |
|  `page-name`  | 文字列 | イベントが発生したページの名前。 |
|  `referral-url`  | 文字列 | ユーザーをサイトに誘導した参照元URL。 |
|  `referral-source`  | 文字列 | サイトへの参照元メディア／ソース（直接流入、オーガニック検索など）。 |
|  `search-value`  | 文字列 | サイト内検索の実行時に入力された検索値。 |

### 識別子

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `first-party-web-id`  | 文字列 | セッションとともに保存されるファーストパーティー顧客識別子。|
|  `first-party-cookie`  | 文字列 | ソースから渡されるファーストパーティーCookie／ハッシュ化ID。 |
|  `visitor-id`  | 文字列 | プロバイダーによって割り当てられた訪問ID。このフィールドはセッションの保存に使用できますが、一意でない、または識別できない可能性があります。 |
|  `device-id`  | 文字列 | イベントに関連付けられたデバイスID。データソースのプライバシー制限によっては非表示になる場合があります。 |
|  `mobile-ad-id`  | 文字列 | イベントに関連付けられたモバイル広告ID（MAID）。信頼性の低い顧客識別子ですが、取得する価値があります。 |
|  `captured-email`  | 文字列 | 注文状況の確認、再入荷通知、購読登録、クレジットカード申込、またはロイヤルティプログラム登録のために入力されたメールアドレス。 |
|  `identifiers.custom`  | 文字列 | 取得可能なその他の顧客識別子。 |

### キャンペーン／広告情報

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `campaign-id`  | 文字列 | メール、デジタル広告、またはその他の形式のキャンペーンから得られた参照元／トラッキング対象のキャンペーンID。 |
|  `campaign-name`  | 文字列 | メール、デジタル広告、またはその他の形式のキャンペーンから得られた参照元／トラッキング対象のキャンペーン名。 |
|  `adword-group`  | 文字列 | ユーザーを誘導した広告ワードグループ。 | 
|  `adword-keyword`  | 文字列 | ユーザーを誘導した広告／検索キーワードのリスト。 |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `order-id`（`_corder`を上書き） | [数値、文字列] | 注文ID |
| `product-id`（`_cprod`を上書き） | 配列 | 商品ID |

### イベントパラメータ

| 変数 | 型 |説明 |
|:---------|:------------|:------------|
|  `event-datetime`  | DATETIME | イベントが発生した日時 | 

### イベントトリガー

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `purchase` | 購入 |
| `productDetailPageBrowse` | 商品詳細ページの閲覧 |
| `viewProduct` | 商品の表示 |
| `categoryPageBrowse` | カテゴリーページの閲覧 |
| `viewCartAbandon` | カート放棄の表示 | 
| `storeLocatorSearch` | 店舗検索 | 
| `highValuePageView` | 重要度の高いページの表示 |
| `productFilterSelections` | 商品フィルターの選択 |
| `accountCreation` | アカウント作成 |
| `emailListServ` | メールリストサービス |
| `promoCodeSignup` | プロモーションコード登録 |
| `creditCardBrowse` | クレジットカードの閲覧 |
| `creditCardSignup` | クレジットカードの申込 |
| `checkOrderStatus` | 注文状況の確認 |
| `leaveReview` | レビューの投稿 |
| `siteSearch` | サイト内検索 |
| `supportContact` | サポート／問い合わせ |
| `productRestockAlert` | 商品の再入荷通知 |
| `addToWishlist` | ウィッシュリストへの追加 |

### イベント固有のパラメータ

このオプションを選択すると、利用可能な任意のマッピングを特定のイベントトリガー専用に構成できます。