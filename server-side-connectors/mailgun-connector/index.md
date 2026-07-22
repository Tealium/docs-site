---
title: Mailgun Connector Setup Guide
description: This article describes how to set up the Mailgun connector.
url: https://docs.tealium.com/server-side-connectors/mailgun-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Mailgun API
* API Version: v3
* API Endpoint: `https://api.mailgun.net`
* Documentation: [Mailgun API](https://documentation.mailgun.com/en/latest/)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Email | ✓ | ✓ |
| Upsert Member in List | ✓ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Mailgun Domain**: (Required) Select the appropriate region-based domain.
* **API Key**: (Required) You can find your private API key on your Mailgun dashboard.

## Action Settings - Parameters and Options

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action - Send Email

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Sending Domain | (Required) The domain of the Mailgun account. |
| From | (Required) Email address of the sender. |
| To | (Required) Email address of the recipient.  |
| Subject | Email subject. |
| Text | The body of the message. |
| CC | The email address or addresses to carbon copy. |
| BCC |The email address or addresses to blind carbon copy. |
| Template Name | A Mailgun email sending template name. |
| Template Text | Set this parameter to **yes** if you want to render the text of the message through the template. |
| Template Version | Send the email to a specific version of a template. |
| Template Variables | Map attributes to populate a JSON-encoded dictionary used as the input for template variable expansion. For more information, see [Mailgun API Reference](https://documentation.mailgun.com/en/latest/api-sending.html#sending). |

### Action - Upsert Member in List

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Address | (Required) The email address of the list. |
| Member Address | (Required) The email address to add to the list. |
| Member Name | The name of email address to add. |
| Subscribe | <ul><li>**yes**: Subscribe the new member.</li><li>**no**: Do not subscribe the new member.</li></ul> |
| Upsert | <ul><li>**yes**: Update list member, if it exists in the list.</li><li>**no**: Add list member, even if it is a duplicate.</li></ul> |
| Variables | Map attributes to pass additional member parameters. For more information, see [Mailgun API Reference](https://documentation.mailgun.com/en/latest/api-sending.html#sending). |
