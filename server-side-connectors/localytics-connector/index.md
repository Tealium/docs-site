---
title: Localytics Connector Setup Guide for AudienceStream
description: This article describes how to set up the Localytics connector.
url: https://docs.tealium.com/server-side-connectors/localytics-connector/
---
## Requirements

* Localytics Account
* API Key
* API Secret

You can find your org’s API Key/Secret by navigating to the **API Keys** section of the **Account** page in your [Localytics dashboard](https://dashboard.localytics.com/settings/apikeys) (requires login).

## Supported Actions

| **Action Name** | **Trigger on Audience** | **Trigger on Streams** |
|:----------------|:------------------------|:-----------------------|
| Send Event      | ✓                       | ✓                      |

## Configure Settings

Go to the Connector Marketplace and add a new Localytics Connector. Read the [Connector Overview]Localytics article for general instructions on how to add a connector.

To configure your vendor, follow these steps:

1. In the **Configure** tab, provide a title for the Connector instance.
1. Enter the API key and secret that you received from Localytics for your account.
1. Provide additional notes about your implementation.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. It&#39;s where you&#39;ll set up actions and trigger them.

This section describes how to set up parameters and options for each action.

### Action - Send Event

#### Parameters

**Event Attributes**: (Required) Map your Attribute(s) to the required track event fields. Select the field of choice from the **To** dropdown or enter a custom value.

#### Options - Event Attributes

| **Option**             | **Description**                                                                                                                                                        | **Example**                                                    |
|:-----------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------|
| Event Name  | (Required) Name of the action that a user has performed                                                                                                                           | `Purchase_Completed`                                           |
| Customer Id  | (Required) Localytics Customer ID that identifies the end user who completed the event.                                                                                           | `joanna@example.com`                                           |
| App Key  | (Required) Your Localytics App ID                                                                                                                                                 | `91e6f7bf1c6004b029c3082-602f5774-ae2b-11e2-0c2c-004a77f8b47f` |
| Event Time             | The time that the event occurred. Event timestamps must be more recent than 72 hours in the past and must not exceed 2 days in the future.                             | `1412090428444`                                                |
| LTV Change             | Incremental change in user’s lifetime value associated with this event.                                                                                                | `2.99`                                                         |
| UUID                   | Randomly generated UUID to uniquely identify the event request. This is required to mitigate networking problems and ensure that each event is processed exactly once. | `fabfec96-7aff-40cc-a37d-972c4b4265de`                         |

## Vendor Documentation

* [Events API](https://docs.localytics.com/dev/events-api.html#events-api-intro)
