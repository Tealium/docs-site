---
title: Collect customer data
description: Learn how Tealium collects customer data from websites, mobile apps, servers, files, and your data cloud, and applies quality checks and consent at collection.
url: https://docs.tealium.com/get-started/collect-data/
---
Every source sends customer data to Tealium in the same format: an event and the attributes that describe it. Because the format is the same, a purchase on your website and a purchase recorded by your call center update the same visitor profiles and trigger the same connectors.

## Collect from websites

Tag management replaces the hard-coded vendor tags on your site with a single container tag. You add, remove, and update vendor tags from the tag management interface instead of in your site code.

The data layer defines the attributes of your website and the visitor behaviors that you track, such as purchases and logins.

The collection tag sends each tracked event from the browser to your server-side profile, which receives your events and builds visitor profiles.


![](https://docs.tealium.com/images/icons/icon-tag.svg)

#### Tag management

Manage the vendor tags on your site with a single container tag.



![](https://docs.tealium.com/images/icons/icon-cubes.svg)

#### Data layer

Define the attributes and behaviors that you track.



![](https://docs.tealium.com/images/icons/icon-code.svg)

#### Collection tag

Send events from your website to your server-side profile.


## Collect from mobile apps

A mobile SDK sends events from your app to your server-side profile, where connectors deliver the data to your vendors. You can also send app data directly from the app to vendors.


![](https://docs.tealium.com/images/icons/icon-mobile.svg)

#### Mobile concepts

Collect app events and send them to Tealium with mobile SDKs.


## Collect from servers and files

Data from outside your websites and apps, such as orders from an order management system or calls from a contact center, reaches Tealium through data sources. A data source is a connection between an external system and your server-side profile. Each data source receives data in one of these ways:

* **File import**: Tealium reads files from a file service, such as an Amazon S3 bucket, and processes each row as an event. Use file import for historical and offline data.
* **HTTP API**: Backend systems send events over HTTP as they happen.
* **Webhooks**: Partner systems post events to a webhook URL that Tealium provides.


![](https://docs.tealium.com/images/icons/icon-code.svg)

#### HTTP API

Send events from any application that can send HTTP requests.



![](https://docs.tealium.com/images/icons/icon-arrow-right-into.svg)

#### Data sources

Connect external systems to your server-side profile.



![](https://docs.tealium.com/images/icons/icon-file-arrow-up.svg)

#### File import

Import files of historical and offline data as events.



![](https://docs.tealium.com/images/icons/icon-connector.svg)

#### Incoming webhooks

Receive events from partner systems that post to a Tealium webhook URL.


## Import from your data cloud

Cloud data sources read rows from tables in your data cloud and process each row as an event. Imported rows update visitor profiles and trigger connectors like any other event. To activate data cloud data without copying it into Tealium, use zero-copy warehouse activation instead. For more information, see [Work with your data cloud](https://docs.tealium.com/work-with-your-data-cloud/).

## Validate and group events

Event specifications describe the attributes that each type of event requires, so your teams implement events the same way on every platform. Tealium checks incoming events against the specifications in real time and shows which events are missing required attributes.

Event feeds group events that match conditions that you define. Connectors and data storage use event feeds to select the events that they receive.


![](https://docs.tealium.com/images/icons/icon-cubes-check.svg)

#### Event specifications

Define the attributes that each event requires and monitor event quality.



![](https://docs.tealium.com/images/icons/icon-chart-line.svg)

#### Event feeds

Group events by their attributes and send them to connectors or data storage.


## Capture consent at collection

On your website, a consent manager blocks vendor tags that a visitor has not consented to and queues events while consent is pending. On the server side, consent orchestration checks consent on each event before Tealium processes or activates the event. For more information, see [Govern customer data](https://docs.tealium.com/govern-customer-data/).
