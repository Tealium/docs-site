---
title: ActiveCampaign Connector Setup Guide
description: This article describes how to set up the ActiveCampaign connector.
url: https://docs.tealium.com/server-side-connectors/activecampaign-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: ActiveCampaign API
* API Version: v3
* Documentation: [ActiveCampaign API](https://developers.activecampaign.com/reference/overview)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:
* **Account Name**  
  * Access the API using a base URL that is specific to your account.
  * Go to ActiveCampaign and click **Settings &gt; Developer** to get your API URL.
* **API Token**  
  * Go to ActiveCampaign and click **Settings &gt; Developer** to get your API token.
  * Each user in your ActiveCampaign account has their own unique API token.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Upsert Contact | ✓ | ✓ |
| Add Tags to Contact | ✓ | ✓ |
| Add Contact to Automation | ✓ | ✓ |
| Update List Status for a Contact |  ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action - Upsert Contact

#### Contact Parameters

| Parameter | Description |
| --- | --- |
| Email | (Required) Email address of the contact to synchronize. |
| First Name | (Required) First name of contact. |
| Last Name | (Required) Last name of contact. |
| Phone | (Required) Phone number of contact. |

#### Field Values

An array of the contact’s field values. Customer field values are referenced by `id` and not the field name. This is an integer value and must be found through the ActiveCampaign field management.

| Parameter | Description |
| --- | --- |
| Field | The field name. |
| Value | The value of the field. |

### Action - Add Tags to Contact

#### Parameters

| Parameter | Description |
| --- | --- |
| Contact ID | The ID of the contact. |
| Tag ID | Enter the exact name of the tag to assign the visitor to. Select the tag from the drop-down. |

### Action - Add Contact to Automation

#### Parameters

| Parameter | Description |
| --- | --- |
| Contact ID | The ID of the contact. |
| Automation ID | The ID of the automation. |

### Action - Update List Status for a Contact

#### Parameters

| Parameter | Description |
| --- | --- |
| List ID | (Required) The ID of the list to subscribe the contact to. |
| Contact ID | <ul><li>Either **Contact ID** or **Email** is required. ID of the contact to subscribe to the list.</li></ul> |
| Email Address |  <ul><li>Either **Contact ID** or **Email** is required.</li><li>The email of the contact.</li><li>This field is necessary if the user does not store the **Contact ID** in Tealium. If they do not use the **Contact ID**, search for the user’s email address through a API call and use the **ID** field in the response as the **Contact ID**.</li></ul> |
| Status | <ul><li>(Required) Set to `1` to subscribe the contact to the list.</li><li>Set to `2` to unsubscribe the contact from the list.</li><li>WARNING: If you change a status from unsubscribed to active, you can re-subscribe a contact to a list from which they had manually unsubscribed.</li></ul> |
| Source ID | <ul><li>(Optional) A unique identifier associated with the contact's origin.</li><li>Set to `4` when re-subscribing a contact to a list.</li></ul> |