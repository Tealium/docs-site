---
title: Manage event specifications
description: This article explains how to manage event specifications.
url: https://docs.tealium.com/server-side/event-health/manage-event-specifications/
---
Event specifications define and validate your event data structure. For an overview of how event specifications fit into event health monitoring, see [About event health](https://docs.tealium.com/about-event-health/).

Event specifications (also referred to as "event specs") can be added directly from the event details view of **Live Events** or the **Event Specifications** page.

The system automatically adds the event's attributes to the **Add Event Specification** modal. If the event is unknown, define it as a custom specification from the event details view in the live events chart. 


<blockquote>
You can define unknown attributes later from the event details page in the live events chart. After you define them, add the attributes to the event specification.
</blockquote>


## Create an event specification

1. From the interface you are on:
    * **Event Specifications**: Click **+ New Event Specification**.
    * **Live Events**: Click an event, and then click **Create Event Specification**.
        * The event specification is pre-populated with the event's attributes.
        * A confirmation dialog is displayed that lists all unknown attributes in the event. Click **Exclude unknown attributes** to exclude these attributes from the new event specification.
1. Under **Rule**, enter the event name to use for the event specification.
1. (Optional) Enter any **Notes** about the event specification.
1. To add more attributes that define the event specification, click **+ Add Definitions**.
    * Under **Event Attributes**, select the attributes to add as definitions for the event specification. For more information about the attribute, click **View Details**.
    * Click **Add**.
1. All attributes are automatically set to **Required**. If the attribute is not required, set the corresponding toggle to `Off`.
1. Click **Create**.

When you create an event specification, a matching event feed is also created. 

## Edit an event specification

To edit an event specification:

1. In the **Defined Events** table, click an event to display the **Edit Details** page.
1. In the **Overview** tab of the event details page, make any necessary changes to **Notes**.
1. Click **Event Spec**.
1. To add more attributes that define the event specification, click **+ Add Definitions**.
    * Under **Event Attributes**, select the attributes to add as definitions for the event specification. For more information about the attribute, click **View Details**.
    * Click **Add**.
1. To delete an attribute from an event specification, click the corresponding **Delete** button.
1. Change the **Required** toggle for any attributes that need to be required or not required.
1. Click **Done**.

## Delete an event specification

To delete an event specification, click the more actions button in the **Defined Events** table and **Delete**, then confirm that you want to delete it. 