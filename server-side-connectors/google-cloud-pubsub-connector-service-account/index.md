---
title: Google Cloud Pub/Sub Connector Setup Guide
description: This article describes how to set up the Google Cloud Pub/Sub connectors. Tealium offers two Pub/Sub connectors in the Connector Marketplace: the Google Could Pub/Sub Connector (3-legged OAuth) and Google Cloud Pub/Sub (Service Account) Connector (2-legged OAuth).
url: https://docs.tealium.com/server-side-connectors/google-cloud-pubsub-connector-service-account/
---
## Prerequisites

### Google Cloud Pub/Sub Connector

This connector uses a three-legged OAuth flow for authentication that requires a client ID and secret with user input. Before configuring this connector, complete the following steps:

1. Create an OAuth client ID credential in your Google Cloud project with an application type of web application.
1. Update the Google Cloud web application settings to allowlist Tealium servers and provide the required callback upon successful connection. In the Google Cloud console, go to **Credentials** and edit the OAuth client ID settings with the following values. For each selection, add one of the values depending on the subdomain used in the URL of your Tealium instance.
    * Authorized JavaScript origins:
      * `https://my.tealiumiq.com`
      * `https://my.tealiumiq.com`
      * `https://[privatecloud subdomain].tealiumiq.com`
    * Authorized redirect URIs:
      * `https://my.tealiumiq.com/oauth/google/callback.html`
      * `https://my.tealiumiq.com/oauth/google/callback.html`
      * `https://[private cloud subdomain].tealiumiq.com/oauth/google/callback.html`
1. Make note of the following configuration settings to use in the connector configuration
    * Project ID
    * Client ID
    * Client Secret

### Google Cloud Pub/Sub (Service Account) Connector

This connector uses two-legged OAuth flow, based on a Google Cloud service account for access. Before configuring the connector, create a service account in a Google Cloud project with a role of Pub/Sub Publisher. For more information about creating a service account, see [Access Control with IAM](https://cloud.google.com/pubsub/docs/access-control) in the Google Cloud documentation. After you create your service account, make note of the following configuration settings to use in the connector configuration:

* Project ID
* Service Account Email
* Service Account Key

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings based on which connector you added:

### Google Cloud Pub/Sub Connector

* **Google Cloud Platform Project ID**  
(Required) Your Google Cloud Platform Project ID.
* **Client ID**  
(Required) The OAuth Client ID in your Google Cloud project with an application type of web application.
* **Client Secret**  
(Required) Enter the client secret assigned to you in your Google Cloud project.

### Google Cloud Pub/Sub (Service Account) Connector

* **Google Cloud Platform Project ID**  
(Required) Your Google Cloud Platform Project ID.
* **Client Email**  
(Required) The service account email address used in your Google Cloud project.
* **Private Key**  
(Required) The private key generated for your Google Cloud project service account.

## Actions

### Google Cloud Pub/Sub Connector

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Event Data to Topic | ✗ | ✓ |
| Send Visitor Data to Topic | ✓ | ✗ |
| Send Customized Data to Topic (Advanced) | ✓ | ✓ |
| Send Log Event to Topic | ✓ | ✓ |

### Google Cloud Pub/Sub (Service Account) Connector

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event Data to Topic | ✗ | ✓ |
| Send Event Data with Custom URL | ✗ | ✓ |
| Send Visitor Data to Topic | ✓ | ✗ |
| Send Customized Data to Topic (Advanced) | ✓ | ✓ |
| Send Log Event to Topic | ✓ | ✓ |

If the Pub/Sub topic you are publishing to has a schema attached, use the **Send Customized Data to Topic** action to specify a strict JSON definition which matches your schema.

### Send Event Data to Topic

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Project Topic| (Required) Select the topic in your Pub/Sub project to publish the message to. |
|Message Attributes| Map your attribute values to custom Pub/Sub message attributes. Enter the message attribute key in the **To** drop-down list. |
|Print Attribute Names|  If attribute names are updated, the names in the payload automatically reflect the updated name in the published message.|
|Ordering Key|Map or enter an ordering key-value to enable Pub/Sub topic subscribers to receive messages in the order they are published. For more information, see [Google: Order messages](https://cloud.google.com/pubsub/docs/ordering).|

### Send Visitor Data to Topic

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Project Topic|(Required) Select the topic in your Pub/Sub project to publish the message to. |
|Message Attributes|Map your attribute values to custom Pub/Sub message attributes. Enter the message attribute key in the **To** drop-down list. |
|Include Current Visit Data| Check this box to include both visitor data and current visit data in the published message. |
|Print Attribute Names| If attribute names are updated, the names in the payload automatically reflect the updated name in the published message. |
|Ordering Key|Map or enter an ordering key-value to enable Pub/Sub topic subscribers to receive messages in the order they are published. For more information, see [Google: Order messages](https://cloud.google.com/pubsub/docs/ordering).|

### Send Customized Data to Topic (Advanced)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Project Topic|(Required) Select the topic in your Pub/Sub project to publish the message to. |
| Message Data|(Required) Provide values to construct message data. For template support, reference the template name to generate message data from the template. Map values to names for simple one-level JSON format, otherwise reference the template name and select only the **Custom Message Definition** option.|
|Message Attributes| Map your attribute values to custom Pub/Sub message attributes.Enter the message attribute key in the **To** drop-down list.|
|Template Variables|Provide template variables as data input for templates. For more information, see . Name nested template variables with the dot notation. For example: `items.name`. Nested template variables are typically built from data layer list attributes.|
|Templates| Provide templates to be referenced in either message attributes or data. For more information, see . Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.
|Ordering Key|Map or enter an ordering key-value to enable Pub/Sub topic subscribers to receive messages in the order they are published. For more information, see [Google: Order messages](https://cloud.google.com/pubsub/docs/ordering).|

### Send Log Event to Topic

#### Parameters

| Parameter | Description |
| --- | --- |
| Project Topic | (Required) Select the topic to send log event to. |
| Message Attributes | (Optional) Map values to message attributes. |

### Send Event Data with Custom URL

| **Parameter** | **Description** |
| --- | --- |
| URL Override | (Required) Enter custom `URL` to send data to. |
| Message Attributes | Map values to message attributes |
| Print Attribute Names | If attribute names are updated, the names in the payload will reflect the update. |
|Ordering Key|Map or enter an ordering key-value to enable Pub/Sub topic subscribers to receive messages in the order they are published. For more information, see [Google: Order messages](https://cloud.google.com/pubsub/docs/ordering).|

## Vendor Documentation

* [Pub/Sub: What is Pub/Sub?](https://cloud.google.com/pubsub/docs/overview)
* [Setting Up Authentication for Server to Server Production Applications](https://cloud.google.com/docs/authentication/production#obtaining_and_providing_service_account_credentials_manually)