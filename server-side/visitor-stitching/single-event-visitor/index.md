---
title: Single event visitor
description: This article explains how Tealium handles single event visitors.
url: https://docs.tealium.com/server-side/visitor-stitching/single-event-visitor/
---
## How it works

A single event visitor occurs when Tealium receives one real-time event from a new visitor to your website or mobile app, with no additional activity during the visit.

A visitor is considered a single event visitor if all the following are true:

* **Only one event received**  
  Exactly one event is received during the visit.
* **No visitor stitching**  
  The event does not trigger visitor stitching.
* **No badges assigned**  
  No badges are assigned during the visit.
* **Not from file import**  
  The event is not generated from a file import.

## AudienceStream

Single event visitors are persisted in AudienceStream, passed to AudienceStore, and stored in AudienceDB.

If the visitor returns in a new session, they are recognized as a returning visitor.


<blockquote>
Prior to April 29, 2026, AudienceStream did not persist single event visitor records.
</blockquote>


## EventStore and EventDB

Events from single event visitors are stored in EventStore and EventDB, with corresponding records in AudienceStore and AudienceDB.

## Visit length

The default session length is 30 minutes. However, a single event visit ends after 10 minutes if no additional events occur.

This applies even for a visitor’s first visit.

For more information, see .
