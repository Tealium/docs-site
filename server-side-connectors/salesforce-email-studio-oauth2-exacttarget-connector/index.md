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
1. Navigate to **Platform Tools &gt; Apps &gt; Installed Packages**.
1. At the top right of the **Installed Packages** panel, click **New** to create a new package.
1. In the opened dialog box, name your package and click **Save**.
1. In the newly created package, click **Add Component**.
1. Select **API Integration** as the component type and **Server-to-Server** as the integration type.
1. Set appropriate Server-to-Server properties. 
When you create an installed package, it is enabled only for the Business Unit where it was created. To make the package available in additional Business Units:
   1. Go to the installed package’s configuration page.
   1. Under **Access**, select **Add Business Units**.
   1. Select the checkboxes next to each MID (Business Unit) that require access to the package. If correct permissions are not provided, the integration may fail. Changing permissions after the package has been created may require some wait time for the permissions to apply. 
1. Save your component. 
In the package window, the component named **API Integration** displays the authentication information.
1. Copy the following values to use later in the connector configuration:
   * **Client ID**
   * **Client Secret**
   * **SOAP Base URI**
1. Also copy your account&#39;s **MID** value, found in the top menu bar.

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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

This connector requires the following information to connect to ExactTarget&#39;s SOAP protocol, upgraded with OAuth2 authentication scheme.

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

See [Salesforce Marketing Cloud Email Studio]() for details about actions setup.

This section describes how to set up parameters and options for each action.

### Action - Send Email to User

#### Parameters
| **Parameter** | **Description** |
|:-------|:--------|
| Business Unit | &lt;ul&gt;&lt;li&gt;(Recommended) Select appropriate business unit.&lt;/li&gt;&lt;li&gt;If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.&lt;/li&gt;&lt;/ul&gt; |
| Triggered Send Email Interaction | &lt;ul&gt;&lt;li&gt;(Required) Select triggered send email interaction.&lt;/li&gt;&lt;/ul&gt; |
| Subscriber Lookup By Key | &lt;ul&gt;&lt;li&gt;(Required) Lookup existing subscriber by key to send them an email.&lt;/li&gt;&lt;/ul&gt; |
| Disable Subscriber Lookup | &lt;ul&gt;&lt;li&gt;To disable lookup, check **Disable Subscriber Lookup** and configure the **&#34;Subscriber Email** section.&lt;/li&gt;&lt;/ul&gt; |
| Subscriber Email | &lt;ul&gt;&lt;li&gt;Provide email to send message to (required if subscriber lookup is disabled).&lt;/li&gt;&lt;li&gt;Email can be left blank to use looked-up subscriber&#39;s email instead.&lt;/li&gt;&lt;/ul&gt; |
| Attributes to Add or Overwrite | &lt;ul&gt;&lt;li&gt;Map values to keys to include dynamic contents in your email and a sample input, see: [Passing Content to a Triggered Send Message at Send Time](https://salesforce.stackexchange.com/questions/222420/pass-content-to-a-triggered-send-message-at-send-time).&lt;/li&gt;&lt;li&gt;To manage your Profile Attributes, see: [Profile and Preference Attributes](https://help.salesforce.com/s/articleView?id=sf.mc_es_profile_pref_attributes.htm&amp;language=en_US&amp;type=5).&lt;/li&gt;&lt;/ul&gt; |
| Don&#39;t Send Email to Subscriber with Status | &lt;ul&gt;&lt;li&gt;If looked-up subscriber has one of the following statuses then do not send the email.&lt;/li&gt;&lt;/ul&gt; |
| Enable Asynchronous Processing | &lt;ul&gt;&lt;li&gt;Check option to enable asynchronous processing. API calls will be queued before being processed, rather than directly at the time the API call is received.&lt;/li&gt;&lt;li&gt;Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.&lt;/li&gt;&lt;li&gt;For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).&lt;/li&gt;&lt;/ul&gt; |

### Action - Add to Email List

#### Parameters
| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | &lt;ul&gt;&lt;li&gt;(Recommended) Select appropriate business unit.&lt;/li&gt;&lt;li&gt;If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.&lt;/li&gt;&lt;/ul&gt; |
| Email List | &lt;ul&gt;&lt;li&gt;(Required) Select email list.&lt;/li&gt;&lt;/ul&gt; |
| Subscriber Lookup By Key | &lt;ul&gt;&lt;li&gt;(Required) Provide subscriber key to find existing subscriber.&lt;/li&gt;&lt;/ul&gt; |
| Enable Asynchronous Processing | &lt;ul&gt;&lt;li&gt;(Optional) Check option to enable asynchronous processing.&lt;/li&gt;&lt;li&gt;API calls will be queued before being processed, rather than directly at the time the API call is received.&lt;/li&gt;&lt;li&gt;Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.&lt;/li&gt;&lt;li&gt;For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).&lt;/li&gt;&lt;/ul&gt; |

### Action - Remove from Email List

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | &lt;ul&gt;&lt;li&gt;(Recommended) Select appropriate business unit.&lt;/li&gt;&lt;li&gt;If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.&lt;/li&gt;&lt;/ul&gt; |
| Email List | &lt;ul&gt;&lt;li&gt;(Required) Select email list.&lt;/li&gt;&lt;/ul&gt; |
| Subscriber Lookup By Key | &lt;ul&gt;&lt;li&gt;(Required) Provide subscriber key to find existing subscriber.&lt;/li&gt;&lt;/ul&gt; |
| Enable Asynchronous Processing | &lt;ul&gt;&lt;li&gt;(Optional) Check option to enable asynchronous processing.&lt;/li&gt;&lt;li&gt;API calls will be queued before being processed, rather than directly at the time the API call is received.&lt;/li&gt;&lt;li&gt;Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.&lt;/li&gt;&lt;li&gt;For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).&lt;/li&gt;&lt;/ul&gt; |

### Action - Upsert Subscriber and Add to Email List(s)

#### Parameters

| **Parameter** | **Description** |
|:--------|:-------|
| Business Unit | &lt;ul&gt;&lt;li&gt;(Recommended) Select appropriate business unit.&lt;/li&gt;&lt;li&gt;If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.&lt;/li&gt;&lt;/ul&gt; |
| Subscriber Key | &lt;ul&gt;&lt;li&gt;Required.&lt;/li&gt;&lt;/ul&gt; |
| Subscriber Email Address | &lt;ul&gt;&lt;li&gt;Required.&lt;/li&gt;&lt;/ul&gt; |
| Add Subscriber to Email List(s) | &lt;ul&gt;&lt;li&gt;(Optional) Select one or more email lists to add subscriber to.&lt;/li&gt;&lt;/ul&gt; |
| User Status | &lt;ul&gt;&lt;li&gt;(Optional) Select value to update user&#39;s status to.&lt;/li&gt;&lt;/ul&gt; |
| Enable Asynchronous Processing | &lt;ul&gt;&lt;li&gt;(Optional) Check option to enable asynchronous processing.&lt;/li&gt;&lt;li&gt;API calls will be queued before being processed, rather than directly at the time the API call is received.&lt;/li&gt;&lt;li&gt;Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.&lt;/li&gt;&lt;li&gt;For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).&lt;/li&gt;&lt;/ul&gt; |

### Action - Data Extension - Add Record

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | &lt;ul&gt;&lt;li&gt;(Recommended) Select appropriate business unit.&lt;/li&gt;&lt;li&gt;If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.&lt;/li&gt;&lt;/ul&gt; |
| Data Extension | &lt;ul&gt;&lt;li&gt;(Required) Select data extension.&lt;/li&gt;&lt;li&gt;The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.&lt;/li&gt;&lt;li&gt;If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.&lt;/li&gt;&lt;ul&gt; |
| Record Fields | &lt;ul&gt;&lt;li&gt;(Required) Map values to fields to add new record to data extension.&lt;/li&gt;&lt;/ul&gt; |
| Enable Asynchronous Processing | &lt;ul&gt;&lt;li&gt;(Optional) Check option to enable asynchronous processing.&lt;/li&gt;&lt;li&gt;API calls will be queued before being processed, rather than directly at the time the API call is received.&lt;/li&gt;&lt;li&gt;Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.&lt;/li&gt;&lt;li&gt;For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).&lt;/li&gt;&lt;/ul&gt; |

### Action - Data Extension - Add Multiple Records

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | &lt;ul&gt;&lt;li&gt;(Recommended) Select appropriate business unit.&lt;/li&gt;&lt;li&gt;If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.&lt;/li&gt;&lt;/ul&gt; |
| Data Extension | &lt;ul&gt;&lt;li&gt;(Required) Select data extension.&lt;/li&gt;&lt;li&gt;The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.&lt;/li&gt;&lt;li&gt;If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.&lt;/li&gt;&lt;/ul&gt; |
| Record Fields | &lt;ul&gt;&lt;li&gt;(Required) Map array type attributes to add multiple data extension records.&lt;/li&gt;&lt;li&gt;Array type attributes must be of equal length.&lt;/li&gt;&lt;li&gt;Single value attributes can be used and will apply to each record.&lt;/li&gt;&lt;/ul&gt; |
| Enable Asynchronous Processing | &lt;ul&gt;&lt;li&gt;(Optional) Check option to enable asynchronous processing.&lt;/li&gt;&lt;li&gt;API calls will be queued before being processed, rather than directly at the time the API call is received.&lt;/li&gt;&lt;li&gt;Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.&lt;/li&gt;&lt;li&gt;For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).&lt;/li&gt;&lt;/ul&gt; |

### Action - Data Extension - Delete Record

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | &lt;ul&gt;&lt;li&gt;(Recommended) Select appropriate business unit.&lt;/li&gt;&lt;li&gt;If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.&lt;/li&gt;&lt;/ul&gt; |
| Data Extension | &lt;ul&gt;&lt;li&gt;(Required) Select data extension.&lt;/li&gt;&lt;li&gt;The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.&lt;/li&gt;&lt;li&gt;If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.&lt;/li&gt;&lt;/ul&gt; |
| Record Lookup | &lt;ul&gt;&lt;li&gt;(Required) Map values to record files by which to find existing record to delete.&lt;/li&gt;&lt;/ul&gt; |
| Enable Asynchronous Processing | &lt;ul&gt;&lt;li&gt;(Optional) Check option to enable asynchronous processing.&lt;/li&gt;&lt;li&gt;API calls will be queued before being processed, rather than directly at the time the API call is received.&lt;/li&gt;&lt;li&gt;Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.&lt;/li&gt;&lt;li&gt;For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).&lt;/li&gt;&lt;/ul&gt; |

### Action - Data Extension - Update Record

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | &lt;ul&gt;&lt;li&gt;(Recommended) Select appropriate business unit.&lt;/li&gt;&lt;li&gt;If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.&lt;/li&gt;&lt;/ul&gt; |
| Data Extension | &lt;ul&gt;&lt;li&gt;(Required) Select data extension.&lt;/li&gt;&lt;li&gt;The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.&lt;/li&gt;&lt;li&gt;If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.&lt;/li&gt;&lt;/ul&gt; |
| Record Lookup | &lt;ul&gt;&lt;li&gt;(Required) Map values to record fields by which to find existing record to update.&lt;/li&gt;&lt;/ul&gt; |
| Enable Asynchronous Processing | &lt;ul&gt;&lt;li&gt;(Optional) Check option to enable asynchronous processing.&lt;/li&gt;&lt;li&gt;API calls will be queued before being processed, rather than directly at the time the API call is received.&lt;/li&gt;&lt;li&gt;Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.&lt;/li&gt;&lt;li&gt;For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).&lt;/li&gt;&lt;/ul&gt; |

### Action - Data Extension - Upsert Record

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
|:-------|:-------|
| Business Unit | &lt;ul&gt;&lt;li&gt;(Recommended) Select appropriate business unit.&lt;/li&gt;&lt;li&gt;If not specified then default option will be used, which corresponds to default business unit of configured Marketing Cloud user.&lt;/li&gt;&lt;/ul&gt; |
| Data Extension | &lt;ul&gt;&lt;li&gt;(Required) Select data extension.&lt;/li&gt;&lt;li&gt;The dropdown list of Data Extensions is listed from newest to oldest and shows a maximum of 2000 entries.&lt;/li&gt;&lt;li&gt;If a Data Extension is not shown in the dropdown list, paste the Data Extension External Key from the Data Extension details page in Salesforce, then press Enter to use that Data Extension.&lt;/li&gt;&lt;/ul&gt; |
| Record Lookup | &lt;ul&gt;&lt;li&gt;(Required) Map values to record fields by which to find existing record to update.&lt;/li&gt;&lt;/ul&gt; |
| Enable Asynchronous Processing | &lt;ul&gt;&lt;li&gt;(Optional) Check option to enable asynchronous processing.&lt;/li&gt;&lt;li&gt;API calls will be queued before being processed, rather than directly at the time the API call is received.&lt;/li&gt;&lt;li&gt;Async API calls are generally faster to complete and always return successful responses, even if underlying queued operation fails at a later point.&lt;/li&gt;&lt;li&gt;For more information, see: [Asynchronous Processing](https://architect.salesforce.com/decision-guides/async-processing).&lt;/li&gt;&lt;/ul&gt; |

## Vendor Documentation

* [Salesforce Marketing Cloud: Create an OAuth 2.0 API Integration in Enhanced Packages](https://developer.salesforce.com/docs/atlas.en-us.mc-app-development.meta/mc-app-development/create-integration-enhanced.htm)
* [Salesforce Marketing Cloud: API Integration](https://developer.salesforce.com/docs/atlas.en-us.mc-app-development.meta/mc-app-development/api-integration.htm)
* [Salesforce Marketing Cloud: Authenticate Your SOAP API Calls](https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/authenticate-soap-api.htm)
