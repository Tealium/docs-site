---
title: Microsoft Dynamics 365 Connector Setup Guide
description: Microsoft Dynamics 365 is a multifaceted CRM solutions platform to streamline processes and increase profitability in sales, marketing and service divisions.
url: https://docs.tealium.com/server-side-connectors/microsoft-dynamics-365-connector/
---## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add or Update Contact| ✓| ✗|
|Add Custom Entity to Contact| ✓| ✗|
|Add or Update Lead| ✓| ✗|
|Qualify Lead to Contact| ✓| ✗|
|Update Custom Entity| ✓| ✗|
|Create or Update Custom Entity| ✓| ✗|
|Add Contact to Marketing List| ✓| ✗|
|Remove Contact from Marketing List| ✓| ✗|

## Requirements

* Microsoft Dynamics 365 account
* Organization URI (root web address you received from Microsoft)

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Organization URI**: (Required) Provide your Microsoft Dynamics root web address (example: <https://your-domain.crm.dynamics.com>).  

<blockquote>
URL must be secure and if it does not specify https, then prefix "https://" will automatically be added.
</blockquote>


## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.


<blockquote>
Contacts, Leads, and Custom Entities from your Microsoft Dynamics account are dynamically populated as options in the **To** list. If you don't find the option you are looking for, you must add them in your account first.
</blockquote>


### Action - Add or Update Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Data|  <ul><li>(Required) Map Attributes to the data options you want to add or update for the contact.</li></ul> |
|Contact Lookup|  <ul><li>(Required) Map Attributes to the lookup options you want to use for searching the target contact.</li><li>If the contact is found, its data will be updated. Otherwise a new contact will be created</li></ul> |


<blockquote>
For a full list of Contact fields, see [Contact EntityType](https://msdn.microsoft.com/en-us/library/mt593097.aspx).
</blockquote>


### Action - Add Custom Entity to Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Custom Entity|  <ul><li>(Required) Select custom entity</li></ul> |
|Custom Entity to Contact Relationship|  <ul><li>(Required) Select lookup field that associates custom entity with contact (see:[Entity Relationships](https://technet.microsoft.com/en-us/library/dn531171.aspx))</li></ul> |

### Action - Add or Update Lead

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Lead Data|  <ul><li>(Required) Map Attributes to the data options you want to add or update for the lead.</li></ul> |
|Lead Lookup|  <ul><li>(Required) Map Attributes to the lookup options you want to use for searching the target lead.</li><li>If the lead is found, its data will be updated. Otherwise a new lead will be created.</li></ul> |


<blockquote>
For full list of fields see: [Lead EntityType](https://msdn.microsoft.com/en-us/library/mt607693.aspx)
</blockquote>


### Action - Update Custom Entity

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Custom Entity|  <ul><li>(Required) Select custom entity</li></ul> |

### Action - Create or Update Custom Entity

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  <ul><li>(Required) Select applicable update strategy</li><li>Create Only: create new entity without lookup</li><li>Update Only: lookup existing entity and update it</li><li>Create or Update: lookup existing entity and if found update it, otherwise create new entity</li></ul> |
|Custom Entity|  <ul><li>(Required) Select custom entity</li></ul> |

### Action - Add Contact to Marketing List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Marketing List|  <ul><li>(Required) Select marketing list to add contact to.</li><li>Only static and non-locked lists targeting contacts are shown.</li></ul> |

### Action - Remove Contact from Marketing List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Marketing List|  <ul><li>(Required) Select marketing list to remove the contact from.</li><li>Only static and non-locked lists targeting contacts are shown.</li></ul> |

## Vendor documentation

For additional information, see the following vendor documentation:

* [Lead EntityType](https://msdn.microsoft.com/en-us/library/mt607693.aspx)
* [Contact EntityType](https://msdn.microsoft.com/en-us/library/mt593097.aspx)
* [Create a New Entity](https://www.microsoft.com/en-us/dynamics/crm-customer-center/create-a-new-entity.aspx)
* [Create and Edit Entity Relationships](https://technet.microsoft.com/en-us/library/dn531171.aspx)
