---
title: 分析の管理
description: この記事では、分析の作成、印刷、公開について説明します。
url: https://docs.tealium.com/ja/server-side/insights/manage-analyses/
---
著者の役割を持つユーザーは、分析を作成して保存し、他の人と共有したり、カスタムダッシュボードとして公開することができます。

## 分析の作成

分析を作成または編集するとき、**AUTOSAVE**はデフォルトでオンになっています。これをオフにして再度分析を開くと、**AUTOSAVE**は再度オンになります。

<blockquote>
**AUTOSAVE**をオフにしてから分析を変更し、ダッシュボードを公開すると、分析の変更は保存されず、公開されたダッシュボードには含まれません。**AUTOSAVE**をオフにした場合は、変更を保存する必要がある場合は再度オンにすることを確認してください。
</blockquote>


以下の手順で分析を作成します：

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. **New analysis**をクリックします。  
利用可能なデータセットが表示されます。
1. データセットを選択し、**USE IN ANALYSIS**をクリックします。
1. シートの**AutoGraph**にフィールドを追加するには、**Data**リストのフィールドをクリックします。
1. **Visual Types**の下で視覚的なタイプを選択します。
1. 別のビジュアルを追加するには、**Visuals**セクションの**+ ADD**をクリックし、**Fields list**からフィールドを追加し、**Visual Types**の下で視覚的なタイプを選択します。

## 分析の公開

著者の役割を持つユーザーは、分析を公開または共有することができます。分析を公開すると、その分析のダッシュボードが作成され、リーダーの役割を持つユーザーが閲覧できます。

以下の手順で分析を公開します：

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択します。
1. **File**をクリックし、**Publish**をクリックします。

## 分析の共有

他のInsightsの著者や管理者と分析を共有することができます。

以下の手順で分析を共有します：

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択します。
1. **File**をクリックし、**Share**をクリックします。
1. ユーザー名、グループ、またはメールアドレスを入力します。
1. ユーザー、グループ、またはメールアドレスの追加が完了したら、**Share**をクリックします。

## 複数のデータセットの使用

異なるタイプのデータのビジュアルを表示するために、分析に複数のデータセットを追加することができます。

以下の手順で分析にデータセットを追加します：

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択します。
1. **Data**セクションのデータセットのドロップダウンリストを展開し、次の図に示すように**Add a new dataset**をクリックします：  
![](https://docs.tealium.com/images/server-side/data-insights/data-insights-add-dataset.png)
1. 追加するデータセットを選択し、**Select**をクリックします。
1. **Close**をクリックするか、**Add a dataset**をクリックして分析に別のデータセットを追加します。

新しいデータセットのビジュアルを追加することができます。

## フィルターの追加

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択します。
1. フィルターアイコンをクリックします。  
![](https://docs.tealium.com/images/server-side/data-insights/data-insights-icon-bar.png) 
1. **Filter**セクションで**+ ADD**をクリックします。
1. フィルタリングするフィールドを選択し、追加したフィールドをクリックしてフィルターの詳細を表示します。
1. フィルターの詳細で、**Filter condition**を選択し、**Enter a value**を入力します。
1. フィルターが適用されるビジュアルを変更するには、**Applied To**をクリックし、次のいずれかを選択します：  
    * **Only this visual** &ndash; フィルターは選択したビジュアルにのみ適用されます。
    * **Some visuals** &ndash; フィルターは有効な列マッピングを持つビジュアルに適用されます。
    * **All visuals of this dataset** &ndash; フィルターはこのデータセットに基づくすべてのアイテムに適用されます。
    * **All applicable visuals** &ndash; フィルターは有効な列マッピングを持つ任意のビジュアルに適用されます。
1. フィルターをシートに追加し、ダッシュボード上で可視化するには、フィルターメニューをクリックし、**Add to sheet**を選択します。
1. ビジュアルにフィルターを追加するには、**APPLY**をクリックします。
1. 公開されたダッシュボードを更新するには、**PUBLISH**をクリックします。

フィルターメニューからフィルターを**Edit**、**Delete**、または**Disable**することができます。

## ビジュアルのタイトルの変更

以下の手順でビジュアルのタイトルを変更します：

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択します。
1. 変更したいビジュアルのタイトルをダブルクリックします。
1. **Edit title**ウィンドウで、テキストボックスに新しいタイトルを入力し、**Save**をクリックします。
1. 公開されたダッシュボードを更新するには、**PUBLISH**をクリックします。

## ビジュアルのタイプの変更

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択し、変更するビジュアルを選択します。
1. **Visuals**セクションの**CHANGE VISUAL TYPE**の下で、新しいビジュアルタイプを選択します。  
ビジュアルタイプにホバーすると、そのビジュアルタイプに必要なフィールドが表示されます。
1. 必要に応じて、ビジュアルの選択フィールドを更新します。
1. ビジュアルのタイトルを更新するには、タイトルをダブルクリックし、**Edit title**ウィンドウで新しいタイトルを入力し、**Save**をクリックします。
1. 公開されたダッシュボードを更新するには、**PUBLISH**をクリックします。

## 分析にビジュアルを追加する

以下の手順で分析にビジュアルを追加します：

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択します。
1. **Visuals**の下で**Add**をクリックします。
1. [Create an analysis]()で説明されているように、フィールドとビジュアルを追加します。
1. 公開されたダッシュボードを更新するには、**PUBLISH**をクリックします。

## ビジュアルのデータ集約を変更する

以下の手順でデータ集約を変更します：

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択します。
1. **Visuals**の下で、変更したいフィールドのメニューをクリックし、**Aggregate**の値を選択します。
1. 公開されたダッシュボードを更新するには、**PUBLISH**をクリックします。

## 分析の印刷

著者の役割を持つユーザーは、以下のように分析を印刷することができます：

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択し、**File**をクリックし、**Print**をクリックします。  

## 分析のエクスポート

著者の役割を持つユーザーは、以下のように分析をエクスポートすることができます：

1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択し、**File**をクリックし、**Export as PDF**をクリックします。  
PDFが準備できたとき、次のメッセージが表示されます：
![](https://docs.tealium.com/images/server-side/data-insights/data-insights-pdf-ready-msg.png) 
1. エクスポートしたPDFをダウンロードするには、**DOWNLOAD**をクリックします。

## 分析のコピー
1. **Analyze > Analyze > Insights > Dashboards**に移動し、**Analyses**をクリックします。
1. 分析を選択し、**File**をクリックし、**Save As Analysis**をクリックします。 
1. 新しい分析のコピーの名前を入力し、**SAVE**をクリックします。