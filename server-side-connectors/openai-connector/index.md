---
title: OpenAI Connector Setup Guide
description: Set up the OpenAI connector to send a prompt with Tealium event or visitor data and return model responses for real-time enrichment.
url: https://docs.tealium.com/server-side-connectors/openai-connector/
---
For an overview of how AI connectors work and guidance on when to use an AI connector or Tealium functions, see [AI connectors and Tealium functions]().

## How it works

This connector invokes an OpenAI model with your custom prompt and mapped Tealium data, then sends the response as a JSON event to Tealium Collect for real-time enrichment.

Use the OpenAI connector for targeted, high-value interactions rather than high-volume events. Excessive usage may result in rate limits or increased API costs in your OpenAI account and add to your inbound Tealium event volume.

## Usage and cost considerations

Before activating the OpenAI connector, review your OpenAI account limits, usage tier, and pricing model. The connector can generate a high volume of requests depending on your event and audience triggers, which may result in unexpected usage or overage costs.

For more information, see [OpenAI Developers: Rate limits](https://developers.openai.com/api/docs/guides/rate-limits).

**Key considerations**

* **Usage tier and rate limits**  
  OpenAI enforces rate limits based on your account tier, measured in requests per minute and tokens per minute. High-frequency events or large audiences can quickly reach these limits, causing throttling or failed requests.
* **Pricing and token consumption**  
  OpenAI charges based on the number of input and output tokens processed by the model. Longer prompts, larger payloads, and higher-capacity models increase per‑request cost. Review pricing for the specific models you plan to use.
* **Monthly spend and budget controls**  
  Set usage caps or alerts in your OpenAI account to prevent unplanned spend. Without limits in place, automated workflows can accumulate significant costs.
* **Trigger volume**  
  Avoid attaching the connector to high-volume, low-value events such as page views. Use events or audiences that represent meaningful customer actions and occur at manageable frequency.

## Best practices

To get the most value from this connector, follow these guidelines to build effective solutions:

* **High-value triggers**: Choose event feed or audience triggers that contain rich context or meaningful customer input. Triggering this connector for a high-volume use case may incur additional costs in your OpenAI account or lead to failed requests.
* **Be specific**: Include details about what the model evaluates and how it determines each output field.
* **Prompt parameters**: Map Tealium attributes to placeholder names in the **Prompt Parameters** section, then reference them in your prompt using double curly braces. For example, if you map an attribute to the placeholder `product_id`, write `{{product_id}}` in your prompt.

## API information

This connector uses the following vendor API:

* API Name: OpenAI API
* API Version: v1
* API Endpoint: `https://api.openai.com/v1`
* Documentation: [OpenAI API](https://platform.openai.com/docs/api-reference)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **API Key**: The OpenAI API key used to authenticate requests. The key must have permission to create responses (model inference) with either **All** or **Restricted** permission. It cannot have **Read Only** permission. For more information, see [OpenAI: Assign API Key Permissions](https://help.openai.com/en/articles/8867743-assign-api-key-permissions).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Prompt to OpenAI | ✓ | ✓ |
| Send Prompt to OpenAI (Deprecated) | ✓ | ✓ |

### Send Prompt to OpenAI

This action sends your custom prompt and mapped Tealium data to an OpenAI model. The connector sends the structured JSON output to Tealium Collect for real-time enrichment.

#### Parameters

| Parameter | Description |
| --- | --- |
| Model | Select the OpenAI model to use for this prompt, for example **gpt-4.1-mini** or **gpt-4.1**.&lt;br&gt;We recommend using a model optimized for structured output (JSON) that meets your performance and cost requirements. |

#### Tealium Context

The connector automatically includes Tealium identifiers (`tealium_account`, `tealium_profile`, `tealium_visitor_id`) in the prompt sent to the AI model and in the structured output schema. These values come from the current event. You do not need to reference them in the prompt.

Use this mapping section to set the required `tealium_event` value and optionally override the default identity values.

| Vendor parameter | Description |
| --- | --- |
| Tealium Event | (Required) The `tealium_event` value included in the AI response returned to Tealium. The connector uses this event name when forwarding the AI result back into Tealium. |
| Tealium Datasource | The datasource key associated with this connector. |
| Tealium Account | Overrides the account value. Defaults to the current event value. |
| Tealium Profile | Overrides the profile value. Defaults to the current event value. |
| Tealium Visitor ID | Overrides the visitor ID. Defaults to the current event value. |

#### Prompt Parameters

Use this mapping section to pass Tealium attribute values into your prompt. Map a Tealium attribute in the left column to a placeholder name in the right column. Reference the placeholder name in the **Prompt** field using double curly braces.

For example, if you map the attribute `product_review_text` to the placeholder name `review_text`, write `{{review_text}}` in your prompt to insert the attribute value at runtime.

#### Event Payload

Enable **Add Event Payload** to include the full event payload in the prompt template as `{{event_payload}}`.

#### Prompt

Enter the prompt to send to the selected model.

* Reference mapped placeholder names using double curly braces, such as `{{review_text}}`, `{{product_name}}`.
* Reference `{{event_payload}}` after you enable **Add Event Payload**.
* Describe how the model determines and sets each output field.
* Do not include JSON formatting instructions (for example, &#34;Return only JSON&#34;). The connector enforces the JSON structure automatically through the **Structured Output** mapping.

#### Advanced Model Settings

| Parameter | Description |
| --- | --- |
| temperature | Controls randomness and creativity. |
| max_output_tokens | Maximum number of tokens the model can generate. |
| max_tool_calls | The maximum number of built-in tool calls processed in a response. |
| top_p | Controls diversity by sampling only from the top-p probability mass. |
| parallel_tool_calls | Whether to allow the model to run tool calls in parallel. Defaults to `true`. |
| prompt_cache_key | Used by OpenAI to cache responses for similar requests to optimize your cache rate. |
| service_tier | Specifies the processing type used for serving the request. |
| tool_choice | Controls how the model selects which tool (or tools) to use when generating a response. |

#### Structured Output (JSON Schema)

Use this section to define the fields the AI model returns in its response. Unlike the other mapping sections, **Structured Output** does not map Tealium attributes. Instead, you define the output field names, data types, and whether they are required.

The connector sends these definitions to OpenAI as a JSON schema using `text.format`. This requires the model to return structured JSON that matches your schema instead of free-form text. The connector then parses the response and forwards it to Tealium Collect as an event. You must define at least one field.

The schema automatically includes the Tealium context fields: `tealium_account`, `tealium_profile`, `tealium_visitor_id`, `tealium_event`.

Each row defines one output field with three inputs:

| Input | Description |
| --- | --- |
| Required / Optional | Select **Required** to require the model to return this field. Select **Optional** to include the field in the schema but not require it. Defaults to required. |
| Data type | Data type for the output field: `string`, `integer`, `number`, or `boolean`. Defaults to `string`. The data type tells the model what format to use for the value. A mismatched type may cause validation to fail. |
| Attribute name | Name of the output field. This name appears as a key in the JSON response. Create a matching event attribute to capture the value for enrichment. |

#### Debug Mode

Select **Enable Debug Mode** to accept the raw OpenAI response without forwarding it to Tealium Collect. Use Trace to validate the response format before enabling full processing.

#### Example: Classify review sentiment

This example shows a configured action that classifies customer product review sentiment.

**Trigger**: An event feed fires when a `product_review_submitted` event occurs.

**Tealium Context**:

| Event Attribute | Vendor Parameter |
| --- | --- |
| `ai_response` | Tealium Event |

**Prompt Parameters**:

| Tealium Attribute | Placeholder Name |
| --- | --- |
| `product_review_text` | `review_text` |
| `product_name` | `product_name` |

**Event Payload**: Disabled.

**Prompt**:

```wrap
A customer submitted a review for {{product_name}}:

{{review_text}}

Classify the customer&#39;s sentiment as one of: &#34;dissatisfied&#34;, &#34;neutral&#34;, or &#34;satisfied&#34;. Provide a confidence score between 0 and 1.
```

**Structured Output (JSON Schema)**:

| Required / Optional | Data type | Attribute name |
| --- | --- | --- |
| Required | string | `ai_review_sentiment` |
| Required | number | `ai_confidence_score` |

**Result**: The connector returns a JSON event to Tealium Collect containing `tealium_event: &#34;ai_response&#34;`, `ai_review_sentiment`, and `ai_confidence_score`. Create matching event attributes to capture these values for enrichment.

### Send Prompt to OpenAI (Deprecated)

This action invokes an OpenAI model with your custom prompt and mapped Tealium data. If the model responds with a valid JSON event object, this event is sent back to your account where you can capture the generated value in a real-time enrichment.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Model | Select the OpenAI model to use for this prompt, for example **gpt-4.1-mini** or **gpt-4.1**.&lt;br&gt;We recommend using a model optimized for structured output (JSON) that supports your performance and cost requirements. For more information, see [OpenAI Developers: Production best practices](https://developers.openai.com/api/docs/guides/production-best-practices). |
| Add Event Payload | (Available for event actions) Check this box to include the event payload for use in the prompt template as variable `{{event_payload}}`. |
| Add Visitor Profile | (Available for audience actions) Check this box to include the visitor profile for use in the prompt template as variable `{{visitor_profile}}`. |
| Add Current Visit | (Available for audience actions) Check this box to include the current visit within the variable `{{visitor_profile}}`. |
| Prompt | Enter the prompt to send to the selected OpenAI model. Follow these guidelines to ensure consistent and machine-readable output:&lt;br&gt;&lt;br&gt;Use **double curly braces** (`{{ }}`) to reference mapped parameters, for example: `{{tealium_account}}`, `{{tealium_visitor_id}}`, `{{visitor_profile}}`.&lt;br&gt;&lt;br&gt;Use `{{event_payload}}` to include the event payload in the prompt after first enabling the **Add Event Payload** checkbox.&lt;br&gt;&lt;br&gt;Avoid ambiguous phrasing; prompts should be deterministic so the output can be parsed reliably.&lt;br&gt;&lt;br&gt;Define a valid Tealium event JSON object to be returned in the response. Explicitly instruct the model to include `tealium_account`, `tealium_profile`, and `tealium_visitor_id` and your output variable in this event JSON so the connector can forward the event to the Tealium Collect endpoint.&lt;br&gt;&lt;br&gt;The connector automatically includes instructions in the prompt to force the model to return JSON.&lt;br&gt;&lt;br&gt;For example prompts, see [How it works](#how-it-works).|

#### Advanced Model Settings

| **Parameter** | **Description** |
| --- | --- |
| `temperature` | Controls randomness and creativity. |
| `max_output_tokens` | The maximum number of tokens the model can generate. |
| `max_tool_calls` | The maximum number of total calls to built-in tools that can be processed in a response. |
| `top_p` | Controls diversity by sampling only from the top-p probability mass. |
| `parallel_tool_calls` | Whether to allow the model to run tool calls in parallel. Defaults to `true`. |
| `prompt_cache_key` | Used by OpenAI to cache responses for similar requests to optimize your cache hit rates. |
| `service_tier` | Specifies the processing type used for serving the request. |
| `tool_choice` | How the model should select which tool or tools to use when generating a response. |
| Debug Mode | When debug mode is enabled, the connector accepts the raw OpenAI response without sending it to Tealium Collect. Use trace to validate the response format before enabling full processing. |
