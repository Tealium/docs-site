---
title: APSIS Connector Setup Guide
description: This article describes how to set up the APSIS connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/apsis-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Create Subscriber and Add to Mailing List (Queued)| ✓| ✗|
|Update Subscriber (Queued)| ✓| ✗|
|Add Subscriber to Mailing List| ✓| ✗|
|Remove Subscriber from Mailing List| ✓| ✗|
|Delete Subscriber (Queued)| ✓| ✗|
|Send Transactional Email| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**
  * To get an API key, log in to your APSIS Pro account and select the **Account** section.
  * Find the **API Keys** link and click to generate a new API key.
  * One account can have multiple API keys.
  * You can manage your keys using the **Account Settings** section in APSIS Pro.
  * For more information, see [APSIS: Getting Started](http://se.apidoc.anpdm.com/Help/GettingStarted/Getting%20started)

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Create Subscriber and Add to Mailing List (Queued)

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10
* Max time since oldest request: 1 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Mailing List|  <ul><li>The ID of the list the subscriber should be added to.</li><li>If you know mailing list ID, you can enter it as Custom Value.</li><li>Select the list the subscriber should be added to, or provide list ID directly.</li><li>For more information, see [SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber).</li></ul> |
|Create Mode|  <ul><li>If the subscriber's account already exists and this parameter is set to "Create or Update", then the subscriber's data will be updated.</li><li>It is not possible to update existing subscriber when subscribing with double opt-in.</li></ul> |
|Country code|  <ul><li>The subscriber's country code.</li></ul> |
|Desired format|  <ul><li>The format the subscriber wants.</li></ul> |
|Email address|  <ul><li>(Required) The subscriber's email address.</li></ul> |
|External ID|  <ul><li>The subscriber's external ID.</li></ul> |
|Name|  <ul><li>The name of the subscriber.</li></ul> |
|Password|  <ul><li>The subscriber's password.</li></ul> |
|Phone number|  <ul><li>The subscriber's phone number.</li></ul> |
|Demographic Data|  <ul><li>The subscriber's list of demographic data fields.</li><li>The keys and possible values of data fields are defined in the APSIS account management console.</li></ul> |
|Template Variables|  <ul><li>(Optional) Provide template variables for Demographic Data.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Templates|  <ul><li>(Optional) provide templates to be referenced in Demographic Data.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |

### Action - Update Subscriber (Queued)

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10
* Max time since oldest request: 1 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Country code|  <ul><li>The subscriber's country code.</li></ul> |
|Desired format|  <ul><li>The format the subscriber wants.</li></ul> |
|Email address|  <ul><li>(Required) The subscriber's email address</li></ul> |
|Name|  <ul><li>The name of the subscriber.</li></ul> |
|Password|  <ul><li>The subscriber's password.</li></ul> |
|Phone number|  <ul><li>The subscriber's phone number.</li></ul> |
|User ID|  <ul><li>The subscriber's ID.</li><li>For more information, see [Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)</li></ul> |
|Demographic Data|  <ul><li>The subscriber's list of demographic data fields.</li><li>The keys and possible values of data fields are defined in the account management console.</li></ul> |
|Template Variables|  <ul><li>(Optional) Provide template variables for Demographic Data.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Templates|  <ul><li>(Optional) provide templates to be referenced in Demographic Data.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |

### Action - Add Subscriber to Mailing List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Mailing List|  <ul><li>Select the list the subscriber should be added to, or provide list ID directly.</li><li>For more information, see [SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber).</li><li>If you know mailing list ID, you can enter it as Custom Value</li></ul> |
|Subscriber's Email|  <ul><li>(Required) The subscriber's email address</li></ul> |
|Subscriber's ID|  <ul><li>The subscriber's ID.</li><li>For more information, see [Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)</li></ul> |

### Action - Remove Subscriber from Mailing List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Mailing List|  <ul><li>Select the list the subscriber should be added to, or provide list ID directly.</li><li>For more information, see [SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber).</li><li>If you know mailing list ID, you can enter it as Custom Value</li></ul> |
|Subscriber's Email|  <ul><li>(Required) The subscriber's email address</li></ul> |
|Subscriber's Id|  <ul><li>The subscriber's ID.</li><li>For more information, see [Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)</li></ul> |

### Action - Delete Subscriber (Queued)

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10
* Max time since oldest request: 1 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Subscriber's Email|  <ul><li>(Required) The subscriber's email address</li></ul> |

### Action - Send Transactional Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Transactional Project|  <ul><li>Select the transactional project.</li><li>ID of the project.</li><li>For more information, see [Send Transactional Email](http://se.apidoc.anpdm.com/Browse/Method/TransactionalService/SendTransactionalEmail)</li></ul> |
|Disable inactive projects|  <ul><li>True or false indicating if sending should be allowed when project is inactive</li><li>Default value is **true**.</li></ul> |
|Country code|  <ul><li>The subscriber's country code.</li></ul> |
|Demographic data for HTML|  <ul><li>The subscriber's list of demographic data fields.</li><li>The keys and possible values of data fields are defined in the APSIS account management console.</li></ul> |
|Desired format|  <ul><li>The format the subscriber wants.</li></ul> |
|Email address|  <ul><li>(Required) The subscriber's email address</li></ul> |
|External ID|  <ul><li>The subscriber's external ID.</li></ul> |
|Name|  <ul><li>The name of the subscriber.</li></ul> |
|Phone number|  <ul><li>The subscriber's phone number.</li></ul> |
|Send Date|  <ul><li>Send date.</li></ul> |
|Sending Type|  <ul><li>Possible values:  <ul><li>**m** - marketing</li><li>**t** - transactional (default)</li></ul> </li></ul> |
|Demographic Data|  <ul><li>The subscriber's list of demographic data fields.</li><li>The keys and possible values of data fields are defined in the APSIS account management console.</li></ul> |
|Template Variables|  <ul><li>(Optional) Provide template variables for Demographic Data.</li><li>>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Templates|  <ul><li>(Optional) provide templates to be referenced in Demographic Data.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |