---
title: AI connectors and Tealium functions overview
description: Overview of how AI connectors and Tealium functions work, with guidance on when to use AI connectors for LLM activation or Tealium functions to invoke your own model.
url: https://docs.tealium.com/guides/ai-connectors-and-functions/
---
Tealium supports two approaches for integrating AI models into real-time data workflows:

* **AI connectors**: Integrate with supported large language model (LLM) providers for prompt-based interactions.
* **Tealium functions**: Invoke your own model or call custom endpoints.

Use this guide to understand how each approach works and when to use each one.

## AI connectors

### How it works

AI connectors integrate with hosted LLM APIs from supported providers and require prompt-based interactions that return structured JSON. They follow a consistent prompt, response, and activation pattern across all supported providers.

To use an AI connector, you need authentication credentials for your provider and at least one configured action that defines a prompt and the Tealium data to send to the AI model.

AI connectors are designed for LLM activation only. They are not intended for invoking traditional machine learning models that return numeric scores or tabular predictions. For those use cases, use Tealium functions.

### Data flow

![](/images/guides/ai-connectors-flow.png)

1. **Trigger fires**: An event or audience change triggers a connector action.
1. **Prompt sent**: The connector sends your prompt and Tealium data to the AI model endpoint.
1. **Response received**: The model generates the requested values and returns a JSON object.
1. **Event ingested**: The connector forwards the response to Tealium Collect.
1. **Profile enriched**: Enrichment rules write the response values to visitor profile attributes.
1. **Audiences activate**: Audience rules evaluate the updated attributes and downstream connectors fire.

### Prompts

The prompt instructs the model about the context data to evaluate, asks a specific question, and defines the expected response. Depending on the vendor connector, you may or may not need to include specific instructions about the response output. See the specific connector instructions for details.

#### Context data

You can include specific attributes or the entire event or visitor data object as context in the prompt.

To include specific attributes, map them in the connector action then reference them in the prompt. For example, if you map `product_review`, you can reference `{{product_review}}` in your prompt.

To include entire data objects in the prompt, enable **Add Event Payload** or **Add Visitor Profile** in the connector action settings, then reference `{{event_payload}}` or `{{visitor_profile}}` in your prompt.

For audience actions, you can also enable **Add Current Visit** to include current visit data within the visitor profile object.

**Important**  
If the connector requires prompt instructions about the context data, include it as the first line of your prompt. For example:

```wrap
You receive a JSON object describing a customer event:
{{event_payload}}
```

If the connector requires prompt instructions about the response format, include it at the end of the prompt. For example:

```wrap
Return only a single JSON object on one line with the following structure: 
{
  &#34;tealium_account&#34;: &#34;{{tealium_account}}&#34;,
  &#34;tealium_profile&#34;: &#34;{{tealium_profile}}&#34;,
  &#34;tealium_visitor_id&#34;: &#34;{{tealium_visitor_id}}&#34;,
  &#34;tealium_event&#34;:  &#34;ai_response&#34;,
  &#34;ai_review_sentiment&#34;: &#34;&lt;customer review sentiment&gt;&#34;
}
```

#### Question

Your prompt tells the model how to evaluate the data and asks to generate one or more specific values.

For example, this prompt asks to generate a text value representing the sentiment of the customer&#39;s review:

```wrap
Based on the provided product review event, classify the customer&#39;s sentiment as one of: &#34;dissatisfied&#34;, &#34;neutral&#34;, or &#34;satisfied&#34;.
```

### Response event

The connector parses the AI response and extracts a JSON object, which is sent back to Tealium Collect as an event.

Example response event:

```json
{
  &#34;tealium_account&#34;: &#34;acme&#34;,
  &#34;tealium_profile&#34;: &#34;main&#34;,
  &#34;tealium_visitor_id&#34;: &#34;383...05d&#34;,
  &#34;tealium_event&#34;: &#34;ai_response&#34;,
  &#34;ai_review_sentiment&#34;: &#34;satisfied&#34;
}
```

### Examples

#### Event trigger
In this example, the customer has just submitted a product review and the prompt asks the model to evaluate the sentiment.

**Example prompt**:

```wrap
You receive a JSON object describing a customer&#39;s product review:
{{event_payload}}

Based on the provided product review event, classify the customer&#39;s sentiment as one of: &#34;dissatisfied&#34;, &#34;neutral&#34;, or &#34;satisfied&#34;.

Return only a single JSON object on one line with the following structure: 
{
  &#34;tealium_account&#34;: &#34;{{tealium_account}}&#34;,
  &#34;tealium_profile&#34;: &#34;{{tealium_profile}}&#34;,
  &#34;tealium_visitor_id&#34;: &#34;{{tealium_visitor_id}}&#34;,
  &#34;tealium_event&#34;:  &#34;ai_response&#34;,
  &#34;ai_review_sentiment&#34;: &#34;&lt;customer review sentiment&gt;&#34;
}
```

**Example response event**:

```json
{
  &#34;tealium_account&#34;: &#34;acme&#34;,
  &#34;tealium_profile&#34;: &#34;main&#34;,
  &#34;tealium_visitor_id&#34;: &#34;383...05d&#34;,
  &#34;tealium_event&#34;: &#34;ai_response&#34;,
  &#34;ai_review_sentiment&#34;: &#34;satisfied&#34;
}
```

#### Audience trigger

In this example, the customer joined an audience named &#34;Frequent Browser, No Purchases&#34; and the prompt asks the model to evaluate the customer&#39;s intent.

**Example prompt**:

```wrap
You receive a JSON object describing a retail visitor:
{{visitor_profile}}

Based on the customer data provided, classify their likely shopping intent as: &#34;bargain hunting&#34;, &#34;product comparison&#34;, &#34;researching for later&#34;, or &#34;not interested&#34;. If data is missing, make a best effort guess.

Return only a single JSON object on one line with the following structure: 
{
  &#34;tealium_account&#34;: &#34;{{tealium_account}}&#34;,
  &#34;tealium_profile&#34;: &#34;{{tealium_profile}}&#34;,
  &#34;tealium_visitor_id&#34;: &#34;{{tealium_visitor_id}}&#34;,
  &#34;tealium_event&#34;:  &#34;ai_response&#34;,
  &#34;ai_shopping_intent&#34;: &#34;&lt;customer shopping intent&gt;&#34;
}
```

**Example response event**:

```json
{
  &#34;tealium_account&#34;: &#34;acme&#34;,
  &#34;tealium_profile&#34;: &#34;main&#34;,
  &#34;tealium_visitor_id&#34;: &#34;383...05d&#34;,
  &#34;tealium_event&#34;: &#34;ai_response&#34;,
  &#34;ai_shopping_intent&#34;: &#34;bargain hunting&#34;
}
```

### Activation

If the model returns a valid JSON object, the connector forwards it to Tealium Collect as an inbound event. Enrichment rules then write the response values to visitor profile attributes. From there, audiences and downstream connectors activate based on the enriched profile.

Setting a value for `tealium_event` that&#39;s unique to the connector and naming the response attribute specific to the use case makes it easy to create event feeds or rules that match these events.

Example rule for AI response event activation:


[
  [
    {
      &#34;input&#34;: &#34;tealium_event&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;ai_response&#34;
    },
    {
      &#34;input&#34;: &#34;ai_review_sentiment&#34;,
      &#34;operator&#34;: &#34;is populated&#34;
    }
  ]  
]


### Test

Before activating an AI connector in production, enable **Debug Mode** in the connector mappings and test your setup with trace to validate your configuration and prompt behavior. Using debug mode helps catch errors and optimize prompts before incurring production costs or affecting live data.

In debug mode, the connector executes the AI request but logs the result without sending the response event back to your account. Use the trace tool to inspect the full request and response, verify the generated output, and ensure that the trigger conditions and attribute mappings are working as expected.

### Supported vendors

Configuration details such as authentication, model selection, prompt requirements, and action parameters are specific to each connector.

The following AI connectors are available:



## Functions for AI

### How it works

Tealium functions provide a code-based approach for invoking your own model (IYOM). Instead of using a preconfigured connector, you write JavaScript to call any model endpoint directly from an event or visitor function. Use cases include traditional machine learning models returning numeric scores, LLMs hosted on platforms without a dedicated AI connector, and endpoints on data platforms such as Snowflake Cortex, Databricks Model Serving, or Amazon SageMaker.

Tealium functions support both event functions (triggered after an event is processed) and visitor functions (triggered after a visitor profile updates), allowing you to score either immediate event context or accumulated visitor history.

When a function fires, it follows these steps:

1. Collect event attributes or visitor profile data.
1. Build a request payload for your model endpoint.
1. Call the endpoint using `fetch()`.
1. Parse the response.
1. Send the prediction to Tealium Collect using `track()`.
1. Enrichments write the prediction values to the visitor profile.

Because functions cannot directly modify visitor profiles, predictions must flow through Tealium Collect and be written to the profile through enrichments.

Functions support both synchronous and asynchronous model invocation. For models that respond within 10 seconds, use a standard `await` pattern. For slower models, use a fire-and-forget pattern. The function sends the request and exits immediately. The model then POSTs the result to a callback URL when inference completes.

For implementation details, see [Create a function for AI activation]().

## Choosing between connectors and functions

### Use an AI connector when

* You are invoking a large language model for prompt-based inference.
* Your use case maps to one of the supported AI providers.
* Your prompt uses a consistent template with event or visitor data as input.
* The model returns structured JSON that can be forwarded directly as a Tealium event.
* You want to configure the integration through the Tealium UI without writing code.
* Your use case consists of targeted, high-value events or audiences rather than high-volume, low-value events such as page views.

AI connectors are designed for use cases that return structured, predictable JSON output, such as classification labels, confidence values, or identifiers from a predefined list. They are not designed for long-form content or media generation. If your use case requires free-form output, align with your organization&#39;s AI governance processes before moving to production.

### Use Tealium functions when

* You need to invoke a traditional machine learning model that returns numeric scores or tabular predictions.
* Your model is hosted on a platform without a dedicated AI connector.
* Your payload requires custom logic, data transformation, or PII filtering before sending to the model.
* You need to handle asynchronous model responses or custom network configuration.

When you must remove or tokenize PII before sending data to a model, use Tealium functions to apply custom filtering and send only the approved fields to the endpoint.

## Comparison summary

| Consideration | AI connectors | Tealium functions |
|---------------|---------------|-------------------|
| Setup | Configure through the UI | Write JavaScript code |
| Model types supported | LLMs only | Any ML or AI model, including traditional ML |
| Supported providers | See [Supported vendors](#supported-vendors) | Any HTTPS endpoint |
| Prompt control | Template-based with variable substitution | Fully programmable |
| Authentication | Managed in connector settings | Stored as authentication tokens in Tealium functions |
| Payload structure | Fixed based on event or visitor data | Fully customizable |
| PII filtering before model call | Platform-level only (consent categories and restricted attributes). No custom pre-processing code inside the connector | Fully customizable filtering and transformation in JavaScript before calling the model |
| Response handling | Automatic JSON parsing and event forwarding | Custom parsing in code |
| Asynchronous support | Limited. The Bedrock AI Workflow action supports asynchronous responses through Lambda callbacks | Supported through fire-and-forget pattern and model callbacks to Tealium Collect |

## Common use cases

The following table lists common AI use cases and the recommended integration approach for each.

| Use case | Description | Recommended approach |
|----------|-------------|----------------------|
| Sentiment analysis | Classify customer feedback or review events as positive, neutral, or negative. | AI connector |
| Intent classification | Identify a customer&#39;s likely intent based on browsing or purchase history. | AI connector |
| Next-best-action (playbook selection) | Select from a finite set of approved actions or offers based on visitor context. | AI connector |
| Propensity scoring | Predict the likelihood of a conversion, churn, or high-value action using a trained machine learning model. | Tealium functions |
| Next-best-action (score optimization) | Score a set of candidate actions using a numeric model and select the highest-scoring one. | Tealium functions |
| Feature store lookup | Retrieve pre-calculated scores or features from a data platform for activation. | Tealium functions |
| Custom endpoint inference | Invoke a model hosted on a platform without a dedicated AI connector. | Tealium functions |
