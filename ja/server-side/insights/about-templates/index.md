---
title: テンプレートについて
description: この記事では、テンプレートと事前定義されたダッシュボードについての情報を提供します。
url: https://docs.tealium.com/ja/server-side/insights/about-templates/
---
インサイトテンプレートを使用すると、`Total Events Count` や `Total Visits Count` などの事前定義されたダッシュボードをオンデマンドで生成できます。

## 仕組み

テンプレートは、データセット、分析、およびダッシュボードで構成されています。データセットは、ダッシュボードに表示されるデータベース内のデータの集合です。分析は、データベースのフィールドとダッシュボードに表示されるビジュアルを指定します。

**テンプレート詳細** 画面では、ダッシュボードの各ビジュアルの例と、テンプレートで使用される各データセットの情報の要約が表示されます。

例えば、以下の **テンプレート詳細** の例は、トータルイベント数ダッシュボードのビジュアルを示しています：
![](https://docs.tealium.com/images/server-side/data-insights/data-insights-template-details.png)

ビジュアルの後にデータセット情報が表示されます：
![](https://docs.tealium.com/images/server-side/data-insights/data-insights-templates-dataset-info.png)

## 事前定義されたダッシュボードのテンプレート

以下の事前定義されたダッシュボードのテンプレートは、DataAccess（AudienceDBまたはEventDB）からの事前定義された属性に基づいています：
* **Total Events Count**  
時間経過に伴うイベント数、イベントタイプ、最も頻繁に訪れたページに関する情報を表示します。
* **Total Visits Count**  
訪問、訪問ごとの総イベント数、訪問時間に関する情報を表示します。
* **Total Visitors Count**  
訪問と訪問の活動に関する情報を表示します。

イベント数、訪問数、訪問数のダッシュボードに表示されるデータは、夜に一度更新されます。

## テンプレートの状態

**テンプレート** 画面にリストされているテンプレートには、以下のラベルのいずれかが付けられている場合があります：
* **Generated** &ndash; ダッシュボードが生成され、ダッシュボード画面で表示できます。例：![](https://docs.tealium.com/images/server-side/data-insights/generated-label.png)

テンプレートにラベルがない場合、ダッシュボードは生成されていません。