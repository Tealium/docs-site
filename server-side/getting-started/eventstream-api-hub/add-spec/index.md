---
title: Event Specifications: Add a Spec
description: Add event specifications directly from the event details view in Live Events.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/add-spec/
---
Live Events detects unknown events, and you can create a custom specification directly from the event details view. When doing this, the event attributes from the event are automatically included in the **Add Event Specification** window.

## How it works

Any event specification, whether custom or from the marketplace, can be created from the event details view on the **Live Events** screen. In this example, you&#39;ll pick up where we left off with the `search` event.

Here&#39;s how it works:

1. With an event detail in view, click **Create Event Specification**  
    * The event specification is pre-populated with the event’s attributes.
    * A confirmation dialog is displayed that lists all unknown attributes in the event. Click **Exclude unknown attributes** to exclude these attributes from the new event specification.
1. Under **Rule**, enter the event name to use for the event specification. For example, `search`.
1. Click **Create**.

Now that you have an event specification created, you can observe data quality on the **Live Events** screen.

The next tutorial demonstrates how data validation works.

