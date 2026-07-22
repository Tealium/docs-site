---
title: About Tealium Audience Discovery for Snowflake
description: Overview of Tealium Audience Discovery for Snowflake, its capabilities, and how it integrates with Tealium for audience activation.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/about/
---
Tealium Audience Discovery for Snowflake is a native Snowflake application that lets you build audiences from Snowflake data and activate them in Tealium without moving data out of Snowflake.

## How it works

The app runs entirely within your Snowflake account. It defines audiences from your data and stores each audience as a Snowflake table with a corresponding view for external access. The audience data refreshes on a schedule you configure. Tealium reads from the view using a Snowflake data source to load records for activation.

The overall flow is:

1. Create an audience in Tealium Audience Discovery for Snowflake.
1. The app stores the audience as a Snowflake table and a corresponding view.
1. The app refreshes the table on the schedule you configure.
1. In Tealium, create a Snowflake data source that connects to the audience.
1. Tealium loads the data for activation through connectors and data workflows.

![](https://docs.tealium.com/images/server-side/data-sources/tealium-audience-discovery-architecture.png)


<blockquote>
The app reads data from Snowflake and creates audience tables. It does not modify existing customer data. Audience activation and downstream workflows run in Tealium.
</blockquote>


## Requirements

* A Snowflake account owner or administrator role to install the app and manage user and data access.
* Access to the Snowflake databases and schemas to use for audience creation.
* A Tealium account with permission to configure data sources.


<blockquote>
CloudStream is recommended for easier setup because it automatically creates attributes based on incoming data. If you use AudienceStream, you must manually create attributes and audiences.
</blockquote>


For installation instructions, see [Install Tealium Audience Discovery for Snowflake](https://docs.tealium.com/install-tealium-audience-discovery/).

## Use cases

* Data teams identifying high-value or lapsed customers by exploring and querying warehouse data.
* Marketers applying point-and-click filters to Snowflake data without writing SQL.
* Teams using Cortex natural language queries to explore audience ideas and schedule them as datasets for activation.

## Next steps

* [Get started with Tealium Audience Discovery for Snowflake](https://docs.tealium.com/get-started/)
* [Install Tealium Audience Discovery for Snowflake](https://docs.tealium.com/install-tealium-audience-discovery/)
* [Manage audiences in Tealium Audience Discovery for Snowflake](https://docs.tealium.com/manage-discovery-audiences/)
* [Connect Snowflake audiences to Tealium](https://docs.tealium.com/connect-snowflake-audiences/)