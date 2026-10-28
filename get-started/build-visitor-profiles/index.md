---
title: Build visitor profiles
description: Learn how Tealium builds real-time visitor profiles from events, merges profiles across devices, and evaluates audiences from profile attributes.
url: https://docs.tealium.com/get-started/build-visitor-profiles/
---
A visitor profile is a running record of one visitor. Each new event updates the profile in real time, so audiences and connectors always work from current data.

## What a profile contains

A visitor profile stores visitor attributes. Visitor attributes follow the visitor from visit to visit, such as lifetime order total or favorite product category.

Two shorter-lived scopes describe the moment instead of the visitor:

* **Event attributes**: Describe a single event, such as the page name or the order total.
* **Visit attributes**: Describe the current visit, such as the number of pages viewed in the session.


![](https://docs.tealium.com/images/icons/icon-cube.svg)

#### Attributes

Learn about attribute scopes and data types.


## How events update a profile

Enrichments are the business logic of your event and customer data. An enrichment updates an attribute when an event arrives, such as adding the order total to a lifetime value or recording the category that a visitor views most. Rules determine when each enrichment applies, such as only on purchase events.

Enrichments also assign and remove badges. A badge labels visitors who show a behavior pattern, such as frequent buyers.

Tealium processes each event in this order:

1. Tealium receives the event.
1. Tealium enriches event attributes.
1. Tealium finds the visitor profile, stitches profiles if needed, and enriches visit and visitor attributes.
1. Tealium evaluates audiences.
1. Tealium triggers connectors, which send data to vendors.


![](https://docs.tealium.com/images/icons/icon-cubes.svg)

#### Enrichments

Learn how enrichments apply business logic to event and visitor data.



![](https://docs.tealium.com/images/icons/icon-badge-check.svg)

#### Badges

Learn how badges label visitors who show specific behavior patterns.



![](https://docs.tealium.com/images/icons/icon-sitemap-light.svg)

#### Order of operations

Learn the exact sequence that Tealium follows for each event.


## Merge profiles by identity

Tealium creates an anonymous profile the first time it sees a visitor. If someone browses on a laptop and later on a phone, Tealium sees two visitors and creates two profiles.

When that person logs in on both devices, Tealium can recognize them and merge the two profiles into one. This process is called visitor stitching.

Visitor stitching relies on a visitor ID attribute. A visitor ID attribute is a special attribute that holds a known identifier that you choose, such as an email address or customer ID. When a visitor ID value matches more than one profile, Tealium merges those profiles into a new visitor profile. After a visitor ID attribute has a value, the value cannot change, and you cannot separate stitched profiles.

<!-- TODO: Insert identity diagram here: two anonymous profiles (laptop, phone) merge into one profile after login. -->


![](https://docs.tealium.com/images/icons/icon-arrows-merge.svg)

#### Visitor stitching

Learn how Tealium merges profiles for the same visitor across devices.


## Enrich profiles with offline and data cloud data

Events from your websites and apps show what visitors do online. Other customer data, such as CRM records, loyalty status, offline purchases, and model scores, often lives in files or in your data cloud. Tealium brings that data in as events, so it updates the same visitor profiles:

* **Cloud data sources**: Tealium reads rows from a table or view in your data cloud at a frequency that you set, such as hourly or daily.
* **File import**: Tealium reads files of historical or offline data, such as CRM exports, from a file service.
* **Data sources**: External systems send records over HTTP or webhooks, so backend data such as order updates or call center records reaches visitor profiles in real time.

Enrichments then write the imported values to visitor attributes, next to the behavioral data from your websites and apps.


![](https://docs.tealium.com/images/icons/icon-cloud-down.svg)

#### Cloud data sources

Import rows from your data cloud as events.



![](https://docs.tealium.com/images/icons/icon-file-arrow-up.svg)

#### File import

Import files of historical and offline data as events.


## Define audiences

An audience is a group of visitors who share a set of attributes. You define an audience with conditions on profile attributes, such as visitors who viewed a product category several times this week but have not purchased. Marketing teams use an audience like this one to retarget visitors with ads or to start an email series.

Audiences update as events arrive. When an event changes a visitor's attributes, Tealium evaluates the audience conditions again. When a visitor joins or leaves an audience, connectors can send that change to your vendors. For more information, see [Activate customer data](https://docs.tealium.com/activate-customer-data/).


![](https://docs.tealium.com/images/icons/icon-audience.svg)

#### Audiences

Learn how to define audiences from visitor attributes.

