---
title: Google Vertex AI Setup Guide
description: Set up the Google Vertex AI connector to invoke Vertex AI models with Tealium event data and return model responses for real-time visitor enrichment.
url: https://docs.tealium.com/server-side-connectors/google-vertex-ai-connector/
---
For an overview of how AI connectors work and guidance on when to use an AI connector or Tealium functions, see [AI connectors and Tealium functions]().

## How it works

This connector invokes an AI model with your custom prompt and mapped Tealium data, then sends the response as a JSON event back to Tealium Collect for real-time enrichment.

The connector should be used for targeted, high-value interactions rather than high-volume events. Excessive usage may result in rate limits or increased API costs in your vendor account and add to your inbound Tealium event volume.

## Usage and cost considerations

Before activating the Google Vertex AI connector, review your Google Cloud quotas and limits. The connector can generate a high volume of requests depending on your event and audience triggers, which may result in unexpected usage or overage costs.

For more information, see [Google: Vertex AI quotas and limits](https://docs.cloud.google.com/vertex-ai/docs/quotas).

**Key considerations**

* **Usage tier and rate limits**  
  Google Vertex AI enforces rate limits based on your account tier (requests per minute and tokens per minute). High‑frequency events or large audiences can quickly reach these limits, causing throttling or failed requests.
* **Pricing and token consumption**  
  Google Vertex AI charges based on the number of input and output tokens processed by the model. Longer prompts, larger payloads, and higher‑capacity models increase per‑request cost. Review pricing for the specific models you plan to use.
* **Monthly spend and budget controls**  
  Set usage caps or alerts in your Google Cloud account to prevent unplanned spend. Without limits in place, automated workflows can accumulate significant costs.
* **Trigger volume**
  Avoid attaching the connector to high‑volume, low‑value events (such as page views). Use events or audiences that represent meaningful customer actions and occur at manageable frequency.

## Best practices

To get the most value from this connector, follow these guidelines to build effective solutions: 

* **High-value triggers**: Choose event feed or audience triggers that contain rich context or meaningful customer input. Triggering this connector for a high-volume use case may incur additional costs in your Google Cloud account or lead to failed requests.
* **Be specific**: Include details about what the model should evaluate and what values you expect. List the exact values you expect.
* **JSON format**: Include a valid JSON response template that can be sent as a Tealium event.
* **Response values**: Reference the response values to capture. For example, if your prompt asks to evaluate the purchase intent, reference `&lt;customer purchase intent&gt;` in the prompt where you want that value to appear in the event JSON.
* **Tealium data**: Reference Tealium data and mapped parameters using double-curly braces. For example, to reference the mapped value for `tealium_account`, write `{{tealium_account}}` in your prompt.

## API information

This connector uses the following vendor API:

* API Name: Vertex API
* API Version: v1
* API Endpoint: `https://aiplatform.googleapis.com/v1`
* Documentation: [Google API](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/reference/rest/v1/projects.locations.endpoints/generateContent)

## Configuration

Go to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Google Cloud Platform Project ID**: (Required) Your Google Cloud project ID with Vertex AI enabled.
* **Private key JSON file**: (Required) Paste the content of the JSON key generated for your Service Account. Grant the service account the Vertex AI User role (`roles/aiplatform.user`) in the project. This role allows the connector to both list available models and invoke the selected model through the Vertex AI Generative APIs.
* **Location**: Select the Vertex AI location where your model runs. Use **global** for Google publisher Gemini models. Choose a regional location if required for data residency or if your Vertex resources are regional.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Prompt to Vertex AI | ✓ | ✓ |

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Send Prompt to Vertex AI

This action invokes a Vertex AI model with your custom prompt and mapped Tealium data. If the model responds with a valid JSON event object, this event is sent back to your account where you can capture the generated value in a real-time enrichment.

#### Parameters

| Parameter | Description |
| --- | --- |
| Model | &lt;ul&gt;&lt;li&gt;Select the Vertex model to use for this prompt.&lt;/li&gt;&lt;li&gt;The list shows Google&#39;s Gemini generative models that are suitable for text or JSON-style responses.&lt;/li&gt;&lt;li&gt;If your team uses a private or fine-tuned Vertex AI model, you can enter its model resource name manually (for example: `projects/{{PROJECT}}/locations/{{REGION}}/models/{{MODEL_ID}}`).&lt;/li&gt;&lt;li&gt;We recommend using a model that is optimized for structured output (JSON) and supports your performance and cost requirements.&lt;/li&gt;&lt;/ul&gt; |

#### Prompt Parameters

| Parameter | Description |
| --- | --- |
| Add Event Payload | (Available for event actions) Check this box to include the event payload for use in the prompt template as variable `{{event_payload}}`. |
| Add Visitor Profile | (Available for audience actions) Check this box to include the visitor profile for use in the prompt template as variable `{{visitor_profile}}`. |
| Add Current Visit | (Available for audience actions) Check this box to include the current visit within the variable `{{visitor_profile}}`. |
| Prompt | &lt;ul&gt;&lt;li&gt;Enter the prompt to send to the selected Vertex AI model. Use the guidelines below to ensure consistent and machine-readable output:&lt;/li&gt;&lt;li&gt;Use double curly braces to reference mapped parameters, for example: `{{tealium_account}}`, `{{visitor_id}}`, `{{event_value}}`.&lt;/li&gt;&lt;li&gt;When using a visitor action, use `{{visitor_profile}}` to include the visitor profile in the prompt after first enabling the **Add Visitor Profile** checkbox.&lt;/li&gt;&lt;li&gt;Avoid ambiguous phrasing; prompts should be deterministic so the output can be parsed reliably.&lt;/li&gt;&lt;li&gt;Define the JSON fields and structure you expect in the response.&lt;/li&gt;&lt;li&gt;Explicitly instruct the model to return `tealium_account`, `tealium_profile`, and `tealium_visitor_id` in its response in order for the connector to correctly parse and forward the response to the Collect endpoint.&lt;/li&gt;&lt;li&gt;The connector will include `response_mime_type`: `application/json` in the request to force the model to return JSON.&lt;/li&gt;&lt;li&gt;For more information and examples, refer to the Tealium documentation for this connector.&lt;/li&gt;&lt;/ul&gt; |
| Debug Mode | When debug mode is enabled, the connector accepts the raw Vertex AI response without sending it to Tealium Collect. Use a trace to validate the response format before enabling full processing. |

#### Advanced Model Settings

| Parameter | Description |
| --- | --- |
| `temperature` | Controls randomness and creativity. A lower value results in a sharper distribution curve with more focused and predictable answers, while a higher value results in a flatter distribution curve and more varied and creative answers. Allowed values are between `0` and `2`. |
| `maxOutputTokens` | The maximum number of tokens to generate in the response. |
| `topP` | Specifies the nucleus sampling threshold.  A lower `topP` value is safer and more focused, while a higher `topP` value is more varied and creative. Allowed values are between `0` and `1`. For example, if `topP` is set to `0.9`, only tokens whose cumulative probability reaches 90% are considered and low‑probability tail tokens are dropped. |
| `topK` | Specifies the top-k sampling threshold. A lower `topK` value is more deterministic and less diverse, while a higher `topK` value is more diverse but potentially less coherent. For example, if `topK` is set to `40`, the next token is chosen (probabilistically, using temperature) from only the 40 highest‑probability tokens and everything else is ignored. |