---
title: Anthropic Connector Setup Guide
description: Set up the Anthropic connector to send a prompt with Tealium event or visitor data and return model responses for real-time enrichment.
url: https://docs.tealium.com/server-side-connectors/anthropic-connector/
---

<blockquote>
For an overview of how AI connectors work and how to structure your prompts, see our guide to [AI connectors](https://docs.tealium.com/ai-connectors-and-functions/).
</blockquote>


## How it works

This connector invokes an Anthropic model with your custom prompt and mapped Tealium data, then sends the response as a JSON event back to Tealium Collect for real-time enrichment.


<blockquote>
The connector should be used for targeted, high-value interactions rather than high-volume events. Excessive usage may result in rate limits or increased API costs in your vendor account and add to your inbound Tealium event volume.
</blockquote>


## Usage and cost considerations

Before activating this connector, review your account limits, usage tier, and pricing model. This connector can generate a high volume of requests depending on your event and audience triggers, which may result in unexpected usage or overage costs.

For more information, see [Claude API Docs: Rate limits](https://platform.claude.com/docs/en/api/rate-limits).

## API Information

This connector uses the following vendor API:

* API Name: Anthropic API
* API Version: v1
* API Endpoint: `https://api.anthropic.com/v1`
* Documentation: [Anthropic API](https://platform.claude.com/docs/en/home)

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Anthropic API Key**: Your Anthropic API key to authenticate requests from this connector to the Anthropic API. Create and manage API keys in your Anthropic account settings.

## Actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Prompt to Anthropic | ✓ | ✓ |

### Send Prompt to Anthropic


<blockquote>
For an overview of how AI connectors work and how to structure your prompts, see our guide to [AI connectors](https://docs.tealium.com/ai-connectors-and-functions/).
</blockquote>


#### Mappings

| **Parameter** | **Description** |
| --- | --- |
| Model | Select the Anthropic model to use for this prompt. Choose a model that aligns with your performance and cost requirements. |

#### Tealium Context

The connector automatically includes important Tealium attributes when invoking the AI model and when returning the structured response.

The following attributes are automatically added to the AI request and included in the structured output JSON: `tealium_account`, `tealium_profile`, `tealium_visitor_id`.

These values are taken from the current event and do not need to be referenced in the prompt. You may override these values using mappings.

| **Parameter** | **Description** |
| --- | --- |
| `tealium_event` | (Required) Enter the `tealium_event` value to include in the AI response returned to Tealium. |
| `tealium_datasource` | (Optional) The data source key associated with the response events from this connector. |
| Prompt Parameters | Map Tealium attributes to placeholder names used in your prompt template. For example, map `Lifetime Value` to `lifetime_val`, then reference `{{lifetime_val}}` in the prompt template. |
| Include Event Payload | (Available for event actions) Check this box to include the event payload for use in the prompt template as variable `{{event_payload}}`. |
| Include Visitor Profile | (Available for audience actions) When enabled, the full visitor profile is made available to the prompt as `{{visitor_profile}}`. |
| Include Current Visit | (Available for audience actions) When enabled, current visit attributes are added to the `{{visitor_profile}}` object (keyed by attribute name). |
| Prompt | Enter the prompt to send to the selected Anthropic model. Use the guidelines below to ensure consistent and machine-readable output:<br>Use double curly braces for mapped parameters, for example: `{{product_id}}`, `{{event_value}}`.<br>For audience connector actions, reference `{{visitor_profile}}` after enabling `Include visitor profile`.<br>For event connector actions, reference `{{event_payload}}` after enabling `Include current event payload`.<br>Do not include JSON formatting instructions (for example, `Return only JSON`). The connector enforces the JSON structure automatically. |

#### Advanced Model Settings

| **Parameter** | **Description** |
| --- | --- |
| `temperature` | Controls randomness and creativity (lower = more deterministic). |
| `max_tokens` | Maximum number of tokens the model can generate. If a value is not provided, the connector sets the default to 512. |
| `top_p` | Controls diversity by sampling only from the top-p probability mass. |

#### Structured Output (JSON Schema)

Define the attributes to include in the AI response. These mappings determine the schema sent to Anthropic using `output_config` to ensure the response JSON matches the schema.


<blockquote>
Do not add JSON formatting instructions to your prompt. The schema derived from these mappings enforces the structure automatically.
</blockquote>


| **Parameter** | **Description** |
| --- | --- |
| Attribute name | The attribute name to include in the AI response event. You must create a matching event attribute for enrichment. |
| Required/Optional | Determines if the attribute is required or optional in the response event. |
| Data type | The data type of the field (string, number, integer, or boolean). |
| Debug Mode | When enabled, the connector does not send responses to Tealium Collect. Use Trace to inspect the raw Anthropic response and validate that it is valid JSON before enabling full processing. |
