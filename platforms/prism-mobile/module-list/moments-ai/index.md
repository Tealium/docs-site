---
title: Moments AI module
description: Configure on-device AI inference for mobile profiles using the Moments AI module.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/moments-ai/
---
The Moments AI module adds on-device AI inference to mobile apps using the Tealium Prism SDK. It runs locally on the device using Gemini Nano with no server-side component. Configure the module through the **Mobile Configuration** slideout in Tealium iQ. The module is available only in mobile profiles.

## Module configuration

When adding the module, configure the following settings:

* **System Prompt**: Define the AI model's role and output format. This prompt sets the overall behaviour and constraints for every inference. Example: instruct the model to return JSON in a specific schema, or to act as a particular type of assistant. Supports variable substitution using <code>{{handlebars}}</code> syntax.
* **User Prompt**: Provide the per-request instructions sent to the model. Use <code>{{event.<key>}}</code> to insert values from the current event (e.g. <code>{{event.user_name}}</code>), and <code>{{history}}</code> to include recent event history. These placeholders are replaced at runtime with real data from the mapped context. Supports variable substitution using <code>{{handlebars}}</code> syntax.
* **Temperature**: Numeric input for model temperature.
* **Max Tokens**: Max output tokens for the on-device model.
* **Max Event History**: Number of recent events to retain as context for the model.

## Variable substitution

The System Prompt and User Prompt fields support handlebars-style `{{variable}}` substitution at runtime. The module resolves these placeholders before sending the prompt to the on-device model.

The following built-in variables are available:

| Variable | Description |
| :--- | :--- |
| `{{history}}` | Injects the stored event history, as defined by Max Event History and context mappings. |
| `{{event.<key>}}` | Injects the value of a specific key from the latest event context. Replace `<key>` with the data layer variable name. For example, `{{event.user_name}}`. |

Custom variables are also available through [prompt variable mappings](#prompt-variable-mappings).

## Mappings

Configure mappings in the **Mappings** section of the Moments AI module in Tealium iQ.

### Command triggers

Map event conditions to SDK commands. When the mapped condition is met, the specified command runs. To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Command | Description |
| :--- | :--- |
| `trigger_inference` | Sends the current event and event history to the on-device model to generate an inference result. |
| `store_event` | Stores the current event in the event history buffer for use as future model context. |

### Config overrides

Map data layer values to override module configuration fields at runtime. The following destinations are supported:

| Destination | Description |
| :--- | :--- |
| `system_prompt` | Overrides the System Prompt field. |
| `user_prompt` | Overrides the User Prompt field. |
| `temperature` | Overrides the Temperature field. |
| `max_tokens` | Overrides the Max Tokens field. |

### Context mappings

Map variables to capture into the stored event history. Enter the context key name to store in event history. For example, mapping to `checkout` produces `context.checkout`.

### Prompt variable mappings

Map data layer values to custom variable names for use in prompt substitution. After mapping, reference the variable as `{{variable_name}}` in the System Prompt or User Prompt fields.

## Example

The following example uses Moments AI to generate a personalized cart abandonment notification.

**Configuration:**

System Prompt:

```wrap
You are an on-device e-commerce personalization assistant for a mobile retail app. Your job is to turn a shopper's current activity and recent behavior into a single, timely next-best-action.
Respond with ONLY a compact JSON object, no prose, no markdown, matching exactly:
  {"headline": string, "message": string, "recommended_category": string, "urgency": "low"|"medium"|"high"}
Rules:
  - "headline": <=6 words, action-oriented.
  - "message": <=160 characters, warm and specific to what they browsed or bought. Never invent products, prices, or discounts that aren't in the provided data.
  - "recommended_category": choose from the categories the shopper has shown interest in; if unknown, use "trending".
  - Do not repeat back email, user IDs, or any personal identifiers.
  - If you have insufficient signal, set urgency to "low" and keep the message generic but on-brand.
  ```

User Prompt:

```wrap
Current event: {{event.tealium_event}}
Shopper location: {{event.customer_city}}
Products in view/cart: {{event.product_names}}
Categories: {{event.product_categories}}
Brands: {{event.product_brands}}
Price(s): {{event.prices}} {{event.currency}}
Recent activity (most recent last): {{history}}
```

* Temperature: `0.7`
* Max Tokens: `150`
* Max Event History: `5`

**Mappings:**

* Command triggers:
    * `event_name == "product_view"` → `store_event`
    * `event_name == "app_background"` → `trigger_inference`
* Context mappings:
    * `product_name`, `product_price`, and `page_name` → `context`
* Prompt variable mappings:
    * `cart_contents` → `cart_contents`

When the `app_background` event fires, the module sends the configured prompts to the on-device model. It injects the last five stored events as `{{history}}` and the current cart contents from the data layer as `{{event.cart_contents}}`. The model returns a JSON response the app parses to display a personalized push notification.
