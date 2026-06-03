---
title: Criteo OneTag タグの構成ガイド
description: この記事では、Tealium iQ Tag Management アカウントに Criteo OneTag タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/criteo-onetag-tag/
---
## タグのヒント

* マッピングを使用して以下の値を構成します：
  * アカウント ID の上書き
  * 必須およびオプションのパラメータの構成
  * イベントのトリガーとイベントパラメータの値の構成

* サポートされる E-コマース拡張パラメータ：
  * 注文 ID (`_corder`)
  * 製品 ID のリスト (`_cprod`)
  * 数量のリスト (`_cquan`)
  * 価格のリスト (`_cprice`)

## タグの構成

まず、タグマーケットプレイスに移動し、Criteo OneTag タグを追加します（[タグの追加方法について詳しくはこちら]()）。

タグを追加した後、以下の構成を構成します：

* **アカウント ID**：必須。複数のアカウントの場合は、カンマで区切ってください。
* **ページビュー ID の生成**：Criteo トラッキングイベントごとに自動的にページビュー ID を生成し、コネクタの重複を回避します。

## データマッピング

マッピングとは、[データレイヤー変数]()からベンダータグの対応する変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法についての手順は、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

| タグの宛先         | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|:--------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| アカウント ID       | &lt;ul&gt;&lt;li&gt;Criteo アカウント番号。&lt;/li&gt;&lt;li&gt;`account` を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                          |
| `email`             | &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;顧客のメールアドレス。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                               |
| `retailer_visitor_id` | &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;リテーラーの訪問 ID&lt;/li&gt;&lt;li&gt;同じデバイスで複数のセッションで一貫して使用される一意の未認証 ID。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                         |
| `customer_id`       | &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;顧客 ID&lt;/li&gt;&lt;li&gt;すべてのログインセッションで一貫して使用される認証済みユーザーの識別子。&lt;/li&gt;&lt;li&gt;Criteo では、この ID に名前、メールアドレス、暗号化されていない電話番号などの個人を特定できる情報を含めないようにする必要があります。&lt;/li&gt;&lt;li&gt;顧客が不明な場合やサイトに一意の ID がない場合は空のままにしてください。&lt;/li&gt;&lt;li&gt;この変数は、e-コマース拡張の `_ccustid` 変数とは関係ありません。&lt;/li&gt;&lt;/ul&gt; |
| `site_type`         | &lt;ul&gt;&lt;li&gt;サイトのタイプ。&lt;/li&gt;&lt;li&gt;サイトのバージョン。&lt;/li&gt;&lt;li&gt;次のいずれかの値を指定できます：&lt;ul&gt;&lt;li&gt;`m` - サイトのモバイルバージョン&lt;/li&gt;&lt;li&gt;`t` - サイトのタブレットバージョン&lt;/li&gt;&lt;li&gt;`d`（デフォルト） - サイトのクラシックバージョン。これは通常、ブラウザがアクセスするサイトです。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt;                                                                                                                                                  |
| `hashed_email`      | &lt;ul&gt;&lt;li&gt;ハッシュ化されたメールアドレス。&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;顧客のハッシュ化されたメールアドレス。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                      |
| `zip_code`          | &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;顧客の郵便番号。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                                   |

### E-コマース

| タグの宛先       | 説明                                                                                                                                                                                                 |
|:------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `order_id`       | &lt;ul&gt;&lt;li&gt;注文 ID&lt;/li&gt;&lt;li&gt;一意のトランザクション識別子。&lt;/li&gt;&lt;li&gt;`_corder` を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                    |
| 製品 ID           | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品 ID&lt;/li&gt;&lt;li&gt;製品配列内の各製品の一意の識別子。&lt;/li&gt;&lt;li&gt;`_cprod` を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                     |
| 製品価格         | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品配列内の各製品の単価。&lt;/li&gt;&lt;li&gt;`_cprice` を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                           |
| 製品数量         | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品配列内の各製品の数量。&lt;/li&gt;&lt;li&gt;`_cquan` を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                           |

### イベント

ページで Criteo イベントをトリガーするには、変数をこれらの宛先にマッピングします。指定した値がデータレイヤーで見つかった場合、イベントがトリガーされます。

1. **イベント** ドロップダウンリストからイベントを選択します。
1. **トリガー** フィールドにマッピングされる変数の値を入力します。
1. **&#43; 追加** をクリックします。
1. 追加のイベントをマッピングするには、手順 1、2、3 を繰り返します。

| イベント名           | 説明                       |
|:---------------------|:---------------------------|
| `viewHome`           | ホームページが表示されました。 |
| `viewCategory`       | 製品カテゴリが表示されました。 |
| `viewSearchResult`   | 検索結果が表示されました。   |
| `viewItem`           | 製品が表示されました。       |
| `viewBasket`         | カートが表示されました。     |
| `viewList`           | 製品リストが表示されました。 |
| `addToCart`          | 製品がカートに追加されました。 |
| `trackTransaction`   | トランザクションページのアクティビティ。 |

### ロードルール

[ロードルール]() は、Criteo OneTag のインスタンスをサイトのどのページでいつ読み込むかを決定します。

カスタムのロードルールを作成して、Criteo イベントをトリガーする任意のページでこのタグを読み込むようにします。たとえば、コンバージョンイベントを追跡している場合は、このタグをチェックアウトページや確認ページで読み込みます。

### データマッピング

マッピングとは、[データレイヤー変数]()からベンダータグの対応する変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法についての手順は、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Criteo OneTag の宛先変数は、**データマッピング** タブに組み込まれています。利用可能な宛先変数については、次のセクションで説明します。

#### イベントでパラメータを渡す

マッピングした Criteo イベントの宛先に追加のデータを渡すには、変数を対応するパラメータにマッピングします。ユーザーが製品リストをフィルタリングした場合、フィルターをパラメータとして含めることができます。

マッピングされた Criteo イベントにパラメータを渡すには：

1. **イベント** ドロップダウンリストからイベントを選択します。
1. **パラメータ** ドロップダウンリストからパラメータを選択します。
1. **&#43; 追加** をクリックします。

利用可能なパラメータとフィルターは、次の表に示すように、選択したイベントによって異なります：

| イベント                                 | パラメータ                                                                                                 | フィルター                                               |
|:--------------------------------------|:-----------------------------------------------------------------------------------------------------------|:------------------------------------------------------|
| `viewHome`                            | &lt;ul&gt;&lt;li&gt;ページ ID&lt;/li&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;/ul&gt;                                                                   | &lt;ul&gt;&lt;li&gt;なし&lt;/li&gt;&lt;/ul&gt;                                |
| `viewCategory`&lt;br&gt; `viewSearchResult` | &lt;ul&gt;&lt;li&gt;アイテム&lt;/li&gt;&lt;li&gt;キーワード&lt;/li&gt;&lt;li&gt;カテゴリ&lt;/li&gt;&lt;li&gt;ページ番号&lt;/li&gt;&lt;li&gt;ページ ID&lt;/li&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;/ul&gt; | &lt;ul&gt;&lt;li&gt;名前&lt;/li&gt;&lt;li&gt;演算子&lt;/li&gt;&lt;li&gt;値&lt;/li&gt;&lt;/ul&gt; |
| `viewItem`                            | &lt;ul&gt;&lt;li&gt;アイテム&lt;/li&gt;&lt;li&gt;価格&lt;/li&gt;&lt;li&gt;在庫状況&lt;/li&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;/ul&gt;                                   | &lt;ul&gt;&lt;li&gt;なし&lt;/li&gt;&lt;/ul&gt;                                |
| `viewBasket`&lt;br&gt; `addToCart`          | &lt;ul&gt;&lt;li&gt;ページ ID&lt;/li&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;/ul&gt;                                                                   | &lt;ul&gt;&lt;li&gt;ID&lt;/li&gt;&lt;li&gt;価格&lt;/li&gt;&lt;li&gt;数量&lt;/li&gt;&lt;/ul&gt;   |
| `viewList`                            | &lt;ul&gt;&lt;li&gt;アイテム&lt;/li&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;/ul&gt;                                                                      | &lt;ul&gt;&lt;li&gt;なし&lt;/li&gt;&lt;/ul&gt;                                |
| `trackTransaction`                    | &lt;ul&gt;&lt;li&gt;トランザクション ID&lt;/li&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;/ul&gt;                                                            | &lt;ul&gt;&lt;li&gt;ID&lt;/li&gt;&lt;li&gt;価格&lt;/li&gt;&lt;li&gt;数量&lt;/li&gt;&lt;/ul&gt;   |

## ベンダーのドキュメント

* [Criteo OneTag の概要](https://support.criteo.com/s/article?article=criteo-onetag&amp;language=en_US)
* [Sponsored Products のための Criteo OneTag](https://support.criteo.com/s/article?article=360001467585-Criteo-OneTag-for-Sponsored-Products&amp;language=en_US)
* [Criteo サポートセンター](https://support.criteo.com/hc/en-us)（ログインが必要です）


