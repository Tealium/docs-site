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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

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

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10
* Max time since oldest request: 1 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Mailing List|  &lt;ul&gt;&lt;li&gt;The ID of the list the subscriber should be added to.&lt;/li&gt;&lt;li&gt;If you know mailing list ID, you can enter it as Custom Value.&lt;/li&gt;&lt;li&gt;Select the list the subscriber should be added to, or provide list ID directly.&lt;/li&gt;&lt;li&gt;For more information, see [SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber).&lt;/li&gt;&lt;/ul&gt; |
|Create Mode|  &lt;ul&gt;&lt;li&gt;If the subscriber&#39;s account already exists and this parameter is set to &#34;Create or Update&#34;, then the subscriber&#39;s data will be updated.&lt;/li&gt;&lt;li&gt;It is not possible to update existing subscriber when subscribing with double opt-in.&lt;/li&gt;&lt;/ul&gt; |
|Country code|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s country code.&lt;/li&gt;&lt;/ul&gt; |
|Desired format|  &lt;ul&gt;&lt;li&gt;The format the subscriber wants.&lt;/li&gt;&lt;/ul&gt; |
|Email address|  &lt;ul&gt;&lt;li&gt;(Required) The subscriber&#39;s email address.&lt;/li&gt;&lt;/ul&gt; |
|External ID|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s external ID.&lt;/li&gt;&lt;/ul&gt; |
|Name|  &lt;ul&gt;&lt;li&gt;The name of the subscriber.&lt;/li&gt;&lt;/ul&gt; |
|Password|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s password.&lt;/li&gt;&lt;/ul&gt; |
|Phone number|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s phone number.&lt;/li&gt;&lt;/ul&gt; |
|Demographic Data|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s list of demographic data fields.&lt;/li&gt;&lt;li&gt;The keys and possible values of data fields are defined in the APSIS account management console.&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables for Demographic Data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) provide templates to be referenced in Demographic Data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update Subscriber (Queued)

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10
* Max time since oldest request: 1 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Country code|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s country code.&lt;/li&gt;&lt;/ul&gt; |
|Desired format|  &lt;ul&gt;&lt;li&gt;The format the subscriber wants.&lt;/li&gt;&lt;/ul&gt; |
|Email address|  &lt;ul&gt;&lt;li&gt;(Required) The subscriber&#39;s email address&lt;/li&gt;&lt;/ul&gt; |
|Name|  &lt;ul&gt;&lt;li&gt;The name of the subscriber.&lt;/li&gt;&lt;/ul&gt; |
|Password|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s password.&lt;/li&gt;&lt;/ul&gt; |
|Phone number|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s phone number.&lt;/li&gt;&lt;/ul&gt; |
|User ID|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s ID.&lt;/li&gt;&lt;li&gt;For more information, see [Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)&lt;/li&gt;&lt;/ul&gt; |
|Demographic Data|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s list of demographic data fields.&lt;/li&gt;&lt;li&gt;The keys and possible values of data fields are defined in the account management console.&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables for Demographic Data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) provide templates to be referenced in Demographic Data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

### Action - Add Subscriber to Mailing List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Mailing List|  &lt;ul&gt;&lt;li&gt;Select the list the subscriber should be added to, or provide list ID directly.&lt;/li&gt;&lt;li&gt;For more information, see [SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber).&lt;/li&gt;&lt;li&gt;If you know mailing list ID, you can enter it as Custom Value&lt;/li&gt;&lt;/ul&gt; |
|Subscriber&#39;s Email|  &lt;ul&gt;&lt;li&gt;(Required) The subscriber&#39;s email address&lt;/li&gt;&lt;/ul&gt; |
|Subscriber&#39;s ID|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s ID.&lt;/li&gt;&lt;li&gt;For more information, see [Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)&lt;/li&gt;&lt;/ul&gt; |

### Action - Remove Subscriber from Mailing List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Mailing List|  &lt;ul&gt;&lt;li&gt;Select the list the subscriber should be added to, or provide list ID directly.&lt;/li&gt;&lt;li&gt;For more information, see [SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber).&lt;/li&gt;&lt;li&gt;If you know mailing list ID, you can enter it as Custom Value&lt;/li&gt;&lt;/ul&gt; |
|Subscriber&#39;s Email|  &lt;ul&gt;&lt;li&gt;(Required) The subscriber&#39;s email address&lt;/li&gt;&lt;/ul&gt; |
|Subscriber&#39;s Id|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s ID.&lt;/li&gt;&lt;li&gt;For more information, see [Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)&lt;/li&gt;&lt;/ul&gt; |

### Action - Delete Subscriber (Queued)

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10
* Max time since oldest request: 1 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Subscriber&#39;s Email|  &lt;ul&gt;&lt;li&gt;(Required) The subscriber&#39;s email address&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Transactional Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Transactional Project|  &lt;ul&gt;&lt;li&gt;Select the transactional project.&lt;/li&gt;&lt;li&gt;ID of the project.&lt;/li&gt;&lt;li&gt;For more information, see [Send Transactional Email](http://se.apidoc.anpdm.com/Browse/Method/TransactionalService/SendTransactionalEmail)&lt;/li&gt;&lt;/ul&gt; |
|Disable inactive projects|  &lt;ul&gt;&lt;li&gt;True or false indicating if sending should be allowed when project is inactive&lt;/li&gt;&lt;li&gt;Default value is **true**.&lt;/li&gt;&lt;/ul&gt; |
|Country code|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s country code.&lt;/li&gt;&lt;/ul&gt; |
|Demographic data for HTML|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s list of demographic data fields.&lt;/li&gt;&lt;li&gt;The keys and possible values of data fields are defined in the APSIS account management console.&lt;/li&gt;&lt;/ul&gt; |
|Desired format|  &lt;ul&gt;&lt;li&gt;The format the subscriber wants.&lt;/li&gt;&lt;/ul&gt; |
|Email address|  &lt;ul&gt;&lt;li&gt;(Required) The subscriber&#39;s email address&lt;/li&gt;&lt;/ul&gt; |
|External ID|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s external ID.&lt;/li&gt;&lt;/ul&gt; |
|Name|  &lt;ul&gt;&lt;li&gt;The name of the subscriber.&lt;/li&gt;&lt;/ul&gt; |
|Phone number|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s phone number.&lt;/li&gt;&lt;/ul&gt; |
|Send Date|  &lt;ul&gt;&lt;li&gt;Send date.&lt;/li&gt;&lt;/ul&gt; |
|Sending Type|  &lt;ul&gt;&lt;li&gt;Possible values:  &lt;ul&gt;&lt;li&gt;**m** - marketing&lt;/li&gt;&lt;li&gt;**t** - transactional (default)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Demographic Data|  &lt;ul&gt;&lt;li&gt;The subscriber&#39;s list of demographic data fields.&lt;/li&gt;&lt;li&gt;The keys and possible values of data fields are defined in the APSIS account management console.&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables for Demographic Data.&lt;/li&gt;&lt;li&gt;&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) provide templates to be referenced in Demographic Data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |