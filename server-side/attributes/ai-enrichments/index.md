---
title: AI enrichments
description: Use AI enrichments to apply LLM-based processing to visitor and event data and route the output back into the Tealium data collection pipeline.
url: https://docs.tealium.com/server-side/attributes/ai-enrichments/
---

<blockquote>
AI enrichments is only available to select customers. If you are interested in trying this feature, [contact support](https://docs.tealium.com/support/).
</blockquote>


AI enrichments apply LLM-based processing to real-time customer data inside the Tealium customer data pipeline. Configure an AI enrichment by writing a prompt, selecting a trigger, and choosing input and output attributes. The AI enrichment evaluates that data, generates a new event containing the output data, and sends it back to the Tealium data pipeline, making it available for audiences, connectors, and downstream activation.

## How it works

Each AI enrichment follows this flow:

**Trigger → Inputs → Prompt → Generate event (Outputs)**

When the trigger fires, the AI enrichment evaluates the input attributes according to the prompt and produces output values. The AI enrichment generates a new AI enrichment event with the output attributes and sends it back to the Tealium data collection pipeline. To complete the enrichment, configure attributes, audiences, and connectors to act on that event.

Every trigger execution generates a new event. 


<blockquote>
The AI enrichment does not modify the triggering event and does not write directly to the visitor profile.
</blockquote>


### Triggers

The trigger determines when the AI enrichment runs. Each trigger execution produces one new AI enrichment event.

The trigger types are:

* **Processed visitor**  
The AI enrichment runs when a visitor joins or leaves a selected audience. Use this trigger to evaluate enrichments based on audience membership changes.
* **Processed event**  
The AI enrichment runs after an event feed processes an event. Use this trigger for high-signal interactions that warrant immediate evaluation.

### Inputs and outputs

_Inputs_ are the visitor, visit, and event attributes the AI enrichment evaluates. To optimize the enrichment, use attributes that meaningfully reflect the condition you want the AI enrichment to detect, such as engagement trends, subscription changes, support interactions, or financial signals.

_Outputs_ are event attributes that appear in the generated AI enrichment event. To persist an output attribute to the visitor profile, configure an enrichment rule that sets the attribute from the generated event.

### Prompts

The prompt is the task instruction for the AI enrichment. It describes the business outcome, the behavior to evaluate, decision criteria, and how to interpret the input attributes.

Tealium automatically appends the configured input attributes to the prompt before sending it to the model.

The AI enrichment receives the following:

* System message: Tealium-controlled prompt guardrails covering safety, scope, and output format.
* Custom message: Your prompt combined with the input data.

For the best results, include the following in your prompt:

* The business goal or decision to make.
* The behavior or signal to detect.
* Explicit criteria, thresholds, or permitted output categories.
* Guidance for interpreting the selected input data.
* Instructions about missing data or ambiguous scenarios.

Do not include the following:

* JSON formatting instructions such as "return only JSON".
* A manually written output schema, field list, or data types.
* Tealium identifiers or fields you did not select as inputs.
* Assumptions about data that is not present.
* Requests for long-form content or media generation.

### AI enrichment event

After processing the input attributes and prompt, the AI enrichment generates a new enrichment event. This event contains `tealium_event` and your output attributes and it flows back into the data collection pipeline. The `tealium_event` value is in the format `async_processed_AI_ENRICHMENT_ID` where `AI_ENRICHMENT_ID` is unique to each enrichment you configure. Use this value when configuring downstream components, such as enrichment rules or event feeds.

Example AI enrichment event:
```json
{
  "tealium_event": "async_processed_00070f98-9134-4901-adeb-2d343a0f4ac",
  "your_output_attribute": "VALUE"
}
```

### Examples

**Example: Classify product review sentiment**

* **Trigger**: Product review event
* **Input**: Product review text (`product_review_text`)
* **Prompt**:  
    ```wrap
    Based on the product review, classify the customer's sentiment as one of: "dissatisfied", "neutral", or "satisfied".
    ```
* **Outputs**: `ai_review_sentiment`

Generated AI enrichment event:
```json
{
  "tealium_event": "async_processed_00070f98-9134-4901-adeb-2d343a0f4ac",
  "ai_review_sentiment": "satisfied"
}
```

**Example: Infer shopping intent**

* **Trigger**: Joined "Abandoned cart" audience
* **Input**: `cart_product_names`, `cart_total_value`, `visit_count_7d`
* **Prompt**:  
    ```wrap
    Infer the shopping mission. Set "mission" to a summary of 6 words or fewer, set "urgency" to "high", "med", or "low", and set "sensitive" to "true" if the mission implies health, pregnancy, minors, or financial distress.
    ```
* **Outputs**: `shopping_mission` (string), `shopping_urgency` (string), `shopping_sensitive` (boolean)

Generated AI enrichment event:
```json
{
  "tealium_event": "async_processed_20470d98-2171-4901-dacf-6a513a0f4bd",
  "shopping_mission": "back to school, high cart value",
  "shopping_urgency": "medium",
  "shopping_sensitive": false
}
```

## Create an AI enrichment

To create an AI enrichment, go to **AI Enrichments** and click **New AI Enrichment**.

### Step 1: Select a trigger

Select **Processed Visitor** to run the AI enrichment based on a visitor's status in an audience. After selecting this option, choose an audience and the specific [audience trigger](https://docs.tealium.com/about-connectors/#terminology).

Select **Processed Event** to run the AI enrichment after an event feed processes an event. After selecting this option, choose an event feed from the list.

### Step 2: Select inputs and outputs

**Inputs**  
Select the attributes the AI enrichment uses as inputs. Choose attributes that reflect the behavior or condition described in your prompt. If the trigger is a processed event, only event attributes can be selected as input attributes. If the trigger is a processed visitor, only visit or visitor attributes can be selected as input attributes.

**Outputs**  
Select the event attributes for the AI enrichment to output. Click **Add Attribute** and define the attribute name and type. These attributes appear in the generated AI enrichment event.

### Step 3: Write a prompt

Describe the business outcome, the behavior to evaluate, and the output values the AI enrichment should produce. For guidance on writing effective prompts, see [Prompts](#prompts).

### Step 4: Review and create

Review the AI enrichment configuration:

* **AI Enrichment Instructions**: Confirm the prompt you wrote.
* **AI Enrichment Name**: Enter a name for the AI enrichment.
* **Status**: New AI enrichments are inactive by default. Activate the AI enrichment after you create it.
* **Trigger**: The audience or event feed that triggers the AI enrichment.
* **Attributes to evaluate**: The input attributes evaluated by the AI enrichment.
* **Outcomes**: The event attributes set in the generated AI enrichment event.

Click **Create** to save the AI enrichment.

Note the generated event name. It follows the format `async_processed_AI_ENRICHMENT_ID`, for example `async_processed_00070f98-9134-4901-adeb-2d343a0f4ac`. Use this value to configure downstream components.

## Configure downstream components

Creating the AI enrichment does not complete the setup. The AI enrichment generates a new AI enrichment event containing the output data, but nothing acts on that event until you configure downstream components.

### Create enrichment rules

Create an enrichment rule to write the output attribute value from the generated event to a visitor attribute.

Match the enrichment condition to the event name (`async_processed_AI_ENRICHMENT_ID`) so that only the generated AI enrichment event triggers the rule.

In this example, the enrichment rule requires that the event comes from the AI enrichment and that visitor review sentiment is not already set:


[
  [
    {
      "input": "tealium_event",
      "operator": "equals",
      "filter": "async_processed_00070f98-9134-4901-adeb-2d343a0f4ac"
    },
    {
      "input": "ai_review_sentiment (visitor)",
      "operator": "not populated"
    }
  ]
]


### Build audiences

Create audience rules that segment visitors based on the new AI enrichment attributes.

### Configure connectors or event feeds

To act on the generated event directly, create an event feed based on the AI enrichment event name, then configure a connector action based on the feed.

To act on the enriched visitor attribute, configure a connector action based on the new audience.

### Validate with Trace

Use Trace to confirm the AI enrichment is running and producing the expected output. When an AI enrichment runs, Trace shows the following:

* Confirmation that the AI enrichment triggered.  
![](https://docs.tealium.com/images/server-side/ai-enrichment-trace-agent-triggered.png)
* The inputs, outputs, and AI enrichment instructions.  
![](https://docs.tealium.com/images/server-side/ai-enrichment-trace-details.png)
* A failure indicator if the AI enrichment did not complete processing.  
![](https://docs.tealium.com/images/server-side/ai-enrichment-trace-failure.png)
