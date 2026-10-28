---
title: Introduction to event data activation
description: This article is an introduction to Tealium event data activation, a data collection and API hub that sits at the center of your data supply chain.
url: https://docs.tealium.com/server-side/getting-started/tutorials/event-data-activation/introduction/
---
## What is event data activation?

![](https://docs.tealium.com/images/tutorials/eventstream-icon.jpg)

Tealium's event data activation is a server-side platform for collecting and transforming data for integration with other server-side applications.

Event data activation offers the following key benefits:

* Reduce the size of your mobile apps.
* Minimize client-side network requests.
* Deploy new vendors without the need for code releases.

Use the platform to manage incoming data, define event requirements, inspect data quality, and configure connector integrations.

## How it works

The platform handles the entire data supply chain: from setting up data sources and validating incoming data to enhancing it with enrichments and enabling real-time actions through event feeds and connectors.

The platform supports this entire data workflow with the following features:

* Data sources (installation and data collection)
* Live Events (real-time data inspection)
* Event specifications and attributes (data layer requirements and validation)
* Event feeds (filtered event types)
* Event connectors (API hub actions)


<blockquote>
The platform is a streaming product that does not save data to disk. The platform only keeps data in memory until it is sent to its next destination.
</blockquote>


## Data sources

![](https://docs.tealium.com/images/server-side/introduction-to-eventstream-data-sources.png)

Data sources represent the platforms where you install Tealium to collect data. The first step is to add a data source. When you add a data source, you receive installation instructions for the platform you chose. Each data source has a unique key that must be used in the code to identify the data coming from that installation.

Data sources can be linked to event specifications and provide more detailed code samples showing how to track your defined events on the given platform. With data sources, you can easily filter incoming events to verify that your installation is working and to inspect data quality.

Learn more about [data sources](https://docs.tealium.com/about-data-sources/).

## Event specifications and attributes

Establish a solid data foundation by creating event specifications. Specifications define your data layer by identifying the events you want to track and their associated attributes. Specifications ensure that you maintain a high quality of data for the platform to process. Specs and attributes help you establish a universal data strategy across all of your digital properties.

Learn more about [event specifications](https://docs.tealium.com/about-event-specifications/) and [attributes](https://docs.tealium.com/about-attributes/).

## Live Events

**Live Events** is a real-time chart that shows incoming data from your data sources. After your data source is installed and sending data, the events appear on this screen. In the **Live Events** chart, click a bar to see the details of the event received. From there, you can define event attributes, see data validation of events, or define new specifications based on incoming events.

![](https://docs.tealium.com/images/server-side/white-ui-event-feed-live-events.png)
In addition, if you activate specifications, the data quality of the incoming events is reflected in the bar chart so you can quickly see if there are invalid events that need attention.

Learn more about [Live Events](https://docs.tealium.com/about-live-events/).

## Event feeds

Event feeds are groups of events that match specific conditions based on their attributes. Feeds are a subset of all events that can be targeted to vendor connectors. Working with feeds makes it easier to inspect incoming events in the **Live Events** chart and to see activity volume over time.

![](https://docs.tealium.com/images/server-side/white-ui-event-specification-search.png)

Learn more about [event feeds](https://docs.tealium.com/about-event-feeds/).

## Event connectors

Event connectors are API integrations with your vendors that send data from an event feed in real-time. Connectors are configured with your vendor account credentials and data mappings to send event attributes to the corresponding parameters expected by your vendor.

![](https://docs.tealium.com/images/server-side/white-ui-event-connectors-google-analytics.png)

Learn more about [event connectors](https://docs.tealium.com/about-connectors/).
