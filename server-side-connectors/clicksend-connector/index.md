---
title: ClickSend Connector Setup Guide
description: This article describes how to set up the ClickSend connector.
url: https://docs.tealium.com/server-side-connectors/clicksend-connector/
---

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Create a New Contact| ✓| ✓|
|Update a Specific Contact| ✓| ✓|
|Delete a Specific Contact| ✓| ✓|
|Send an SMS| ✓| ✓|
|Send a Transactional Email| ✓| ✓|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Username**  
Username is your account username, password is your account password. These are the same credentials that you use to login to the dashboard. For more information, see [ClickSend authentication documentation](https://clicksend.docs.apiary.io/#introduction/authentication).
* **Password**  
Username is your account username, password is your account password. These are the same credentials that you use to login to the dashboard. For more information, see [ClickSend authentication documentation](https://clicksend.docs.apiary.io/#introduction/authentication).

Click **Done** when you are finished configuring the connector.

## Action settings — parameters and options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Create a New Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List ID| The contact list ID where your contact is associated. For more information on this endpoint, read: [ClickSend&#39;s create a new contact documentation](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact).|
|Phone Number| Contact phone number in E.164 format. Note that the fields `phone_number`, `fax_number`, `address_line_1`, and `email` are all optional. However, at least one of them must be specified, otherwise the API call will fail. For more information, read: [ClickSend&#39;s create a new contact documentation](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact).|
|First Name| First name of the contact.|
|Last Name| Last name of the contact.|
|Fax Number| Contact fax number. Note that the fields `phone_number`, `fax_number`, `address_line_1`, and `email` are all optional. However, at least one of them must be specified, otherwise the API call will fail. For more information, read: [ClickSend&#39;s create a new contact documentation](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact).|
|Organization Name| Your organization name.|
|Email| Contact email. Note that the fields `phone_number`, `fax_number`, `address_line_1`, and `email` are all optional. However, at least one of them must be specified, otherwise the API call will fail. For more information, read: [ClickSend&#39;s create a new contact documentation](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact).|
|Address Line 1| Contact address line 1. Note that the fields `phone_number`, `fax_number`, `address_line_1`, and `email` are all optional. However, at least one of them must be specified, otherwise the API call will fail. For more information, read: [ClickSend&#39;s create a new contact documentation](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact).|
|Address Line 2| Contact address line 2.|
|Address City| Contact city.|
|Address State| Contact state.|
|Address Postal Code| Contact postal code.|
|Address Country| Contact two-letter country code defined in ISO 3166.|
|Custom Attributes| Any custom attributes you want to include.|

### Action — Update a Specific Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List ID| Contact list ID you want to access. For more information on this endpoint, read: [ClickSend&#39;s update a contact documentation](https://clicksend.docs.apiary.io/#reference/contacts/contact/update-a-specific-contact).|
|Contact ID| Contact ID you want to access.|
|Phone Number| Contact phone number in E.164 format.|
|First Name| First name of the contact.|
|Last Name| Last name of the contact.|
|Fax Number| Contact fax number.|
|Organization Name| Your organization name.|
|Email| Contact email.|
|Address Line 1| Contact address line 1.|
|Address Line 2| Contact address line 2.|
|Address City| Contact city.|
|Address State| Contact state.|
|Address Postal Code| Contact postal code.|
|Address Country| Contact two-letter country code defined in ISO 3166 format.|
|Custom Attributes| Any custom attributes you want to include.|

### Action — Delete a Specific Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List ID| Your contact list ID you want to access. For more information on this endpoint, read: [ClickSend&#39;s delete a contact documentation](https://clicksend.docs.apiary.io/#reference/contacts/contact/delete-a-specific-contact).|
|Contact ID| Your contact ID you want to access.|

### Action — Send an SMS

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|To| Recipient number in E.164 format or local format. For more information, read: [ClickSend&#39;s send an SMS documentation](https://clicksend.docs.apiary.io/#reference/sms/send-an-sms).|
|Body| Your message.|
|Source| Your method of sending. For example, `wordpress`, `php`, `c#`.|
|From| Your sender ID. For more information, read: [SendGrid&#39;s sender ID or number documentation](https://help.clicksend.com/SMS/what-is-a-sender-id-or-sender-number).|
|Schedule| Your scheduled time as a Unix timestamp. Leave blank for immediate delivery.|
|Custom String| Your reference. Will be passed back with all replies and delivery reports.|
|Country| Recipient country.|
|From Email| An email address where the reply should be emailed to. If omitted, the reply will be emailed back to the user who sent the outgoing SMS.|

### Action — Send a Transactional Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email| The recipient&#39;s email address.|
|Name (to)| The recipient&#39;s name.|
|Email Address ID| The sender&#39;s email address ID.|
|Name (from)| The sender&#39;s name.|
|Subject| The subject of the email.|
|Body| The content of the email.|
