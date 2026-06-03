---
title: Listrak Connector Setup Guide
description: This article describes how to set up the Listrak connector.
url: https://docs.tealium.com/server-side-connectors/listrak-connector/
---
## Requirements

* Listrak Client ID
* Listrak Client Secret

## Supported Actions

|**Action Name**| **Trigger on Audience**| **Trigger on Streams**|
|---| ---| ---|
|Create or Update Contact| ✓| ✗|
|Subscribe Contact| ✓| ✗|
|Unsubscribe Contact| ✓| ✗|
|Send Transactional Message| ✓| ✗|

## Configure Settings&lt;br&gt;

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Client ID**
  * Your Client ID associated with an integration in your Listrak account.
  * You can find your Client ID under the Integration Manager in your Listrak dashboard.
  * To make full use of the connector, ensure that you have the following access levels set: `ListContactSegmentationMessageEvent`
  * For implementation details, see [Listrak Authentication](https://api.listrak.com/email#section/Authentication)

* **Client Secret**
  * Your Client Secret associated with an integration in your Listrak account.
  * You can find your Client Secret under the **Integration Manager** in your Listrak dashboard.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Create or Update Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact List|  &lt;ul&gt;&lt;li&gt;(Required) The list the contact belongs to, if updating, or the list to add the contact to, if creating.&lt;/li&gt;&lt;/ul&gt; |
|Contact Email|  &lt;ul&gt;&lt;li&gt;(Required) The email address of the contact.&lt;/li&gt;&lt;/ul&gt; |
|Double Opt-In|  &lt;ul&gt;&lt;li&gt;Whether a double opt-in email should be sent if a new contact is being created.&lt;/li&gt;&lt;/ul&gt; |
|Events|  &lt;ul&gt;&lt;li&gt;Events that should be raised after the contact is created or updated.&lt;/li&gt;&lt;/ul&gt; |
|New Email|  &lt;ul&gt;&lt;li&gt;If updating an existing contact, the contact&#39;s email address will be changed to this value.&lt;/li&gt;&lt;/ul&gt; |
|Update Type|  &lt;ul&gt;&lt;li&gt;If updating an existing contact, the type of update that will be performed on any submitted segmentation fields.&lt;/li&gt;&lt;li&gt;If not set, the default value is `Update`.&lt;/li&gt;&lt;/ul&gt; |
|Segmentation Group|  &lt;ul&gt;&lt;li&gt;The Segmentation Group that contains a list of segmentation fields.&lt;/li&gt;&lt;/ul&gt; |

### Action - Subscribe Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact List|  &lt;ul&gt;&lt;li&gt;(Required) The list the contact belongs to.&lt;/li&gt;&lt;/ul&gt; |
|Contact Email|  &lt;ul&gt;&lt;li&gt;(Required) The email address of the contact.&lt;/li&gt;&lt;/ul&gt; |
|Events|  &lt;ul&gt;&lt;li&gt;Events that should be raised after the contact is subscribed.&lt;/li&gt;&lt;/ul&gt; |

### Action - Unsubscribe Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact List|  &lt;ul&gt;&lt;li&gt;(Required) The list the contact belongs to.&lt;/li&gt;&lt;/ul&gt; |
|Contact Email|  &lt;ul&gt;&lt;li&gt;(Required) The email address of the contact.&lt;/li&gt;&lt;/ul&gt; |
|Events|  &lt;ul&gt;&lt;li&gt;Events that should be raised after the contact is unsubscribed.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Transactional Message

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact List|  &lt;ul&gt;&lt;li&gt;(Required) The list the contact belongs to.&lt;/li&gt;&lt;/ul&gt; |
|Contact Email|  &lt;ul&gt;&lt;li&gt;(Required) The email address of the contact.&lt;/li&gt;&lt;/ul&gt; |
|Transactional Message|  &lt;ul&gt;&lt;li&gt;(Required) The message to send to the contact.&lt;/li&gt;&lt;/ul&gt; |
|Segmentation Group|  &lt;ul&gt;&lt;li&gt;The Segmentation Group that contains a list of segmentation fields.&lt;/li&gt;&lt;/ul&gt; |

## Vendor Documentation

* [Getting Started](https://api.listrak.com/email)

## APIs

* [Listrak Create or Update Contact HTTP API](https://api.listrak.com/email#operation/Contact_PostContactResource)
* [Listrak Subscribe HTTP API](https://api.listrak.com/email#operation/Contact_PostContactResource)
* [Listrak Unsubscribe HTTP API](https://api.listrak.com/email#operation/Contact_PostContactResource)
* [Listrak Send Transactional Message HTTP API](https://api.listrak.com/email#operation/TransactionalMessage_PostTransactionalMessageSend)
