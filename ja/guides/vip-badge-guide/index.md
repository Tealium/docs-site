---
title: VIP バッジ
description: このガイドでは、最も重要な顧客を識別するための VIP バッジを作成する方法について説明します。
url: https://docs.tealium.com/ja/guides/vip-badge-guide/
---
## 仕組み

![](https://docs.tealium.com/images/server-side/getting-started-audiencestream-badge-vip.png)

VIP とは、サイトに繰り返しアクセスして購入する価値の高い顧客です。VIP は、他の顧客よりも購入する可能性が高く、他のオーディエンスほど価格に敏感ではないため、ターゲットに適したオーディエンスです。

### 条件

VIP 訪問を決定する指標は、業界によって異なります。ビジネスにおける VIP 訪問の定義例を次に示します。

* **旅行**：移動距離、利用金額、訪問した都市数や国数に基づいて VIP を評価できます。
* **金融**：金融機関が保有する個人の資産総額に基づいて VIP を評価できます。
* **メディア**：顧客がプレミアムサービスやサブスクリプションに費やした金額、またはオンデマンド製品に費やした金額に基づいて VIP ステータスを評価できます。
* **テクノロジー**：顧客が最新の製品やサービスに費やした金額に基づいて VIP ステータスを評価できます。

また、VIP の主要指標を測定する方法とタイミングを決めることもできます。

* **累積しきい値**：注文総額、総移動距離、ロイヤルティポイントの合計など。
* **時間ベースのしきい値**：特定の期間における合計値。
* **ソーシャルエンゲージメントのしきい値**：訪問によるブランド関連の投稿への「いいね」の数など、ソーシャルメディアを通じたブランドとのやり取り。
* **フィードバックおよびレビューのエンゲージメントしきい値**：肯定的なフィードバックやレビューを提供する訪問。

Tealium AudienceStream では、異なる条件としきい値を使用して複数の VIP オーディエンスを作成し、各 VIP オーディエンスに合わせてエクスペリエンスを調整できます。

## 要件

#### 必須イベント属性

| 属性名 | タイプ | 例 |
| --- | --- | --- |
| `order_id` | UDO 変数 | `123456` |
| `order_subtotal` | UDO 変数 | `1500.00` |
| `customer_email` | UDO 変数 | `user@example.com` |

#### 必須訪問属性

ライフタイムバリューの例：

| 属性名 | タイプ |
| --- | --- |
| 顧客のメールアドレス | 文字列 |
| ライフタイム注文合計 | 文字列 |

時間ベースの例：

| 属性名 | タイプ |
| --- | --- |
| 顧客のメールアドレス | 文字列 |
| 過去 90 日間のローリング注文合計 | タイムライン |
| 過去 90 日間の注文小計 | 数値 |

## ライフタイムバリューの例

次の例では、ライフタイムの利用額が 10,000 ドルを超える顧客向けの VIP バッジを作成し、そのバッジを持つ訪問でオーディエンスを作成します。

### ステップ 1 - 属性を作成する

最初に、「Lifetime order total」という訪問数値属性を、次のエンリッチメントを使用して作成します。

```
Increment or Decrement Number by "order_subtotal"
WHEN: Any event
Rule "tealium_event" equals (ignore case) "purchase"
Rule "order_id" is assigned
```

![](https://docs.tealium.com/images/guides/lifetime-order-total-attribute.png)

次に、訪問のメールアドレスを収集するため、「Customer email」という訪問文字列属性を作成します。

```
Set String to customer_email
WHEN: Any event
Rule "customer_email" is assigned.
Rule "customer_email" contains "@"
```

![](https://docs.tealium.com/images/guides/customer-email-attribute-assigned.png)

属性の追加について詳しくは、[属性を追加する](https://docs.tealium.com/manage-as-attributes/#add-an-attribute)を参照してください。

### ステップ 2 - VIP バッジを作成する

訪問が費やした合計金額と、メールアドレスがあるかどうかを測定できるようになったため、これらの属性に基づいて VIP バッジを作成できます。

「Customer VIP」という訪問バッジ属性を、次のエンリッチメントを使用して作成します。

```
Assign this badge to visitor
WHEN: Any event
Rule "Lifetime Order Total" greater than or equal to "10000"
Rule "Customer email" is assigned
```

![](https://docs.tealium.com/images/guides/customer-vip-badge-lifetime-total.png)

### ステップ 3 - オーディエンスを作成する

これで、VIP バッジに基づいてオーディエンスを作成できます。

1. **Audiences** に移動します。
1. **+ New Audience** をクリックします。
1. **Title** フィールドに `VIP` と入力します。
1. **Where** ドロップダウンリストから **Customer VIP** を選択します。
1. **is assigned** を選択します。
1. **Done** をクリックします。

![](https://docs.tealium.com/images/guides/vip-badge-audience.png)

詳しくは、を参照してください。

## 時間ベースの例

次の例では、過去 90 日間に 10,000 ドル分を購入した顧客向けの VIP バッジを作成し、そのバッジを持つ訪問でオーディエンスを作成します。要件を満たさなくなった訪問は、90 日後にオーディエンスから削除されます。

### ステップ 1 - 属性を作成する

最初に、「Order subtotals in past 90 days」という訪問タイムライン属性を、次の 2 つのエンリッチメントを使用して作成します。

```
Set each event in timeline Order subtotals in past 90 days to expire after 90 days
WHEN: Any event

Record an event for timeline Order subtotals in past 90 days
Capture data for "order_subtotal"
WHEN: New visit
```

![](https://docs.tealium.com/images/guides/order-subtotals-in-past-90-days.png)

次に、訪問のメールアドレスを収集するため、「Customer email」という訪問文字列属性を作成します。

```
Set String to customer_email
WHEN: Any event
Rule "customer_email" is assigned.
Rule "customer_email" contains "@"
```

![](https://docs.tealium.com/images/guides/customer-email-attribute-assigned.png)

続いて、「Rolling order total for past 90 days」という訪問数値属性を、次のエンリッチメントを使用して作成します。

```
Set Number Rolling order total for past 90 days to the rolling sum of order_subtotal captures in timeline Order subtotals in past 90 days
WHEN Any event
```

![](https://docs.tealium.com/images/guides/rolling-order-total-for-past-90-days.png)

### ステップ 2 - VIP バッジを作成する

訪問が費やした合計金額と、メールアドレスがあるかどうかを測定できるようになったため、これらの属性に基づいて VIP バッジを作成できます。

「Customer VIP」という訪問バッジ属性を、次のエンリッチメントを使用して作成します。

```
Assign this badge to visitor
WHEN: Any event
Rule "Rolling order total for past 90 days" greater than or equal to "10000"

Remove this badge to visitor
WHEN: Any event
Rule "Rolling order total for past 90 days" less than "10000"
```

![](https://docs.tealium.com/images/guides/customer-vip-rolling-total.png)

### ステップ 3 - オーディエンスを作成する

これで、VIP バッジに基づいてオーディエンスを作成できます。

1. **Audiences** に移動します。
1. **+ New Audience** をクリックします。
1. **Title** フィールドに `VIP` と入力します。
1. **Where** ドロップダウンリストから **Customer VIP** を選択します。
1. **is assigned** を選択します。
1. **Options** で、保持期間として 90 日を選択します。
1. **Done** をクリックします。

![](https://docs.tealium.com/images/guides/vip-badge-audience.png)

詳しくは、を参照してください。
## オーディエンスをアクティベートする

この時点で、数百に及ぶベンダー連携を通じてオーディエンスをアクティベートする準備が整っています。

VIP顧客には、どのようにアプローチすればよいでしょうか？

* **限定オファーと割引**：VIP顧客のロイヤルティへの感謝を示すため、限定オファーや割引、新商品やキャンペーンへの先行アクセスを提供します。VIP限定セール、フラッシュセール、期間限定キャンペーンを実施し、リピート購入とエンゲージメントを促進します。
* **VIPロイヤルティプログラム**：購入額の多い顧客を対象に、段階的な特典、特別なメリット、VIP限定の優待を設けたVIPロイヤルティプログラムを導入します。送料無料、専用カスタマーサポート、誕生日プレゼント、VIPイベントなどの特典を提供し、顧客体験を向上させてロイヤルティを醸成します。
* **パーソナルショッピング体験**：専任のアカウントマネージャー、パーソナルショッパー、コンシェルジュサービスなど、VIP顧客向けにパーソナライズされたショッピング体験を提供します。個々の好みやニーズに応じて、最適な商品の提案、スタイリングのアドバイス、カスタマイズオプションを提供します。
* **VIPイベントと体験**：価値の高い顧客との交流や関係構築を図るため、VIP限定イベント、ワークショップ、ネットワーキングの機会を設けます。新商品の発表会、VIP向け先行公開、舞台裏ツアーなどの特別イベントにVIP顧客を招待し、関係をエンリッチメントしてブランドロイヤルティを醸成します。
* **フィードバックとアンケート**：VIP顧客からフィードバックを収集し、その好み、期待、不満点を把握します。アンケート、フォーカスグループ、個別インタビューを実施して、VIP体験の改善やニーズに合わせた提供内容の最適化に役立つ知見や提案を集めます。
* **ソーシャル上での評価と感謝**：ソーシャルメディア、企業ニュースレター、WebサイトでVIP顧客を紹介し、その貢献を称えます。貢献内容、体験談、成功事例を取り上げることで、顧客の価値を示し、ほかの顧客のロイヤルティ向上にもつなげます。