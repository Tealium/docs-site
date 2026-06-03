---
title: オーディエンスサイジングの例
description: この記事では、オーディエンスサイジング機能の例を提供します。
url: https://docs.tealium.com/ja/server-side/audiences/audience-sizing/examples/
---
## 例：過去の購入者をリターゲティングする

この例では、以下の条件を満たす顧客をリターゲティングしたいと考えています：

* 過去1週間にあなたのサイトを訪れた。
* 過去30日間に購入がない。
* 生涯で500ドル以上の購入がある。
* お気に入りの商品カテゴリーが `Jeans` である。

この例では、以下を特定するために必要な日付選択とルールの構成がすでに行われていると仮定します：

* 顧客のお気に入りの商品カテゴリー。
* 彼らの生涯の注文価値。
* 最後の購入からの日数。

### 手順

以下の手順を使用します：

1. サイドバーで **AudienceStream &gt; Discover** に移動します。
1. **Audience Sizing** タブをクリックします。
1. 過去7日間を表す日付範囲を選択します。
1. 次のルールを選択または作成します：


[
  [
    {
      &#34;input&#34;: &#34;Favorite Product Category (favorite)&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;Jeans&#34;
    },
    {
      &#34;input&#34;: &#34;Lifetime Order Value&#34;,
      &#34;operator&#34;: &#34;less than or equal to&#34;,
      &#34;filter&#34;: &#34;500&#34;
    },
    {
      &#34;input&#34;: &#34;Days since last purchase&#34;,
      &#34;operator&#34;: &#34;greater than&#34;,
      &#34;filter&#34;: &#34;30&#34;
    }
  ]
]


## 例：ホリデーシーズンのクーポン利用者をリターゲティングする

この例では、以下の条件を満たす顧客をリターゲティングしたいと考えています：

* 12月のホリデーシーズン中にあなたのサイトを訪れた。
* 現在VIP顧客として分類されている。
* メールでのエンゲージメントが最も多い。
* クーポンを頻繁に使用する。

この例では、以下を特定するために必要な日付選択とルールの構成がすでに行われていると仮定します：

* VIP顧客。
* 最もエンゲージメントのあるマーケティングチャネル。
* 彼らのクーポン使用頻度。

1. サイドバーで **AudienceStream &gt; Discover** に移動します。
1. **Audience Sizing** タブをクリックします。
1. 12月のホリデーシーズンを表す日付範囲を選択します（例：12月1日 - 12月31日）。
1. 次のルールを選択または作成します：


[
  [
    {
      &#34;input&#34;: &#34;VIP Customer&#34;,
      &#34;operator&#34;: &#34;is assigned&#34;,
      &#34;filter&#34;: &#34;&#34;
    },
    {
      &#34;input&#34;: &#34;Marketing Channel Engagement (favorite)&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;email&#34;
    },
    {
      &#34;input&#34;: &#34;Coupon Usage Ratio&#34;,
      &#34;operator&#34;: &#34;greater than or equal to&#34;,
      &#34;filter&#34;: &#34;0.50&#34;
    }
  ]
]
