---
title: Tealium EventStream tutorial
description: This guide introduces you to Tealium EventStream and helps you understand the application interface and the fundamental concepts of event data management.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/tutorial/
---
Step through this guide to learn how to quickly set up a working server-side profile that includes a data source, event specifications, and a vendor connector. You can then see it in action using live data from your site or application.

## Requirements

Here&#39;s what you will need to complete this guide:

* Tealium server-side login credentials
* Access to add or change the code of a website or mobile app
* A vendor that offers a server-side API (Optional)

## What is Tealium EventStream?

![](/images/tutorials/eventstream-icon.jpg)

Tealium EventStream API Hub is lightweight data collection and delivery platform. An API hub takes advantage of server-side vendor integrations, allowing you to reduce the size of your mobile apps, minimize client-side network requests, and deploy new vendors without the need for code releases. Tealium EventStream helps you manage incoming data, define event requirements, inspect data quality, and orchestrate out-going data.

## Explore the user interface

Log in to your account: &lt;https://my.tealiumiq.com/&gt;

Tealium EventStream is organized into the following areas:

* **Data sources** - Data sources represent websites or apps that send data to EventStream. Before you install a Tealium Collect library, you need to create a data source to get the installation instructions for the chosen platform.

* **Live events and event feeds** - Watch incoming data and inspect event details with the **Live Events** screen to validate data quality. Manage event feeds to identify the important types of events to use throughout the API hub.

* **Event specs** - Define the events to track and the attributes that are required. These actions create a standardized data layer and validate the quality of incoming data.

* **Attributes** - Manage event attributes and enrichments, the building blocks of your configuration.

* **Connectors** - Manage the vendor integrations at the core of the EventStream API hub. These server-side triggers send data from your event feeds to your vendors using the data mappings and configurations you set up.

The next tutorial will get you started with adding your first data source.
