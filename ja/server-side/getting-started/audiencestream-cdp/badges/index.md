---
title: 属性バッジ
description: このドキュメントでは、訪問の属性バッジについて説明します。
url: https://docs.tealium.com/ja/server-side/getting-started/audiencestream-cdp/badges/
---
バッジは、興味深い行動パターンを表す訪問の属性です。バッジは、エンリッチメントのロジックに基づいて訪問に割り当てられたり、削除されたりします。このロジックは、バッジを割り当てるタイミングを決定し、通常は一つ以上の条件を使用したり、達成すべき閾値を構成したりします。

## バッジの例

以下にバッジの例をいくつか示します：

|大口顧客|カート放棄者|マルチデバイスユーザー|テストグループB|
|------------|--------------|-----------------|------------|
|![](/images/server-side/getting-started/audiencestream-cdp/attributes-badges/big-spenders.png) | ![](/images/server-side/getting-started/audiencestream-cdp/attributes-badges/cart-abandoner.png) | ![](/images/server-side/getting-started/audiencestream-cdp/attributes-badges/multi-device-user.png) |  ![](/images/server-side/getting-started/audiencestream-cdp/attributes-badges/test-group-b.png) | 
| 平均注文価格が100以上。 | 訪問終了時にカート内に未購入の商品があった。 | 使用したデバイスの総数が1以上。 | ランダムに割り当てられたテストグループの一部。 |

## バッジの作成

![](/images/server-side/getting-started-audiencestream-badge-vip.png)

前の属性、Lifetime Order Valueを基にして、500ドル以上を費やした訪問を識別する**VIP**バッジを作成します。

バッジを作成するには、以下の手順を実行します：

1. **AudienceStream &amp;gt; Attributes**に移動し、**Add Attribute**をクリックします。
1. **Visitor**の範囲を選択し、**Continue**をクリックします。
1. データタイプ**Badge**を選択し、**Continue**をクリックします。
1. 属性の名前を入力します：`VIP`。
1. **Add Enrichment**をクリックし、**Assign Badge**を選択します。
1. **WHEN**を**Any Event**に構成したままにし、**Create a New Rule**をクリックします。
1. ライフタイムオーダーの金額が500に達したときに識別するルールを作成します。例えば：  
`Lifetime Order Value greater than 500`
1. **Save**をクリックし、次に**Finish**をクリックします。

これで、エンリッチメントルールで定義された行動パターンに一致する顧客を追跡する訪問バッジができました。