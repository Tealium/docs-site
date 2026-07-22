---
title: Hubspot Connector Setup Guide
description: This article describes how to set up the Hubspot connector.
url: https://docs.tealium.com/server-side-connectors/hubspot-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Private App Access Token**: (Required) Provide your Private App Access Token. This value must be entered correctly in for the action parameter fields to populate HubSpot data, or an error appears. For more information, see [HubSpot: Private Apps](https://developers.hubspot.com/docs/api/private-apps).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Create Contact (Real-Time) | ✓ | ✗ |
| Create Contact (Batched) | ✓ | ✗ |
| Update Contact (Real-Time) | ✓ | ✗ |
| Update Contact (Batched) | ✓ | ✗ |
| Add Contact to List | ✓ | ✗ |
| Remove Contact from List | ✓ | ✗ |

Enter a name for the action and select the **Action Type**.

The following section describes how to set up parameters and options for each action.
 

### Create Contact (Real-Time)

|**Parameter**| **Description**|
|---| ---|
|Contact Properties| <ul><li>(Required) The contact email address.</li><li>Select a HubSpot field to map to from the list.</li></ul>|

### Create Contact (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 10
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

|**Parameter**| **Description**|
|---| ---|
|Contact Properties| <ul><li>(Required) The contact email address.</li><li>Select a HubSpot field to map to from the list.</li></ul>|

### Update Contact (Real-Time)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Identifiers|  <ul><li>(Required) The email address or contact ID of the contact.</li><li>Select a HubSpot field to map to from the list.</li></ul> |
|Contact Properties| <ul><li>(Required) The email address to set the contact to.</li><li>Select a HubSpot field to map to from the list.</li></ul>|

### Update Contact (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 10
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Identifiers|  <ul><li>(Required) The email address or contact ID of the contact.</li><li>Select a HubSpot field to map to from the list.</li></ul> |
|Contact Properties| <ul><li>(Required) The email address to set the contact to.</li><li>Select a HubSpot field to map to from the list.</li></ul>|

### Add Contact to List

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Contact List|  <ul><li>(Required) Select the contact list to add the contact to.</li></ul> |
|Contact Lookup|  <ul><li>(Required) The email address of the contact.</li><li>Select a HubSpot field to map to from the list.</li></ul> |

### Remove Contact from List

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Contact List|  <ul><li>(Required) Select the contact list to remove the contact from.</li></ul> |
|Contact Lookup|  <ul><li>(Required) The email address of the contact.</li><li>Select a HubSpot field to map to from the list.</li></ul> |