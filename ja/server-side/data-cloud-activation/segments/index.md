---
title: Data Cloud Activation セグメントの管理
description: この記事では、Data Cloud Activation セグメントを管理する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-cloud-activation/segments/
---
## 仕組み

Data Cloud Activation セグメントは、Snowflake や Databricks などの接続済みデータクラウドから取得するレコードの集合を、そのデータソースの属性に適用する構成可能な条件に基づいて定義します。

セグメントを有効化すると、データクラウドにクエリを実行し、定義された条件に一致するレコードのみを取得します。セグメントデータが Tealium システムに永続化または保存されることはありません。データを取得して構成済みのコネクタに送信した後、Tealium はそのデータを破棄します。

## セグメントの表示

**CloudStream > Segments** に移動して、**Segments Overview** ページを表示します。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segments_overview.png)

**Segments Overview** テーブルには、各セグメントについて次の情報が表示されます。

* 名前
* 処理済み合計：セグメント条件に一致する受信データレコードの合計数です。少なくとも 1 つのアクティベーションが構成され、有効になっている場合に計上されます。
* 変更日
* ラベル
* アクティベーション
* ステータス：セグメントをアクティブにするには、アクティブなデータソースとアクティベーションを含む、正常に動作するチェーンが少なくとも 1 つ必要です。

その他の操作ボタンを使用すると、各セグメントへのラベルの追加や、セグメントの削除ができます。

各アクティベーションの横にあるチェックボックスを選択し、一括操作を実行して、セグメントのラベルを編集したり、セグメントを削除したりできます。

## セグメントの追加

次のいずれかの方法でセグメントを作成します。

* [セグメントビルダー](#segment-builder)の手順に従います。
* [セグメントを手動で作成します](#manual-builder)。

`Segment creation requires Cloud Stream Connectors to be enabled in Settings` というエラーが表示された場合は、次の手順でプロファイルのコネクタを有効にします。

1. **Admin menu** > **Server-Side Settings** > **CloudStream Connectors** に移動します。
1. **Activate CloudStream Connectors** をオンに切り替えます。
1. **Save** をクリックします。

### セグメントビルダー

**Segment Builder** をクリックします。**Data Source Configuration** ステップが表示されます。

#### データソースの構成

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_data_source_selection.png)

セグメントで使用するクラウドデータソースを選択します。

データソースが構成されていない場合は、**+ Add Cloud Data Source** をクリックします。クラウドデータソースの構成について詳しくは、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。

データソースを複製するには、データソースを選択して **Duplicate** をクリックします。次に、データソースの新しいコピーの名前を入力します。

各データソースは、一度に 1 つのビューまたはテーブルに接続できます。

* 1 つのデータクラウドにある複数のテーブルまたはビューに接続する必要がある場合は、テーブルまたはビューごとに個別のデータソースを構成します。
* 複数のテーブルのデータを、Data Cloud Activation がセグメントで読み取れるデータレコードに統合する場合は、データクラウド上でテーブルまたはビューを 1 つのテーブルまたはビューに結合し、その結合済みテーブルをセグメントのデータソースとして使用する必要があります。

データソースの構成が完了したら、**Next** をクリックします。

#### セグメントの構成

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_configuration.png)

次の手順でセグメントを構成します。

1. セグメントの **Name** を入力します。
1. 条件を追加するには、属性、演算子、値を選択します。  
期間を指定する演算子の場合は、値と期間を選択します。
1. 別の条件を追加するには、**+ Add Condition** をクリックします。
1. ラベルを追加したり、セグメントに関するメモを入力したりする場合は、**More Options** をクリックして変更を加えます。

#### セグメントのアクティベーション

コネクタまたは関数を使用してセグメントをアクティベートできます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_activation.png)

* コネクタを使用してセグメントをアクティベートする方法については、[add-connector](https://docs.tealium.com/add-connector/)を参照してください。
* 関数を使用してセグメントをアクティベートする方法については、[create-function](https://docs.tealium.com/create-function/)を参照してください。

**Segment Activations** テーブルには、構成したアクションが表示されます。

**Next** をクリックします。

#### 概要

**Summary** ページには、データソースから作成したセグメントを経てアクティベーションに至るデータフローの図が表示されます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_summary.png)

展開矢印をクリックすると、各アクティベーションの個別のアクションと関数が表示されます。

**Save** をクリックし、プロファイルを保存してパブリッシュします。

### 手動ビルダー

セグメントを手動で作成するには、次の手順を実行します。

1. **+ New Segment** をクリックして、セグメントを手動で作成します。
1. セグメントの **Name** を入力します。
1. 条件を追加するには、属性、演算子、値を選択します。  
期間を指定する演算子の場合は、値と期間を選択します。
1. 別の条件を追加するには、**+ Add Condition** をクリックします。
1. ラベルを追加したり、セグメントに関するメモを入力したりする場合は、**More Options** をクリックして変更を加えます。
1. **Done** をクリックします。

データソースの追加と構成、およびアクティベーションの追加とアクションまたは関数の構成は、手動で行う必要があります。

## セグメントの管理

管理するセグメントをクリックします。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_details.png)

**Segment Details** ページには、次の情報が表示されます。

* **Created**：セグメントを作成したユーザーと作成日時。
* **Modified**：セグメントを最後に変更したユーザーと変更日時。
* **Labels**：セグメントに構成されているラベル。

次のいずれかのタブをクリックします。

### 概要

**Overview** ウィンドウには、データソース、セグメント、アクティベーションを示すデータフロー図が表示されます。データソースをクリックすると、そのデータソースからセグメントを経て、接続されているアクティベーションに至る経路を確認できます。

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_path.png)

#### データソースとアクティベーションの管理

セグメントのデータソースを追加または編集できるほか、セグメントのアクティベーションを追加または編集できます。

1. 新しいデータソースを追加して構成すると、**Unused Data Source** として表示されます。
1. **Configuration** をクリックし、新しいデータソースの属性を照会するための条件をセグメントに追加します。
1. **Add Activation** をクリックして、コネクタのアクティベーションを追加します。
1. アクションまたは関数を選択して構成します。  
**Data Source** リストから、セグメントで使用するデータソースを必ず選択してください。
1. データフロー図が更新され、新しいデータソースとアクティベーションが表示されます。

アクティベーション内の切り替えスイッチを使用して、そのアクティベーションを有効または無効にします。セグメント名の横にある切り替えスイッチを使用すると、そのセグメントのすべてのアクティベーションを有効または無効にできます。

### 構成

**Configuration** ウィンドウでは、セグメントの構成を編集できます。セグメントの条件を更新し、**Done** をクリックします。

### インサイト

**Insights** ウィンドウには、選択した期間におけるコネクタのアクティベーションの概要とグラフが表示されます。

* **Matched**：セグメントの稼働状態にかかわらず、いずれかのデータソースからインポートされたレコードのうち、セグメント条件を満たすレコードの数。
* **Processed**：いずれかのデータソースからインポートされたレコードのうち、アクティブなセグメント条件を満たし、有効なアクティベーションをトリガーしたレコードの数。