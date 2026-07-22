---
title: Salesforce Email Studio OAuth2 (ExactTarget) Connector Setup Guide
description: This article describes how to set up the Salesforce Email Studio OAuth2 connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-email-studio-oauth2-exacttarget-connector/
---
## Prerequisites

* Salesforce Marketing Cloud Account
* Salesforce Marketing Cloud App Client Credentials
* Appropriate permissions set on the Salesforce Marketing Cloud App

## Connect Using the OAuth2 Authentication Scheme

Use the following steps to connect Tealium to ExactTarget using OAuth2 authentication scheme:

1. Log into your ExactTarget account and from the top right menu, select **Setup**.
1. Navigate to **Platform Tools > Apps > Installed Packages**.
1. At the top right of the **Installed Packages** panel, click **New** to create a new package.
1. In the opened dialog box, name your package and click **Save**.
1. In the newly created package, click **Add Component**.
1. Select **API Integration** as the component type and **Server-to-Server** as the integration type.
1. Set appropriate Server-to-Server properties. 
When you create an installed package, it is enabled only for the Business Unit where it was created. To make the package available in additional Business Units:
   1. Go to the installed package’s configuration page.
   1. Under **Access**, select **Add Business Units**.
   1. Select the checkboxes next to each MID (Business Unit) that require access to the package. 
<blockquote>
If correct permissions are not provided, the integration may fail. Changing permissions after the package has been created may require some wait time for the permissions to apply.
</blockquote>
 
1. Save your component. 
In the package window, the component named **API Integration** displays the authentication information.
1. Copy the following values to use later in the connector configuration:
   * **Client ID**
   * **Client Secret**
   * **SOAP Base URI**
1. Also copy your account's **MID** value, found in the top menu bar.

## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:-------|:-------|:----------|
| Send Email to User | ✓ | ✓ |
| Add to Email List | ✓ | ✓ |
| Remove from Email List | ✓ | ✓ |
| Upsert Subscriber and Add to Email List(s) | ✓ | ✓ |
| Data Extension - Add Record | ✓ | ✓ |
| Data Extension - Add Multiple Records | ✓ | ✓ |
| Data Extension - Delete Record | ✓ | ✓ |
| Data Extension - Update Record | ✓ | ✓ |
| Data Extension - Upsert Record | ✓ | ✓ |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

This connector requires the following information to connect to ExactTarget's SOAP protocol, upgraded with OAuth2 authentication scheme.

* **Market Cloud App Client ID**
  * (Required) Provide your app client ID.
  * See: [Get OAuth Client Credentials](https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/getting_started_developers_and_the_exacttarget_api.htm)

* **Client Secret**:
  * (Required) Provide your app client secret.

* **Account ID**
  * (Required) Provide the account identifier (MID) of the target business unit.

* **Tenant-specific subdomain**
  * (Required) Provide tenant-specific subdomain for your application.
  * If your SOAP Base URL looks something like this: `https://mctg-xxxxxx.soap.marketingcloudapis.com/`, then provide the portion of this URL between two slashes and the first period, in this example it would be `mctg-xxxxxx`.
  * The connector will automatically augment this subdomain name with correct suffixes for authentication and for SOAP messaging.


* **ExactTarget Account ID (MID)**

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

See [Salesforce Marketing Cloud Email Studio](https://docs.tealium.com/salesforce-email-studio-connector-legacy/) for details about actions setup.

This section describes how to set up parameters and options for each action.

### Action - Send Email to User

#### Parameters
| **Parameter** | **Description** |
|:-------|:--------|
| Business Unit | <ul><li>(Recommended) Select appropriate business unit.</li><li>If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.</li></ul> |
| Triggered Send Email Interaction | <ul><li>(Required) Select triggered send email interaction.</li></ul> |
| Subscriber Lookup By Key | <ul><li>(Required) Lookup existing subscriber by key to send them an email.</li></ul> |
| Disable Subscriber Lookup | <ul><li>To disable lookup, check **Disable Subscriber Lookup** and configure the **"Subscriber Email** section.</li></ul> |
| Subscriber Email | <ul><li>Provide email to send message to (required if subscriber lookup is disabled).</li><li>Email can be left blank to use looked-up subscriber's email instead.</li></ul> |
| Attributes to Add or Overwrite | <ul><li>Map values to keys to include dynamic contents in your email and a sample input, see: [Passing Content to a Triggered Send Message at Send Time](https://salesforce.stackexchange.com/questions/222420/pass-content-to-a-triggered-send-message-at-send-time).</li><li>To manage your Profile Attributes, see: [Profile and Preference Attributes](https://help.salesforce.com/s/articleView?id=sf.mc_es_profile_pref_attributes.htm&language=en_US&type=5).</li></ul> |
| Don't Send Email to Subscriber with Status | <ul><li>If looked-up subscriber has one of the following statuses then do not send the email.</li></ul> |
| Enable Asynchronous Processing | <ul><li>Check option to enable asynchronous processing. API calls will be queued before being processed, rather than directly at the time the API call is received.</li><li>Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.</li><li>For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).</li></ul> |

### Action - Add to Email List

#### Parameters
| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | <ul><li>(Recommended) Select appropriate business unit.</li><li>If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.</li></ul> |
| Email List | <ul><li>(Required) Select email list.</li></ul> |
| Subscriber Lookup By Key | <ul><li>(Required) Provide subscriber key to find existing subscriber.</li></ul> |
| Enable Asynchronous Processing | <ul><li>(Optional) Check option to enable asynchronous processing.</li><li>API calls will be queued before being processed, rather than directly at the time the API call is received.</li><li>Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.</li><li>For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).</li></ul> |

### Action - Remove from Email List

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | <ul><li>(Recommended) Select appropriate business unit.</li><li>If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.</li></ul> |
| Email List | <ul><li>(Required) Select email list.</li></ul> |
| Subscriber Lookup By Key | <ul><li>(Required) Provide subscriber key to find existing subscriber.</li></ul> |
| Enable Asynchronous Processing | <ul><li>(Optional) Check option to enable asynchronous processing.</li><li>API calls will be queued before being processed, rather than directly at the time the API call is received.</li><li>Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.</li><li>For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).</li></ul> |

### Action - Upsert Subscriber and Add to Email List(s)

#### Parameters

| **Parameter** | **Description** |
|:--------|:-------|
| Business Unit | <ul><li>(Recommended) Select appropriate business unit.</li><li>If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.</li></ul> |
| Subscriber Key | <ul><li>Required.</li></ul> |
| Subscriber Email Address | <ul><li>Required.</li></ul> |
| Add Subscriber to Email List(s) | <ul><li>(Optional) Select one or more email lists to add subscriber to.</li></ul> |
| User Status | <ul><li>(Optional) Select value to update user's status to.</li></ul> |
| Enable Asynchronous Processing | <ul><li>(Optional) Check option to enable asynchronous processing.</li><li>API calls will be queued before being processed, rather than directly at the time the API call is received.</li><li>Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.</li><li>For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).</li></ul> |

### Action - Data Extension - Add Record

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | <ul><li>(Recommended) Select appropriate business unit.</li><li>If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.</li></ul> |
| Data Extension | <ul><li>(Required) Select data extension.</li><li>The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.</li><li>If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.</li><ul> |
| Record Fields | <ul><li>(Required) Map values to fields to add new record to data extension.</li></ul> |
| Enable Asynchronous Processing | <ul><li>(Optional) Check option to enable asynchronous processing.</li><li>API calls will be queued before being processed, rather than directly at the time the API call is received.</li><li>Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.</li><li>For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).</li></ul> |

### Action - Data Extension - Add Multiple Records

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | <ul><li>(Recommended) Select appropriate business unit.</li><li>If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.</li></ul> |
| Data Extension | <ul><li>(Required) Select data extension.</li><li>The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.</li><li>If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.</li></ul> |
| Record Fields | <ul><li>(Required) Map array type attributes to add multiple data extension records.</li><li>Array type attributes must be of equal length.</li><li>Single value attributes can be used and will apply to each record.</li></ul> |
| Enable Asynchronous Processing | <ul><li>(Optional) Check option to enable asynchronous processing.</li><li>API calls will be queued before being processed, rather than directly at the time the API call is received.</li><li>Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.</li><li>For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).</li></ul> |

### Action - Data Extension - Delete Record

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | <ul><li>(Recommended) Select appropriate business unit.</li><li>If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.</li></ul> |
| Data Extension | <ul><li>(Required) Select data extension.</li><li>The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.</li><li>If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.</li></ul> |
| Record Lookup | <ul><li>(Required) Map values to record files by which to find existing record to delete.</li></ul> |
| Enable Asynchronous Processing | <ul><li>(Optional) Check option to enable asynchronous processing.</li><li>API calls will be queued before being processed, rather than directly at the time the API call is received.</li><li>Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.</li><li>For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).</li></ul> |

### Action - Data Extension - Update Record

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | <ul><li>(Recommended) Select appropriate business unit.</li><li>If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.</li></ul> |
| Data Extension | <ul><li>(Required) Select data extension.</li><li>The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.</li><li>If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.</li></ul> |
| Record Lookup | <ul><li>(Required) Map values to record fields by which to find existing record to update.</li></ul> |
| Enable Asynchronous Processing | <ul><li>(Optional) Check option to enable asynchronous processing.</li><li>API calls will be queued before being processed, rather than directly at the time the API call is received.</li><li>Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.</li><li>For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).</li></ul> |

### Action - Data Extension - Upsert Record

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | <ul><li>(Recommended) Select appropriate business unit.</li><li>If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.</li></ul> |
| Data Extension | <ul><li>(Required) Select data extension.</li><li>The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.</li><li>If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.</li></ul> |
| Record Lookup | <ul><li>(Required) Map values to record fields by which to find existing record to update.</li></ul> |
| Enable Asynchronous Processing | <ul><li>(Optional) Check option to enable asynchronous processing.</li><li>API calls will be queued before being processed, rather than directly at the time the API call is received.</li><li>Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.</li><li>For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).</li></ul> |

## Vendor Documentation

* [Salesforce Marketing Cloud: Create an OAuth 2.0 API Integration in Enhanced Packages](https://developer.salesforce.com/docs/atlas.en-us.mc-app-development.meta/mc-app-development/create-integration-enhanced.htm)
* [Salesforce Marketing Cloud: API Integration](https://developer.salesforce.com/docs/atlas.en-us.mc-app-development.meta/mc-app-development/api-integration.htm)
* [Salesforce Marketing Cloud: Authenticate Your SOAP API Calls](https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/authenticate-soap-api.htm)
