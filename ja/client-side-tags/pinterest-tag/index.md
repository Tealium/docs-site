---
title: Pinterestタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでPinterestタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pinterest-tag/
---
## 必要条件

* Pinterestビジネスアカウント
* Pinterestタグおよびタグ識別子

## タグのヒント

* &#34;Email Address&#34;パラメータにマッピングするときに&#34;Enhanced Match&#34;をサポート
* Order IDが構成されたときにコンバージョンが発生
* 以下のEコマース拡張パラメータをサポート:
  * Order ID (`_corder`)
  * 小計 (`_csubtotal`)
  * 通貨 (`_ccurrency`)
  * プロモコード (`_cpromo`)
  * 製品IDリスト (`_cprod`)
  * 名前リスト (`cprodname`)
  * ブランドリスト (`_cbrand`)
  * カテゴリリスト (`_ccat`)
  * 数量リスト (`_cquan`)
  * 価格リスト (`_cprice`)

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法については、[タグ概要]()の記事を参照してください。

タグを追加する際には、以下の構成を構成します:

* **PinterestタグID**
  * あなたのPinterestタグID。
  * あなたのPinterestタグIDは、既存のコンバージョンタグIDとは異なります。
* **イベントIDの生成**
  * すべてのPinterestトラッキングイベントに対して自動的にイベントIDを生成します。デフォルト値は`True`です。
* **自動ページ訪問イベント**
  * `true`に構成すると、自動的にページ訪問イベントを生成します。デフォルトはtrueです。**自動ページ訪問イベント**が`true`に構成されている場合、`PageVisit`イベント変数のマッピングは行わないでください。

### Web用コンバージョンAPI

Web用PinterestコンバージョンAPIをサポートするために、タグは各イベントに対して一意のイベントIDを生成し、それをTealium EventStreamに送信してPinterestコンバージョンコネクタで使用します。コネクタでイベントIDをマッピングすることで、ウェブベースのサーバーベースの統合を同期させることができます。この機能にはアクティブな[Tealium Collectタグ]()が必要です。

タグは以下の命名規則を使用して新しいイベント属性を発行します:

```nohl
pinterest_event_id_{PINTEREST_EVENT}_{TAG_UID}
```

例: `pinterest_event_id_Checkout_32 = &#34;11563522&#34;`

詳細については、を参照してください。

## 読み込みルール

すべてのページでタグを読み込むか、タグの読み込み条件を構成します。読み込みルールについての詳細は、[読み込みルール]()のドキュメントを参照してください。

推奨ルール: 特定のアクション、イベント、およびコンバージョンを追跡したいページで読み込むためのカスタムルールを作成します。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです:

### 標準

|変数| 説明|
|---| ---|
| `tag_id` |  &lt;ul&gt;&lt;li&gt;タグID。&lt;/li&gt;&lt;li&gt;あなたのPinterestタグの一意の識別子（古いコンバージョンタグではない）。&lt;/li&gt;&lt;/ul&gt; |
| `event_id` |  &lt;ul&gt;&lt;li&gt;イベントID。&lt;/li&gt;&lt;li&gt;イベントの一意の識別子。&lt;/li&gt;&lt;li&gt;この値は**イベントIDの生成**構成オプションによって生成された値を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `email_address` |  &lt;ul&gt;&lt;li&gt;メールアドレス&lt;/li&gt;&lt;/ul&gt; |
|`property`|  &lt;ul&gt;&lt;li&gt;プロパティ。&lt;/li&gt;&lt;li&gt;追跡されるアクション、アイテム、またはイベント。&lt;/li&gt;&lt;/ul&gt; |
|`search_query`|  &lt;ul&gt;&lt;li&gt;検索クエリ。&lt;/li&gt;&lt;li&gt;検索キーワード。&lt;/li&gt;&lt;/ul&gt; |
|`product_variant_id`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;製品バリアントIDのリスト。&lt;/li&gt;&lt;li&gt;同じ製品の利用可能なバリアントの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|`product_variant`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;製品バリアントのリスト。&lt;/li&gt;&lt;li&gt;同じ製品の利用可能なバリアントのリスト。&lt;/li&gt;&lt;/ul&gt; |
|`page_name`|  &lt;ul&gt;&lt;li&gt;ページ名。&lt;/li&gt;&lt;li&gt;あなたのサイトに表示されるページの名前。&lt;/li&gt;&lt;/ul&gt; |
|`page_category`|  &lt;ul&gt;&lt;li&gt;ページカテゴリ。&lt;/li&gt;&lt;li&gt;ページのカテゴリ。&lt;/li&gt;&lt;/ul&gt; |
|`page_title`|  &lt;ul&gt;&lt;li&gt;ページタイトル。&lt;/li&gt;&lt;li&gt;イベントまたはアクションが発生したページの名前。&lt;/li&gt;&lt;/ul&gt; |
|`video_title`|  &lt;ul&gt;&lt;li&gt;ビデオタイトル。&lt;/li&gt;&lt;li&gt;ユーザーが視聴したビデオのタイトル。&lt;/li&gt;&lt;/ul&gt; |
| `lead_type` |  &lt;ul&gt;&lt;li&gt;リードタイプ。&lt;/li&gt;&lt;li&gt;ユーザーが興味を持っている製品またはサービスのタイプ。&lt;/li&gt;&lt;/ul&gt; |
| `generate_event_id` |  &lt;ul&gt;&lt;li&gt;イベントIDの生成。&lt;/li&gt;&lt;li&gt;すべてのPinterestトラッキングイベントに対して自動的にイベントIDを生成します。&lt;/li&gt;&lt;/ul&gt; |

### Eコマース

PinterestタグはEコマース対応であり、デフォルトで[Eコマース拡張]()のマッピングを自動的に使用します。拡張機能で提供されていないEコマース変数を上書きする場合や、拡張機能のマッピングを上書きする場合を除き、このカテゴリでの手動マッピングは通常必要ありません。

### Eコマース変数

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;最終注文に割り当てられた一意の識別子&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;注文小計。&lt;/li&gt;&lt;li&gt;最終注文の小計金額&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;注文通貨。&lt;/li&gt;&lt;li&gt;支払いに使用される通貨&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;プロモコード。&lt;/li&gt;&lt;li&gt;`_cpromo`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;製品IDのリスト。&lt;/li&gt;&lt;li&gt;製品配列内の各製品の一意の識別子。&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;名前のリスト。&lt;/li&gt;&lt;li&gt;製品配列内の各製品の名前。&lt;/li&gt;&lt;li&gt;`_cprodname`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;ブランドのリスト。&lt;/li&gt;&lt;li&gt;製品配列内の各製品のブランド。&lt;/li&gt;&lt;li&gt;`_cbrand`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  配列。製品配列内の各製品のカテゴリ。`_ccat`を上書きします。 |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;製品配列内の各製品の数量。&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列。&lt;/li&gt;&lt;li&gt;製品配列内の各製品の単価。&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |

### イベント

ページ上で指定したトリガー値が見つかったときにイベントをトリガーするためにこれらの宛先にマッピングします。

注文ID値がページ上で利用可能な場合、チェックアウトイベントは自動的にトリガーされます。

|変数| 説明|
|---| ---|
|PageVisit| ページ訪問。重複イベントを避けるため、**自動ページ訪問イベント**が**true**に構成されている場合は`PageVisit`をマッピングしないでください。 |
|ViewCategory| カテゴリ表示。|
|Search| 検索。|
|AddToCart| カートに追加。|
|Checkout| チェックアウト。|
|WatchVideo| ビデオ視聴。|
|Signup| 登録。|
|Lead| リードソース。|
|AddToWishList| お気に入りに追加。|
|InitiateCheckout| チェックアウト開始。|
|Subscribe| 登録。|
|ViewContent| コンテンツ表示。|
|Custom| カスタムイベントの作成。|

イベントのマッピング方法は以下の通りです:

1. ドロップダウンリストからイベントを選択します。  
事前定義されたリストから選択するか、カスタムイベントを作成することができます。
1. カスタムイベントの場合、それを識別する名前を入力します。
1. トリガーフィールドに、この宛先にマッピングする変数の値を入力します。  
値が見つかると、ページ上でイベントがトリガーされます。
1. より多くのイベントをマッピングするには、プラス (**&#43;**) ボタンをクリックして、手順 #1 と #2 を繰り返します。
1. **適用**をクリックします。

マッピングが完了したら、保存して公開します。これで完了です！プロファイルでタグの構成が成功しました。

### 限定データ処理（LDP）

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `opt_out_type` | 文字列 | オプトアウトタイプ。   |
| `st` | 文字列 | オプトアウト状態。  | 
| `country` | 文字列 | オプトアウト国。   | 

## ベンダー文書

* [Pinterest: Pinterestタグについて](https://help.pinterest.com/en/articles/website-conversion-tracking)
* [Pinterest: 広告マネージャーガイド](https://business.pinterest.com/sites/business/files/pinterest-ads-manager-guide.pdf)
