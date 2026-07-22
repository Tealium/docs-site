---
title: Braze Currents data source setup guide
description: This article describes how to use Braze as a data source to send actionable events to Tealium EventStream API Hub and Tealium AudienceStream CDP using Braze Currents.
url: https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/braze-currents/
---
For additional information about Partner Integrations and Tealium Server-Side data sources, see [Data Sources](https://docs.tealium.com/partners/data-sources/#api).

## Prerequisites

* Tealium EventStream and/or Tealium AudienceStream
* Braze account with Currents enabled


<blockquote>
A Currents connector is already included in many Braze pro- and enterprise-level packages. If you do not already have access to Currents, contact your Braze account manager.
</blockquote>


## How it works

The Braze platform tracks a variety of event data from your Braze integration for analysis, retargeting, and other use-cases within your systems. To connect Braze with Tealium EventStream or Tealium AudienceStream, use [Braze Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/) to send Braze data source to your Tealium account.

After you configure Braze Currents, you can create subscriptions based on topics and receive related push notifications to automate use cases, stay informed, and increase productivity.

### Braze Currents data source

Adding the Braze data source to your Tealium Customer Data Hub profile generates a unique URL to use in your Currents configuration in following format:

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

To add the Braze data source to your Tealium Customer Data Hub profile, see [Data Sources](https://docs.tealium.com/about-data-sources/). After adding and connecting the data source, save and publish your profile.

### Braze Currents setup

After you connect Braze to your Tealium Customer Data Hub profile, configure Braze Currents using the following steps:

1. Log in to your Braze account and navigate to the **Currents** page in the **Integrations** section of your Braze Dashboard.
1. From the **Create Current** menu, select **Tealium** as the **Currents connector** or **Partner**.
1. Enter the custom endpoint URL created by adding the Braze data source to your Tealium profile. For example,   
      ```
      https://collect-us-east-1.tealiumiq.com/integration/event/{account}/{profile}/{data_source_key}
      ```

1. Select [Message Engagement Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/message_engagement_events/), [Customer Behavior](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/), and [User Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/) to be sent to Tealium.
1. Enable and save the current.

### Events and attributes

Braze event parameters are pre-defined based on the Engagement behavior or the Customer behavior events you select in your Currents configuration. Events are grouped and sent to the custom endpoint as a JSON array containing all events. For example, `{"events": [event1, event2, event3, etc...]}`, where each element in the array is a JSON object representing a single event.

For example, Braze generates the following JSON event object when a Braze Canvas email makes it successfully to the end-users inbox:

```json
users.messages.email.Delivery
{
    "event_type": "users.messages.email.Delivery",
    "id": "663628f0-3f46-484e-8b6c-51d0a67764e0",
    "time": 1646162118,
    "timezone": "America/Chicago",
    "user": {
        "external_user_id": "62181fc031c9ba304eecb255"
    },
    "properties": {
        "canvas_id": "c176e77e-33ba-44d6-809c-c89483d1e3d7",
        "canvas_name": "My Cool Canvas",
        "canvas_step_name": "Initial Email",
        "canvas_variation_id": "31234567-89ab-cdef-0123-456789abcdef",
        "canvas_variation_name": "Variant 1",
        "canvas_step_id": "d8e31e8e-0584-43dd-8e4e-b657707df800",
        "dispatch_id": "621e70c403115018b55ee12cc214a515",
        "email_address": "test1@tealium.com",
        "sending_ip": "167.89.14.251",
        "subscription_group_id": "41234567-89ab-cdef-0123-456789abcdef"
    }
}
```

All incoming Braze event attributes are automatically prefixed with `braze_`. For example, when Currents sends `id`, the matching EventStream event attribute is `braze_id` (all lowercase). The Tealium Braze data source flattens the events as custom JSON objects as shown in the following example:

```json
{
    "tealium_event": "users.messages.email.Delivery",
    "braze_event_type": "users.messages.email.Delivery",
    "braze_id": "663628f0-3f46-484e-8b6c-51d0a67764e0",
    "braze_time": 1646162118,
    "braze_timezone": "America/Chicago",
    "braze_user_external_user_id": "62181fc031c9ba304eecb255",
    "braze_properties_canvas_id": "c176e77e-33ba-44d6-809c-c89483d1e3d7",
    "braze_properties_canvas_name": "My Cool Canvas",
    "braze_properties_canvas_step_name": "Initial Email",
    "braze_properties_canvas_variation_id": "31234567-89ab-cdef-0123-456789abcdef",
    "braze_properties_canvas_variation_name": "Variant 1",
    "braze_properties_canvas_step_id": "d8e31e8e-0584-43dd-8e4e-b657707df800",
    "braze_properties_dispatch_id": "621e70c403115018b55ee12cc214a515",
    "braze_properties_email_address": "test1@tealium.com",
    "braze_properties_sending_ip": "167.89.14.251",
    "braze_properties_subscription_group_id": "41234567-89ab-cdef-0123-456789abcdef"
}
```

Note that the `tealium_event` attribute inherits the value of the `event_type` parameter from Currents.

The following image is an example of an inbound event into the Tealium Live Events tool and contains parameters passed by the email delivery event:

![](https://docs.tealium.com/images/server-side/braze-currents-event-tealium-live-events-email-delivery.png)

For a full list of supported events, see the Currents Event Glossary in the [Braze Currents documentation](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/).

## **Vendor documentation**

* [Setting up Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/)
* [Braze Currents](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/)
* [Customer Behavior Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/customer_behavior_events/)
* [Message Engagement Events](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/event_glossary/message_engagement_events/)
