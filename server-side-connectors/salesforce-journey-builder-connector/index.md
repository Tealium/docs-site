---
title: Salesforce Journey Builder Connector Setup Guide
description: Connect your Salesforce Marketing Cloud account and send event data to trigger or batch-trigger customer journeys.
url: https://docs.tealium.com/server-side-connectors/salesforce-journey-builder-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Client ID**
  * (Required) Provide your app client ID.
  * For more information, see [Salesforce: Get OAuth Client Credentials](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm).

* **Client Secret**
  * (Required) Provide your app client secret.

* **Account ID**
  * (Required) Provide the account identifier (MID) of the target business unit.

* **Tenant-specific subdomain**
  * (Required) Provide the tenant-specific subdomain for your application.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event to Initiate Journey | ✓ | ✗ |
| Send Event to Initiate Journey (Batched) | ✓ | ✗ |

### Send Event to Initiate Journey

#### Parameters

| Parameter | Description |
| --- | --- |
| Event Entry Definition | (Required) Select an event entry definition or enter it manually. The drop-down list displays entries from newest to oldest and shows a maximum of 2000 entries. For more information, see [Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html). |
| Contact Key | (Required) Provide the contact key. |
| Event Data | Required if defined in a custom event or specified by the event. Map values to contact event attributes. For more information, see [Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html). |

### Send Event to Initiate Journey (Batched)

This action enters a batch of subscribers into a journey asynchronously. Use this action for bulk imports or high-frequency event data.

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. If ordering is important, add a sequence value to events. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 5 minutes
* Max size of requests: 10 MB

The parameters for this action are identical to [Send Event to Initiate Journey](#send-event-to-initiate-journey).

## Vendor documentation

* [Salesforce: Get OAuth Client Credentials](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)
* [Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)
* [Salesforce: Entry Events and Data Definitions](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/event-definition-key.html#:~:text=Event%20definitions%20define%20the%20name,the%20journey%20to%20be%20published.)
* [Salesforce: POST /interaction/v1/async/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/enterContactsIntoJourneyInBatches.html)
