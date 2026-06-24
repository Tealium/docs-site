---
title: Threshold alerts
description: Set up threshold alerts to receive email notifications when a dashboard visual crosses a defined value.
url: https://docs.tealium.com/server-side/insights/threshold-alerts/
---
Threshold alerts send an email notification to the alert creator when a dashboard visual crosses a defined value. You can create multiple alerts for the same visual.

## How threshold alerts work

Alerts are available on KPI, Gauge, Table, and Pivot Table visuals.

When you create an alert, you set a condition (is above, is below, or is equal to) and a threshold value. Each time the underlying dataset refreshes, the alert evaluates the visual against your threshold. If the condition is met, an email notification is sent.

### Notification frequency

The **Notify me** setting controls how often notifications are sent:

* **As frequently as possible**: Sends a notification each time the dataset refreshes and the alert condition is met.
* **Daily at most**: Sends at most one notification per day.
* **Weekly at most**: Sends at most one notification per week.

The frequency of **As frequently as possible** notifications depends on how often the dataset updates.

### Filters and alerts

Filters applied to a visual also apply to its alerts. When you create an alert, the alert locks in the filter settings active at that time and evaluates the threshold against that filtered data.

* **Fixed at creation**: The alert uses the filter settings active at the exact time you create it.
* **Independent of dashboard updates**: Changing or removing a filter on the live dashboard does not affect the existing alert.
* **Filter changes require a new alert**: To use a new filter configuration, create a new alert with the updated settings.

## Create an alert

1. Go to **Insights &gt; Dashboards**.
1. Select a dashboard.
1. Click the **Alerts** icon in the toolbar.
1. Click **Create alert**.
1. From the **Visual on this sheet** drop-down, select a visual.
   Alerts are available on KPI, Gauge, Table, and Pivot Table visuals. Visuals that do not support alerts do not appear in the list.
1. Click **Next**.
1. In the **Name** field, confirm or update the alert name.
1. From the **Condition** drop-down, select a condition:
   * **Is above**
   * **Is below**
   * **Is equal to**
1. In the **Threshold** field, enter a value.
1. From the **Notify me** drop-down, select the notification frequency. For more information, see [Notification frequency](#notification-frequency).
1. To receive a notification when the visual has no data, select **Email me when there is no data**.
1. Click **Save**.

## Manage alerts

To view and manage existing alerts:

1. Go to **Insights &gt; Dashboards**.
1. Select a dashboard.
1. Click the **Alerts** icon in the toolbar.
   The **Manage alerts** panel lists your alerts. Each alert displays its condition and notification frequency, and includes a toggle to enable or disable it.
   ![](/images/server-side/data-insights/manage-alerts.png)
1. To edit, view history, or delete an alert, click the three-dot menu for the alert and select an option.
1. To create another alert, click **Create alert**.

## Example: Set up an alert for total connector errors

The following example shows how to add a gauge visual to the connectors dashboard and configure an alert for total connector errors.

### Add a gauge visual for error count

1. Go to **Insights &gt; Dashboards &gt; Analysis**.
1. Open **Connectors Analysis**.
   ![](/images/server-side/data-insights/threshold-alerts-connectors-analysis.png)
1. Open the **2. Connector and Action Errors** tab.
1. Locate the **Failed connector counts over time** visual.
1. Click the three-dot menu and select **Duplicate visual to &gt; This sheet** to retain the existing error-counting filters.
   ![](/images/server-side/data-insights/threshold-alerts-duplicate-visual.png)
1. Rename the duplicated visual to distinguish it from the original.
1. Update the visual type to **Gauge** to display the total error count.
   ![](/images/server-side/data-insights/threshold-alerts-gauge-type.png)
1. (Optional) Resize the gauge chart by dragging the border sizing handles.
   ![](/images/server-side/data-insights/threshold-alerts-gauge-visual.png)

### Publish and configure the alert

1. Click **Publish**.
1. Select the **New dashboard** tab.
1. In the **Dashboard name** field, enter a name for the dashboard.
1. From the **Select sheets** drop-down, select **All sheets**.
1. Click **Publish Dashboard**.
   ![](/images/server-side/data-insights/threshold-alerts-publish-dashboard.png)
1. Open the **Connector and Action Errors** sheet.
1. Locate the gauge visual.
1. Click the **Alerts** icon.
1. Select the visual and configure the alert. For field descriptions, see [Create an alert](#create-an-alert).
1. Click **Save**.
   ![](/images/server-side/data-insights/threshold-alerts-create-connector-alert.png)

## Example: Set up an alert for total event volume

1. Go to **Insights &gt; Dashboards &gt; Dashboards**.
   ![](/images/server-side/data-insights/threshold-alerts-dashboards-list.png)
1. Select the **Total events count** dashboard.
1. Locate the **Total events count for all time** chart.
1. Select the chart.
1. Click the **Alerts** icon.
   ![](/images/server-side/data-insights/threshold-alerts-total-events-chart.png)
1. Configure the alert. For field descriptions, see [Create an alert](#create-an-alert).
   ![](/images/server-side/data-insights/threshold-alerts-create-events-alert.png)
1. Click **Save**.
   ![](/images/server-side/data-insights/threshold-alerts-events-alert-configured.png)

## Example: Add an alert with a different date range filter

Each date range filter requires its own alert because filters are locked at the time you create an alert.

1. Go to **Insights &gt; Dashboards &gt; Dashboards**.
1. Select the **Total events count** dashboard.
1. Expand the **Controls** panel.
1. Change the **Date range** filter value to the range you want to monitor. For example, select **Last number of days** and enter `90`.
   ![](/images/server-side/data-insights/threshold-alerts-date-range-filter.png)
1. Select the **Total events count for all time** chart.
1. Click the **Alerts** icon.
1. Click **Create alert**.
1. In the **Name** field, enter a name that reflects the chart title and filter value. For example, `Total events count last 90 days`.
   Include the filter value in the alert name. The alert name is the only record of the filter settings used to create it.
1. Configure the alert. For field descriptions, see [Create an alert](#create-an-alert).
1. Click **Save**.
   The **Manage alerts** panel shows both alerts for the same chart, each with its own date range filter and threshold.
