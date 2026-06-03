---
title: AudienceStreamダッシュボード
description: この記事では、AudienceStreamダッシュボードの機能について説明します。
url: https://docs.tealium.com/ja/server-side/audiences/audiencestream-dashboard/
---
## トレンドグラフ

**トレンドグラフ**セクションでは、時間範囲にわたるデータを表示します。以下のオブジェクトのトレンドを表示することができます：

* オーディエンス
* コネクターアクション
* バッジ属性
* 数値属性
* ブール属性

同じグラフで1つ以上の値のトレンドを表示します。2つの値をグラフで表示することで、これらの値を比較し、相関関係を探すことができます。異なる時間範囲で同じ値を表示したり、2つの異なる値のトレンドを比較したりすることができます。

トレンドグラフを設定するには、以下の手順を使用します：

1. サイドバーで、**AudienceStream &gt; Dashboard**に移動します。
1. 表示されているグラフの右下隅にある歯車アイコンをクリックします。
  ![](/images/server-side/audiencestream-dashboard-click-gear-to-flip.png)  
グラフが「反転」して、値と範囲を表示します。
  ![](/images/server-side/audiencestream-dashboard-graph-flipped.png)
2つのドロップダウンリストが表示されます。
1. ドロップダウンリストを使用して、表示する値を選択します。
1. ドロップダウンリストを使用して、**Current**または**Previous**の時間範囲を選択します。
1. ドロップダウンリストを使用して、以下のいずれかを選択します：
    * カレンダー日
    * カレンダー週
    * カレンダー月
    * ローリングデイ
    * ローリングウィーク
    * ローリング月
1. **Finish**をクリックします。グラフはトレンドラインに戻ります。
  ![](/images/server-side/whiteui-audiencestream-select-values-and-finish.png)

## 時間範囲

トレンドグラフで値を表示するときは、時間範囲を選択する必要があります。範囲は、データを表示したい時間範囲であり、今日に対する関係で計算されます。選択する主要なパラメーターは2つあります：CurrentとPrevious。

### Current

この値は、今日が含まれる時間範囲を指します。

* **Day**: 現在の日。
* **Week**: この時間範囲は、最近の日曜日から始まり、現在の日まで終わります。
* **Month**: この時間範囲は、今月の初日から始まり、現在の日まで終わります。
* **Rolling Day**
* **Rolling Week**
* **Rolling Month**

この値は、今日が含まれる時間範囲の前の時間範囲です。

* **Day**: 前日の時間範囲。たとえば、今日が水曜日の場合、この日付範囲は火曜日の午前0時から午後11時59分までをカバーします。
* **Week**: 前週の時間範囲。週は日曜日に始まり、土曜日に終わります。
* **Month**: 前月の時間範囲。たとえば、今日が6月14日の場合、この日付範囲は5月1日から31日までをカバーします。
* **Rolling Day**
* **Rolling Week**
* **Rolling Month**

### バッジ活動

**Badge activity**ウィンドウは画面の右側に表示され、指定した時間範囲でバッジが訪問者に割り当てられたり、訪問者から削除されたりした回数をリストします。

![](/images/server-side/whiteui-audiencestream-badgeactivity.png)

バッジをクリックして、訪問者に割り当てられたり削除されたりした方法と時間の詳細を表示します。

![](/images/server-side/whiteui-audiencestream-badge-activity-details.png)

### ダッシュボードシート

ダッシュボードシートは、トレンドグラフのカスタマイズされたビューです。デフォルトのシートは**Main**という名前で、名前を変更したり削除したりすることはできません。ダッシュボードシートは番号付けされており、ここで見ることができるダッシュボードのサイドバーを通じて利用できます：

![](/images/server-side/whiteui-audiencestream-dashboard-dashboardsheetscollapsed.png)

サイドバーの上部にある矢印をクリックして、シートの名前を表示し、シートを編集します。ダッシュボードのサイドバーを使用して、以下のアクションを実行できます：

![](/images/server-side/whiteui-audiencestream-dashboard-dashboard-sheets-expanded.png)

* **シートを追加する**: サイドバーの下部にある**&#43; Add Dashboard Sheet**をクリックしてシートを追加し、編集アイコンをクリックしてシートに名前を付けます。新しい名前でシートを保存するには**Save**をクリックします。
* **シートの名前を変更する**: 編集アイコンをクリックしてシートの名前を変更し、**Save**をクリックします。
* **シートを削除する**: 名前の右側にある&#34;**X**&#34;アイコンをクリックしてシートを削除し、**Yes**をクリックして確認します。
