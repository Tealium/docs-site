---
title: VIPバッジ
description: このガイドでは、最も重要な顧客を識別するVIPバッジの作成方法について説明します。
url: https://docs.tealium.com/ja/guides/vip-badge-guide/
---
## 仕組み

![](https://docs.tealium.com/images/server-side/getting-started-audiencestream-badge-vip.png)

VIPは、サイトに何度も戻ってきて購入する価値の高い顧客です。VIPは、他の顧客よりも購入する可能性が高く、価格に敏感でないため、ターゲットにするのに適した顧客層です。

### 条件

VIP訪問を決定する指標は業界によって異なります。以下は、ビジネスにおけるVIP訪問の意味の例です：

* **旅行**：移動距離、費やした金額、訪れた都市や国の数でVIPを測定することができます。
* **金融**：機関が保有する個人の資産総額でVIPを測定することができます。
* **メディア**：プレミアムサービスやサブスクリプションに費やした金額、オンデマンド製品に費やした金額でVIPのステータスを測定することができます。
* **技術**：最新の製品やサービスに費やした金額でVIPのステータスを測定することができます。

さらに、重要なVIP指標を測定する方法とタイミングを決定できます：

* **累積閾値**：総注文価値、総移動距離、総ロイヤルティポイント。
* **時間ベースの閾値**：特定の時間枠での合計。
* **ソーシャルエンゲージメント閾値**：ブランドに関する訪問の投稿の「いいね！」の数など、ソーシャルメディアを通じたブランドとのインタラクション。
* **フィードバックおよびレビューエンゲージメント閾値**：肯定的なフィードバックやレビューを提供する訪問。

Tealium AudienceStreamの素晴らしい点は、異なる基準と閾値を持つ複数のVIPオーディエンスを作成し、各VIPオーディエンスに合わせた体験を提供できることです。

## 要件

#### 必要なイベント属性

| 属性名 | タイプ| 例| 
| --- | --- | --- |
| `order_id` |  UDO変数 |  `123456` | 
| `order_subtotal` |  UDO変数 |  `1500.00` | 
| `customer_email` |  UDO変数 |  `user@example.com` | 

#### 必要な訪問属性

ライフタイムバリューの例：

| 属性名 | タイプ| 
| --- | --- |
| 顧客メール |  文字列 | 
| ライフタイム注文合計 | 文字列 |

時間ベースの例：

| 属性名 | タイプ| 
| --- | --- |
| 顧客メール |  文字列 | 
| 過去90日間の注文小計 | タイムライン |
| 過去90日間の注文小計 | 数値 |

## ライフタイムバリューの例

次の例では、生涯で$10,000以上を費やした顧客にVIPバッジを作成し、そのバッジを持つ訪問でオーディエンスを作成します。

### ステップ1 - 属性を作成する

まず、「ライフタイム注文合計」という訪問数値属性を以下のエンリッチメントで作成します：

```
Increment or Decrement Number by "order_subtotal"
WHEN: Any event
Rule "tealium_event" equals (ignore case) "purchase"
Rule "order_id" is assigned
```

![](https://docs.tealium.com/images/guides/lifetime-order-total-attribute.png)

次に、「顧客メール」という訪問文字列属性を作成して、訪問のメールアドレスを収集します：

```
Set String to customer_email
WHEN: Any event
Rule "customer_email" is assigned.
Rule "customer_email" contains "@"
```

![](https://docs.tealium.com/images/guides/customer-email-attribute-assigned.png)

属性の追加についての詳細は、[属性を追加する](https://docs.tealium.com/manage-as-attributes/#add-an-attribute)を参照してください。

### ステップ2 - VIPバッジを作成する

これで、訪問が費やした合計額とメールアドレスの有無を測定できるようになったので、これらの属性に基づいてVIPバッジを作成できます。

「顧客VIP」という訪問バッジ属性を以下のエンリッチメントで作成します：

```
Assign this badge to visitor
WHEN: Any event
Rule "Lifetime Order Total" greater than or equal to "10000"
Rule "Customer email" is assigned
```

![](https://docs.tealium.com/images/guides/customer-vip-badge-lifetime-total.png)

### ステップ3 - オーディエンスを作成する

これでVIPバッジに基づいてオーディエンスを作成できます：

1. **オーディエンス**に移動します。
1. **+ 新しいオーディエンス**をクリックします。
1. **タイトル**欄に`VIP`と入力します。
1. **Where**ドロップダウンリストから**顧客VIP**を選択します。
1. **is assigned**を選択します。
1. **完了**をクリックします。

![](https://docs.tealium.com/images/guides/vip-badge-audience.png)

詳細については、を参照してください。

## 時間ベースの例

次の例では、過去90日間に$10,000の購入を行った顧客にVIPバッジを作成し、そのバッジを持つ訪問でオーディエンスを作成します。要件を満たさなくなった訪問は、90日後にオーディエンスから削除されます。

### ステップ1 - 属性を作成する

まず、「過去90日間の注文小計」という訪問タイムライン属性を以下の2つのエンリッチメントで作成します：

```
Set each event in timeline Order subtotals in past 90 days to expire after 90 days
WHEN: Any event

Record an event for timeline Order subtotals in past 90 days
Capture data for "order_subtotal"
WHEN: New visit
```

![](https://docs.tealium.com/images/guides/order-subtotals-in-past-90-days.png)

次に、「顧客メール」という訪問文字列属性を作成して、訪問のメールアドレスを収集します：

```
Set String to customer_email
WHEN: Any event
Rule "customer_email" is assigned.
Rule "customer_email" contains "@"
```

![](https://docs.tealium.com/images/guides/customer-email-attribute-assigned.png)

次に、「過去90日間の注文合計」という訪問数値属性を以下のエンリッチメントで作成します：

```
Set Number Rolling order total for past 90 days to the rolling sum of order_subtotal captures in timeline Order subtotals in past 90 days
WHEN Any event
```

![](https://docs.tealium.com/images/guides/rolling-order-total-for-past-90-days.png)

### ステップ2 - VIPバッジを作成する

これで、訪問が費やした合計額とメールアドレスの有無を測定できるようになったので、これらの属性に基づいてVIPバッジを作成できます。

「顧客VIP」という訪問バッジ属性を以下のエンリッチメントで作成します：

```
Assign this badge to visitor
WHEN: Any event
Rule "Rolling order total for past 90 days" greater than or equal to "10000"

Remove this badge to visitor
WHEN: Any event
Rule "Rolling order total for past 90 days" less than "10000"
```

![](https://docs.tealium.com/images/guides/customer-vip-rolling-total.png)

### ステップ3 - オーディエンスを作成する

これでVIPバッジに基づいてオーディエンスを作成できます：

1. **オーディエンス**に移動します。
1. **+ 新しいオーディエンス**をクリックします。
1. **タイトル**欄に`VIP`と入力します。
1. **Where**ドロップダウンリストから**顧客VIP**を選択します。
1. **is assigned**を選択します。
1. **オプション**の下で、90日間の保持時間を選択します。
1. **完了**をクリックします。

![](https://docs.tealium.com/images/guides/vip-badge-audience.png)

詳細については、を参照してください。
## 聴衆を活性化する

この段階で、数百のベンダー統合のいずれかを通じて聴衆を活性化する準備が整います。

VIP顧客をどのようにターゲットにしますか？

* **独占オファーと割引**: VIP顧客に独占オファー、割引、または新商品やプロモーションへの早期アクセスを提供し、彼らの忠誠心に感謝の意を示します。VIP専用のセールイベント、フラッシュディール、または期間限定プロモーションを作成して、リピート購入を促し、エンゲージメントを高めます。
* **VIPロイヤルティプログラム**: 上位の顧客向けに階層化された報酬、特別な利点、VIP専用の特典を提供するVIPロイヤルティプログラムを実施します。無料配送、専用のカスタマーサービスサポート、誕生日の贈り物、またはVIPイベントなどの特典を提供し、顧客体験を向上させ、忠誠心を育みます。
* **パーソナルショッピング体験**: 専用のアカウントマネージャー、パーソナルショッパー、またはコンシェルジュサービスなど、VIP顧客向けのパーソナライズされたショッピング体験を提供します。彼らの個々の好みやニーズに合わせて、テーラーメイドの商品推薦、スタイルアドバイス、またはカスタマイズオプションを提供します。
* **VIPイベントと体験**: 高価値顧客とのエンゲージメントとつながりを深めるために、独占的なVIPイベント、ワークショップ、またはネットワーキングの機会を主催します。VIP顧客を商品発売、VIPプレビュー、または舞台裏ツアーなどの特別イベントに招待して、関係をエンリッチメントし、ブランドの忠誠心を育みます。
* **フィードバックと調査**: VIP顧客からのフィードバックを求めて、彼らの好み、期待、および問題点を理解します。調査、フォーカスグループ、または一対一のインタビューを実施して、VIP体験を改善し、彼らのニーズに合わせた提供内容を調整するための洞察と提案を収集します。
* **ソーシャルでの認識と感謝**: ソーシャルメディアプラットフォーム、会社のニュースレター、またはウェブサイトでVIP顧客を認識し、祝います。彼らの貢献、証言、または成功事例を強調して、他の顧客の間で忠誠心を鼓舞します。