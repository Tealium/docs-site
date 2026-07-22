---
title: CloudStreamについて
description: この記事ではCloudStreamについての情報を提供します。
url: https://docs.tealium.com/ja/server-side/cloudstream/about/
---
CloudStreamは、Tealiumにデータを保存またはロードすることなく、データクラウドから直接顧客データを活用するセグメントビルダーです。主にバッチマーケティングリストとウェアハウスの活用を目的として設計されており、データクラウドからセグメントを作成・管理し、サポートされているコネクタを使用してそれらを活用することができます。

これにより、以下のようなオーバーヘッドが削減されます：

* データの複製や同期にかかるコストがない。
* データの複製と同期から生じるエラーを排除。
* よりシンプルなデータガバナンス。
* データ管理の負担を軽減。

## 要件

* データソースへのアクセス（アカウントおよびテーブルの権限が必要）。
* アクティベーション先の認証情報（メール、SMS、広告プラットフォームなど）。
* データ移動とコンプライアンスポリシーの確認。
    * データ転送、処理、保護に関する規制ガイドラインの遵守を確認します。DatabricksやSnowflakeのようなプラットフォームを通じてデータを活用する際に、プライバシーとセキュリティを維持するためのポリシーを確認してください。

## 動作原理

CloudStreamはデータクラウドに直接接続し、Tealiumにデータを移動または保存することなく顧客データを活用します。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_workflow.png)

専用のサーバーサイドプロファイルで、データクラウド内のテーブルまたはビューに接続するデータソースを定義し、その列をクラウド属性にマッピングします。データの属性をさらに処理するためにエンリッチメントを追加することができます。また、平均値やその他の計算で追加のクラウド属性をエンリッチすることもできます。これらの属性を使用して、特定の基準を満たすユーザーやエンティティのグループであるセグメントを構築します。最後に、これらのセグメントをコネクタを通じて選択した宛先に送信して活用します。

CloudStreamは専用のCloudStreamプロファイルを使用し、ワークフローを整理し、他のTealium製品とは別に保持します。

### 専用プロファイル

CloudStreamは、他のプラットフォームプロファイルとは別の専用のサーバーサイドプロファイルを使用します。この分離により、大規模なデータセットや複雑なセグメントの属性、セグメント、ルール、コネクタを管理することができ、AudienceStreamやEventStreamのワークフローに影響を与えることなく行えます。


<blockquote>
専用のCloudStreamプロファイルを作成するには、Tealiumサポートに連絡してください。
</blockquote>


### データサプライチェーンダッシュボード

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_profile_dashboard.png)

CloudStreamデータサプライチェーンダッシュボードには、以下の情報が表示されます：

* 構成されたクラウドデータソースの数。
* 受信したデータレコードの数。
* 適用されたエンリッチメントの数。
* アクティブなセグメントの数。
* トリガーされた関数とコネクタアクションの数。
* 構成されたコネクタの数。

テーブルには、プロファイルで構成されたクラウドデータソース、セグメント、および宛先（コネクタおよび関数）がリストされています。

### データソース

データソースは、SnowflakeやDatabricksなどのデータクラウドへの定義済み接続です。CloudStreamはこれらのデータソースに接続してセグメントを取得し、Tealiumにデータを保存することなく活用します。これにより、既存のデータインフラストラクチャの力を活用して、クラウドから直接大規模なデータセットを扱うことができます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_datasource_summary.png)


<blockquote>
プロファイルで最大10個のデータソースに接続できます。
</blockquote>


CloudStreamデータソースは、データクラウドに保存されているデータを直接扱うように設計されています。データはデータクラウドに残り、コネクタを通じて活用するために一時的にインポートされるだけで、Tealiumには保存されません。

Tealiumデータソースは、データを処理するための2つの構成をサポートしています：基本と高度。

* 基本：データソース構成で指定したデフォルトスキーマを使用してデータがインポートされます。一つのテーブルまたはビューからのみデータを処理できます。
* 高度：高度なSQLエディタを使用して、複数のスキーマからの一つまたは複数のテーブルを結合することができます。


<blockquote>
CloudStreamはクラウドデータソースのみをサポートしています。
</blockquote>


クラウドデータソースについての詳細は、次の記事を参照してください：

* [about-cloud-data-sources](https://docs.tealium.com/about-cloud-data-sources/)  
データソースの機能についての一般情報、サポートされているデータタイプ、制限、SQLクエリ、クエリモード、処理情報、データマッピングなど。
* [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)   
データソース接続の作成、構成、マッピングに関する情報および構成のテスト方法についての指示。

### クラウド属性

CloudStreamでデータソースを作成するときに定義されるクラウド属性です。データクラウドのテーブルに接続すると、CloudStreamはテーブルの列を分析し、そのデータタイプを決定し、対応するクラウド属性を生成します。データソースの構成プロセス中にこれらの属性マッピングを確認および調整して、アクティベーションのニーズに合わせることができます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloud_attributes.png)

クラウド属性は構造と動作がイベント属性と同一ですが、[制限データ](https://docs.tealium.com/about-restricted-data/)としてマークすることはできず、CloudStreamには[プリロードされた属性](https://docs.tealium.com/preloaded-attributes/)が含まれていません。


<blockquote>
プロファイルで500以上の属性が必要な場合は、[サポートにお問い合わせください](https://docs.tealium.com/support/)。
</blockquote>


詳細については、[manage-cloudstream-attributes](https://docs.tealium.com/manage-cloudstream-attributes/)を参照してください。

### セグメント

セグメントは、データソースで定義されたクラウド属性に基づいて一連の条件を満たすユーザーやエンティティのグループです。CloudStreamのセグメントはシステムに永続化されず、データがデータクラウドからインポートされ、コネクタを通じて活用される間にリアルタイムで動的に評価されます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_details.png)

詳細については、[manage-cloudstream-segments](https://docs.tealium.com/manage-cloudstream-segments/)を参照してください。

#### 複数のデータソースを持つセグメント

CloudStreamでは、複数のデータソースを直接結合することはできません。しかし、高価値の顧客や高い潜在的な見込み客を特定するなど、共有目的を持つ複数のデータソースをセグメントに組み合わせたい場合があります。

たとえば、見込み客のテーブルと試乗をした人々のテーブルから、車を購入する高い潜在的な見込み客を見つけるための単一のセグメントを作成したい場合、まずこれらのデータソースを含むセグメントを作成します。次に、見込み客に対してフィルタを構成し、OR条件を使用し、試乗参加者に対して別のフィルタを構成します。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_combined_segment_details.png)
### アクティベーション

アクティベーションは、マーケティング、分析、広告プラットフォームへのセグメントの配信プロセスです。コネクタアクションまたは関数を通じてアクティベーションを構成できます。詳細については、[add-connector](https://docs.tealium.com/add-connector/) および [about-data-record-functions](https://docs.tealium.com/about-data-record-functions/) を参照してください。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_path.png)

セグメントを複数のコネクタアクションまたは関数に出力できます。ただし、構成された各アクティベーションは、選択されたデータソースからのデータのみを使用できます。追加のデータソースからアクティベーションを通じてデータをアクティブ化したい場合は、各データソースごとに別のアクションまたは関数を構成してください。


<blockquote>
CloudStream コネクタと関数を有効にするには、**管理メニュー** > **サーバーサイド構成** > **CloudStream コネクタ** に移動し、**CloudStream コネクタを有効にする** を `On` に構成し、**保存** をクリックします。
</blockquote>


## 比較

CloudStream、EventStream、AudienceStream の主な違いは以下の通りです：

| 機能                   | CloudStream                | EventStream / AudienceStream         |
|-----------------------|----------------------------------|--------------------------------------|
| データソース           | データクラウド（Snowflake、Databricks）      | データクラウド、ウェブ、モバイル、サーバー、API イベント      |
| データ保存          | Tealium にデータは保存されない        | Tealium にデータがロードおよび保存される（訪問プロファイルおよびDataAccess）    |
| セグメントの持続性   | 動的で持続されない           | 訪問プロファイルに持続される        |
| アクティベーション           | AudienceStream コネクタと関数  | AudienceStream および EventStream コネクタと関数                            |
| コネクタアクション     | 各データソースごとに分けられる    | 複数のデータソースごとにアクション。   |
| 主な使用例      | バッチ/ウェアハウスアクティベーション       | リアルタイム処理およびアクティベーション    |