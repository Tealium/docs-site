---
title: Manage event specifications
description: This article explains how to manage event specifications.
url: https://docs.tealium.com/server-side/event-health/manage-event-specifications/
---
Event specifications define and validate your event data structure. For an overview of how event specifications fit into event health monitoring, see [About event health](https://docs.tealium.com/about-event-health/).

Add event specifications (also referred to as "event specs") directly from the event details view of **Live Events** or the **Event Specifications** page.

The system automatically adds the event's attributes to the **Add Event Specification** modal. If the event is unknown, define it as a custom specification from the event details view in the live events chart. 


<blockquote>
You can define unknown attributes later from the event details page in the live events chart. After you define them, add the attributes to the event specification.
</blockquote>


## Create an event specification

1. From the interface you are on:
    * **Event Specifications**: Click **+ New Event Specification**.
    * **Live Events**: Click an event, and then click **Create Event Specification**.
        * The event specification is pre-populated with the event's attributes.
        * A confirmation dialog lists all unknown attributes in the event. Click **Exclude unknown attributes** to exclude them from the new event specification.
1. Under **Rule**, enter the event name to use for the event specification.
1. (Optional) Enter any **Notes** about the event specification.
1. To add more attributes that define the event specification, click **+ Add Definitions**.
    * Under **Event Attributes**, select the attributes to add as definitions for the event specification. For more information about the attribute, click **View Details**.
    * Click **Add**.
1. All attributes default to **Required**. If an attribute is not required, set the corresponding toggle to `Off`.
1. Click **Create**.

Creating an event specification also creates a matching event feed.

## Edit an event specification

To edit an event specification:

1. In the **Defined Events** table, click an event to display the **Edit Details** page.
1. In the **Overview** tab of the event details page, make any necessary changes to **Notes**.
1. Click **Event Spec**.
1. To add more attributes that define the event specification, click **+ Add Definitions**.
    * Under **Event Attributes**, select the attributes to add as definitions for the event specification. To view attribute details or configure a validation rule, click **View Details**.
    * Click **Add**.
1. To delete an attribute from an event specification, click the corresponding **Delete** button.
1. Change the **Required** toggle for any attributes that need to be required or not required.
1. Click **Done**.

## Add a validation rule to an attribute

Validation rules check the value of an attribute against conditions you define. A required attribute that fails the rule produces an invalid event. An optional attribute that fails the rule produces a warn event.

To add a validation rule to an attribute in an event specification:

1. In the **Defined Events** table, click an event to display the **Edit Details** page.
1. Click the **Event Spec** tab.
1. In the **Definitions** table, click the attribute you want to add a rule to.  
   The **View Details** panel opens.
1. Click the **Validation Rule Details** tab.
1. Click **+ Add Rule**.  
   The **Create Rule** dialog opens.
1. Enter a **Title** for the rule.
1. Click **+ Attribute Condition** and configure the condition.  
   For example, to require that `video_platform` equals `YouTube`, select `video_platform`, set the operator to **equals**, and enter `YouTube`.
1. To add more conditions to the same rule, click **+ Attribute Condition**. To add an alternative set of conditions, click **+ OR**.
1. Click **Save**.

Tealium applies the rule during validation for every incoming event that matches this specification. To remove a rule, open **Validation Rule Details** and delete the rule.

## Delete an event specification

To delete an event specification, click the actions menu in the **Defined Events** table, click **Delete**, then confirm.
