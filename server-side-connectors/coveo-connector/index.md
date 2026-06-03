---
title: Coveo Connector Setup Guide
description: This article describes how to set up the Coveo connector.
url: https://docs.tealium.com/server-side-connectors/coveo-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Coveo API
* API Version: v15
* API Endpoint: `https://analytics.cloud.coveo.com`
* Documentation: [Coveo API](https://docs.coveo.com/en/18/api-reference/usage-analytics-write-api#tag/Analytics-API-Version-15)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Log View Event via POST| ✗| ✓|
|Log Search Event via POST| ✗| ✓|
|Log Search Event Batch via POST| ✗| ✓|
|Log Custom Event via POST| ✗| ✓|
|Log Click Event via POST| ✗| ✓|

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **API Key**  
(Required) The Coveo API key.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Log View Event via POST

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Language| (Required) The language of the end user. Must be a valid ISO 639-1 language code.|
|Location| (Required) The URL of the viewed page or component. For example, `document.location.href`.|
|Anonymous| Whether the interaction that caused the search interface to log the event was triggered by an anonymous user. Available values are: `true` and `false`.|
|Client ID|
|Content ID Key|
|Content ID Value|
|Content Type|
|Origin Context|
|Origin Level 1|
|Origin Level 2|
|Origin Level 3|
|Outcome| An indication of the quality of the event. A value of `-5` corresponds to the worst possible outcome, a value of  corresponds to a neutral outcome, and a value of `5` corresponds to the best possible outcome.|
|Referrer|
|Split Test Run Name|
|Split Test Run Version|
|Title|
|User Agent|
|User Display Name|
|Username|
|Custom Data| The user-defined dimensions and their values.&lt;br&gt; Keys can only contain alphanumeric or underscore characters. Whitespaces in keys are converted to underscores. Uppercase characters in keys are converted to lowercase characters.&lt;br&gt; The value could be any valid JSON. The value is converted to a string data type when passed to Coveo usage analytics.&lt;br&gt; We highly recommend that you create your custom dimension before adding custom data.|
|Custom Data Template Variables| Provide template variables as data input. For more information, see .&lt;br&gt; Name nested template variables with dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes.|
|Custom Data Templates| Provide templates to be referenced in Custom Data. For more information, see .&lt;br&gt; Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|

### Action — Log Search Event via POST

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Action Cause| (Required) The type of operation that triggered this event.|
|Language| (Required) The language of the end user. Must be a valid ISO 639-1 language code.|
|Query Text| (Required) The original basic query expression (`q`) in the corresponding search request.|
|Response Time| (Required) The amount of time (in milliseconds) between the moment the query that caused the search interface to log a search event was sent to the Search API and the moment the Search API returned the results. Must be greater than zero.|
|Search Query UID| (Required) The unique identifier of the event that led the search interface to log the search event. We recommend using the **Search Query UID** in the response of the corresponding search request to the Search API, or any UUID v4 of length less than or equal to 36 characters. UUIDs longer than 36 characters are truncated by the service.|
|Advanced Query|
|Anonymous| Whether the interaction that caused the search interface to log the event was triggered by an anonymous user. Available values are: `true` and `false`.|
|Client ID|
|Contextual| Indicates if the query is modified by contextual filters. For example, a query to find similar items. Available values are `true` and `false`.|
|Index ID|
|Number of Results| The number of results which were returned by the query that caused the search interface to log a search event. Must be equal to or greater than zero.|
|Origin Context| The origin of the event. This value is used to specify the original context of the user-performed action. Suggested values:`Search`, `InternalSearch`, `CommunitySearch`, or the `originLevel1` value.|
|Origin Level 1|
|Origin Level 2|
|Origin Level 3|
|Outcome| An indication of the quality of the event. A value of `-5` corresponds to the worst possible outcome, a value of 5 corresponds to the best possible outcome.|
|Query Pipeline|
|Split Test Run Name|
|Split Test Run Version|
|User Agent|
|User Display Name|
|Username|
|Facet Type| (Required) The facet data type.|
|Field| (Required) The facet field.|
|ID| (Required) The unique identifier of the facet in the search interface. Must match the following character set: `^[a-zA-Z0-9@-_]{1,60}$.`|
|State| (Required) The facet action type. Available values are: `auto_selected`, `selected`, and `excluded`.|
|Value| (Required) The name of the facet value.|
|Display Value| The display name of the facet value.|
|Facet Position| The 1-based position of the facet.|
|Title| The facet title.|
|Value Position| The 1-based position of the value in the facet.|
|User Groups| The groups that the end-user performing the event is a member of. If the request is authenticated with a search token, the service also attempts to extract the **userGroups** value from the access token that authenticated the log search event request, and logs those groups as well.|
|Custom Data| The user-defined dimensions and their values.&lt;br&gt; Keys can only contain alphanumeric or underscore characters. Whitespaces in keys are converted to underscores. Uppercase characters in keys are converted to lowercase characters.&lt;br&gt; The value could be any valid JSON. The value is converted to a string data type when passed to Coveo usage analytics.&lt;br&gt; We highly recommend that you create your custom dimension before adding custom data.|
|Custom Data Template Variables| Provide template variables as data input. For more information, see .&lt;br&gt; Name nested template variables with dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes.|
|Custom Data Templates| Provide templates to be referenced in Custom Data.  For more information, see .&lt;br&gt; Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|

### Action — Log Search Event Batch via POST

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Action Cause| (Required) The type of operation that triggered this event.|
|Language| (Required) The language of the end user. Must be a valid ISO 639-1 language code.|
|Query Text| (Required) The original basic query expression (`q`) in the corresponding search request.|
|Response Time| (Required) The amount of time (in milliseconds) between the moment the query that caused the search interface to log a search event was sent to the Search API and the moment the Search API returned the results. Must be greater than zero.|
|Search Query UID| (Required) The unique identifier of the event that led the search interface to log the search event. We recommend using the **Search Query UID** in the response of the corresponding search request to the Search API, or any UUID v4 of length less than or equal to 36 characters. UUIDs longer than 36 characters are truncated by the service.|
|Advanced Query|
|Anonymous| Whether the interaction that caused the search interface to log the event was triggered by an anonymous user. Available values are: `true` and `false`.|
|Client ID|
|Contextual| Indicates if the query is modified by contextual filters. For example, a query to find similar items. Available values are: `true` and `false`.|
|Index ID|
|Number of Results| The number of results which were returned by the query that caused the search interface to log a search event. Must be equal to or greater than zero.|
|Origin Context| The origin of the event. This value is used to specify the original context of the user-performed action. Suggested values: `Search`, `InternalSearch`, `CommunitySearch`, or the `originLevel1` value.|
|Origin Level 1|
|Origin Level 2|
|Origin Level 3|
|Outcome| An indication of the quality of the event. A value of `-5` corresponds to the worst possible outcome, a value of  corresponds to a neutral outcome, and a value of `5` corresponds to the best possible outcome.|
|Query Pipeline|
|Split Test Run Name|
|Split Test Run Version|
|User Agent|
|User Display Name|
|Username|
|Facet Type| (Required) The facet data type.|
|Field| (Required) The facet field.|
|ID| (Required) The unique identifier of the facet in the search interface. Must match the character set `^[a-zA-Z0-9@-_]{1,60}$`.|
|State| (Required) The facet action type. Available values are: `auto_selected`, `selected`, and `excluded`.|
|Value| (Required) The name of the facet value.|
|Display Value| The display name of the facet value.|
|Facet Position| The 1-based position of the facet.|
|Title| The facet title.|
|Value Position| The 1-based position of the value in the facet.|
|User Groups| The groups that the end-user performing the event is a member of. If the request is authenticated with a search token, the service also attempts to extract the **userGroups** value from the access token that authenticated the log search event request, and logs those groups as well.|
|Custom Data| The user-defined dimensions and their values.&lt;br&gt; Keys can only contain alphanumeric or underscore characters. Whitespaces in keys are converted to underscores. Uppercase characters in keys are converted to lowercase characters.&lt;br&gt; The value could be any valid JSON. The value is converted to a string data type when passed to Coveo usage analytics.&lt;br&gt; We highly recommend that you create your custom dimension before adding custom data.|
|Custom Data Template Variables| Provide template variables as data input. For more information, see .&lt;br&gt; Name nested template variables with dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes.|
|Custom Data Templates| Provide templates to be referenced in Custom Data. For more information, see .&lt;br&gt; Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|

### Action — Log Custom Event via POST

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Type| (Required) The custom event type.|
|Event Value| (Required) The custom event value.|
|Language| (Required) The language of the end user. Must be a valid ISO 639-1 language code.|
|Anonymous| Whether the interaction that caused the search interface to log the event was triggered by an anonymous user. Available values are: `true` and `false`.|
|Client ID|
|Last Search Query UID|
|Origin Context|
|Origin Level 1|
|Origin Level 2|
|Origin Level 3|
|Outcome| An indication of the quality of the event. A value of `-5` corresponds to the worst possible outcome, a value of  corresponds to a neutral outcome, and a value of `5` corresponds to the best possible outcome.|
|Split Test Run Name|
|Split Test Run Version|
|User Agent|
|User Display Name|
|Username|
|Custom Data| The user defined dimensions and their values.&lt;br&gt; Keys can only contain alphanumeric or underscore characters. Whitespaces in keys are converted to underscores. Uppercase characters in keys are converted to lowercase characters.&lt;br&gt; The value could be any valid JSON. The value is converted to a string data type when passed to Coveo usage analytics.&lt;br&gt; We highly recommend that you create your custom dimension before adding custom data.|
|Custom Data Template Variables| Provide template variables as data input. For more information, see .&lt;br&gt; Name nested template variables with dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes.|
|Custom Data Templates| Provide templates to be referenced in Custom Data. For more information, see .&lt;br&gt; Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|

### Action — Log Click Event via POST

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Action Cause| (Required) The type of operation that triggered this event.|
|Document Position| (Required) The 1-based index position of the item that was clicked in the result list. This number must take into consideration pagination settings. If the pages contain ten results each, the third item of the second page is at the position 23.|
|Document URI| (Required) The `@uri` of the item that was clicked.|
|Document URI Hash| (Required) The `@urihash` of the item that was clicked.|
|Language| (Required) The language of the end user. Must be a valid ISO 639-1 language code.|
|Search Query UID| (Required) The unique identifier of the event that led the search interface to log the search event. We recommend using the **Search Query UID** in the response of the corresponding search request to the Search API, or any UUID v4 of length less than or equal to 36 characters. UUIDs longer than 36 characters are truncated by the service.|
|Source Name| (Required) The `@source` of the item that was clicked.|
|Anonymous| Whether the interaction that caused the search interface to log the event was triggered by an anonymous user. Available values are: `true` and `false`.|
|Client ID|
|Collection Name|
|Document Author|
|Document Category|
|Document Title|
|Document URL|
|Origin Context|
|Origin Level 1|
|Origin Level 2|
|Origin Level 3|
|Outcome| An indication of the quality of the event. A value of `-5` corresponds to the worst possible outcome, a value of  corresponds to a neutral outcome, and a value of `5` corresponds to the best possible outcome.|
|Query Pipeline|
|Ranking Modifier|
|Split Test Run Name|
|Split Test Run Version|
|User Agent|
|User Display Name|
|Username|
|Custom Data| The user defined dimensions and their values.&lt;br&gt; Keys can only contain alphanumeric or underscore characters. Whitespaces in keys are converted to underscores. Uppercase characters in keys are converted to lowercase characters.&lt;br&gt; The value could be any valid JSON. The value is converted to a string data type when passed to Coveo usage analytics.&lt;br&gt; We highly recommend that you create your custom dimension before adding custom data.|
|Custom Data Template Variables| Provide template variables as data input. For more information, see .&lt;br&gt; Name nested template variables with dot notation. For example, `items.name`.&lt;br&gt; Nested template variables are typically built from data layer list attributes.|
|Custom Data Templates| Provide templates to be referenced in Custom Data. For more information, see .&lt;br&gt; Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|