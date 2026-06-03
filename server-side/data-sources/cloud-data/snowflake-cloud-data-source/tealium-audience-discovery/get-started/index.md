---
title: Get started with Tealium Audience Discovery for Snowflake
description: Set up Tealium Audience Discovery for Snowflake and connect your first audience to Tealium.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/get-started/
---
This guide walks you through setting up Tealium Audience Discovery for Snowflake for the first time. By the end, you have an audience running in Snowflake and connected to Tealium for activation.

## Requirements

* A Snowflake account with owner or administrator permissions to install the app and configure access.
* Access to the Snowflake databases, schemas, and tables you want to use for audience creation.
* A Tealium account with permission to configure data sources.

## Step 1: Install the app

Install Tealium Audience Discovery for Snowflake from the Snowflake Marketplace and grant the app access to the databases and schemas you want to use.

For detailed instructions, see [Install Tealium Audience Discovery for Snowflake]().

## Step 2: Create your first audience

1. Open Tealium Audience Discovery for Snowflake.
1. Go to **Audiences** and click **&#43; Create new audience**.
1. Enter an audience name and description.
1. Select **Point &amp; Click**.
1. Select a **Database**, **Schema**, and **Table / View**.
1. Select a **User ID column** to uniquely identify each user.
1. Click **Next**.
1. (Optional) Add filter conditions to refine the audience.
1. Click **Next**.
1. Set a refresh schedule, then click **Next**.
1. Review the configuration and click **Create audience**.

The app runs an initial load and begins refreshing the audience on the schedule you set. Monitor progress from the audience details view.

For detailed configuration options, see [Manage audiences in Tealium Audience Discovery for Snowflake]().

## Step 3: Connect the audience to Tealium

1. In the audience list, open the actions menu and click **Share**.
1. Copy the **Database**, **Schema**, and **Role** values.
1. In Tealium, go to **Sources &gt; Data Sources** and click **Add Data Source**.
1. Select **Snowflake** under **Data Cloud**.
1. Enter a name and configure the connection using the copied values.
1. Enable processing and configure processing settings.
1. Under **Build query**, select the audience table and the columns to import.
1. Set the query mode to **Timestamp &#43; Incrementing** and map the following columns:

   * **Timestamp column** — `TEALIUM_CTRL_COL_CREATED_AT`
   * **Incrementing column** — `TEALIUM_CTRL_COL_INCREMENTAL_ID`

1. Click **Test query** and verify the preview results before continuing.
1. Map the imported columns to Tealium event attributes.
1. Configure visitor ID mapping to stitch records with existing visitor profiles.
1. Review the summary and save the data source.

Tealium begins loading audience records on the schedule you configured.

For detailed configuration options, see [Connect Snowflake audiences to Tealium]().

## Next steps

* Configure connectors to activate audience segments
* Enrich audience data using Tealium attributes and audiences
* [Track membership changes]() using the `TEALIUM_CTRL_COL_IS_ACTIVE` column to trigger actions when users leave or re-qualify for an audience
