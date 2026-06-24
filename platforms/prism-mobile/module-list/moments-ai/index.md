---
title: Moments AI module
description: Add and configure the Moments AI module in your Prism SDK app.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/moments-ai/
---
## Configuration

When adding the module, configure the following settings:

* **System Prompt**: Define the AI model&#39;s role and output format. This prompt sets the overall behaviour and constraints for every inference. Example: instruct the model to return JSON in a specific schema, or to act as a particular type of assistant. Supports variable substitution using `{{handlebars}}` syntax.
* **User Prompt**: Provide the per-request instructions sent to the model. Use `{{event.&lt;key&gt;}}` to insert values from the current event (e.g. `{{event.user_name}}`), and `{{history}}` to include recent event history. These placeholders are replaced at runtime with real data from the mapped context. Supports variable substitution using `{{handlebars}}` syntax.
* **Temperature**: Numeric input for model temperature.
* **Max Tokens**: Max output tokens for the on-device model.
* **Max Event History**: Number of recent events to retain as context for the model.

## Rules

The module dispatches (or collects for) any event. For more information, see [Rules](/platforms/prism-mobile/rules/).

## Data mappings

Mapping is the process of sending the value of an event variable to the corresponding destination variable in the vendor module.

The available categories are:

### Command Triggers
To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `trigger_inference` | Run the AI model |
| `store_event` | Save the event into history for context |


### Config Overrides

| Variable | Description |
|:---------|:------------|
| `system_prompt` | System Prompt |
| `user_prompt` | User Prompt |
| `temperature` | Temperature |
| `max_tokens` | Max Tokens |
