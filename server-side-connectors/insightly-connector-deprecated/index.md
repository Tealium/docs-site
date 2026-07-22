---
title: Insightly Connector Setup Guide (Deprecated)
description: This article describes how to set up the Insightly connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/insightly-connector-deprecated/
---

<blockquote>
This connector is now deprecated and no longer available in the tag marketplace. For information about the Insightly CRM connector, see the [Insightly CRM Connector Setup Guide](https://docs.tealium.com/insightly-crm-connector/).
</blockquote>


## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add a Contact| ✓| ✗|
|Update a Contact| ✓| ✗|
|Add a Lead| ✓| ✗|
|Update a Lead| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**
  * For information on where to find your Insightly API Key, see: [Finding or Resetting your API Key](https://support.insight.ly/hc/en-us/articles/204864594-Finding-your-Insightly-API-key)

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Add a Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|First Name|  <ul><li>First name of the contact.</li><li>Either first name or last name is required.</li></ul> |
|Last Name|  <ul><li>Last name of the contact.</li><li>Either first name or last name is required.</li></ul> |
|Attributes|  <ul><li>Additional attributes for the contact.</li><li>These parameters must exist within Insightly.</li><li>For a list of available attributes, see: [Insightly's documentation](https://api.insight.ly/v2.3/Help#!/Contacts/AddContact).</li></ul> |
|Tags|  <ul><li>Tags to assign to the contact.</li></ul> |

### Action - Update a Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact ID|  <ul><li>The ID of the contact to be updated.</li></ul> |
|First Name|  <ul><li>The first name of the contact.</li><li>Either first name or last name is required.</li></ul> |
|Last Name|  <ul><li>The last name of the contact.</li><li>Either first name or last name is required.</li></ul> |
|Attributes|  <ul><li>Additional attributes to be updated.</li><li>For a list of available attributes, see: [Insightly's documentation](https://api.insight.ly/v2.3/Help#!/Contacts/UpdateContact).</li></ul> |
|Tags|  <ul><li>Tags to be updated.</li></ul> |

### Action - Add a Lead

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Last Name|  <ul><li>Last name of the lead.</li></ul> |
|First Name|  <ul><li>First name of the lead.</li></ul> |
|Attributes|  <ul><li>Additional attributes for the lead.</li><li>For a list of available attributes, see: [Insightly's documentation](https://api.insight.ly/v2.3/Help#!/Leads/AddLead).</li></ul> |
|Tags|  <ul><li>Tags to assign to the lead.</li></ul> |

### Action - Update a Lead

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Lead ID|  <ul><li>The ID of the lead to be updated.</li></ul> |
|Last Name|  <ul><li>Last name of the lead.</li></ul> |
|First Name|  <ul><li>First name of the lead.</li></ul> |
|Attributes|  <ul><li>Additional attributes to be updated.</li><li>For a list of available attributes, see: [Insightly's documentation](https://api.insight.ly/v2.3/Help#!/Leads/UpdateLead).</li></ul> |
|Tags|  <ul><li>Tags to be updated.</li></ul> |
