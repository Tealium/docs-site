---
title: About data sources
description: An overview of the data source types available in Tealium, including real-time, scheduled, and batch ingestion options.
url: https://docs.tealium.com/server-side/data-sources/about-data-sources/
---
A data source is a configured connection between an external system and Tealium, defined at the server-side profile level.

The type of data source you create depends on where your data originates and whether it needs to arrive in real time or on a schedule.

## Tag management and web-based collection

If you use Tealium Tag Management, your web data source is the Tealium Collect tag. Tealium Collect sends each web tracking call to your server-side profile. For more information, see [Data sources for Tag Management](https://docs.tealium.com/data-sources-for-iq-tag-management/).

You can also collect events using the Tealium Collect library for many other web platforms. For setup instructions, see [Install on web](https://docs.tealium.com/platforms//#install-on-web).

## Mobile and app SDKs

Tealium provides native SDKs for iOS and Android, with support for many other platforms. The Tealium Collect library sends app lifecycle events, user interactions, and custom events directly to your server-side profile.

For setup instructions, see [Getting started with mobile](https://docs.tealium.com/getting-started-mobile/).

## Server-side and HTTP API

Any server application, backend system, or API gateway can post events directly to your
server-side profile using the Tealium Collect HTTP API. Use this method when data originates outside a browser or app, such as an order management system, a CRM export, an IoT device, or a custom backend integration.

For setup instructions, see [Install on server](https://docs.tealium.com/platforms//#server).

## Incoming webhooks

Some partner systems send events to Tealium by posting to a Tealium-provided webhook URL. When you create one of these data sources, Tealium generates a URL and configuration code that you use to configure the sending system.

For more information, see [Incoming webhooks](https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/).

## Cloud data sources

Cloud data sources read data from a warehouse or database on a defined schedule. The event pipeline processes each imported row as an event and copies it into Tealium for enrichment, profile building, and activation.

Use cloud data sources when you need to enrich visitor profiles or trigger connector actions from warehouse data.

For more information, see [About cloud data sources](https://docs.tealium.com/about-cloud-data-sources/).


<blockquote>
To use zero-copy cloud data sources without replicating data into Tealium, use [Tealium CloudStream](https://docs.tealium.com/about-cloudstream/).
</blockquote>


## Offline and batch import

The following options are available for importing data into Tealium outside of a direct SDK or API integration:

* [**CSV file import**](https://docs.tealium.com/about-file-import/)  
A polling-based import that reads offline data from CSV files every 10 minutes. Supports event data and customer data processing. Requires a file transfer service (Tealium S3 or your own provider).
* [**Data Connect**](https://docs.tealium.com/about-data-connect/)  
A low-code integration that connects external systems (SaaS apps, CRMs, and data warehouses) to Tealium using configurable recipes. Supports scheduled, triggered, or near real-time ingestion. Supports event data and customer data processing.
