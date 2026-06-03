---
title: Create a function for AI activation
description: Connect external AI models to Tealium functions to invoke real-time predictions and enrich visitor profiles using event and visitor data.
url: https://docs.tealium.com/guides/function-for-ai-activation/
---
This guide explains how to integrate external AI models with Tealium functions for real-time activation. Connect securely to model endpoints, invoke AI predictions using event and visitor data, and enrich visitor profiles with model outputs. It also covers asynchronous responses and common integration issues.

For information on when to use Tealium functions or AI connectors for your use case, see [AI connectors and Tealium functions]().

## How it works

Use functions to call external AI models for tasks such as churn risk, fraud detection, propensity scoring, or next-best-action recommendations. The function collects event data and visitor profile attributes, builds a payload, sends it to your model endpoint, receives a prediction, and updates the visitor profile for activation.

The data flow for real-time model inference and activation includes the following steps:

1. **Customer action**: User performs an action (for example, view product, add to cart, submit form).
1. **Function trigger**: An event or visitor function fires based on configured triggers and returns a prediction (score, classification, recommendation).
1. **Event to Collect**: The function sends prediction data to Tealium Collect through the `track()` method.
1. **Enrichment processing**: Configured enrichments write the prediction values to visitor profile attributes.
1. **Downstream activation**: Audiences evaluate and connectors fire based on updated profile attributes.

Because functions cannot directly modify visitor profiles, predictions must flow through Tealium Collect and be written to profiles through enrichments.

The `track()` method sends events to Tealium Collect. You must configure enrichments to write these event attribute values to visitor profile attributes.

### Function types

| Function type | Trigger | Signature | Use case |
|-------------|----------------|------------|----------------|
| Event Function | Fires after a specific event is processed | `{ event, helper }` | Score based on immediate event context (for example, product recommendation on product view) |
| Visitor Function | Fires after a visitor profile is updated | `{ visitor, visit, helper }` | Score based on accumulated profile data (for example, churn prediction based on engagement history) |

Using functions to call external AI models for real-time inference and activation provides several benefits, such as:

* Detect customer churn risk from visitor behavior in real time.
* Improve targeting for retention campaigns by identifying high-risk visitors.
* Support personalized experiences by using AI-based predictions for segmentation.
* Increase accuracy of downstream activation by enriching profiles with model-driven insights.
* Handle high-throughput data streams for timely analysis and response.
* Improve data quality for marketing, analytics, and compliance workflows.

### Prerequisites

Before you create a function to invoke your AI model, ensure that you have the following:

* A trained ML model deployed to a REST API endpoint, such as Snowflake Cortex, Databricks Model Serving, AWS SageMaker, Google Vertex AI, Azure ML, Hugging Face Inference Endpoints, or any HTTPS endpoint.
* API credentials for your model endpoint, such as API key, bearer token, or JWT.
* Add Tealium IP addresses for your profile region to the allowlist for your data cloud. For more information, see [Tealium IP addresses to allow]().
* The request payload schema your model expects.
* The response payload schema your model returns.

## Key components for AI-based churn risk analysis

* **Data transformation function**  
    Evaluates incoming event data and applies regular expressions to identify behaviors relevant to churn risk.

* **Derived attribute**  
    Calculates a churn risk score from event data. The function sets this value for each event.

* **AudienceStream event filter**  
    Filters events using the churn risk score. Only high-risk events enrich visitor profiles.

* **Event feed**  
    Streams flagged high-risk events for further processing by connectors, storage, or other functions.

* **External model invocation function**  
    Sends enriched event or profile data to an external AI model endpoint for advanced churn prediction.

* **Enrichment**  
    Writes AI model predictions to visitor profile attributes for activation and segmentation.

## Requirements

To implement this solution, you need:

* Tealium requirements
    * AudienceStream enabled
    * Tealium functions enabled
    * A configured data source for receiving `track()` events
    * Enrichments to write prediction attributes to visitor profiles
* Model endpoint requirements
    * Use HTTPS protocol
    * Responds within 10 seconds. We recommend a response time of under 500 milliseconds for real-time personalization.
    * Uses a bearer token, API key, or header-based authentication
    * Responds in JSON format.

## Step 1: Create the function

You can implement your AI activation logic using either an event function or a visitor function. Choose the function type that best matches your use case and the data available at the time of scoring.

### Code reference

| Object/Method | Description |
| ---------- | ----------|
| `event.data.udo.*` | Event attributes from the triggering event |
| `visitor.properties.*` | Visitor profile string attributes |
| `visitor.metrics.*` |  Visitor profile numeric attributes |
| `visitor.audiences` | Visitor audience membership  |
| `visitor.current_visit.*` | Visit attributes from the visitor’s current session |
| `helper.getAuth(&#39;name&#39;)` | Retrieve stored authentication token |
| `helper.getGlobalVariable(&#39;name&#39;)` | Retrieve stored global variable |
| `track(data, config)` | Send event to Tealium Collect (max 6 calls per invocation) |

### Platform-specific notes

The following code examples show a generic REST API pattern. Actual implementations vary by platform:

| Platform                | Notes         |
|-------------------------|---------------|
| Snowflake Cortex        | Cortex functions are called through SQL statements using the Snowflake SQL API. Requires JWT authentication.                                   |
| Databricks Model Serving| MLflow models are exposed as REST endpoints. Uses personal access token (PAT) authentication. Supports asynchronous inference through jobs API.|
| AWS SageMaker           | Endpoints require AWS Signature V4 authentication. Consider using a Lambda proxy for simplified authentication. Supports async inference endpoints for long-running jobs. |
| Hugging Face            | Inference Endpoints use bearer token authentication. Response format depends on the model type.                                                |
| GCP Vertex              | Vertex AI endpoints use OAuth 2.0 or service account authentication.                                                                          |
| Azure                   | Azure ML managed endpoints use API key or Azure AD token authentication.                                                                      |

Refer to your platform&#39;s API documentation for request/response formats and authentication requirements.

### Event function example

The following example shows how to call an external model API from an event function. Adapt the payload structure and response parsing to match your model&#39;s API.


```js
activate(async ({ event, helper }) =&gt; {
  // 1. Assemble feature payload from event data
  // Adapt this to match your model&#39;s expected input format
  const payload = {
    product_id: event.data.udo.product_id,
    category: event.data.udo.product_category,
    price: event.data.udo.product_price
  };
  // 2. Call your model API
  const response = await fetch(
    helper.getGlobalVariable(&#39;MODEL_ENDPOINT_URL&#39;),
    {
      method: &#39;POST&#39;,
      headers: {
        &#39;Authorization&#39;: &#39;Bearer &#39; &#43; helper.getAuth(&#39;model_api_token&#39;),
        &#39;Content-Type&#39;: &#39;application/json&#39;
      },
      body: JSON.stringify(payload)
    }
  );
  if (!response.ok) {
    console.error(&#39;Model API error:&#39;, response.status);
    return;
  }
  const result = await response.json();
  // 3. Send prediction to Tealium Collect
  // Adapt the attribute names to match your model&#39;s response
  track({
    tealium_event: &#39;model_prediction&#39;,
    prediction_score: result.score,
    prediction_label: result.label
  }, {
    tealium_account: event.account,
    tealium_profile: event.profile,
    tealium_datasource: helper.getGlobalVariable(&#39;DATASOURCE_KEY&#39;)
  });
});
```


### Visitor function example

Visitor functions can access accumulated profile data for scoring. However, visitor functions do not have access to the `event` object, so you must use global variables for `account`, `profile`, and `datasource` values.


```js
activate(async ({ visitor, visit, helper }) =&gt; {
  // Assemble payload from visitor profile attributes
  const payload = {
    lifetime_value: visitor.metrics.lifetime_value,
    purchase_count: visitor.metrics.purchase_count,
    days_since_last_purchase: visitor.metrics.days_since_last_purchase,
    loyalty_tier: visitor.properties.loyalty_tier
  };
  const response = await fetch(
    helper.getGlobalVariable(&#39;MODEL_ENDPOINT_URL&#39;),
    {
      method: &#39;POST&#39;,
      headers: {
        &#39;Authorization&#39;: &#39;Bearer &#39; &#43; helper.getAuth(&#39;model_api_token&#39;),
        &#39;Content-Type&#39;: &#39;application/json&#39;
      },
      body: JSON.stringify(payload)
    }
  );
  if (!response.ok) {
    console.error(&#39;Model API error:&#39;, response.status);
    return;
  }
  const result = await response.json();
  // For Visitor Functions, use Global Variables for routing
  // Include visitor_id to ensure the event stitches to the correct profile
  track({
    tealium_event: &#39;churn_prediction&#39;,
    tealium_visitor_id: visitor.properties.visitor_id,
    churn_score: result.churn_probability,
    churn_risk_tier: result.risk_tier
  }, {
    tealium_account: helper.getGlobalVariable(&#39;TEALIUM_ACCOUNT&#39;),
    tealium_profile: helper.getGlobalVariable(&#39;TEALIUM_PROFILE&#39;),
    tealium_datasource: helper.getGlobalVariable(&#39;DATASOURCE_KEY&#39;)
  });
});
```


### Slow model response handling

When model inference takes longer than 10 seconds, use an asynchronous pattern. The function sends a request and exits immediately. The model calls back to Tealium when processing completes.

1. Function sends visitor data and a callback URL to your model endpoint
1. Model endpoint returns 202 Accepted immediately
1. Function exits (no timeout)
1. Model completes inference asynchronously
1. Model POSTs prediction to Tealium&#39;s HTTP API
1. Enrichments write prediction to visitor profile

#### Create an HTTP API data source for the model callback

Create an HTTP API data source for receiving model callbacks. For more information, see [Create a data source]().

### Async function code

Use the following function code:


```js
activate(async ({ visitor, visit, helper }) =&gt; {
  const payload = {
    visitor_id: visitor.properties.visitor_id,
    lifetime_value: visitor.metrics.lifetime_value,
    purchase_count: visitor.metrics.purchase_count,
    callback_url: helper.getGlobalVariable(&#39;TEALIUM_CALLBACK_URL&#39;),
    callback_datasource: helper.getGlobalVariable(&#39;DATASOURCE_KEY&#39;)
  };
  // Fire and forget - don&#39;t await the response
  fetch(
    helper.getGlobalVariable(&#39;MODEL_ENDPOINT_URL&#39;),
    {
      method: &#39;POST&#39;,
      headers: {
        &#39;Authorization&#39;: &#39;Bearer &#39; &#43; helper.getAuth(&#39;model_api_token&#39;),
        &#39;Content-Type&#39;: &#39;application/json&#39;
      },
      body: JSON.stringify(payload)
    }
  ).catch(error =&gt; console.error(&#39;Request failed:&#39;, error.message));
  // Function exits immediately - model will callback when ready
});
```


### Model callback payload

Your model endpoint should POST to the Tealium HTTP API when inference completes:

```
POST https://collect.tealiumiq.com/event?tealium_account={account}&amp;tealium_profile={profile}&amp;tealium_datasource={datasource_key}

{
  &#34;tealium_event&#34;: &#34;model_prediction_complete&#34;,
  &#34;tealium_visitor_id&#34;: &#34;original_visitor_id_from_request&#34;,
  &#34;churn_score&#34;: 0.82,
  &#34;churn_risk_tier&#34;: &#34;high&#34;,
  &#34;model_version&#34;: &#34;v2.1&#34;
}
```

Including `tealium_visitor_id` ensures the prediction stitches to the correct visitor profile. Configure enrichments as described in Step 3 to write these attributes to the profile.

## Step 2: Configure credentials for the ML platform

Store your model API credentials and configuration in Tealium functions for secure access.

### Add authentication tokens for the ML platform

To store API credentials for a function on the Tealium platform, add an authentication token. In this example, you will store the API key or token endpoint URL as `model_api_token`. For more information, see [Add authentication]().

Retrieve the token in your function with the following code:

```
    {
      method: &#39;POST&#39;,
      headers: {
        &#39;Authorization&#39;: &#39;Bearer &#39; &#43; helper.getAuth(&#39;model_api_token&#39;),
        &#39;Content-Type&#39;: &#39;application/json&#39;
      },
      body: JSON.stringify(payload)
    }
```

Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder.

### Add global variables for the ML platform

Store configuration information for a function such as the model endpoint URL and name as global variables. In this example, you will store the model endpoint URL as `MODEL_ENDPOINT_URL`. For more information, see [Manage global variables]().

Retrieve the variable in your function with the following code:

```
  const response = await fetch(
    helper.getGlobalVariable(&#39;MODEL_ENDPOINT_URL&#39;),
    {
...
    }
  );
```

## Step 3: Add churn score to visitor profile

Before you can activate predictions in downstream systems, you must configure attributes and enrichments to store and process model outputs in visitor profiles.

### Create churn score profile attribute

Create an attribute to store model predictions in visitor profiles. In this example, create a `churn_score` number attribute.

For more information, see [Create an attribute]().

Enrich the attribute you created to write model predictions from events to visitor profiles. Without an enrichment, predictions do not appear on visitor profiles. In this example, create an enrichment to write the `prediction_score` event attribute from your `track()` call to the `churn_score` visitor attribute when `tealium_event` equals `model_prediction` (or your event name).


[
  [
    {
      &#34;input&#34;: &#34;tealium_event&#34;,
      &#34;operator&#34;: &#34;equals (ignore case)&#34;,
      &#34;filter&#34;: &#34;model_prediction&#34;
    }
  ] 
]


For more information, see [Add enrichment]().

## Step 4: Activate a high churn risk audience

Use your prediction attributes to build audiences and trigger actions to activate on churn risk.

### Create churn risk audience

Create an audience based on prediction attributes. In this example, create a `High Churn Risk` audience for visitors with a `churn_score` greater than `0.7`.


[
  [
    {
      &#34;input&#34;: &#34;churn_score&#34;,
      &#34;operator&#34;: &#34;greater than&#34;,
      &#34;filter&#34;: &#34;0.7&#34;
    }
  ] 
]


For more information, see [Create an audience]().

### Configure connectors

Attach connector actions to audiences to activate on prediction values. In this example, you can trigger retention emails for high churn risk or add users to remarketing audiences based on purchase intent.

For more information, see [Add connector]().

## Debugging

### View logs

Use `console.log()` for debugging:

```
console.log(&#39;Payload:&#39;, JSON.stringify(payload));
console.log(&#39;Response status:&#39;, response.status);
console.log(&#39;Result:&#39;, JSON.stringify(result));
```

To view logs, click the **Logs** tab in the functions editor.

### Common issues

| Issue                        | Solution                                                                                                   |
|------------------------------|------------------------------------------------------------------------------------------------------------|
| Function times out           | Ensure model responds within 10 seconds. Use dedicated or provisioned endpoints. Consider asynchronous model invocation depending on average model response time. |
| Predictions not on profiles  | Verify enrichments are configured. Check `tealium_datasource` value.                                       |
| Authentication errors        | Verify token value in **Auth Tokens**. Check token expiration.                                                 |
| `track()` not executing      | Check for errors before `track()`. Verify data source is active.                                           |

## Resources

* [Functions]()