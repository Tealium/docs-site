---
title: How Tealium works
description: Learn how Tealium collects events, builds real-time visitor profiles, and activates customer data across your tools, apps, and AI agents.
url: https://docs.tealium.com/get-started/how-tealium-works/
---
Tealium is a real-time customer data collection and activation platform. Tealium receives events from your websites, apps, servers, and data cloud. It builds visitor profiles from those events and sends the data to your marketing and analytics vendors, apps, and AI agents.

<!-- TODO: Insert overview diagram here. See the dependency map in claude-workspace/DOC-3614/analysis.md for the Mermaid source. Use generic labels with no product names. -->

## Real-time event ingestion

An event is a record of something a visitor did, such as a page view, a login, or a purchase. Attributes are the values that describe the event, such as the page name or the order total.

Every source sends data to Tealium as events. Sources include websites, mobile apps, backend servers, files, and tables in your data cloud. For more information, see [Collect customer data](https://docs.tealium.com/collect-customer-data/).

## Instant profile enrichment

Tealium can act on an event when it arrives, without visitor profile data. For example, Tealium can send every page view to your analytics vendor as it happens.

Tealium can also use the event to update a visitor profile, which is a running record of data about one visitor. One event can trigger an action and update a profile. For more information, see [Build visitor profiles](https://docs.tealium.com/build-visitor-profiles/).

## Activation across your stack

Activation delivers event and profile data to the tools you use and returns data to apps and services on request:

* **Connectors**: Send data to vendors when events arrive or when visitor profiles meet conditions you define.
* **Context API**: Returns current profile data to apps and services on request.

For more information, see [Activate customer data](https://docs.tealium.com/activate-customer-data/) and [Use AI with Tealium](https://docs.tealium.com/use-ai-with-tealium/).

## Native data cloud integration

A data cloud is a platform for storing and querying large datasets, such as Snowflake, Databricks, or Google BigQuery. Unlike vendor connectors, the data cloud integration is bidirectional: Tealium can read from and write to your data cloud. Your data cloud connects to Tealium in the following ways:

* **Activate in place**: Tealium reads data cloud tables and sends segments (groups of rows that match conditions) to connectors without storing the data in Tealium. This zero-copy approach keeps your data cloud as the system of record.
* **Export**: Tealium sends events and visitor data to your data cloud.
* **Import**: Tealium reads rows from your data cloud and processes each row as an event.

For more information, see [Work with your data cloud](https://docs.tealium.com/work-with-your-data-cloud/).

## Enterprise-grade data governance

Consent and identity controls apply as data moves through Tealium. Consent orchestration checks consent on each event before Tealium processes the event. Identity controls decide which events belong to which visitor. For more information, see [Govern customer data](https://docs.tealium.com/govern-customer-data/).
