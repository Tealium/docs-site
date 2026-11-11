---
title: Pinterestタグ構成ガイド
description: この記事では、タグ管理アカウントでPinterestタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pinterest-tag/
---
## 要件

* Pinterestビジネスアカウント
* Pinterestタグおよびタグ識別子

## タグに関するヒント

* 「メールアドレス」パラメータにマッピングすると、「Enhanced Match」がサポートされます
* 注文IDが構成されると、コンバージョンが発生します。
* 次のEコマース拡張機能パラメータをサポートしています。
  * 注文ID（`_corder`）
  * 小計（`_csubtotal`）
  * 通貨（`_ccurrency`）
  * プロモーションコード（`_cpromo`）
  * 商品IDのリスト（`_cprod`）
  * 商品名のリスト（`cprodname`）
  * ブランドのリスト（`_cbrand`）
  * カテゴリのリスト（`_ccat`）
  * 数量のリスト（`_cquan`）
  * 価格のリスト（`_cprice`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **PinterestタグID**
  * PinterestタグID。
  * PinterestタグIDは、既存または以前のコンバージョンタグIDとは異なります。
* **イベントIDを生成**
  * Pinterestの各トラッキングイベントに対して、イベントIDを自動的に生成します。デフォルト値は`True`です。
* **ページ訪問イベントの自動生成**
  * `true`に構成すると、ページ訪問イベントが自動的に生成されます。デフォルト値はtrueです。**ページ訪問イベントの自動生成**を`true`に構成した場合は、`PageVisit`イベント変数をマッピングしないでください。

### Web向けConversions API

Pinterest Conversions API for Webをサポートするため、このタグはトラッキング対象の各イベントに一意のイベントIDを生成し、Pinterest Conversionsコネクタで使用できるようにEvent Streamingへ送信します。Webベースとサーバーベースの統合を同期するため、コネクタでイベントIDをマッピングできます。この機能を使用するには、有効な[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)が必要です。

タグは、次の命名規則を使用して新しいイベント属性を生成します。

```nohl
pinterest_event_id_{PINTEREST_EVENT}_{TAG_UID}
```

例：`pinterest_event_id_Checkout_32 = "11563522"`

詳細については、[pinterest-conversions-connector](https://docs.tealium.com/pinterest-conversions-connector/)を参照してください。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。ロードルールの詳細については、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

推奨ルール：特定のアクション、イベント、コンバージョンをトラッキングするページでタグをロードするためのカスタムルールを作成します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---|---|
| `tag_id` | <ul><li>タグID。</li><li>Pinterestタグの一意の識別子（旧コンバージョンタグではありません）。</li></ul> |
| `event_id` | <ul><li>イベントID。</li><li>イベントの一意の識別子。</li><li>この値は、**イベントIDを生成**構成オプションによって生成された値を上書きします。</ul> |
| `email_address` | <ul><li>メールアドレス</li></ul> |
|`property`| <ul><li>プロパティ。</li><li>トラッキング対象のアクション、項目、またはイベント。</li></ul> |
|`search_query`| <ul><li>検索クエリ。</li><li>検索キーワード。</li></ul> |
|`product_variant_id`| <ul><li>配列。</li><li>商品バリアントIDのリスト。</li><li>同じ商品で使用可能なバリアントの一意の識別子。</li></ul> |
|`product_variant`| <ul><li>配列。</li><li>商品バリアントのリスト。</li><li>同じ商品で使用可能なバリアントのリスト。</li></ul> |
|`page_name`| <ul><li>ページ名。</li><li>サイトに表示されるページの名前。</li></ul> |
|`page_category`| <ul><li>ページカテゴリ。</li><li>ページのカテゴリ。</li></ul> |
|`page_title`| <ul><li>ページタイトル。</li><li>イベントまたはアクションが発生したページの名前。</li></ul> |
|`video_title`| <ul><li>動画タイトル。</li><li>ユーザーが視聴した動画のタイトル。</li></ul> |
| `lead_type` | <ul><li>リードタイプ。</li><li>ユーザーが関心を持っている商品またはサービスの種類。</li></ul> |
| `generate_event_id` | <ul><li>イベントIDを生成。</li><li>Pinterestの各トラッキングイベントに対して、イベントIDを自動的に生成します。</li></ul> |

### Eコマース

PinterestタグではEコマースが有効になっているため、デフォルトの[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)のマッピングが自動的に使用されます。拡張機能のマッピングを上書きする場合や、拡張機能でEコマース変数が提供されていない場合を除き、通常、このカテゴリで手動マッピングを行う必要はありません。

### Eコマース変数

|変数|説明|
|---|---|
|`order_id`| <ul><li>注文ID。</li><li>確定した注文に割り当てられる一意の識別子。</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`| <ul><li>注文小計。</li><li>確定した注文の小計金額。</li><li>`_csubtotal`を上書きします。</li></ul> |
|`order_currency`| <ul><li>注文通貨。</li><li>支払いに使用された通貨。</li><li>`_ccurrency`を上書きします。</li></ul> |
|`order_coupon_code`| <ul><li>プロモーションコード。</li><li>`_cpromo`を上書きします。</li></ul> |
|`product_id`| <ul><li>配列。</li><li>商品IDのリスト。</li><li>商品配列内の各商品の一意の識別子。</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`| <ul><li>配列。</li><li>名前のリスト。</li><li>商品配列内の各商品の名前。</li><li>`_cprodname`を上書きします。</li></ul> |
|`product_brand`| <ul><li>配列。</li><li>ブランドのリスト。</li><li>商品配列内の各商品のブランド。</li><li>`_cbrand`を上書きします。</li></ul> |
|`product_category`| 配列。商品配列内の各商品のカテゴリ。`_ccat`を上書きします。 |
|`product_quantity`| <ul><li>配列。</li><li>商品配列内の各商品の数量。</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`| <ul><li>配列。</li><li>商品配列内の各商品の単価。</li><li>`_cprice`を上書きします。</li></ul> |

### イベント

指定したトリガー値がページで検出されたときにイベントを発生させるには、これらの宛先にマッピングします。


<blockquote>
ページに注文IDの値がある場合、Checkoutイベントが自動的に発生します。
</blockquote>


|変数|説明|
|---|---|
|PageVisit| ページへの訪問。イベントの重複を避けるため、**ページ訪問イベントの自動生成**が**true**に構成されている場合は、`PageVisit`をマッピングしないでください。 |
|ViewCategory| カテゴリの閲覧。|
|Search| 検索。|
|AddToCart| カートへの追加。|
|Checkout| チェックアウト。|
|WatchVideo| 動画の視聴。|
|Signup| サインアップ。|
|Lead| リードソース。|
|AddToWishList| ウィッシュリストへの追加。|
|InitiateCheckout| チェックアウトの開始。|
|Subscribe| 購読。|
|ViewContent| コンテンツの閲覧。|
|Custom| カスタムイベントの作成。|

イベントをマッピングする方法は次のとおりです。

1. ドロップダウンリストからイベントを選択します。  
事前定義されたリストから選択するか、カスタムイベントを作成できます。
1. カスタムイベントの場合は、そのイベントを識別するための名前を入力します。
1. 「トリガー」フィールドに、この宛先へマッピングする変数の値を入力します。  
その値が検出されると、ページでイベントが発生します。
1. さらにイベントをマッピングするには、プラス（**+**）ボタンをクリックし、手順1と2を繰り返します。
1. **適用**をクリックします。

マッピングが完了したら、保存してパブリッシュします。以上で、プロファイルへのタグの構成は完了です。

### 制限付きデータ処理（LDP）

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `opt_out_type` | 文字列 | オプトアウトの種類。 |
| `st` | 文字列 | オプトアウトの州。 | 
| `country` | 文字列 | オプトアウトの国。 | 

## ベンダーのドキュメント

* [Pinterest：Pinterestタグについて](https://help.pinterest.com/en/articles/website-conversion-tracking)
* [Pinterest：広告マネージャーガイド](https://business.pinterest.com/sites/business/files/pinterest-ads-manager-guide.pdf)