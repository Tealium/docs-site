---
title: About attributes
description: This article provides an overview of how attributes are used and steps to add, duplicate, or remove an attribute.
url: https://docs.tealium.com/server-side/attributes/about/
---
Attributes are the foundation of your implementation and are used to define your customers&#39; behaviors and interactions with your brand. Attributes define the properties of a visitor, a visitor&#39;s session, and events collected. Common examples of attributes include Email Address, Member ID, Product Category, Date of Last Visit, and Active Browser.

Each profile can contain a maximum of 500 visitor and visit attributes. You can see your current attribute total on the **Visit/Visitor Attributes** screen:

![](/images/server-side/attributes/count-of-attributes.png)

 If you need more than 500 attributes in a profile, contact your Customer Success Manager. 

## Scope

Scope refers to how long an attribute persists in real-time. The following table lists supported scopes:

|Scope| Description / Examples| Uses|
|---| ---| ---|
| Event |  Attributes associated with individual events that describe the page, content, and real-time actions being taken by a customer. Examples: Page Name, Product Price, Event Name, Order Total, etc. | **Attribute Sources**&lt;br&gt; Event attributes are sourced from the following:&lt;br&gt; &lt;ul&gt;&lt;li&gt;**Universal Variables** [Universal Data Object]()&lt;/li&gt;&lt;li&gt;**Javascript Page Variables** Global JavaScript variables (browser)&lt;/li&gt;&lt;li&gt;**HTML Metadata** Metadata tag (browser)&lt;/li&gt;&lt;li&gt;**First-Party Cookies** Browser cookie&lt;/li&gt;&lt;li&gt;**Querystring Parameters** Current page&#39;s URL querystring (browser)&lt;/li&gt;&lt;/ul&gt; |
| Visit |  Attributes about a particular visit (or session). Data persists for the length of the visit. Examples: Visit Duration, Browser Used, Referring URL, and Carted Products. |  These attributes represent visitor activity from the current session. Visit attributes persist for the length of the session. See [Session Length]() for more detail. |
| Visitor |  Attributes about a particular visitor across all visits. Examples: Email Address, Member ID, Lifetime Order Total, and Category Views. |  This data follows a visitor from session to session and across different devices. Visitor data persists even after the current visit ends. |
| Omnichannel | For importing offline data through the Omnichannel service. This scope does not require a data type. |  Omnichannel attributes are defined when you define your file imports. Omnichannel is a legacy scope and has been replaced with [File Import](). |

### Session length

Session length determines when a visit ends after it becomes inactive. When a visit reaches the session length without a new event, the visit ends and AudienceStream performs end-of-visit processing. The next event from the visitor starts a new visit. AudienceStream has a maximum visit length of 24 hours, regardless of event activity.

For more information, see [Server-side session length]().

## Data types

Attributes come in a variety of types, from a basic number to the more powerful tally and badge. The data type determines the format in which the attribute value is stored.

The following data types are supported:

|Data type| Description|
|---| ---|
|[Number]()| Stores numerical values such as order total, lifetime event count, or number of days since last visit.|
|[String]()| Stores text values such as first/last name, address, favorite product, and page name.|
|[Boolean]()| Stores only one of two values: &#39;true&#39; and &#39;false&#39;. Boolean can be used for indicating the status of a visitor action or visit.|
|[Array of Numbers]()| Stores multiple numeric values as an array. The array may contain unique or duplicate numeric values.|
|[Array of Strings]()| Stores multiple string values as an array. The array may contain unique or duplicate string values.|
|[Array of Booleans]()| Stores multiple Boolean values as an array. The array may contain unique or duplicate Boolean values.|
|[Tally]()| Stores one or more key-value pairs.|
|[Set of Strings]()| Stores a collection of unique string values as a set.|
|[Date]()| Stores the date of an event, a visitor event, or particular visit.|
|[Funnel]()| Tracks the status of every step in a multi-step event, such as payment funnel and registration.|
|[Timeline]()| Records all occurrences of a visitor action within a time range.|
|[Badge]()| Assigns a visual mark or symbol to visitors who meet certain criteria or browsing behavior.|
|[Visitor ID]()| Stores visitor&#39;s unique traits as their secondary identifier.|

### Scope and data type matrix

This matrix shows which data types are available for each scope.

|Data type| Visitor scope| Visit scope| Event scope|
|---| ---| ---| ---|
|Number| ✔| ✔| ✔|
|String| ✔| ✔| ✔|
|Boolean| ✔| ✔| ✔|
|Array of Numbers| ✔| ✔| ✔|
|Array of Strings| ✔| ✔| ✔|
|Array of Booleans| ✔| ✔| ✔|
|Tally| ✔| ✔|
|Set of Strings| ✔| ✔|
|Date| ✔| ✔| ✔|
|Funnel| ✔| ✔|
|Timeline| ✔| ✔|
|Badge| ✔|
|Visitor ID| ✔|

## Attribute IDs

All event, visit, and visitor attributes have a unique attribute identifier. The value of this ID may influence the order in which enrichments run and may be required for more complex data source or visitor stitching configurations.

You can find the attribute ID next to the attribute name in the attribute list or within the expanded details.

**Event Attributes**
![](/images/server-side/event-attribute-id.png)  

**Visit/Visitor Attributes**
![](/images/server-side/attributes/attribute-details-slideout-id.png)

## Size limits

Most attributes for EventStream and AudienceStream have storage capacity limits and specific behaviors for when those limits are exceeded. Note that the entire visitor profile has a limit of 400 KB compressed and encrypted.

## Event limits

To protect both the Tealium platform and individual customer accounts, AudienceStream has a limit of 10,000 events per visit.

If a visitor reaches 10,000 events in a single visit, the visitor is permanently banned. When a visitor is banned, the visitor profile is deleted and all future events for the visitor ID, or any IDs that stitch to it, are ignored in both AudienceStream and EventStream. In addition, log messages are written that include the account, profile, visitor ID, and an indication that a ban occurred.

The ban is permanent, or until maintenance is performed by the Tealium Operations team to purge the banned visitors collection. If you believe a visitor has been banned incorrectly, or you have a visitor that needs to be removed from the banned list, contact Tealium Support.

If a permanent visitor ban is removed and the visitor again exceeds the 10,000 events in a visit limit, another ban will occur.

## Event attributes

|Attribute| Storage capacity limits| Exceeded limit behavior|
|---| ---| ---|
|**Strings**| 1,500 characters| Strings are truncated to 1,500 characters if they are longer than the limit.|
|**Arrays of any type**| 30,000 entries | If an attribute is set or updated to exceed the limit, the attribute is trimmed to 30,000 entries and set. |
|**Dates**|  Minimum: &#34;-292275055-05-16T16:47:04.192Z&#34; maximum: &#34;&#43;292278994-08-17T07:12:55.807Z&#34; |
|**Numbers**| Represented with `java.lang.Number`, which has dynamic precision.|

## Visit/visitor attributes

|Attribute| Storage capacity limits| Exceeded limit behavior|
|---| ---| ---|
|**Strings**| 1,000 characters| If an enrichment results in a string larger than 1,000 characters, the value is not saved.|
|**Timelines**| 100 entries|  Earliest entries are discarded when the limit is reached (First-In, First-Out). For example, if a timeline contains 100 entries, and a new entry is added, the first entry is deleted. |
|**Tallies**| 30,000 entries. | If an attribute is set or updated to exceed the limit, the attribute is trimmed to 30,000 entries and set. |
|**Arrays of any type**| 30,000 entries. | If an attribute is set or updated to exceed the limit, the attribute is trimmed to 30,000 entries and set. |
|**Set of Strings**| 30,000 entries. | If an attribute is set or updated to exceed the limit, the attribute is trimmed to 30,000 entries and set. |
|**Dates**|  Minimum: &#34;-292275055-05-16T16:47:04.192Z&#34; Maximum: &#34;&#43;292278994-08-17T07:12:55.807Z&#34; |
|**Numbers**|Represented with `java.lang.Number`, which has dynamic precision.| |
|**Visitor ID**| 2 KB| If the visitor ID is over 2 KB, the record is not saved. |
|**Funnel**| No limits\*| |

\*No limits, but the attribute is still limited by the maximum size of the profile after encryption and compression (400 KB).

## Connect client-side and server-side

### Import attributes from iQ Tag Management

An imported attribute is a variable that was originally created in the corresponding Tealium iQ profile. Tealium iQ variables are automatically exported to the server-side profile of the same name as event-scoped attributes. These attributes use the **Any** data type. When you modify a variable in Tealium iQ (and publish to **prod**), the changes are instantly applied to the matching attribute in EventStream.

Imported attributes are not editable. You must use Tealium iQ to manage them.

![](/images/server-side/imported-tealium-iq-variables1.png)  
![](/images/server-side/imported-tealium-iq-variables2.png)  

Imported attributes only contain data if you use the [Tealium Collect tag]() to gather that data.

You cannot enrich imported attributes directly. However, you can duplicate the imported attribute, enrich the duplicate attribute with the imported attribute&#39;s value, and then further enrich the duplicate attribute as needed.

#### Troubleshooting

If variables from Tealium iQ do not appear in EventStream, verify that the Tealium iQ variables are in the Tealium iQ profile that corresponds to the server-side profile and that the variables have been saved and published. Make sure you refresh the EventStream page in the browser after publishing variable changes. If you need assistance with making Tealium iQ variables available in server-side, contact Tealium Support.

### Export attributes to iQ Tag Management

To make server-side attributes available as iQ Tag Management variables, use Data Layer Enrichment.

For more information, see .

## Restricted data

This property is used to identify attributes that contain data that should not be sent out of the system, such as third-party [Connectors]() or [DataAccess](). Learn more about [Restricted Data]().

## Rules

A rule provides additional logic for the purpose of triggering an enrichment. For more information about how rules work and when to use them, see [About enrichment rules]().

* To apply a predefined rule, make a selection from the drop-down list and click **Add Rule**.  
      Creating a new rule through the enrichments dialog box automatically applies it to the enrichment.

* To apply a new rule, click **Create Rule**.  
      ![](/images/server-side/whiteui-using-attributes-rules.png)

## Preloaded attributes

AudienceStream and EventStream contain a set of preloaded event, visit, and visitor attributes that are preconfigured with statistical information to help you determine useful information about each visitor, visit, or event.

![](/images/server-side/attributes/preloaded-attribute-filter.png)

For more information about these attributes, see [Preloaded attributes]().

## Dependencies

Dependencies are all of the objects that are dependent on this attribute, such as:

* Attributes
* Audiences
* Segments
* Connectors
* Rules
* Predict
* Data sources

You cannot delete an attribute if a dependency includes that attribute.

To view an attribute&#39;s dependencies, click the attribute in the **Attributes** table and then click the **Dependencies** tab. To view a dependency&#39;s details, click **Go To**.

![](/images/server-side/ea-visitor-dependencies.png)
