---
title: About AudienceStore and EventStore
description: This article describes how to access AudienceStore and EventStore services.
url: https://docs.tealium.com/server-side/data-storage/audiencestore-eventstore/about/
---

<blockquote>
[Contact support](https://docs.tealium.com/support/) to have AudienceStore and EventStore services activated for your account.
</blockquote>


## Prerequisites

* Tealium DataAccess must be enabled.
* To send visitor profile data to the Tealium S3 bucket, an active AudienceStore connector is required. For more information, see the [AudienceStore Connector Setup Guide](https://docs.tealium.com/audiencestore-connector/).  
* To send event data to the Tealium S3 bucket, at least one active event feed is required.
* Audience names must be less than 128 characters in length. Longer audience names may be trimmed and errors may occur.

## How it works

AudienceStore and EventStore are services that store semi-structured visitor and event data on a customer-accessible Amazon S3 bucket provided by Tealium. Data is stored as shown in the following table:

| **Service** | **Storage Format** |
|---|---|
| EventStore | JSON |
| AudienceStore | JSON or CSV |

Both services write a new file to S3 whenever the file reaches 100MB (before compression) or 1 hour elapses, whichever happens first. In most cases, files are written significantly more often than that.

### Data retention

The semi-structured data stored in EventStore and AudienceStore remains available in Amazon S3 for the length of time specified in your contract. When an event, visit, or visitor record reaches its expiration date, that record is automatically purged. Even if a visitor record is updated, the expiration date remains the same, and the record will still be purged.

For more information, see [Server-Side Account Settings]().

### Activate EventStore

To save event data to EventStore, activate EventStore for one or more event feeds. For more information, see [Configure EventStore]().

When EventStore is enabled for an event feed, EventDB uses EventStore as a data source, importing the data from the EventStore S3 bucket into the Amazon Redshift database provided by Tealium.

### Activate AudienceStore

To save audience data to AudienceStore, add an AudienceStore connector for the audience. For more information, see [Configure AudienceStore]().

AudienceStore is not a prerequisite to activate AudienceDB; these services operate independently. For more information, see [About AudienceDB and EventDB]().

### AudienceStore file paths

Data files for AudienceStore are stored in the S3 bucket with a path structure that matches your account name, profile name, and the action ID of the AudienceStore connector:

```
{ACCOUNT}/{PROFILE}/audiences/{ACTION_ID}
```

The action ID can be found in the **Details** of the AudienceStore connector action, as seen here:

![](https://docs.tealium.com/images/server-side/actionid-asactiondetails.png)

Example path to AudienceStore file:

```
my-account/main/audiences/bafc28ca-9542-3929-3b94-577a84f3d672
```

### EventStore file paths

Data files for EventStore are stored in the S3 bucket as follows:

```
{ACCOUNT}/{PROFILE}/events/{EVENT_FEED_ID}
```

The event feed ID can be found in the URL for the event feed. Go to **Live Events** and click the feed to select it. Inspect the URL to retrieve the feed ID, as shown below:

![](https://docs.tealium.com/images/server-side/eventstore-id-in-url-highlighted.png)

Example path to EventStore file:

```
my-account/main/events/bafc28ca-9542-3929-3b94-577a84f3d672
```