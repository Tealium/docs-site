---
title: エンリッチメントの管理
description: この記事では、エンリッチメントとその追加方法について説明します。
url: https://docs.tealium.com/ja/administration/early-access/attributes-improvements/enrichments/
---

<blockquote>
新しい属性インターフェイスは早期アクセス段階にあり、一部のお客様のみが利用できます。この機能の利用を希望する場合は、Tealiumサポート担当者にお問い合わせください。
</blockquote>


## 仕組み

エンリッチメントとは、カスタムロジックを使用して属性を静的な値から動的な値に変換することです。新しいデータ値の作成や、受信データの変更に使用されます。利用可能なエンリッチメントは、属性のデータ型によって異なります。たとえば、数値を増加または減少させる機能は、数値属性で使用できます。

## エンリッチメントの表示

エンリッチメントを表示するには、次の手順を実行します。

1. 左側のナビゲーションバーから、**Transform > Visitor / Visit Attributes**に移動して属性を表示します。![](https://docs.tealium.com/images/server-side/attributes/visit-visitor-attributes-table.png)
1. テーブル内の任意の属性をクリックして、その属性の詳細を表示します。![](https://docs.tealium.com/images/server-side/attributes/attribute-details-slideout.png)

## エンリッチメントの追加

エンリッチメントを追加するには、次の手順を実行します。

1. **Add Attribute**ダイアログで、**Add Enrichment**をクリックし、目的のエンリッチメントを選択します。
1. 構成は、エンリッチメントのデータ型によって異なります。各データ型のエンリッチメントについて詳しくは、[データ型](https://docs.tealium.com/data-types/)を参照してください。
1. エンリッチメントをトリガーするタイミングとして、**WHEN**を選択します。この構成により、エンリッチメントが実行されるタイミングが制御されます。
    * **New Visitor** – 訪問が初めてサイトを訪れたときに発生します。
    * **New Visit** – 訪問による新しい訪問時に発生します。
    * **Any Event** – 任意のイベントで発生します。
    * **Visit Ended** – 次の非アクティブ時間に基づいて、訪問が終了したときに発生します。
        * Webセッション：30分（[イベントを1件しか受信していない場合](https://support.tealiumiq.com/en/support/solutions/articles/36000363388-how-are-single-page-visits-processed-in-audiencestream-)は10分）
        * モバイルアプリセッション：2分
        * オムニチャネルセッション：1分

1. 既存の**Rule**条件を選択するか、[新しいルールを作成]()します。
1. **Finish**をクリックします。
1. 変更を適用するには、プロファイルを保存してパブリッシュします。

## サイズ制限

Join Attributesエンリッチメントなど、一部のエンリッチメントは属性のサイズを増加させる可能性があります。Event StreamingおよびCustomer Data Platform（CDP）のほとんどの属性には、保存容量の上限と、その上限を超えた場合の固有の動作があります。また、訪問または訪問プロファイル全体には、圧縮および暗号化された状態で400 KBの上限があります。

詳しくは、[属性について](https://docs.tealium.com/about-attributes/#size-limits)を参照してください。