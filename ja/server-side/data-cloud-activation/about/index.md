---
title: Data Cloud Activation について
description: この記事では、Data Cloud Activation について説明します。
url: https://docs.tealium.com/ja/server-side/data-cloud-activation/about/
---
Data Cloud Activation は、Tealium にデータを保存または読み込むことなく、データクラウドから直接セグメントを作成および管理できる機能です。Data Cloud Activation は、主にバッチマーケティングリストとデータウェアハウスのアクティベーションを目的として設計されており、データクラウドからセグメントを作成、管理し、サポートされているコネクタを使用してアクティベートできます。

これにより、次のような方法でオーバーヘッドが軽減されます。

* データの複製や同期にコストがかかりません。
* データの複製と同期に起因するエラーを排除します。
* データガバナンスを簡素化します。
* データ管理の負担を軽減します。

## 要件

* データソースへのアクセス権（アカウントおよびテーブルの権限が必要）。
* アクティベーション先（メール、SMS、広告プラットフォームなど）の認証情報。
* データ移動とコンプライアンスポリシーの確認。
    * Data Cloud Activation におけるデータの転送、処理、保護に関する規制ガイドラインへの準拠を確保してください。Databricks や Snowflake などのプラットフォームを通じてデータをアクティベートする際のプライバシーとセキュリティを維持するために、ポリシーを確認してください。

## 仕組み

Data Cloud Activation はデータクラウドに直接接続するため、顧客データを Tealium に移動または保存することなくアクティベートできます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_workflow.png)

専用のサーバーサイドプロファイルで、データクラウド内のテーブルまたはビューに接続するデータソースを定義し、その列をクラウド属性にマッピングします。エンリッチメントを追加して属性内のデータをさらに処理したり、平均値やその他の計算結果で追加のクラウド属性を拡張したりできます。これらの属性を使用して、特定の条件を満たすユーザーまたはエンティティのグループであるセグメントを作成します。最後に、コネクタを介して選択した宛先にセグメントを送信してアクティベートします。

Data Cloud Activation では専用の Data Cloud Activation プロファイルを使用するため、ワークフローを整理し、他の Tealium 製品から分離できます。

### 専用プロファイル

Data Cloud Activation では、他のプラットフォームプロファイルとは別に、独自の専用サーバーサイドプロファイルを使用します。この分離により、Customer Data Platform（CDP）またはイベントストリーミングのワークフローに影響を与えることなく、大規模なデータセットや複雑なセグメントに使用する属性、セグメント、ルール、コネクタを管理できます。


<blockquote>
Data Cloud Activation 専用プロファイルを作成するには、Tealium サポートにお問い合わせください。
</blockquote>


### データサプライチェーンダッシュボード

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_profile_dashboard.png)

Data Cloud Activation のデータサプライチェーンダッシュボードには、次の情報が表示されます。

* 構成されているクラウドデータソースの数。
* 受信したデータレコードの数。
* 適用されたエンリッチメントの数。
* アクティブなセグメントの数。
* トリガーされた関数とコネクタアクションの数。
* 構成されているコネクタの数。

各テーブルには、プロファイルで構成されているクラウドデータソース、セグメント、および宛先（コネクタと関数）が一覧表示されます。

### データソース

データソースは、Snowflake や Databricks などのデータクラウドへの接続を定義したものです。Data Cloud Activation はこれらのデータソースに接続し、Tealium にデータを保存することなくセグメントを取得してアクティベートします。これにより、既存のデータインフラストラクチャの能力を活用しながら、クラウドから直接、大規模なデータセットを操作できます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_datasource_summary.png)


<blockquote>
1 つのプロファイルで最大 10 個のデータソースに接続できます。
</blockquote>


Data Cloud Activation のデータソースは、データクラウドに保存されているデータを直接処理するように設計されています。データはデータクラウド内に保持され、Tealium に保存されることなく、コネクタによるアクティベーションのために一時的にのみインポートされます。

Tealium のデータソースでは、データを処理するために基本と詳細の 2 つの構成がサポートされています。

* 基本：データソース構成で指定したデフォルトのスキーマを使用してデータがインポートされます。処理できるのは、1 つのテーブルまたはビューのデータのみです。
* 詳細：詳細 SQL エディターを使用して、結合する 1 つ以上のテーブルを選択できます。複数のスキーマに属するテーブルを使用できます。


<blockquote>
Data Cloud Activation では、クラウドデータソースのみがサポートされています。
</blockquote>


クラウドデータソースの詳細については、次の記事を参照してください。

* [about-cloud-data-sources](https://docs.tealium.com/about-cloud-data-sources/)  
サポートされるデータ型、制限、SQL クエリ、クエリモード、処理情報、データマッピングなど、データソース機能に関する一般的な情報。
* [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)   
データソース接続の作成、構成、マッピングに関する情報、および構成をテストする方法。

### クラウド属性

クラウド属性は、Data Cloud Activation でデータソースを作成するときに定義されます。データクラウド内のテーブルに接続すると、Data Cloud Activation はテーブルの列を分析し、そのデータ型を判別して、対応するクラウド属性を生成します。データソースの構成プロセス中にこれらの属性マッピングを確認および調整し、アクティベーションのニーズに合致していることを確認できます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloud_attributes.png)

クラウド属性は、構造と動作においてイベント属性と同じですが、[制限付きデータ](https://docs.tealium.com/about-restricted-data/)としてマークできない点、および Data Cloud Activation には[事前読み込み済み属性](https://docs.tealium.com/preloaded-attributes/)が含まれていない点が異なります。


<blockquote>
プロファイルに 500 個を超える属性が必要な場合は、[サポートにお問い合わせください](https://docs.tealium.com/support/)。
</blockquote>


詳細については、[manage-data-cloud-activation-attributes](https://docs.tealium.com/manage-data-cloud-activation-attributes/)を参照してください。

### セグメント

セグメントとは、データソースで定義されているクラウド属性に基づく一連の条件を満たすユーザーまたはエンティティのグループです。Data Cloud Activation のセグメントはシステム内に永続化されず、データがデータクラウドからインポートされ、コネクタを介してアクティベートされる際にのみ、リアルタイムで動的に評価されます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_details.png)

詳細については、[manage-data-cloud-activation-segments](https://docs.tealium.com/manage-data-cloud-activation-segments/)を参照してください。

#### 複数のデータソースを使用するセグメント

Data Cloud Activation 内で複数のデータソースを直接結合することはできません。ただし、高価値顧客や有望な見込み客の特定など、共通の目的を持つ複数のデータソースを 1 つのセグメントにまとめたい場合があります。

たとえば、見込み客テーブルと、試乗した人のテーブルから、自動車を購入する可能性が高い見込み客を見つける単一のセグメントを作成するとします。まず、これらの各データソースを含むセグメントを作成します。次に、見込み客のフィルターを構成し、OR 条件を使用して、試乗参加者用の別のフィルターを構成します。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_combined_segment_details.png)
### アクティベーション

アクティベーションとは、セグメントをマーケティング、分析、広告プラットフォームに配信するプロセスです。アクティベーションは、コネクタアクションまたは関数を使用して構成できます。詳細については、[add-connector](https://docs.tealium.com/add-connector/)および[about-data-record-functions](https://docs.tealium.com/about-data-record-functions/)を参照してください。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_path.png)

1 つのセグメントを複数のコネクタアクションまたは関数に出力できます。ただし、構成した各アクティベーションで使用できるのは、選択したデータソースのデータのみです。1 つのアクティベーションを通じて追加のデータソースからデータをアクティベートする場合は、データソースごとに個別のアクションまたは関数を構成してください。


<blockquote>
Data Cloud Activation のコネクタと関数を有効にするには、**Admin menu** > **Server-Side Settings** > **CloudStream Connectors**に移動し、**Activate CloudStream Connectors**を`On`に構成して、**Save**をクリックします。
</blockquote>


## 比較

Data Cloud Activation、Event Streaming、CDP の主な違いは次のとおりです。

| 機能 | Data Cloud Activation | Event Streaming / CDP |
|-----------------------|----------------------------------|--------------------------------------|
| データソース | データクラウド（Snowflake、Databricks） | データクラウド、Web、モバイル、サーバー、API イベント |
| データ保存 | Tealium にデータを保存しない | Tealium にデータを読み込んで保存（訪問プロファイルおよび DataAccess） |
| セグメントの永続性 | 動的、永続化されない | 訪問プロファイルに永続化 |
| アクティベーション | CDP のコネクタおよび関数 | CDP および Event Streaming のコネクタと関数 |
| コネクタアクション | データソースごとに個別に構成 | 1 つのアクションで複数のデータソースを使用可能 |
| 主なユースケース | バッチ／ウェアハウスのアクティベーション | リアルタイムの処理とアクティベーション |