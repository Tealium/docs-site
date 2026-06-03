---
title: Splunk Connector Setup Guide
description: This article describes how to set up the Splunk connector.
url: https://docs.tealium.com/server-side-connectors/splunk-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Splunk token**: The HTTP Event Collector token. Create a token at **Settings &gt; Data Inputs &gt; HTTP Event Collector**.
* **Host**: The Splunk instance that runs HTTP Event Collector. For example, `https://hec.example.com`.
* **Port**: (Optional) The HTTP Event Collector port number.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Entire Event Data | ✗ | ✓ |
| Send Entire Event Data (Batch) | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Custom Event Data (Batch) | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |
| Send Entire Event | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Entire Visitor Data (Batch) | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data (Batch) | ✓ | ✗ |

Enter a name for the action and select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Send Entire Event Data

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |
| Print Attribute Names | If attribute names get updated, the names in the payload will reflect the update. |

### Send Entire Event Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |
| Print Attribute Names | If attribute names get updated, the names in the payload will reflect the update. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. Default is `15` minutes. |

### Send Custom Event Data

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Custom Message Definition | Provide values to construct message data. For template support, reference the template name to generate message data from the template. If using a template, map it to Custom Message Definition. Any other key-value pairs will be ignored if the template is used.|
|Template Variables|&lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected into supported fields by name with double curly braces. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

### Send Custom Event Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Custom Message Definition | Provide values to construct message data. For template support, reference the template name to generate message data from the template. If using a template, map it to Custom Message Definition. Any other key-value pairs will be ignored if the template is used.|
|Template Variables|&lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected into supported fields by name with double curly braces. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. Default is `15` minutes. |

### Send Entire Visitor Data

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |
| Include Current Visit Data With Visitor Data | Add the current visit data to the payload. This includes event visit data, unless Exclude Current Visit Event Data is checked. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Print Attribute Names | If attribute names get updated, the names in the payload will reflect the update. |

### Send Entire Visitor Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Print Attribute Names | If attribute names get updated, the names in the payload will reflect the update. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. Default is `15` minutes. |

### Send Custom Visitor Data

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Custom Message Definition | Provide values to construct message data. For template support, reference the template name to generate message data from the template. If using a template, map it to Custom Message Definition. Any other key-value pairs will be ignored if the template is used.|
|Template Variables|&lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected into supported fields by name with double curly braces. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

### Send Custom Visitor Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Custom Message Definition | Provide values to construct message data. For template support, reference the template name to generate message data from the template. If using a template, map it to Custom Message Definition. Any other key-value pairs will be ignored if the template is used.|
|Template Variables|&lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected into supported fields by name with double curly braces. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. Default is `15` minutes. |

### Send Log Event

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Custom Message Definition | Provide values to construct message data. For template support, reference the template name to generate message data from the template. If using a template, map it to Custom Message Definition. Any other key-value pairs will be ignored if the template is used.|
|Template Variables|&lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected into supported fields by name with double curly braces. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

### Send Entire Log Event

#### Metadata

| **Parameter** | **Description** |
| --- | --- |
| Splunk request channel | Channel identifier when the indexer acknowledgment is enabled. |
| Time | The event time. |
| Host | The host value to assign to the event data. |
| Source | The source value to assign to the event data. For example, if you&#39;re sending data from an app you&#39;re developing, set this key to the name of the app. |
| Source type | The source type value to assign to the event data. |
| Index | The name of the index used to index the event data. The index you specify here must be in the list of allowed indexes if the token has the indexes parameter set. |
| Custom Fields | The fields key isn&#39;t applicable to raw data. This key specifies a JSON object that contains a flat (not nested) list of explicit custom fields to be defined at index time. Requests containing the `fields` property must be sent to the `/collector/event` endpoint, or else they aren&#39;t indexed. For more information, see [Splunk Enterprise: Automate indexed field extractions with HTTP Event Collector](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-with-http-event-collector/automate-indexed-field-extractions-with-http-event-collector). |
