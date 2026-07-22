---
title: 閾値アラート
description: ダッシュボードのビジュアルが定義された値を超えたときにメール通知を受け取るための閾値アラートを構成します。
url: https://docs.tealium.com/ja/server-side/insights/threshold-alerts/
---
閾値アラートは、ダッシュボードのビジュアルが定義された値を超えるとアラート作成者にメール通知を送信します。同じビジュアルに対して複数のアラートを作成することができます。

## 閾値アラートの仕組み

アラートはKPI、ゲージ、テーブル、ピボットテーブルビジュアルで利用可能です。

アラートを作成するとき、条件（以上、以下、または等しい）と閾値を構成します。基礎となるデータセットが更新されるたびに、アラートは閾値に対してビジュアルを評価します。条件が満たされると、メール通知が送信されます。

### 通知の頻度

**通知する** 構成は通知が送信される頻度を制御します：

* **可能な限り頻繁に**：データセットが更新され、アラート条件が満たされるたびに通知を送信します。
* **最大で日に一回**：一日に一回まで通知を送信します。
* **最大で週に一回**：一週間に一回まで通知を送信します。

**可能な限り頻繁に** の通知の頻度は、データセットが更新される頻度に依存します。

### フィルターとアラート

ビジュアルに適用されたフィルターは、そのアラートにも適用されます。アラートを作成するとき、その時点でアクティブなフィルター構成をアラートが固定し、そのフィルターされたデータに対して閾値を評価します。

* **作成時に固定**：アラートは作成時にアクティブだったフィルター構成を使用します。
* **ダッシュボードの更新とは独立**：ライブダッシュボード上でフィルターを変更または削除しても、既存のアラートには影響しません。
* **フィルターの変更は新しいアラートが必要**：新しいフィルター構成を使用するには、更新された構成で新しいアラートを作成します。

## アラートの作成

1. **Insights > Dashboards** に移動します。
1. ダッシュボードを選択します。
1. ツールバーの **Alerts** アイコンをクリックします。
1. **Create alert** をクリックします。
1. **Visual on this sheet** ドロップダウンからビジュアルを選択します。
   アラートはKPI、ゲージ、テーブル、ピボットテーブルビジュアルで利用可能です。アラートをサポートしていないビジュアルはリストに表示されません。
1. **Next** をクリックします。
1. **Name** フィールドで、アラート名を確認または更新します。
1. **Condition** ドロップダウンから条件を選択します：
   * **Is above**
   * **Is below**
   * **Is equal to**
1. **Threshold** フィールドに値を入力します。
1. **Notify me** ドロップダウンから通知の頻度を選択します。詳細は [Notification frequency](#notification-frequency) を参照してください。
1. ビジュアルにデータがないときに通知を受け取るには、**Email me when there is no data** を選択します。
1. **Save** をクリックします。

## アラートの管理

既存のアラートを表示および管理するには：

1. **Insights > Dashboards** に移動します。
1. ダッシュボードを選択します。
1. ツールバーの **Alerts** アイコンをクリックします。
   **Manage alerts** パネルにはアラートがリストされており、各アラートはその条件と通知の頻度を表示し、有効または無効にするトグルが含まれています。
   ![](https://docs.tealium.com/images/server-side/data-insights/manage-alerts.png)
1. アラートを編集、履歴を表示、または削除するには、アラートの三点リーダーメニューをクリックしてオプションを選択します。
1. 別のアラートを作成するには、**Create alert** をクリックします。

## 例：トータルコネクタエラーのアラートを構成する

次の例は、コネクタダッシュボードにゲージビジュアルを追加し、トータルコネクタエラーのアラートを構成する方法を示しています。

### エラー数のためのゲージビジュアルを追加する

1. **Insights > Dashboards > Analysis** に移動します。
1. **Connectors Analysis** を開きます。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-connectors-analysis.png)
1. **2. Connector and Action Errors** タブを開きます。
1. **Failed connector counts over time** ビジュアルを探します。
1. 三点リーダーメニューをクリックし、**Duplicate visual to > This sheet** を選択して、既存のエラー数カウントフィルターを保持します。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-duplicate-visual.png)
1. 複製されたビジュアルの名前を変更して元のビジュアルと区別します。
1. ビジュアルタイプを **Gauge** に更新して、トータルエラー数を表示します。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-gauge-type.png)
1. (オプション) ゲージチャートのサイズを変更するには、境界サイズハンドルをドラッグします。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-gauge-visual.png)

### 公開してアラートを構成する

1. **Publish** をクリックします。
1. **New dashboard** タブを選択します。
1. **Dashboard name** フィールドにダッシュボードの名前を入力します。
1. **Select sheets** ドロップダウンから **All sheets** を選択します。
1. **Publish Dashboard** をクリックします。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-publish-dashboard.png)
1. **Connector and Action Errors** シートを開きます。
1. ゲージビジュアルを探します。
1. **Alerts** アイコンをクリックします。
1. ビジュアルを選択し、アラートを構成します。フィールドの説明については、[Create an alert](#create-an-alert) を参照してください。
1. **Save** をクリックします。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-create-connector-alert.png)

## 例：トータルイベント量のアラートを構成する

1. **Insights > Dashboards > Dashboards** に移動します。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-dashboards-list.png)
1. **Total events count** ダッシュボードを選択します。
1. **Total events count for all time** チャートを探します。
1. チャートを選択します。
1. **Alerts** アイコンをクリックします。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-total-events-chart.png)
1. アラートを構成します。フィールドの説明については、[Create an alert](#create-an-alert) を参照してください。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-create-events-alert.png)
1. **Save** をクリックします。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-events-alert-configured.png)

## 例：異なる日付範囲フィルターでアラートを追加する

各日付範囲フィルターには独自のアラートが必要です。フィルターはアラートを作成するときに固定されます。

1. **Insights > Dashboards > Dashboards** に移動します。
1. **Total events count** ダッシュボードを選択します。
1. **Controls** パネルを展開します。
1. **Date range** フィルターの値を監視したい範囲に変更します。たとえば、**Last number of days** を選択して `90` を入力します。
   ![](https://docs.tealium.com/images/server-side/data-insights/threshold-alerts-date-range-filter.png)
1. **Total events count for all time** チャートを選択します。
1. **Alerts** アイコンをクリックします。
1. **Create alert** をクリックします。
1. **Name** フィールドに、チャートのタイトルとフィルター値を反映した名前を入力します。たとえば、`Total events count last 90 days`。
   
<blockquote>
フィルター値をアラート名に含めます。アラート名は、それを作成するために使用されたフィルター構成の唯一の記録です。
</blockquote>

1. アラートを構成します。フィールドの説明については、[Create an alert](#create-an-alert) を参照してください。
1. **Save** をクリックします。
   **Manage alerts** パネルは、同じチャートの両方のアラートを表示し、それぞれに独自の日付範囲フィルターと閾値があります。