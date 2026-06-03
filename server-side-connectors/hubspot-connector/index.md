---
title: Hubspot Connector Setup Guide
description: This article describes how to set up the Hubspot connector.
url: https://docs.tealium.com/server-side-connectors/hubspot-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

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
|Contact Properties| &lt;ul&gt;&lt;li&gt;(Required) The contact email address.&lt;/li&gt;&lt;li&gt;Select a HubSpot field to map to from the list.&lt;/li&gt;&lt;/ul&gt;|

### Create Contact (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 10
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

|**Parameter**| **Description**|
|---| ---|
|Contact Properties| &lt;ul&gt;&lt;li&gt;(Required) The contact email address.&lt;/li&gt;&lt;li&gt;Select a HubSpot field to map to from the list.&lt;/li&gt;&lt;/ul&gt;|

### Update Contact (Real-Time)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Identifiers|  &lt;ul&gt;&lt;li&gt;(Required) The email address or contact ID of the contact.&lt;/li&gt;&lt;li&gt;Select a HubSpot field to map to from the list.&lt;/li&gt;&lt;/ul&gt; |
|Contact Properties| &lt;ul&gt;&lt;li&gt;(Required) The email address to set the contact to.&lt;/li&gt;&lt;li&gt;Select a HubSpot field to map to from the list.&lt;/li&gt;&lt;/ul&gt;|

### Update Contact (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 10
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Identifiers|  &lt;ul&gt;&lt;li&gt;(Required) The email address or contact ID of the contact.&lt;/li&gt;&lt;li&gt;Select a HubSpot field to map to from the list.&lt;/li&gt;&lt;/ul&gt; |
|Contact Properties| &lt;ul&gt;&lt;li&gt;(Required) The email address to set the contact to.&lt;/li&gt;&lt;li&gt;Select a HubSpot field to map to from the list.&lt;/li&gt;&lt;/ul&gt;|

### Add Contact to List

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Contact List|  &lt;ul&gt;&lt;li&gt;(Required) Select the contact list to add the contact to.&lt;/li&gt;&lt;/ul&gt; |
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;(Required) The email address of the contact.&lt;/li&gt;&lt;li&gt;Select a HubSpot field to map to from the list.&lt;/li&gt;&lt;/ul&gt; |

### Remove Contact from List

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Contact List|  &lt;ul&gt;&lt;li&gt;(Required) Select the contact list to remove the contact from.&lt;/li&gt;&lt;/ul&gt; |
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;(Required) The email address of the contact.&lt;/li&gt;&lt;li&gt;Select a HubSpot field to map to from the list.&lt;/li&gt;&lt;/ul&gt; |