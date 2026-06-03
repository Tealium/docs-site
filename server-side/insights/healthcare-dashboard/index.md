---
title: Healthcare dashboard
description: This article provides information about the healthcare dashboard.
url: https://docs.tealium.com/server-side/insights/healthcare-dashboard/
---
The healthcare dashboard provides prebuilt reports for healthcare organizations using event-based data from EventDB. Use this dashboard for visitor and session insights across traffic sources, device types, new and returning traffic, and UTM parameters.

## Requirements

The healthcare dashboard requires:

* EventDB
* The `utag_main__se` attribute which tracks the number of sessions for a visitor. If you encounter errors when generating the dashboard, this attribute may need to be configured as a first-party cookie in EventStream and made available in EventDB.

## Generate and access the dashboard

To generate the healthcare dashboard:

1. Go to **Server-Side &gt; Insights &gt; Templates**.
1. Find the **Healthcare dashboard** template, and click **View Details**.
1. Click **Generate Dashboard**.

After generation, access the dashboard in **Insights &gt; Dashboards**.

For more information about managing dashboards, see [Manage dashboards]().
If you have trouble accessing or using the dashboard, contact your Tealium Account Manager.

## List of prebuilt reports

The healthcare dashboard includes the following prebuilt reports:

### General

Displays visitor and session counts over time, categorized by:

* Bot vs Real User 
* Browser type
* Referrer URL
* Device
* New vs Returning Traffic

### New vs Returning Traffic – UTM parameters

Displays visitor and session counts over time for new vs. returning traffic, grouped by the following UTM parameters:

* UTM Source  
* UTM Medium  
* UTM Campaign  
* UTM Term  
* UTM Content

### Device Traffic – UTM Parameters

Displays visitor and session counts over time for various device types, grouped by the following UTM parameters:

* UTM Source  
* UTM Medium  
* UTM Campaign  
* UTM Term  
* UTM Content

The following figure shows an example of the healthcare dashboard visuals.
![](/images/server-side/healthcare-dashboard-example.png)

## Check dashboard status

Dashboards created from templates may display a status label, such as **Generated** or **Update available**.  
For more information, see .

## Update dashboard template

If a new version of the healthcare dashboard template is available, you can update it from the **Dashboards** or **Templates** screen.
For more information, see .
