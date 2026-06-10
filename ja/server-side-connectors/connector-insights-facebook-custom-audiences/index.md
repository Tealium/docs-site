---
title: コネクターインサイト：Facebookカスタムオーディエンス
description: インサイトは、そのパフォーマンスを評価するためにベンダーからTealiumアカウントに追加のコネクターデータをもたらします。
url: https://docs.tealium.com/ja/server-side-connectors/connector-insights-facebook-custom-audiences/
---
Facebookカスタムオーディエンスインサイトは、Facebookオーディエンスコネクターとの統合であり、Facebookからあなたのアカウントにカスタムオーディエンスデータをもたらします。この記事では、この機能にアクセスしてデータを探索する方法を示します。

## コネクターインサイトの概要

Facebookオーディエンスコネクターのインサイトは、Facebookによって受信されたカスタムオーディエンスデータの要約を提供します。これらのインサイトは、パラメータとその値の要約で提示されます。

## カスタムオーディエンスパラメータ

パラメータの要約は、コネクターからFacebookに送信された1つのオーディエンスのカスタムオーディエンスデータを示します。パラメータの要約には、**カスタムオーディエンス名/ID**、Facebookによって収集された各カスタムオーディエンスパラメータ、および各パラメータの値が表示されます。

![](/images/server-side-connectors/2022-03-28-09-56-45.png)

## コネクターインサイトの使用

コネクターインサイトにアクセスするには、**Connect &gt; Audience Connectors**に移動し、Facebookオーディエンスコネクターを見つけて**インサイト**をクリックします。&lt;br&gt;

![](/images/server-side-connectors/connector-insights-btn.png)

## Facebookカスタムオーディエンスインサイトの理解

Facebookカスタムオーディエンスインサイトは、構成されたオーディエンスに関する情報を提供するために[Facebook Graph API for Audiences](https://developers.facebook.com/docs/marketing-api/reference/custom-audience/)を使用します。

|**パラメータ**| **説明**|
|----|----|
|作成時間| オーディエンスが作成された時間。|
|オーディエンスステータス| 最後にオーディエンスに対して行われた操作のステータスを表す`operational_status`フィールドを使用します。可能な状態についての詳細は、[Facebook Graph API](https://developers.facebook.com/docs/marketing-api/reference/custom-audience/)のドキュメントを参照してください。|
|オーディエンス数の下限| このオーディエンスに含まれる人々のおおよその数の下限。 |
|オーディエンス数の上限| このオーディエンスに含まれる人々のおおよその数の上限。 |

## 追加リソース

* [Facebook Graph API](https://developers.facebook.com/docs/marketing-api/reference/custom-audience/)
* [Facebookオーディエンスコネクター構成ガイド](/ja/server-side-connectors/facebook-audiences-connector/)
