---
title: クラウド属性
description: この記事では、クラウド属性の使用方法の概要と、属性を追加、複製、削除する手順について説明します。
url: https://docs.tealium.com/ja/server-side/data-cloud-activation/attributes/
---
![](https://docs.tealium.com/images/early-access/cloudstream/cloud_attributes.png)

クラウド属性は、Data Cloud Activation 内で使用される基礎的なデータ要素です。クラウド属性は、Data Cloud Activation でデータソースを作成するときに定義されます。データクラウド内のテーブルに接続すると、Data Cloud Activation はテーブルの列を分析してデータ型を判定し、対応するクラウド属性を生成します。

![](https://docs.tealium.com/images/early-access/cloudstream/datasource_cloud_attribute_mapping.png)

クラウドデータソースは、すべてのデータ型をサポートしています。データソースの構成プロセス中に属性マッピングを確認および調整し、各属性のデータ型が正しく、セグメンテーションやオーディエンスターゲティングなどのデータアクティベーションの要件に適合していることを確認してください。

一般に、データが正しくインポートされるように、次のデータ型マッピングを使用します。

| クラウドデータ | Tealium |
|------------------|------------------------------------|
| 数値 | 数値属性 |
| 文字列 | 文字列属性 |
| 論理値 | ブール属性 |
| 日付と時刻 | 日付属性 |
| 配列 | 文字列の配列、数値の配列、またはブール値の配列 |
| その他 | 文字列属性 |

データ型の詳細については、[クラウドデータソースについて > データ型](https://docs.tealium.com/about-cloud-data-sources/#data-types)を参照してください。

マッピングで既存のクラウド属性を選択し、Data Cloud Activation 内の異なるデータソースやセグメント間で再利用することもできます。


<blockquote>
現在のクラウド属性の合計数は、**属性**画面で確認できます。1 つのプロファイルで 500 を超える属性が必要な場合は、[サポートにお問い合わせください](https://docs.tealium.com/support/)。
</blockquote>


クラウド属性は、構造と動作の点でイベント属性と同一です。ただし、制限対象データとしてマークすることはできず、Data Cloud Activation には事前に読み込まれた属性が含まれていません。

詳細については、[about-attributes](https://docs.tealium.com/about-attributes/)を参照してください。