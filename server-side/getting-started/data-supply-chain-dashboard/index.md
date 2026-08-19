---
title: Data Supply Chain dashboard
description: Monitor your data pipeline, review connector health, and navigate to data sources, feeds, and connectors from a single view.
url: https://docs.tealium.com/server-side/getting-started/data-supply-chain-dashboard/
---
## How it works

The data supply chain dashboard shows a summary of your data pipeline: event volume, connector health, and active audiences. Use it to monitor data flow, identify connection issues, and navigate to components.

The dashboard displays three panels:

* **Filters:** Adjust the view by product and by time period.
* **Data Flow Summary:** See summary metrics and status alerts.
* **Data Flow Details:** Inspect specific components, view connections, and navigate to edit.

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-dashboard.png)

## Data supply chain views

The dashboard view changes based on the product and time period you select. Select a product, then use the drop-down to select a time period.

Most views include the following shared views, with additional views described in the product-specific sections below.

* **Data Sources:** Go to data sources.
* **Events Received:** Go to live events.
* **Events Inspected:** Go to event specifications and summary metrics for event types.

### All Products

From the **All Products** summary view, select from the shared views or one of the following additional views:

* **Actions and Functions Triggered:** View the number of successful and failed connector actions and functions.
* **Connectors:** Go to Event Data and Customer Data connectors.

The **All Products** view also displays a list of created [functions]() and their status at the bottom of the screen.

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-all-products-view.png)

### Event Data

From the **Event Data** summary view, select from the shared views or one of the following additional views:

* **Enrichments Applied:** Go to attributes.
* **Active Feeds:** Go to feeds.
* **Event Data Actions and Functions Triggered:** View the number of successful or failed Event Data actions and functions.
* **Event Data Connectors:** Go to Event Data connectors.

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-event-data-view.png)

### Customer Data

From the **Customer Data** summary view, select from the shared views or one of the following additional views:

* **Visit Count:** View the number of visitors in the time period selected.
* **Active Audiences:** Go to audiences.
* **Customer Data Actions and Functions Triggered:** View the number of successful or failed Customer Data actions and functions.
* **Customer Data Connectors:** Go to Customer Data connectors.

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-customer-data-view.png)

DataAccess products (EventStore, EventDB, AudienceStore, and AudienceDB) include the following additional views.

### EventStore

From the **EventStore** summary view, select from the shared views or one of the following additional views:

* **EventStore Feeds:** Go to feeds.
* **Events Sent to S3:** View the number of events sent to your S3 bucket.

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-eventstore-view.png)

### EventDB

From the **EventDB** summary view, select from the shared views or one of the following additional views:

* **EventDB Feeds:** Go to feeds.
* **Events Sent to Redshift:** View the number of events sent to Redshift.

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-eventdb-view.png)

### AudienceStore

From the **AudienceStore** summary view, select **Data Sources** or one of the following views:

* **Active Audiences:** Go to audiences.
* **Visitors Sent to S3:** View the number of visitors sent to your S3 bucket.

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-audiencestore-view.png)

### AudienceDB

From the **AudienceDB** summary view, select **Data Sources** or one of the following views:

* **Active Audiences:** Go to audiences.
* **Visitors Sent to Redshift:** View the number of visitors sent to Redshift.

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-audiencedb-view.png)

## Data flow and relationships

The lower portion of the screen shows data relationships and data flow. Drill down into the details of related items to navigate and edit.

![](https://docs.tealium.com/images/server-side/e44f1444-fdc8-40f6-a6b1-2e181191468e-1-201-a.jpeg)

## Working with the dashboard

* To expand or collapse the details for an item, click the expand icon next to it.
* To sort a list, use the up (▲) or down (▼) arrows to sort by volume, action success, or action failure.
* To go directly to a data source, connector, or event feed to edit, click the actions menu (**︙**).
* To view error or warning details, hover over the warning icon. Click **Learn More** to read about how to resolve the issue.
