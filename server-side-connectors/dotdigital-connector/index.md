---
title: dotdigital Connector Setup Guide
description: This article describes how to set up the dotdigital connector.
url: https://docs.tealium.com/server-side-connectors/dotdigital-connector/
---## How it Works

The dotdigital connector provides digital marketing professionals with SaaS technology solutions and tools, and offers an email marketing platform.

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Trigger Campaign| ✓| ✓|
|Send Email Using a Triggered Campaign| ✓| ✓|
|Send SMS| ✓| ✓|
|Create or Update Contact| ✓| ✗|
|Add Contact to Address Book| ✓| ✗|
|Delete Contact from Address Book| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Username**
  * Username for your API user.
  * To get started using the API, you must first create an API user.
  * These API user credentials (username/password) are required to authenticate each operation/method call and to ensure that you are connected to the correct account.
  * For setup information, see the following vendor documentation: [Getting Started with the API](https://developer.dotmailer.com/docs/getting-started-with-the-api)

* **API Password**
  * Password for your API user.

* **Region ID**
  * Region ID to be included in every API endpoint.
  * You can find your API endpoint under **Settings &amp;gt; Access &amp;gt; API users**.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Trigger Campaign

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Campaign ID|  &lt;ul&gt;&lt;li&gt;The ID of the campaign, which needs to be included within the request body.&lt;/li&gt;&lt;/ul&gt; |
|Address Book ID|  &lt;ul&gt;&lt;li&gt;The Address Book ID the campaign is to be sent to.&lt;/li&gt;&lt;li&gt;You must specify either an Address Book ID or a Contact ID.&lt;/li&gt;&lt;/ul&gt; |
|Contact ID|  &lt;ul&gt;&lt;li&gt;The Contact ID the campaign is to be sent to.&lt;/li&gt;&lt;li&gt;You must specify either an Address Book ID or a Contact ID.&lt;/li&gt;&lt;/ul&gt; |
|Send Date|  &lt;ul&gt;&lt;li&gt;The date and time at which you want the campaign to be sent.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Email Using a Triggered Campaign

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|To Address|  &lt;ul&gt;&lt;li&gt;The email address of the recipient.&lt;/li&gt;&lt;/ul&gt; |
|Campaign ID|  &lt;ul&gt;&lt;li&gt;The ID of the triggered campaign.&lt;/li&gt;&lt;li&gt;For more information on this endpoint, see the following vendor documentation: [Send transactional email using a triggered campaign](https://developer.dotmailer.com/docs/send-transactional-email-using-a-triggered-campaign).&lt;/li&gt;&lt;/ul&gt; |
|Personalization Values|  &lt;ul&gt;&lt;li&gt;Each personalization value is a key-value pair.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send SMS

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Telephone Number|  &lt;ul&gt;&lt;li&gt;The mobile number of the contact.&lt;/li&gt;&lt;/ul&gt; |
|Message|  &lt;ul&gt;&lt;li&gt;The SMS message to be sent to your contact&#39;s mobile phone.&lt;/li&gt;&lt;/ul&gt; |

### Action - Create or Update Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email|  &lt;ul&gt;&lt;li&gt;The email address of the contact.&lt;/li&gt;&lt;li&gt;For more information on this endpoint, see the following vendor documentation: [Create contact](https://developer.dotmailer.com/docs/create-contact).&lt;/li&gt;&lt;/ul&gt; |
|Data Fields|  &lt;ul&gt;&lt;li&gt;Each contact data field is a key-value pair.&lt;/li&gt;&lt;/ul&gt; |
|Opt-In Type|  &lt;ul&gt;&lt;li&gt;The opt-in type of the contact.&lt;/li&gt;&lt;/ul&gt; |
|Email Type|  &lt;ul&gt;&lt;li&gt;The email type of the contact.&lt;/li&gt;&lt;/ul&gt; |
|Contact Id|  &lt;ul&gt;&lt;li&gt;The ID of the contact.&lt;/li&gt;&lt;li&gt;This must be set to update a contact.&lt;/li&gt;&lt;/ul&gt; |

### Action - Add Contact to Address Book

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Address Book ID|  &lt;ul&gt;&lt;li&gt;The ID of the Address Book.&lt;/li&gt;&lt;li&gt;For more information on this endpoint, see the following vendor documentation: [Add contact to address book](https://developer.dotmailer.com/docs/add-contact-to-address-book).&lt;/li&gt;&lt;/ul&gt; |
|Email|  &lt;ul&gt;&lt;li&gt;The email address of the contact.&lt;/li&gt;&lt;li&gt;For more information on this endpoint, see the following vendor documentation: [Create contact](https://developer.dotmailer.com/docs/create-contact).&lt;/li&gt;&lt;/ul&gt; |
|Data Fields|  &lt;ul&gt;&lt;li&gt;Each contact data field is a key-value pair.&lt;/li&gt;&lt;/ul&gt; |
|Opt-In Type|  &lt;ul&gt;&lt;li&gt;The opt-in type of the contact.&lt;/li&gt;&lt;/ul&gt; |
|Email Type|  &lt;ul&gt;&lt;li&gt;The email type of the contact.&lt;/li&gt;&lt;/ul&gt; |

### Action - Delete Contact from Address Book

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Address Book ID|  &lt;ul&gt;&lt;li&gt;The ID of the Address Book.&lt;/li&gt;&lt;li&gt;For more information on this endpoint, see the following vendor documentation: [Delete contact from address book](https://developer.dotmailer.com/docs/delete-contact-from-address-book).&lt;/li&gt;&lt;/ul&gt; |
|Contact ID|  &lt;ul&gt;&lt;li&gt;The ID of the contact to be deleted.&lt;/li&gt;&lt;/ul&gt; |
