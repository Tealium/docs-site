---
title: Connect Snowflake audiences to Tealium
description: Connect an audience from Tealium Audience Discovery for Snowflake to Tealium using a Snowflake cloud data source.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/connect-snowflake-audiences/
---
After creating an audience in the app, connect it to Tealium to load audience records and activate them using connectors or other downstream workflows.

## Requirements

* An active audience in Tealium Audience Discovery for Snowflake. See [Create an audience]().
* A Tealium account with permission to configure data sources.
* Access to the app and the Snowflake connection values configured during installation.
* (Optional) To use webhook or other outbound integrations, your Snowflake administrator must configure a network rule and external access integration for the destination URL. Snowflake blocks outbound traffic by default.

## Get connection details from the app

1. From the **Audiences** list, open the actions menu for the audience.
1. Click **Share**.
1. Note the following values from the dialog:
   * **Database** — the database name (for example, `TEALIUM_AUDIENCE_DISCOVERY_APP`)
   * **Schema** — the schema name (for example, `TEALIUM_EXTERNAL_ACCESS`)
   * **View name** — the generated view name for the audience
   * **Audience view** — the fully qualified view name in `DATABASE.SCHEMA.VIEW_NAME` format
   * **Query** — a pre-built `SELECT` statement you can use when configuring the data source

![](/images/server-side/data-sources/tealium-audience-discovery-share-dialog.png)

## Create the Snowflake data source

1. In Tealium, go to **Sources &gt; Data Sources**.
1. Click **Add Data Source**.
1. Select **Snowflake** under **Data Cloud**.

When configuring the connection, use the values from the app:

* **Database Name** — the **Database** value from the share dialog (for example, `TEALIUM_AUDIENCE_DISCOVERY_APP`)
* **Database Schema** — the **Schema** value from the share dialog (for example, `TEALIUM_EXTERNAL_ACCESS`)
* **Connection Role** — the role configured during installation (for example, `TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE`)
* **Connection Warehouse** — the warehouse configured during installation (for example, `TEALIUM_AUDIENCE_DISCOVERY_WH`)

For complete configuration steps, see [Snowflake cloud data source]().


If you have multiple audiences, reuse the same Snowflake connection configuration. Create a separate data source for each audience.


## Configure the query mode for audience tables

Audience tables include system-managed control columns that track when records are added and updated.

For audience tables, use **Timestamp &#43; Incrementing**. This configuration reliably loads new users as they are added to the audience.

Map the columns as follows:

* **Timestamp column** — `TEALIUM_CTRL_COL_CREATED_AT`
* **Incrementing column** — `TEALIUM_CTRL_COL_INCREMENTAL_ID`

Tealium uses the timestamp column to load records added since the last run. The incrementing column ensures records are processed in order.

### Track membership changes

To process users who leave and later re-qualify for the audience, use a different timestamp column:

* **Timestamp column** — `TEALIUM_CTRL_COL_LAST_UPDATED_AT` or `TEALIUM_CTRL_COL_MEMBERSHIP_CHANGED_AT`
* **Incrementing column** — `TEALIUM_CTRL_COL_INCREMENTAL_ID`
* **Filter condition (recommended)** — `TEALIUM_CTRL_COL_IS_ACTIVE = true`

This approach processes users who re-qualify for the audience after leaving.

This configuration ensures that Tealium:

* Loads new or updated audience records
* Processes data incrementally
* Aligns with how the audience table is updated in Snowflake


Set the data source schedule to match or be less frequent than the audience refresh schedule in the app. Running the data source more frequently results in empty loads.


## Complete the data source configuration

After setting the query mode, complete the remaining steps:

1. Select the audience view using the **View name** value from the share dialog.
1. Validate the query.
1. Map columns to event attributes.
1. Configure visitor ID mapping.

These steps follow the standard Snowflake data source workflow. For details, see [Snowflake cloud data source]().

## Next steps

After configuring the data source:

* Enrich and manage audience data using Tealium attributes and audiences
* Configure connectors to activate audience segments