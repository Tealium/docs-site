---
title: Emarsys Connector Setup Guide
description: This article describes how to set up the Emarsys connector.
url: https://docs.tealium.com/server-side-connectors/emarsys-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Authentication type**:
  * **OAuth**: Uses client credentials to authenticate with Emarsys v3 API. For more information, see [Emarsys: Authentication in v3 API](https://dev.emarsys.com/docs/emarsys-core-api-guides/b3c3a1eba8515-authentication-in-v3-api).
  * **WSSE**: Uses username and password to authenticate with Emarsys v2 API. For more information, see [Emarsys: v2 WSSE Authentication](https://dev.emarsys.com/docs/emarsys-core-api-guides/branches/main/b3c3a1eba8515-authentication).
* **Client ID**:  
Required for OAuth authentication type. The client ID for authenticating with the Emarsys v3 API.
* **Client Secret**:  
Required for OAuth authentication type. The client secret for authenticating with the Emarsys v3 API.
* **Username**:  
Required for WSSE authentication type. Username with permissions to access Emarsys APID. For more information about the Emarsys APID username, see [Emarsys: Set Up Your Account](https://dev.emarsys.com/docs/core-api-reference/branches/main/a12e08c686f0f-2-set-up-your-account).
* **Password**:  
Required for WSSE authentication type. Password for provided username.
* **Environment**:  
Environment to make API calls against.

## Actions

|**Action Name**| **AudienceStream**| **EventStream**|
| --- | --- | --- |
| Add Contact to Contact List (Real-Time) | ✓ | ✗ |
| Add Contact to Contact List (Batched) | ✓ | ✗ |
| Create or Update Email Contact (Real-Time) | ✓ | ✗ |
| Create or Update Email Contact (Batched) | ✓ | ✗ |
| Remove Contact From Contact List (Real-Time) | ✓ | ✗ |
| Remove Contact From Contact List (Batched) | ✓ | ✗ |
| Trigger Transactional Email (Real-Time) | ✓ | ✗ |
| Trigger Transactional Email (Batched) | ✓ | ✗ |
| Unsubscribe Contact From Email Campaign | ✓ | ✗ |
| Trigger an External Event (Real-Time) | ✓ | ✓ |
| Trigger an External Event (Batched) | ✓ | ✓ |
| Upsert record in an RDS table (Real-Time) | ✓ | ✗ |
| Upsert record in an RDS table (Batched) | ✓ | ✗ |
| Delete record in an RDS table (Real-Time) | ✓ | ✗ |
| Delete record in an RDS table (Batched) | ✓ | ✗ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

#### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 4 minutes and 45 seconds
* Max size of requests: 10 MB

### Add Contact to Contact List (Real-Time)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Contact List|  &lt;ul&gt;&lt;li&gt;(Required) The contact list to add the contact to.&lt;/li&gt;&lt;li&gt; If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt; |
|Contact Data|  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt;For more information, see [Emarsys: Core API Reference](https://dev.emarsys.com/docs/emarsys-api/365efd9f5e931-remove-contacts-from-a-contact-list).&lt;/li&gt;&lt;/ul&gt; |

### Add Contact to Contact List (Batched)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Contact List|  &lt;ul&gt;&lt;li&gt;(Required) The contact list to add the contact to.&lt;/li&gt;&lt;li&gt; If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt;|
|Contact Data|  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt;For more information, see [Emarsys: Core API Reference](https://dev.emarsys.com/docs/emarsys-api/365efd9f5e931-remove-contacts-from-a-contact-list).&lt;/li&gt;&lt;/ul&gt; |

### Create or Update Email Contact (Real-Time)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Create If Not Exists| When enabled, if the contact does not exist, it is created automatically.|
|Contact Identifier Data|  &lt;ul&gt;&lt;li&gt;(Required) This is the field used to identify a contact.&lt;/li&gt;&lt;li&gt;If you know the ID of the target contact field and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt; |
|Contact Data|  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt;At least one field is required to identify the contact.&lt;/li&gt;&lt;li&gt;The only date format supported by the contact fields is `YYYY-MM-DD`.&lt;/li&gt;&lt;li&gt;Some contact fields have limited acceptable values. For more information, see [Emarsys: Core API Reference](https://dev.emarsys.com/docs/emarsys-api/1a17c3d6fcebc-list-available-choices-of-a-single-choice-field).&lt;/li&gt;&lt;li&gt;If you know the ID of the target contact field and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt; |

#### Optional

|**Parameter**| **Description**|
|---| ---|
|Source ID|  &lt;ul&gt;&lt;li&gt;An ID assigned to a customer&#39;s external application, and is used to identify contacts created or modified by the external applications.&lt;/li&gt;&lt;/ul&gt; |

### Create or Update Email Contact (Batched)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Create If Not Exists| When enabled, if the contact does not exist, it is created automatically.|
|Contact Identifier Data|  &lt;ul&gt;&lt;li&gt;(Required) This is the field used to identify a contact.&lt;/li&gt;&lt;li&gt;If you know the ID of the target contact field and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt; |
|Contact Data|  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt;At least one field is required to identify the contact.&lt;/li&gt;&lt;li&gt;The only date format supported by the contact fields is `YYYY-MM-DD`.&lt;/li&gt;&lt;li&gt;Some contact fields have limited acceptable values. For more information, see [Emarsys: Core API Reference](https://dev.emarsys.com/docs/emarsys-api/1a17c3d6fcebc-list-available-choices-of-a-single-choice-field).&lt;/li&gt;&lt;li&gt;If you know the ID of the target contact field and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt; |

#### Optional

|**Parameter**| **Description**|
|---| ---|
|Source ID|  &lt;ul&gt;&lt;li&gt;An ID assigned to a customer&#39;s external application, and is used to identify contacts created or modified by the external applications.&lt;/li&gt;&lt;/ul&gt; |

### Remove Contact From Contact List (Real-Time)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Contact List| &lt;ul&gt;&lt;li&gt;(Required) The contact list to add the contact to.&lt;/li&gt;&lt;li&gt; If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt; |
|Contact Data|  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt;If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;li&gt;For more information, see [Emarsys: Core API Reference](https://dev.emarsys.com/docs/emarsys-api/365efd9f5e931-remove-contacts-from-a-contact-list).&lt;/li&gt;&lt;/ul&gt; |

### Remove Contact From Contact List (Batched)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Contact List| &lt;ul&gt;&lt;li&gt;(Required) The contact list to add the contact to.&lt;/li&gt;&lt;li&gt; If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt; |
|Contact Data|  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt; If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;li&gt;For more information, see [Emarsys: Core API Reference](https://dev.emarsys.com/docs/emarsys-api/365efd9f5e931-remove-contacts-from-a-contact-list).&lt;/li&gt;&lt;/ul&gt; |

### Trigger Transactional Email (Real-Time)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|External Event|  &lt;ul&gt;&lt;li&gt;(Required) Select the event set to trigger email.&lt;/li&gt;&lt;/ul&gt; |
|Contact Data|  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt; If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt; |

#### Optional

|**Parameter**| **Description**|
|---| ---|
|Content Personalization Data|  &lt;ul&gt;&lt;li&gt;(Optional) Placeholder in email and the value to replace it with.&lt;/li&gt;&lt;/ul&gt; |

### Trigger Transactional Email (Batched)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|External Event|  &lt;ul&gt;&lt;li&gt;(Required) Select the event set to trigger email.&lt;/li&gt;&lt;/ul&gt; |
|Contact Data|  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt; If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;/ul&gt; |

#### Optional

|**Parameter**| **Description**|
|---| ---|
|Content Personalization Data|  &lt;ul&gt;&lt;li&gt;(Optional) Placeholder in email and the value to replace it with.&lt;/li&gt;&lt;/ul&gt; |

### Unsubscribe Contact From Email Campaign

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Launch List ID| (Required) Provide the launch list ID from the unsubscribe link in email. |
|Email Campaign ID| (Required) Provide the email campaign ID from the unsubscribe link in email.|
|Contact ID| (Required) Map a randomly generated string to contact ID. Provided by unsubscribe link in email.|

### Trigger an External Event (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| External Event | Select the event to trigger. |
|Contact Data |  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt; If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;li&gt;For more information, see [Emarsys: Core API Reference](https://dev.emarsys.com/docs/emarsys-api/365efd9f5e931-remove-contacts-from-a-contact-list).&lt;/li&gt;&lt;/ul&gt; |

#### Optional

| **Parameter** | **Description** |
| --- | --- |
| External Event Data | The external data used for the trigger. 
| Template Variables | Provide template variables as data input for Templates. For more information, see . Name nested template variables with the dot notation (for example: `items.name`). Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in External Event Data. For more information, see . Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |

### Trigger an External Event (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| External Event | Select the event to trigger. |
|Contact Data |  &lt;ul&gt;&lt;li&gt;(Required) The field and corresponding field data to identify the contact.&lt;/li&gt;&lt;li&gt; If you know the ID of the target contact list and want to configure it manually, use a custom value.&lt;/li&gt;&lt;li&gt;For more information, see [Emarsys: Core API Reference](https://dev.emarsys.com/docs/emarsys-api/365efd9f5e931-remove-contacts-from-a-contact-list).&lt;/li&gt;&lt;/ul&gt; |

#### Optional

| **Parameter** | **Description** |
| --- | --- |
| External Event Data | The external data used for the trigger. 
| Template Variables | Provide template variables as data input for Templates. For more information, see . Name nested template variables with the dot notation (for example: `items.name`). Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in External Event Data. For more information, see . Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |

### Upsert record in an RDS table (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Connection Name | The name of the connection to the relational data service (RDS) . |
| Table Name | The name of the table in the RDS. |
| Table Records | The attributes to include in the new or updated record. Map each attribute to a column in the table. |

### Upsert record in an RDS table (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Connection Name | The name of the connection to the RDS. |
| Table Name | The name of the table in the RDS. |
| Table Records | The attributes to include in the new or updated record. Map each attribute to a column in the table. |

### Delete record in an RDS table (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Connection Name | The name of the connection to the RDS. |
| Table Name | The name of the table in the RDS. |
| Table Records | The attributes that identify the record to delete. Map each attribute to a column in the table. |

### Delete record in an RDS table (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Connection Name | The name of the connection to the RDS. |
| Table Name | The name of the table in the RDS. |
| Table Records | The attributes that identify the record to delete. Map each attribute to a column in the table.  |