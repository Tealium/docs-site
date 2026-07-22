---
title: 顧客の支出レベルガイド
description: このガイドでは、指定した期間内に彼らが支払った金額に基づいて、リアルタイムで訪問をターゲットにする方法を説明します。
url: https://docs.tealium.com/ja/guides/customer-spending-levels-guide/
---
## 利点

顧客の支出レベルを基にした戦略を構築することは、以下の理由で有用です：

* **パーソナライズされた顧客エンゲージメント**：
    * 低支出者に対しては、彼らの支出行動に合わせた初回オファー、割引、または商品の推奨を通じて追加の購入を促します。
    * 中間の支出者に対しては、クロスセルまたはアップセルの機会を提供し、より高い支出カテゴリーへと誘導します。
    * 高支出者に対しては、独占的な特典やロイヤルティインセンティブを提供し、リテンションをエンリッチメントし、ライフタイムバリューを増加させます。
* **最適化された予算配分**：支出レベルによるキャンペーンのセグメンテーションにより、マーケティング予算が効果的に分配され、成長または保持のための最も有望な顧客セグメントにリソースを集中します。
* **エンリッチメントされた顧客洞察**：顧客の支出パターンを追跡することで、季節性の行動や商品の嗜好などのトレンドを特定し、戦略や在庫計画を調整することができます。
* **キャンペーンのROIの改善**：支出レベルに基づいてメッセージングとオファーをカスタマイズすることで、コンバージョンの可能性が高まり、マーケティング投資のリターンが高まります。

## 測定するもの

顧客の支出レベルは、いくつかの異なる方法で追跡することができます：

* 顧客が特定の期間に支払った総額を追跡します。
* 顧客が各購入で支払う平均額を追跡します。
* 時間とともに支出のトレンドを追跡し、それが増加するか減少するかを追跡します。

このガイドでは、基本的な追跡構成を作成する方法を示します。これには、総ライフタイム支出、30日間の支出、60日間の支出ウィンドウの追跡が含まれます。その後、各時間枠で低支出グループと高支出グループに顧客をセグメント化します。

訪問が特定された後、サーバーサイドコネクタを通じてメールマーケティングサービスに対してアクションを実行することができます。

## 必要条件

このユースケースでは、以下が必要です：

* 追跡されたイベント: 
* Tealium AudienceStream

一般的に、以下のイベント属性は、購入活動を追跡し、顧客の支出レベルを評価するのに役立ちます。実際の属性名は異なる場合があります。

| 属性名         | 例の値 |
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
| Email Address | String | Visitor | 訪問のメールアドレスを取得します。   |
| Lifetime Purchase Total | Number | Visitor | 訪問のライフタイム中の購入総額を収集します。 |
| 30 Day Purchases | Timeline | Visitor | 過去30日間の訪問による購入を収集します。 |
| 60 Day Purchases | Timeline | Visitor | 過去30日間の訪問による購入を収集します。 |
| 30 Day Purchases Running Total | Number | Visitor | 過去30日間の訪問による購入総額を計算します。 |
| 60 Day Purchases Running Total | Number | Visitor | 過去30日間の訪問による購入総額を計算します。 |

## ステップ1：属性を作成する

以下の属性を作成します：

### Email Address属性を作成する

以下のエンリッチメントで`Email Address`という名前の文字列訪問属性を作成します：

* `customer_email`が割り当てられている場合、**ANY EVENT**で`customer_email`に構成します。

![](https://docs.tealium.com/images/guides/email_address_attribute.png)

### Purchased属性を作成する

以下のエンリッチメントで`Purchased`という名前のブール訪問属性を作成します：

* **NEW VISIT**で`false`に構成します。
* `tealium_event`が`purchase`に**等しい（大文字小文字を無視）**場合、**ANY EVENT**で`true`に構成します。

![](https://docs.tealium.com/images/guides/boolean_purchased.png)

### Lifetime Purchase Total属性を作成する

以下のエンリッチメントで`Lifetime Purchase Total`という名前の数値訪問属性を作成します：

* `Purchased`が**trueである**場合、かつ`order_total`が割り当てられている場合、**ANY EVENT**で`order_total`によって**Numberを増加**させます。

![](https://docs.tealium.com/images/guides/lifetime_purchase_total_attribute.png)

### 30 Day Purchases timeline属性を作成する

以下のエンリッチメントで`30 Day Purchases timeline`という名前のタイムライン訪問属性を作成します：

* **Set Expiration For Timeline Events**を`30 days`に構成します。
* `Purchased`が**trueである**場合、かつ`order_total`が割り当てられている場合、**Time of event received**で**Update Timeline**を行い、`order_total`の属性データを取得します。

![](https://docs.tealium.com/images/guides/30_day_purchases_timeline_attribute.png)

### 60 Day Purchases timeline属性を作成する

以下のエンリッチメントで`60 Day Purchases timeline`という名前のタイムライン訪問属性を作成します：

* **Set Expiration For Timeline Events**を`60 days`に構成します。
* `Purchased`が**trueである**場合、かつ`order_total`が割り当てられている場合、**ANY EVENT**で**Time of event received**で**Update Timeline**を行い、`order_total`の属性データを取得します。

![](https://docs.tealium.com/images/guides/60_day_purchases_timeline_attribute.png)

### 30 Day Purchases Running Total属性を作成する

以下のエンリッチメントで`30 Day Purchases Running Total`という名前の数値訪問属性を作成します：

* **Set Number** 30 Day Purchases Running Totalを、ANY EVENTでタイムライン`30 Day Purchases`で取得した`order_total`のローリング合計に構成します。

![](https://docs.tealium.com/images/guides/30_day_purchases_running_total_attribute.png)

### 60 Day Purchases Running Total属性を作成する

以下のエンリッチメントで`60 Day Purchases Running Total`という名前の数値訪問属性を作成します：

* **Set Number** 60 Day Purchases Running Totalを、ANY EVENTでタイムライン`60 Day Purchases`で取得した`order_total`のローリング合計に構成します。

![](https://docs.tealium.com/images/guides/60_day_purchases_running_total_attribute.png)

## ステップ2：オーディエンスを作成する

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

### High Value 60 Dayオーディエンスを作成する

以下の条件で`High Value Lifetime`オーディエンスを作成します：
* **60日間の購入合計**が`3000`以下
* **メールアドレス**が割り当てられている

![](https://docs.tealium.com/images/guides/high_value_60_day_audience.png) 

### 30日間の低価値オーディエンスを作成する

以下の条件で`Low Value Lifetime`オーディエンスを作成します：

* **30日間の購入合計**が`100`以下
* **メールアドレス**が割り当てられている

![](https://docs.tealium.com/images/guides/low_value_30_day_audience.png) 

### 60日間の低価値オーディエンスを作成する

以下の条件で`Low Value Lifetime`オーディエンスを作成します：

* **60日間の購入合計**が`200`以下
* **メールアドレス**が割り当てられている

![](https://docs.tealium.com/images/guides/low_value_60_day_audience.png) 

## ステップ3：コネクタを構成する

属性、バッジ、オーディエンスが構成されたら、この新しいオーディエンスをメールマーケティングツールに接続し、これらのオーディエンスを再エンゲージメントし、コンバートする準備が整います。

顧客の支出レベルキャンペーンに対する一般的なコネクタとアクションには以下のようなものがあります：

* [Adobe Campaign Classic](https://docs.tealium.com/adobe-campaign-classic-connector/)
* [Iterable](https://docs.tealium.com/iterable-connector/): **ユーザーをリストに登録する**、**ユーザーをアップサートする**アクション
* [Marketo](https://docs.tealium.com/marketo-connector/): **リードをリストに追加する**アクション
* [SendGrid](https://docs.tealium.com/sendgrid-connector/): **コンタクトをアップサートする**アクション

例えば、Marketoコネクタを構成して、訪問のメールアドレスを高価値顧客支出リストに追加することができます。コネクタのアクションをカスタマイズして、訪問がHigh Value 60 Dayオーディエンスに参加したときや、訪問の終わりにそのオーディエンスにいるときだけトリガーするようにします。

![](https://docs.tealium.com/images/guides/customer_spending_levels_marketo_connector_1.png) 

![](https://docs.tealium.com/images/guides/customer_spending_levels_marketo_connector_1.png) 

詳細については、を参照してください。

### 遅延アクション

特定の支出レベルを達成した直後にユーザーにメールを送信してその達成を認め、さらなる支出を促すことがよくありますが、ターゲットオーディエンスに対するメールの送信を遅らせることで、コンバージョンの可能性が高まるかもしれません。Tealiumでコネクタアクションの遅延を構成し、選択したベンダーでメールワークフローをトリガーするために遅延アクションを使用します。


<blockquote>
より多くの購入に興味がある訪問に再マーケティングするために、1時間の遅延を構成することをお勧めします。また、ほとんどのメールマーケティングツールは、顧客が受け取ったメールの数を監視する機能を提供しており、メッセージで彼らを圧倒しないようにします。
</blockquote>


Tealiumで遅延アクションを使用する方法の詳細については、[about-delayed-actions](https://docs.tealium.com/about-delayed-actions/)を参照してください。

## 次のステップ

このガイドでは、基本的な支出レベルベースのキャンペーンの構築方法を説明しています。キャンペーンに追加の属性を使用することで、顧客の行動についての理解を深めることができます。以下の表は、顧客の支出に関連する属性の可能性をいくつか示しています：

| 属性名                  | 属性タイプ | スコープ  | カテゴリ         | ノート |
|---|---|---|---|---|
| 平均アイテム価格              | 数値         | 訪問| ライフタイム行動 | 一般的な行動理解と将来のユースケース拡張。           |
| お気に入りのカテゴリ             | 集計          | 訪問| ライフタイム行動 | 一般的な行動理解と将来のユースケース拡張。          |

属性とオーディエンスを作成した後、追加の顧客行動属性を統合したり、Tealium Moments APIのような高度なパーソナライゼーション機能を利用したりして、キャンペーンをさらにエンリッチメントすることができます。詳細については、[About Moments API](https://docs.tealium.com/about-moments-api/)を参照してください。