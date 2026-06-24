---
title: About Tealium Insights
description: This article provides information about Tealium Insights, which provides business intelligence capabilities for the Tealium Customer Data Hub.
url: https://docs.tealium.com/server-side/insights/about/
---
Insights is a customizable reporting tool, powered by AWS QuickSight. Insights provides predefined dashboards that visualize event data from EventDB and  visit and visitor data from AudienceDB. These dashboards are based on predefined attributes that are defined by Tealium and are available to all profiles by default.

You can also create custom dashboards by creating a new analysis and publishing it as a dashboard. For more information, see [Manage analyses]().

Visualizations can be created for operational data such as the volume and quality of data collected or the success/failure rates of triggered actions, as well as customer behavioral data such as traffic to customer experience channels or the population of audience segments.

Insights must be enabled for your account. For additional information, contact your customer success manager.

## Requirements

The following DataAccess products are required for Insights:

* **EventDB** &amp;ndash; Must be enabled for dashboards based on event data.
* **AudienceDB** &amp;ndash; Must be enabled for dashboards based on visit and visitor data.

## How it works

Insights provides dashboard templates that you can use to generate the predefined dashboards. The templates specify the dataset (the source of the data) and the fields used for the dashboard, as well as the types of graphs that are displayed. For more information, see [About templates]() and [Manage dashboards]().

Using templates, you can quickly generate predefined dashboards for your data without the need to configure datasets and dashboards. Generated dashboards can be exported to PDF or CSV and downloaded.

If dashboard errors occur, check the **Templates &gt; Template Details** screen. The dataset may need to be refreshed. For more information, see [Refresh a dataset]().

### Custom dashboards

To create a custom dashboard, you create an analysis. An analysis specifies the dataset, the fields from the dataset to be included in graphs, and the graphs for the dashboard. You can use an existing dataset or configure a new dataset based on an existing data source. After you have created an analysis, you can publish it as a dashboard.

#### Export and import custom dashboards

To avoid having to create a custom dashboard in multiple profiles, you can export a custom dashboard to a JSON file and import this JSON file into other profiles. For more information, see [Export a custom dashboard]().

### Datasets

The datasets for predefined dashboards are based on the predefined attributes stored in DataAccess (EventDB and AudienceDB). Datasets can be edited.

Insights uses SPICE (Super-fast Parallel In-memory Calculation Engine) datasets for all predefined dashboards. Data for SPICE datasets is stored in quick access memory used by Amazon QuickSight.

Insights datasets are automatically created when predefined dashboards are generated. Each predefined dashboard has its own dataset.

## Author and reader roles

 Insights users must also be a member of a permission group with view access to the Insights feature. For more information, see [Admin roles]() and [Permission groups](). To manage Insights user roles, contact your customer success manager. 

Insights provides the following user roles:

* **All users** &amp;ndash; By default, all users in the profile can:
    * Generate and update dashboards from templates.
    * Export or import custom dashboards.
    * View dashboards and create PDFs for dashboards.
* **Reader** &amp;ndash; Users with the reader role have all the default permissions, plus they can:
    * Subscribe to an existing email schedule for dashboards.
    * Create and manage threshold alerts for dashboard visuals.
* **Author** &amp;ndash; Users with the author role have all the default and reader permissions, plus they can:
    * Create dashboards and share them with other users in the account.
    * Create analyses and datasets.
    * Edit a predefined analysis and save it as a new analysis.
    * Create dashboards from a predefined analysis.
    * Create and subscribe to an email delivery schedule for a dashboard.

Insights provides five reader roles and two author roles per profile. Additional reader and author roles can be purchased. For more information, contact your customer success manager.