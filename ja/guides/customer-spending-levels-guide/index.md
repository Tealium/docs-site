---
title: 顧客の支出レベルガイド
description: このガイドでは、指定された時間枠内で彼らが費やした金額に基づいてリアルタイムで訪問をターゲットにする方法について説明します。
url: https://docs.tealium.com/ja/guides/customer-spending-levels-guide/
---
## メリット

顧客の支出レベルに基づいて戦略を構築することは、以下の理由で有用です：

* **パーソナライズされた顧客エンゲージメント**：
    * 低支出の顧客に対して、彼らの支出行動に合わせた紹介オファー、割引、または商品推薦を通じて追加購入を促します。
    * 中間支出の顧客に対して、クロスセルまたはアップセルの機会を提供し、より高い支出カテゴリーへと誘導します。
    * 高支出の顧客には独占的な特典やロイヤリティインセンティブを提供し、顧客の保持をエンリッチメントし、生涯価値を増加させます。
* **最適化された予算配分**：支出レベルによってキャンペーンをセグメント化することで、マーケティング予算が効果的に配分され、成長または保持のための最も有望な顧客セグメントにリソースを集中させます。
* **エンリッチメントされた顧客洞察**：顧客の支出パターンを追跡することで、季節的な行動や商品の好みなどのトレンドを特定し、戦略や在庫計画を調整することができます。
* **キャンペーンのROI向上**：支出レベルに基づいてメッセージングとオファーを調整することで、コンバージョンの可能性が高まり、マーケティング投資のリターンが向上します。

## 測定するべきこと

顧客の支出レベルは、いくつかの異なる方法で追跡できます：

* 与えられた期間における顧客の総支出額を追跡します。
* 各購入ごとに顧客が支出する平均額を追跡します。
* 時間の経過とともに支出傾向を追跡し、それが増加するか減少するかを確認します。

このガイドでは、基本的な追跡構成の作成方法を示します。これには、顧客の生涯総支出、30日間の支出、および60日間の支出ウィンドウの追跡が含まれます。その後、各時間枠において顧客を低支出グループと高支出グループにセグメント化します。

訪問が特定された後、メールマーケティングサービスへのサーバーサイドコネクタを通じて彼らに対してアクションを取ることができます。

## 要件

このユースケースには、以下が必要です：

* 追跡されるイベント: 
* Tealium AudienceStream

一般的に、顧客の支出レベルを評価するために購入活動を追跡する際に役立つイベント属性は以下の通りです。実際の属性名は異なる場合があります。

| 属性名         | 例 |
|----------------------- |---------------|
| `customer_city` | `San Diego` |
| `customer_country` | `United States` |
| `customer_email` | `john.smith@example.com` |
| `customer_first_name` | `John` |
| `customer_id` | `8237572` |
| `customer_last_name` | `Smith` |
| `customer_postal_code` | `92101` |
| `customer_state` | `CA` |
| `order_currency_code` | `USD` |
| `order_total` | `2549.00` |
| `tealium_event` | `purchase` |

小売のデータレイヤー定義についての詳細は、[retail](https://docs.tealium.com/retail/)を参照してください。

### 必要なAudienceStream属性

| 属性名 | タイプ   | スコープ   | 説明                                                                                   |
|----------------|--------|---------|-----------------------------------------------------------------------------------------------|
| Purchased | Boolean | Visit | **Purchase** イベントが発生したことを示します。   |
| Email Address | String | Visitor | 訪問のメールアドレスをキャプチャします。   |
| Lifetime Purchase Total | Number | Visitor | 訪問の生涯の購入合計を収集します。 |
| 30 Day Purchases | Timeline | Visitor | 過去30日間の訪問の購入を収集します。 |
| 60 Day Purchases | Timeline | Visitor | 過去30日間の訪問の購入を収集します。 |
| 30 Day Purchases Running Total | Number | Visitor | 過去30日間の訪問の購入合計を数えます。 |
| 60 Day Purchases Running Total | Number | Visitor | 過去30日間の訪問の購入合計を数えます。 |

## ステップ1: 属性を作成する

以下の属性を作成します：

### Email Address属性を作成する

`Email Address`という名前の文字列訪問属性を以下のエンリッチメントで作成します：

* **ANY EVENT**で`customer_email`が割り当てられている場合に`customer_email`に構成します。

![](https://docs.tealium.com/images/guides/email_address_attribute.png)

### Purchased属性を作成する

`Purchased`という名前のブール型訪問属性を以下のエンリッチメントで作成します：

* **NEW VISIT**で`false`に構成します。
* **ANY EVENT**で`tealium_event`が**purchase**に**等しい（大文字小文字を無視）**場合に`true`に構成します。

![](https://docs.tealium.com/images/guides/boolean_purchased.png)

### Lifetime Purchase Total属性を作成する

`Lifetime Purchase Total`という名前の数値訪問属性を以下のエンリッチメントで作成します：

* **ANY EVENT**で`Purchased`が**true**であり、`order_total`が割り当てられている場合に`order_total`で**数値を増加**します。

![](https://docs.tealium.com/images/guides/lifetime_purchase_total_attribute.png)

### 30 Day Purchasesタイムライン属性を作成する

`30 Day Purchases timeline`という名前のタイムライン訪問属性を以下のエンリッチメントで作成します：

* **タイムラインイベントの有効期限を構成**して`30 days`にします。
* **イベント受信時にタイムラインを更新**し、`Purchased`が**true**であり、`order_total`が割り当てられている場合に属性データをキャプチャします。

![](https://docs.tealium.com/images/guides/30_day_purchases_timeline_attribute.png)

### 60 Day Purchasesタイムライン属性を作成する

`60 Day Purchases timeline`という名前のタイムライン訪問属性を以下のエンリッチメントで作成します：

* **タイムラインイベントの有効期限を構成**して`60 days`にします。
* **ANY EVENT**で**イベント受信時にタイムラインを更新**し、`Purchased`が**true**であり、`order_total`が割り当てられている場合に属性データをキャプチャします。

![](https://docs.tealium.com/images/guides/60_day_purchases_timeline_attribute.png)

### 30 Day Purchases Running Total属性を作成する

`30 Day Purchases Running Total`という名前の数値訪問属性を以下のエンリッチメントで作成します：

* **ANY EVENT**でタイムライン`30 Day Purchases`でキャプチャされた`order_total`の合計をローリングサムとして**数値を構成**します。

![](https://docs.tealium.com/images/guides/30_day_purchases_running_total_attribute.png)

### 60 Day Purchases Running Total属性を作成する

`60 Day Purchases Running Total`という名前の数値訪問属性を以下のエンリッチメントで作成します：

* **ANY EVENT**でタイムライン`60 Day Purchases`でキャプチャされた`order_total`の合計をローリングサムとして**数値を構成**します。

![](https://docs.tealium.com/images/guides/60_day_purchases_running_total_attribute.png)

## ステップ2: オーディエンスを作成する

これで、作成したバッジを使用して簡単にオーディエンスを作成することができます。

### High Value Lifetimeオーディエンスを作成する

以下の条件で`High Value Lifetime`オーディエンスを作成します：

* **Lifetime purchase total**が`5000`以上である
* **Email Address**が割り当てられている

![](https://docs.tealium.com/images/guides/high_value_lifetime_audience.png) 

### Low Value Lifetimeオーディエンスを作成する

以下の条件で`Low Value Lifetime`オーディエンスを作成します：

* **Lifetime purchase total**が`1000`以下である
* **Email Address**が割り当てられている

![](https://docs.tealium.com/images/guides/low_value_lifetime_audience.png) 

### High Value 30 Dayオーディエンスを作成する

以下の条件で`High Value Lifetime`オーディエンスを作成します：

* **30 Day Purchases Running Total**が`1500`以下である
* **Email Address**が割り当てられている

![](https://docs.tealium.com/images/guides/high_value_30_day_audience.png) 
### 60日間の高価値オーディエンスの作成

以下の条件で `High Value Lifetime` オーディエンスを作成します：

* **60日間の購入累計** が `3000` 以下
* **メールアドレス** が割り当てられている

![](https://docs.tealium.com/images/guides/high_value_60_day_audience.png) 

### 30日間の低価値オーディエンスの作成

以下の条件で `Low Value Lifetime` オーディエンスを作成します：

* **30日間の購入累計** が `100` 以下
* **メールアドレス** が割り当てられている

![](https://docs.tealium.com/images/guides/low_value_30_day_audience.png) 

### 60日間の低価値オーディエンスの作成

以下の条件で `Low Value Lifetime` オーディエンスを作成します：

* **60日間の購入累計** が `200` 以下
* **メールアドレス** が割り当てられている

![](https://docs.tealium.com/images/guides/low_value_60_day_audience.png) 

## ステップ3: コネクタの構成

属性、バッジ、オーディエンスの構成が完了したら、これらの新しいオーディエンスをメールマーケティングツールに接続して、再エンゲージメントとコンバージョンを図ります。

顧客の支出レベルキャンペーンに一般的なコネクタとアクションには以下が含まれます：

* [Adobe Campaign Classic](https://docs.tealium.com/adobe-campaign-classic-connector/)
* [Iterable](https://docs.tealium.com/iterable-connector/): **リストへのユーザー登録**、**ユーザーのアップサート** アクション
* [Marketo](https://docs.tealium.com/marketo-connector/): **リストへのリード追加** アクション
* [SendGrid](https://docs.tealium.com/sendgrid-connector/): **コンタクトのアップサート** アクション

例えば、Marketo コネクタを構成して、訪問のメールアドレスを高価値顧客支出リストに追加することができます。コネクタアクションをカスタマイズして、訪問が60日間の高価値オーディエンスに参加した場合、または訪問の終わりにそのオーディエンスにいる場合にのみトリガーします。

![](https://docs.tealium.com/images/guides/customer_spending_levels_marketo_connector_1.png) 

![](https://docs.tealium.com/images/guides/customer_spending_levels_marketo_connector_1.png) 

詳細については、を参照してください。

### 遅延アクション

特定の支出レベルを達成した直後にユーザーにメールを送信して、その成果を認め、さらなる支出を促すことがよくありますが、ターゲットオーディエンスに対してメールを遅延させることで、コンバージョンの可能性が高まる場合があります。Tealiumでコネクタアクションの遅延を構成し、選択したベンダーでメールワークフローをトリガーします。


<blockquote>
購入意欲のある訪問を再マーケティングするために、1時間の遅延を構成することをお勧めします。また、ほとんどのメールマーケティングツールは、顧客が受け取ったメールの数を監視する機能を提供しており、メッセージで顧客を圧倒しないようにします。
</blockquote>


Tealiumで遅延アクションを使用する方法についての詳細は、[about-delayed-actions](https://docs.tealium.com/about-delayed-actions/)を参照してください。

## 次のステップ

このガイドでは、基本的な支出レベルベースのキャンペーンの構築方法を示しています。キャンペーンで追加の属性を使用することで、顧客の行動をより深く理解することができます。以下の表は、顧客の支出関連属性のいくつかの可能なオプションを示しています：

| 属性名                  | 属性タイプ | スコープ  | カテゴリ         | メモ |
|---|---|---|---|---|
| 平均アイテム価格              | 数値         | 訪問| ライフタイム行動 | 一般的な行動理解と将来のユースケース拡張のため。           |
| お気に入りカテゴリ             | 集計          | 訪問| ライフタイム行動 | 一般的な行動理解と将来のユースケース拡張のため。          |

属性とオーディエンスを作成した後、追加の顧客行動属性を統合することでキャンペーンをさらにエンリッチメントしたり、Tealium Context APIのような高度なパーソナライゼーション機能を活用することができます。詳細については、[About Context API](https://docs.tealium.com/about-context-api/)を参照してください。