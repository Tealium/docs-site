---
title: About AudienceDB and EventDB
description: This article describes how to work with AudienceDB and EventDB.
url: https://docs.tealium.com/server-side/data-storage/audiencedb-eventdb/about/
---

<blockquote>
To have EventDB and AudienceDB enabled for your account and profile, [contact support](https://docs.tealium.com/support/).
</blockquote>


## How it works

AudienceDB and EventDB services store structured audience and event data in Amazon Redshift, a data warehouse based on PostgreSQL. You can query and analyze the data in Amazon Redshift using your preferred SQL client or Business Intelligence (BI) tool.

EventDB uses EventStore as a data source, importing the data from the EventStore S3 bucket into the Amazon Redshift database provided by Tealium.

AudienceStore is not a prerequisite to activate AudienceDB; these services operate independently. AudienceDB saves visitor profile data at the end of each visitor session.

After AudienceDB and EventDB have been enabled, you must select the attributes to be stored. For more information, see [Configure AudienceDB and EventDB]().

### Data storage timing

New data is stored in EventDB and AudienceDB within 30 to 90 minutes, depending on the load for the Redshift cluster.

### Database schemas

When EventDB and AudienceDB are enabled, a database is created in Amazon Redshift to store your data. Each profile has its own database schema within the same Redshift instance, which means that each user has their own username and password for each database schema (profile). The database schemas for AudienceDB and EventDB are created automatically when EventDB or AudienceDB are enabled for a profile.

### Data retention

The data stored in EventDB and AudienceDB remains available in Amazon RedShift for the length of time stated in your contract. When an event, visit, or visitor record reaches its expiration date, that record is automatically purged. Even if a visitor record is updated, the expiration date remains the same, and the record will still be purged.

Contact your account manager to review the terms of your contract that determine the length of time your data is stored.

For more information, see [Server-Side Account Settings]().

#### Changes to stored EventDB and AudienceDB attributes

If you remove an attribute that was previously added for EventDB, the attribute is no longer sent to EventDB and is also removed from EventDB. Changes to EventDB attributes have no effect on EventStore files.

If you remove an attribute that was previously added for AudienceDB, the attribute is no longer sent to AudienceDB and is also removed from AudienceDB. Changes to AudienceDB attributes have no effect on AudienceStore files.

## Tables, views, and normalized views

The columns in the Redshift database tables are named according to the attribute type and the internal attribute ID. Views and normalized views of data contain the same data as tables, but have user friendly names that make it easier to write queries. The normalized view name is similar to the view name but with the attribute ID omitted from the table name. Table names and view names are created as follows:

* **Table names**  
Column names are a combination of the attribute type and the attribute ID.  
For example: `badge_30`
* **View names**  
Column names are a combination of a user-friendly name and the attribute ID.  
For example: `visitor - badge - fan (30)`
* **Normalized view names**  
Column names are user-friendly names without attribute IDs.   
For example: `visitor - badge - fan`

Views and normalized views simplify the process of running queries with aggregations such as `SUM()` , `MIN()`, and `MAX()`.

## AudienceDB tables

Visit and visitor attributes are stored in database table columns according to their attribute type and name. Audiences are stored as columns in the visitors table. The keys for the tables are `visit_id` or `visitor_id`.

The following tables are available for visit and visitor data:

* Visit/Session Data: `visits`
* Visitor Data: `visitors`

In addition, the following tables exist for special attribute types:

* Arrays: `visit_arrays`, `visitor_arrays`
* Set of Strings: `visit_lists`, `visitor_lists`
* Tally: `visit_tallies`, `visitor_tallies`

For detailed information, see the [AudienceDB data guide](https://docs.tealium.com/audiencedb-data-guide/).

## EventDB tables

EventDB table data includes event attributes for all events in the event feed. Table columns are named according to the attribute type and name, with only some attributes referencing internal ID's. Standard Universal Data Object (UDO) variables are named with a `udo_` prefix and most column names match their corresponding attribute names, for example: `udo_event_name`. For additional information, see [Live Events and Feeds](https://docs.tealium.com/about-live-events/).


<blockquote>
Event data coming from the Tealium Collect tag also includes information about which tags executed on the page and page performance metrics. For more information, see [Tealium Collect]().
</blockquote>


The following tables are available for event data:

* Event Feed Data: `events_{FEED}`