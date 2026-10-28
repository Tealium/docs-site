---
title: 顧客支出レベルガイド
description: このガイドでは、指定した期間内の支出額に基づいて、訪問をリアルタイムでターゲティングする方法について説明します。
url: https://docs.tealium.com/ja/guides/customer-spending-levels-guide/
---
## メリット

顧客の支出レベルに基づいて戦略を構築することには、次のようなメリットがあります。

* **顧客エンゲージメントのパーソナライズ**：
    * 支出額の少ない顧客に対し、支出行動に合った初回購入者向けオファー、割引、商品レコメンデーションを提供し、追加購入を促します。
    * 支出額が中程度の顧客をクロスセルやアップセルの機会の対象とし、より支出額の高いカテゴリーへ誘導します。
    * 支出額の多い顧客に限定特典やロイヤルティインセンティブを提供し、顧客維持をエンリッチメントして顧客生涯価値を高めます。
* **予算配分の最適化**：支出レベル別にキャンペーンをセグメント化することで、マーケティング予算を効果的に配分し、成長または維持の可能性が最も高い顧客セグメントにリソースを集中できます。
* **顧客インサイトのエンリッチメント**：顧客の支出パターンを追跡することで、季節ごとの行動や商品の好みなどの傾向を特定し、戦略や在庫計画を調整できます。
* **キャンペーンのROI向上**：支出レベルに応じてメッセージやオファーを調整することで、コンバージョンの可能性が高まり、マーケティング投資からより高い収益を得られます。

## 測定対象

顧客の支出レベルは、いくつかの方法で追跡できます。

* 一定期間に顧客が支出した合計金額を追跡する。
* 顧客が購入ごとに支出する平均金額を追跡する。
* 支出額の経時的な傾向と、その増減を追跡する。

このガイドでは、基本的な追跡構成の作成方法を説明します。顧客生涯全体の支出合計、30日間の支出、60日間の支出期間の追跡が含まれます。その後、各期間について顧客を支出額の低いグループと高いグループにセグメント化します。

訪問を特定した後、メールマーケティングサービスへのサーバーサイドコネクタを通じて、訪問に対するアクションを実行できます。

## 要件

このユースケースには、次のものが必要です。

* 追跡対象イベント：
* Tealium AudienceStream

一般に、購入アクティビティを追跡して顧客の支出レベルを評価するには、次のイベント属性が役立ちます。実際の属性名は異なる場合があります。

| 属性名                  | 値の例 |
|------------------------|--------|
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

小売向けデータレイヤーの定義について詳しくは、[retail](https://docs.tealium.com/retail/)を参照してください。

### 必須のAudienceStream属性

| 属性名 | タイプ | スコープ | 説明 |
|--------|--------|----------|------|
| 購入済み | ブール値 | 訪問 | **購入**イベントが発生したことを示します。 |
| メールアドレス | 文字列 | 訪問 | 訪問のメールアドレスを取得します。 |
| 生涯購入合計 | 数値 | 訪問 | 訪問の生涯における購入額の合計を収集します。 |
| 30日間の購入 | タイムライン | 訪問 | 過去30日間の訪問による購入を収集します。 |
| 60日間の購入 | タイムライン | 訪問 | 過去30日間の訪問による購入を収集します。 |
| 30日間の購入累計 | 数値 | 訪問 | 過去30日間の訪問による購入額の合計を算出します。 |
| 60日間の購入累計 | 数値 | 訪問 | 過去30日間の訪問による購入額の合計を算出します。 |

## ステップ1：属性を作成する

次の属性を作成します。

### メールアドレス属性を作成する

`Email Address`という名前の文字列型訪問属性を、次のエンリッチメントを使用して作成します。

* `customer_email`が割り当てられている場合、**任意のイベント**で値を`customer_email`に構成します。

![](https://docs.tealium.com/images/guides/email_address_attribute.png)

### 購入済み属性を作成する

`Purchased`という名前のブール型訪問属性を、次のエンリッチメントを使用して作成します。

* **新規訪問**で`false`に構成します。
* `tealium_event`が`purchase`と**等しい（大文字と小文字を区別しない）**場合、**任意のイベント**で`true`に構成します。

![](https://docs.tealium.com/images/guides/boolean_purchased.png)

### 生涯購入合計属性を作成する

`Lifetime Purchase Total`という名前の数値型訪問属性を、次のエンリッチメントを使用して作成します。

* `Purchased`が**true**で、`order_total`が割り当てられている場合、**任意のイベント**で`order_total`の値を使用して**数値を増分**します。

![](https://docs.tealium.com/images/guides/lifetime_purchase_total_attribute.png)

### 30日間の購入タイムライン属性を作成する

`30 Day Purchases timeline`という名前のタイムライン型訪問属性を、次のエンリッチメントを使用して作成します。

* **タイムラインイベントの有効期限を構成**を`30 days`に構成します。
* **イベントを受信した時刻**に**タイムラインを更新**し、`Purchased`が**true**で、`order_total`が割り当てられている場合に、`order_total`の属性データを取得します。

![](https://docs.tealium.com/images/guides/30_day_purchases_timeline_attribute.png)

### 60日間の購入タイムライン属性を作成する

`60 Day Purchases timeline`という名前のタイムライン型訪問属性を、次のエンリッチメントを使用して作成します。

* **タイムラインイベントの有効期限を構成**を`60 days`に構成します。
* **任意のイベント**の**イベントを受信した時刻**に**タイムラインを更新**し、`Purchased`が**true**で、`order_total`が割り当てられている場合に、`order_total`の属性データを取得します。

![](https://docs.tealium.com/images/guides/60_day_purchases_timeline_attribute.png)

### 30日間の購入累計属性を作成する

`30 Day Purchases Running Total`という名前の数値型訪問属性を、次のエンリッチメントを使用して作成します。

* **数値を構成**を使用し、30日間の購入累計を、任意のイベントでタイムライン`30 Day Purchases`に取得された`order_total`の移動合計に構成します。

![](https://docs.tealium.com/images/guides/30_day_purchases_running_total_attribute.png)

### 60日間の購入累計属性を作成する

`60 Day Purchases Running Total`という名前の数値型訪問属性を、次のエンリッチメントを使用して作成します。

* **数値を構成**を使用し、60日間の購入累計を、任意のイベントでタイムライン`60 Day Purchases`に取得された`order_total`の移動合計に構成します。

![](https://docs.tealium.com/images/guides/60_day_purchases_running_total_attribute.png)

## ステップ2：オーディエンスを作成する

作成したバッジを使用して、オーディエンスを簡単に作成できるようになりました。

### 生涯高価値オーディエンスを作成する

次の条件で`High Value Lifetime`オーディエンスを作成します。

* **生涯購入合計**が`5000`以上
* **メールアドレス**が割り当てられている

![](https://docs.tealium.com/images/guides/high_value_lifetime_audience.png) 

### 生涯低価値オーディエンスを作成する

次の条件で`Low Value Lifetime`オーディエンスを作成します。

* **生涯購入合計**が`1000`以下
* **メールアドレス**が割り当てられている

![](https://docs.tealium.com/images/guides/low_value_lifetime_audience.png) 

### 30日間の高価値オーディエンスを作成する

次の条件で`High Value Lifetime`オーディエンスを作成します。

* **30日間の購入累計**が`1500`以下
* **メールアドレス**が割り当てられている

![](https://docs.tealium.com/images/guides/high_value_30_day_audience.png)
### 高価値の60日間オーディエンスを作成する

次の条件で `High Value Lifetime` オーディエンスを作成します。

* **60日間の購入額累計**が `3000` 以下
* **メールアドレス**が割り当てられている

![](https://docs.tealium.com/images/guides/high_value_60_day_audience.png) 

### 低価値の30日間オーディエンスを作成する

次の条件で `Low Value Lifetime` オーディエンスを作成します。

* **30日間の購入額累計**が `100` 以下
* **メールアドレス**が割り当てられている

![](https://docs.tealium.com/images/guides/low_value_30_day_audience.png) 

### 低価値の60日間オーディエンスを作成する

次の条件で `Low Value Lifetime` オーディエンスを作成します。

* **60日間の購入額累計**が `200` 以下
* **メールアドレス**が割り当てられている

![](https://docs.tealium.com/images/guides/low_value_60_day_audience.png) 

## ステップ3：コネクタを構成する

属性、バッジ、オーディエンスの構成が完了したら、この新しいオーディエンスをメールマーケティングツールに接続し、オーディエンスに再度働きかけてコンバージョンにつなげる準備が整います。

顧客の支出レベルに基づくキャンペーンでよく使用されるコネクタとアクションには、次のものがあります。

* [Adobe Campaign Classic](https://docs.tealium.com/adobe-campaign-classic-connector/)
* [Iterable](https://docs.tealium.com/iterable-connector/)：**ユーザーをリストに登録**、**ユーザーをアップサート**アクション
* [Marketo](https://docs.tealium.com/marketo-connector/)：**リードをリストに追加**アクション
* [SendGrid](https://docs.tealium.com/sendgrid-connector/)：**連絡先をアップサート**アクション

たとえば、訪問のメールアドレスを高価値顧客の支出リストに追加するように、Marketoコネクタを構成できます。訪問が「高価値の60日間」オーディエンスに参加したとき、または訪問終了時にそのオーディエンスに含まれている場合にのみトリガーされるように、コネクタアクションをカスタマイズします。

![](https://docs.tealium.com/images/guides/customer_spending_levels_marketo_connector_1.png) 

![](https://docs.tealium.com/images/guides/customer_spending_levels_marketo_connector_1.png) 

詳細については、を参照してください。

### 遅延アクション

ユーザーが特定の支出レベルに到達した直後にメールを送信し、その達成を評価するとともに、さらなる購入を促すことができます。ただし、対象オーディエンスへのメール送信を遅らせることで、コンバージョンの可能性が高まる場合があります。遅延アクションを使用してTealiumでコネクタアクションの遅延を構成し、選択したベンダーでメールワークフローをトリガーします。


<blockquote>
さらに購入することに関心がある訪問へリマーケティングするには、1時間の遅延を構成することをお勧めします。また、ほとんどのメールマーケティングツールには、顧客が受信したメール数を監視し、過剰なメッセージ送信を防ぐ機能があります。
</blockquote>


Tealiumで遅延アクションを使用する方法の詳細については、[about-delayed-actions](https://docs.tealium.com/about-delayed-actions/)を参照してください。

## 次のステップ

このガイドでは、支出レベルに基づく基本的なキャンペーンを構築する方法について説明しました。キャンペーンで追加の属性を使用することで、顧客行動への理解を深めることができます。次の表は、顧客の支出に関連する属性として考えられる選択肢の一部を示しています。

| 属性名 | 属性タイプ | スコープ | カテゴリ | 備考 |
|---|---|---|---|---|
| 商品の平均価格 | 数値 | 訪問 | ライフタイム行動 | 行動の全般的な把握と、今後のユースケース拡張に使用します。 |
| お気に入りのカテゴリ | 集計 | 訪問 | ライフタイム行動 | 行動の全般的な把握と、今後のユースケース拡張に使用します。 |

属性とオーディエンスを作成した後、追加の顧客行動属性を統合したり、Tealium Context APIなどの高度なパーソナライゼーション機能を活用したりすることで、キャンペーンをさらにエンリッチメントできます。詳細については、[Context APIについて](https://docs.tealium.com/about-context-api/)を参照してください。