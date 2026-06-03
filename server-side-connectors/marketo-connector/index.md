---
title: Marketo Connector Setup Guide
description: This article describes how to set up the Marketo connector.
url: https://docs.tealium.com/server-side-connectors/marketo-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **REST API Client ID**: (Required) Provide the client ID found in **Marketo &gt; Admin &gt; LaunchPoint**. The API user must have permissions for **Read-Write Lead**, **Read/Execute Campaigns**, and **Read Lists**. For more information, see [Marketo: Create a Custom Service for Use with ReST API](http://docs.marketo.com/display/public/DOCS/Create&#43;a&#43;Custom&#43;Service&#43;for&#43;Use&#43;with&#43;ReST&#43;API).
* **REST API Client Secret**: (Required) Provide the client secret found in **Marketo &gt; Admin &gt; LaunchPoint**.
* **REST API Endpoint URL**: (Required) REST API Endpoint found in **Marketo &gt; Admin &gt; Web Service**. For example, `https://123-ABC-123.mktorest.com/rest`.
* **REST API Identity URL**: (Required) REST API Identity found in **Marketo &gt; Admin &gt; Web Service**. For example, `https://123-ABC-123.mktorest.com/identity`.

## Actions

|**Action Name**| **AudienceStream**| **EventStream**|
| --- | --- | --- |
| Add Lead to a List | ✓ | ✓ |
| Add Lead to a List (Batched) | ✓ | ✓ |
| Remove Lead from a List | ✓ | ✓ |
| Remove Lead from a List (Batched) | ✓ | ✓ |
| Send Transactional Email | ✓ | ✓ |
| Create or Update a Lead | ✓ | ✓ |
| Create or Update a Lead (Batched) | ✓ | ✓ |
| Merge a Lead | ✓ | ✓ |
| Bulk Import Leads (optionally add to list) | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Add Lead to a List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| Target Static List | (Required) Select a list. The platform loads a maximum of 300 lists. If the list does not appear, enter the list ID.  |
| Target Lead ID |  Use if the **Lead ID** for the user is known. Leave **Lead ID Lookup** blank. |
| Lead ID Lookup | Use if the **Lead ID** for the user is unknown. Leave **Target Lead ID** blank and use this field to search for the Lead ID with a variety of filters. Possible values: `id`, `cookies`, `email`, `twitterId`, `facebookId`, `linkedInId`, `sfdcAccountId`, `sfdcContactId`, `sfdcLeadId`, `sfdcLeadOwnerId`, `sfdcOpptyId`. |
| Add lead | Add the lead if it does not exist. |

### Add Lead to a List (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 300
* Max time since oldest request: 30 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Target Static List | (Required) Select a list. The platform loads a maximum of 300 lists. If the list does not appear, enter the list ID.  |
| Target Lead ID |  Use if the **Lead ID** for the user is known. Leave **Lead ID Lookup** blank. |
| Lead ID Lookup | Use if the **Lead ID** for the user is unknown. Leave **Target Lead ID** blank and use this field to search for the Lead ID with a variety of filters. Possible values: `id`, `cookies`, `email`, `twitterId`, `facebookId`, `linkedInId`, `sfdcAccountId`, `sfdcContactId`, `sfdcLeadId`, `sfdcLeadOwnerId`, `sfdcOpptyId`. |
| Add lead | Add lead if it does not exist. |

### Remove Lead from a List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| Target Static List | (Required) Select a list. The platform loads a maximum of 300 lists. If the list does not appear, enter the list ID.  |
| Target Lead ID |  Use if the **Lead ID** for the user is known. Leave **Lead ID Lookup** blank. |
| Lead ID Lookup | Use if the **Lead ID** for the user is unknown. Leave **Target Lead ID** blank and use this field to search for the Lead ID with a variety of filters. Possible values: `id`, `cookies`, `email`, `twitterId`, `facebookId`, `linkedInId`, `sfdcAccountId`, `sfdcContactId`, `sfdcLeadId`, `sfdcLeadOwnerId`, `sfdcOpptyId`. |
| Add lead | Add lead if it does not exist. |

### Remove Lead from a List (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 300
* Max time since oldest request: 30 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| Target Static List | (Required) Select a list. The platform loads a maximum of 300 lists. If the list does not appear, enter the list ID.  |
| Target Lead ID |  Use if the **Lead ID** for the user is known. Leave **Lead ID Lookup** blank. |
| Lead ID Lookup | Use if the **Lead ID** for the user is unknown. Leave **Target Lead ID** blank and use this field to search for the lead ID with a variety of filters. Possible values: `id`, `cookies`, `email`, `twitterId`, `facebookId`, `linkedInId`, `sfdcAccountId`, `sfdcContactId`, `sfdcLeadId`, `sfdcLeadOwnerId`, `sfdcOpptyId`. |
| Add lead | Add lead if it does not exist. |

### Send Transactional Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| Target Email Campaign | Select the target smart campaign created for transactional email. For more information, see [Marketo: Transactional Email](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/assets/transactional-email). |
| Target Lead ID | (Required) Provide a target lead ID. |
| Token Data to Set | (Optional) Map token value to token name. Use the full token format from the Marketo UI. For example, `{ { my.message } }`. |

### Create or Update a Lead

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| Update Strategy | (Required) Select the update strategy. |
| Lead Lookup Filter | &lt;ul&gt;&lt;li&gt;(Optional) Select the filter field to look up an existing lead.&lt;/li&gt;&lt;li&gt;The selected lookup filter field must have a value set in the **Lead Data** section.&lt;/li&gt;&lt;/ul&gt; |
| Lead Data to Set | (Required) Map values to lead property names. Date attributes are automatically formatted to ISO 8601 format. |

### Create or Update a Lead (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 300
* Max time since oldest request: 30 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| Update Strategy | (Required) Select the update strategy. |
| Lead Lookup Filter | &lt;ul&gt;&lt;li&gt;(Optional) Select the filter field to look up an existing lead.&lt;/li&gt;&lt;li&gt;The selected lookup filter field must have a value set in the **Lead Data** section.&lt;/li&gt;&lt;/ul&gt; |
| Lead Data to Set | (Required) Map values to lead property names. Date attributes are automatically formatted to ISO 8601 format. |

### Merge a Lead

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| General Data to Set | (Required) &lt;ul&gt;&lt;li&gt;**Winning Lead ID**: The winning lead.&lt;/li&gt;&lt;li&gt;**Losing Lead ID**: Lead to merge (losing lead).&lt;/li&gt;&lt;/ul&gt; |
| Merge in CRM | Specify if the merge should also occur in CRM. |

### Bulk Import Leads (optionally add to list)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 25,000
* Max time since oldest request: 30 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Target Static List | (Required) Select a list. The platform loads a maximum of 300 lists. If the list does not appear, enter the list ID.  |
| Lead Lookup Field | (Required) Field used for lead lookup.&lt;ul&gt;&lt;li&gt;The selected lookup field must have a value set in **Lead Data** section.&lt;/li&gt;&lt;li&gt;Possible values: `id`, `cookies`, `email`, `twitterId`, `facebookId`, `linkedInId`, `sfdcAccountId`, `sfdcContactId`, `sfdcLeadId`, `sfdcLeadOwnerId`, `sfdcOpptyId`.&lt;/li&gt;&lt;/ul&gt; |
| Lead Data | (Required) Map values to lead property names. The lookup field must also be mapped. |
