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

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Organization URI**: (Required) Provide your Microsoft Dynamics root web address (example: &lt;https://your-domain.crm.dynamics.com&gt;).  
URL must be secure and if it does not specify https, then prefix &#34;https://&#34; will automatically be added.

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

Contacts, Leads, and Custom Entities from your Microsoft Dynamics account are dynamically populated as options in the **To** list. If you don&#39;t find the option you are looking for, you must add them in your account first.

### Action - Add or Update Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Data|  &lt;ul&gt;&lt;li&gt;(Required) Map Attributes to the data options you want to add or update for the contact.&lt;/li&gt;&lt;/ul&gt; |
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;(Required) Map Attributes to the lookup options you want to use for searching the target contact.&lt;/li&gt;&lt;li&gt;If the contact is found, its data will be updated. Otherwise a new contact will be created&lt;/li&gt;&lt;/ul&gt; |

For a full list of Contact fields, see [Contact EntityType](https://msdn.microsoft.com/en-us/library/mt593097.aspx).

### Action - Add Custom Entity to Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Custom Entity|  &lt;ul&gt;&lt;li&gt;(Required) Select custom entity&lt;/li&gt;&lt;/ul&gt; |
|Custom Entity to Contact Relationship|  &lt;ul&gt;&lt;li&gt;(Required) Select lookup field that associates custom entity with contact (see:[Entity Relationships](https://technet.microsoft.com/en-us/library/dn531171.aspx))&lt;/li&gt;&lt;/ul&gt; |

### Action - Add or Update Lead

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Lead Data|  &lt;ul&gt;&lt;li&gt;(Required) Map Attributes to the data options you want to add or update for the lead.&lt;/li&gt;&lt;/ul&gt; |
|Lead Lookup|  &lt;ul&gt;&lt;li&gt;(Required) Map Attributes to the lookup options you want to use for searching the target lead.&lt;/li&gt;&lt;li&gt;If the lead is found, its data will be updated. Otherwise a new lead will be created.&lt;/li&gt;&lt;/ul&gt; |

For full list of fields see: [Lead EntityType](https://msdn.microsoft.com/en-us/library/mt607693.aspx)

### Action - Update Custom Entity

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Custom Entity|  &lt;ul&gt;&lt;li&gt;(Required) Select custom entity&lt;/li&gt;&lt;/ul&gt; |

### Action - Create or Update Custom Entity

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Select applicable update strategy&lt;/li&gt;&lt;li&gt;Create Only: create new entity without lookup&lt;/li&gt;&lt;li&gt;Update Only: lookup existing entity and update it&lt;/li&gt;&lt;li&gt;Create or Update: lookup existing entity and if found update it, otherwise create new entity&lt;/li&gt;&lt;/ul&gt; |
|Custom Entity|  &lt;ul&gt;&lt;li&gt;(Required) Select custom entity&lt;/li&gt;&lt;/ul&gt; |

### Action - Add Contact to Marketing List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Marketing List|  &lt;ul&gt;&lt;li&gt;(Required) Select marketing list to add contact to.&lt;/li&gt;&lt;li&gt;Only static and non-locked lists targeting contacts are shown.&lt;/li&gt;&lt;/ul&gt; |

### Action - Remove Contact from Marketing List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Marketing List|  &lt;ul&gt;&lt;li&gt;(Required) Select marketing list to remove the contact from.&lt;/li&gt;&lt;li&gt;Only static and non-locked lists targeting contacts are shown.&lt;/li&gt;&lt;/ul&gt; |

## Vendor documentation

For additional information, see the following vendor documentation:

* [Lead EntityType](https://msdn.microsoft.com/en-us/library/mt607693.aspx)
* [Contact EntityType](https://msdn.microsoft.com/en-us/library/mt593097.aspx)
* [Create a New Entity](https://www.microsoft.com/en-us/dynamics/crm-customer-center/create-a-new-entity.aspx)
* [Create and Edit Entity Relationships](https://technet.microsoft.com/en-us/library/dn531171.aspx)
