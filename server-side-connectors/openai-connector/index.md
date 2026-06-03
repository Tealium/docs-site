---
title: OpenAI Connector Setup Guide
description: Set up the OpenAI connector to send a prompt with Tealium event or visitor data and return model responses for real-time enrichment.
url: https://docs.tealium.com/server-side-connectors/openai-connector/
---
For an overview of how AI connectors work and guidance on when to use an AI connector or Tealium functions, see [AI connectors and Tealium functions]().

## How it works

This connector invokes an OpenAI model with your custom prompt and mapped Tealium data, then sends the response as a JSON event to Tealium Collect for real-time enrichment.

The OpenAI connector should be used for targeted, high-value interactions rather than high-volume events. Excessive usage may result in rate limits or increased API costs in your OpenAI account and add to your inbound Tealium event volume.


## Usage and cost considerations

Before activating the OpenAI connector, review your OpenAI account limits, usage tier, and pricing model. The connector can generate a high volume of requests depending on your event and audience triggers, which may result in unexpected usage or overage costs.

For more information, see [OpenAI Developers: Rate limits](https://developers.openai.com/api/docs/guides/rate-limits).

**Key considerations**

* **Usage tier and rate limits**  
  OpenAI enforces rate limits based on your account tier (requests per minute and tokens per minute). High‑frequency events or large audiences can quickly reach these limits, causing throttling or failed requests.
* **Pricing and token consumption**  
  OpenAI charges based on the number of input and output tokens processed by the model. Longer prompts, larger payloads, and higher‑capacity models increase per‑request cost. Review pricing for the specific models you plan to use.
* **Monthly spend and budget controls**  
  Set usage caps or alerts in your OpenAI account to prevent unplanned spend. Without limits in place, automated workflows can accumulate significant costs.
* **Trigger volume**  
  Avoid attaching the connector to high‑volume, low‑value events (such as page views). Use events or audiences that represent meaningful customer actions and occur at manageable frequency.

## Best practices

To get the most value from this connector, follow these guidelines to build effective solutions: 

* **High-value triggers**: Choose event feed or audience triggers that contain rich context or meaningful customer input. Triggering this connector for a high-volume use case may incur additional costs in your OpenAI account or lead to failed requests.
* **Be specific**: Include details about what the model should evaluate and what values you expect. List the exact values you expect.
* **JSON format**: Include a valid JSON response template that can be sent as a Tealium event.
* **Response values**: Reference the response values to capture. For example, if your prompt asks to evaluate the purchase intent, reference `&lt;customer purchase intent&gt;` in the prompt where you want that value to appear in the event JSON.
* **Tealium data**: Reference Tealium data and mapped parameters using double-curly braces. For example, to reference the mapped value for `tealium_account`, write `{{tealium_account}}` in your prompt.

## API information

This connector uses the following vendor API:

* API Name: OpenAI API
* API Version: v1
* API Endpoint: `https://api.openai.com/v1`
* Documentation: [OpenAI API](https://platform.openai.com/docs/api-reference)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **API Key**: The OpenAI API key used to authenticate requests made by this connector to the OpenAI API. The key must have permission to create responses (model inference) using either **All** or **Restricted** permission. It cannot have **Read Only** permission. For more information, see [OpenAI: Assign API Key Permissions](https://help.openai.com/en/articles/8867743-assign-api-key-permissions).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Prompt to OpenAI | ✓ | ✓ |

### Send Prompt to OpenAI

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

