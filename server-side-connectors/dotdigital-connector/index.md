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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

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
  * You can find your API endpoint under **Settings &gt; Access &gt; API users**.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Trigger Campaign

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Campaign ID|  <ul><li>The ID of the campaign, which needs to be included within the request body.</li></ul> |
|Address Book ID|  <ul><li>The Address Book ID the campaign is to be sent to.</li><li>You must specify either an Address Book ID or a Contact ID.</li></ul> |
|Contact ID|  <ul><li>The Contact ID the campaign is to be sent to.</li><li>You must specify either an Address Book ID or a Contact ID.</li></ul> |
|Send Date|  <ul><li>The date and time at which you want the campaign to be sent.</li></ul> |

### Action - Send Email Using a Triggered Campaign

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|To Address|  <ul><li>The email address of the recipient.</li></ul> |
|Campaign ID|  <ul><li>The ID of the triggered campaign.</li><li>For more information on this endpoint, see the following vendor documentation: [Send transactional email using a triggered campaign](https://developer.dotmailer.com/docs/send-transactional-email-using-a-triggered-campaign).</li></ul> |
|Personalization Values|  <ul><li>Each personalization value is a key-value pair.</li></ul> |

### Action - Send SMS

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Telephone Number|  <ul><li>The mobile number of the contact.</li></ul> |
|Message|  <ul><li>The SMS message to be sent to your contact's mobile phone.</li></ul> |

### Action - Create or Update Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email|  <ul><li>The email address of the contact.</li><li>For more information on this endpoint, see the following vendor documentation: [Create contact](https://developer.dotmailer.com/docs/create-contact).</li></ul> |
|Data Fields|  <ul><li>Each contact data field is a key-value pair.</li></ul> |
|Opt-In Type|  <ul><li>The opt-in type of the contact.</li></ul> |
|Email Type|  <ul><li>The email type of the contact.</li></ul> |
|Contact Id|  <ul><li>The ID of the contact.</li><li>This must be set to update a contact.</li></ul> |

### Action - Add Contact to Address Book

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Address Book ID|  <ul><li>The ID of the Address Book.</li><li>For more information on this endpoint, see the following vendor documentation: [Add contact to address book](https://developer.dotmailer.com/docs/add-contact-to-address-book).</li></ul> |
|Email|  <ul><li>The email address of the contact.</li><li>For more information on this endpoint, see the following vendor documentation: [Create contact](https://developer.dotmailer.com/docs/create-contact).</li></ul> |
|Data Fields|  <ul><li>Each contact data field is a key-value pair.</li></ul> |
|Opt-In Type|  <ul><li>The opt-in type of the contact.</li></ul> |
|Email Type|  <ul><li>The email type of the contact.</li></ul> |

### Action - Delete Contact from Address Book

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Address Book ID|  <ul><li>The ID of the Address Book.</li><li>For more information on this endpoint, see the following vendor documentation: [Delete contact from address book](https://developer.dotmailer.com/docs/delete-contact-from-address-book).</li></ul> |
|Contact ID|  <ul><li>The ID of the contact to be deleted.</li></ul> |
