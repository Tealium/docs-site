---
title: エンリッチメントの管理
description: この記事では、エンリッチメントについて説明し、それを追加する方法について説明します。
url: https://docs.tealium.com/ja/administration/early-access/attributes-improvements/enrichments/
---

<blockquote>
新しい属性インターフェースはEarly Accessであり、選ばれた顧客のみが利用可能です。この機能を試してみたい場合は、Tealiumサポート担当者に連絡してください。
</blockquote>


## 仕組み

エンリッチメントとは、属性を静的な値から動的な値に変換するためのカスタムロジックを使用することです。これは、新しいデータ値を作成するか、受信データを変更するために使用されます。利用可能なエンリッチメントは、属性のデータタイプに依存します。例えば、数値属性には数値を増減する機能があります。

## エンリッチメントの表示

エンリッチメントを表示するには：

1. 左のナビゲーションバーから **Transform > Visitor / Visit Attributes** に移動し、属性を表示します。![](https://docs.tealium.com/images/server-side/attributes/visit-visitor-attributes-table.png)
1. テーブルの任意の属性をクリックして、その属性の詳細を表示します。![](https://docs.tealium.com/images/server-side/attributes/attribute-details-slideout.png)

## エンリッチメントの追加

エンリッチメントを追加するには：

1. **Add Attribute** ダイアログで **Add Enrichment** をクリックし、希望するエンリッチメントを選択します。
1. 構成はエンリッチメントのデータタイプによって異なります。各データタイプのエンリッチメントの詳細については、[Data Types](https://docs.tealium.com/data-types/)を参照してください。
1. エンリッチメントをトリガーする **WHEN** を選択します。これはエンリッチメントのタイミングを制御します。
    * **New Visitor** – 訪問がサイトに初めて来たときに発生します。
    * **New Visit** – 訪問が新しい訪問をするときに発生します。
    * **Any Event** – 任意のイベントで発生します。
    * **Visit Ended** – 訪問が終了したときに発生します。以下の非活動時間に基づきます：
        * Webセッション：30分（イベントが1つだけ受信された場合は10分[https://support.tealiumiq.com/en/support/solutions/articles/36000363388-how-are-single-page-visits-processed-in-audiencestream-]）
        * モバイルアプリセッション：2分
        * オムニチャネルセッション：1分

1. 既存の **Rule** 条件を選択するか、[新しいルールを作成]()します。
1. **Finish** をクリックします。
1. プロファイルを保存して公開し、変更を適用します。

## サイズ制限

Join Attributesのような一部のエンリッチメントは、属性のサイズを増加させることがあります。EventStreamおよびAudienceStreamのほとんどの属性には、保存容量の制限があり、それらの制限を超えた場合の特定の動作があります。また、訪問または訪問プロファイル全体には、圧縮および暗号化された400 KBの制限があります。

詳細については、[About attributes](https://docs.tealium.com/about-attributes/#size-limits)を参照してください。