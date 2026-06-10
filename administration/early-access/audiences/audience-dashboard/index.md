---
title: Audience dashboard
description: This article provides information about the audience dashboard.
url: https://docs.tealium.com/administration/early-access/audiences/audience-dashboard/
---
The audience dashboard is in Early Access and is only available to select customers. If you are interested in trying this feature, contact your Tealium Account Manager.

The audience dashboard provides prebuilt reports for monitoring audience sizes over time, identifying top growing and declining audiences, and tracking join and leave activity.

## Requirements

The audience dashboard requires the Audience Dashboard feature to be enabled on your profile. To enable this feature, contact your Tealium Account Manager.

The audience dashboard is not available in the `ap-southeast-1` (Hong Kong) region.

## Generate the dashboard

To generate the audience dashboard:

1. Go to **Analyze &gt; Insights &gt; Templates**.
1. Find the **Audience dashboard** template, and click **View Details**.
1. Click **Generate Dashboard**.

After you generate the audience dashboard, it may take up to 2 hours for data to appear. The dashboard updates once an hour.

If you disable the Audience Dashboard feature on your profile, the dashboard and associated dataset are scheduled for deletion after 30 days. To retain your data, re-enable the feature within this period.

## Access the dashboard

To access the audience dashboard, go to **Analyze &gt; Audience Dashboard** or **Activate &gt; Audiences** and click the **View Dashboard** link.

You can also access the dashboard in **Analyze &gt; Insights &gt; Dashboards**.

For more information about managing dashboards, see [Manage dashboards]().

## Dashboard filters

The following filters apply to all reports on the dashboard:

* **Label**: filter audiences by label. Supports multiple selections.
* **Is Audience Active**: filter to active audiences, inactive audiences, or both. Supports multiple selections.

## Prebuilt reports

The audience dashboard template includes the following predefined reports for monitoring audience data.

### Audience overview

The Audience Overview tile shows KPI tiles that summarize the audiences in the profile:

* **Total Audiences**: Total count of all audiences defined in the profile.
* **Active Audiences**: Count of audiences that have at least one active connector action.
* **Inactive Audiences**: Count of audiences with no active connector actions.

![](/images/server-side/data-insights/audience-dashboard-kpi.png)

### Top audience changes

Top Audience Changes shows the top audiences by membership change over the last 30 days. Each table includes the audience ID, audience name, current audience size, percentage change, and absolute change.

* **Top Audiences Increases Last 30 Days**: Audiences with the highest percentage growth.
* **Top Audiences Declines Last 30 Days**: Audiences with the largest percentage decline.

![](/images/server-side/data-insights/audience-dashboard-top-changes.png)

### Audiences size

The Audiences Size tile is a horizontal bar chart showing the current size of each audience. Audience Size is a point-in-time snapshot and does not update when the date range filter changes. For the time-series view, see **Audience Size** in the [Details](#details) section.

![](/images/server-side/data-insights/audience-dashboard-audiences-size.png)

### Details

The Details section shows time-series data for individual audiences. Use the following controls to filter the charts in this section:

* **Audience Name**: Select a specific audience or view all audiences.
* **Aggregation**: Group data by day, week, month, quarter, or year.
* **Date range**: Defaults to the last 30 days.

The following charts update based on the selected controls:

* **Audience Size**: Line chart showing audience size over the selected date range.
* **Joined vs. Left**: Bar chart showing join counts against combined leave, delete, purge, and stitch counts over the selected date range.

**Audience Size**

![](/images/server-side/data-insights/audience-dashboard-audience-size.png)

**Joined vs. Left**

![](/images/server-side/data-insights/audience-dashboard-joined-vs-left.png)

## Dashboard status

Dashboards created from templates may display a status label, such as **Generated** or **Update available**.
For more information, see .

## Dashboard template versions

If a new version of the audience dashboard template is available, you can update it from the **Dashboards** or **Templates** screen.
For more information, see .
