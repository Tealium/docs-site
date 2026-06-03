---
title: Amazon Bedrock AI Connector Setup Guide
description: Set up the Amazon Bedrock AI connector to send Tealium event and visitor data to foundation models, managed prompts, or multi-step Bedrock workflows for real-time enrichment.
url: https://docs.tealium.com/server-side-connectors/amazon-bedrock-ai-connector/
---
For an overview of how AI connectors work and guidance on when to use an AI connector or Tealium functions, see [AI connectors and Tealium functions]().

## Supported models

The Amazon Bedrock AI connector supports a wide range of foundation models. For the current list of supported models, see [Amazon Bedrock: Supported foundation models in Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html).

Some Bedrock models require provisioned throughput and cannot be invoked using on-demand inference. If you encounter an on-demand throughput error, use a model that supports `ON_DEMAND` inference or provide a provisioned throughput or inference profile ARN in the configuration list.

## Create IAM roles and permissions

Tealium requires IAM roles and permissions in your AWS account to connect to Amazon Bedrock from your server-side connector. You have two options for authenticating the connection:

* [Provide an Access Key and Access Secret](#access-key-and-secret-credentials).
* [Provide STS credentials](#sts-credentials).

### Access key and secret credentials

To create your AWS access key and secret:

1. Log in to the AWS Management Console and go to the **IAM** (Identity and Access Management) service.
1. Click **Users** and then click **Add user**.
1. Enter a username. For example, `TealiumBedrockUser`.
1. Attach policies to the user. For more information, see [Attach policies](#attach-policies).
1. Create the keys.
    * Go to the **Security credentials** tab and click **Create Access Key**.
    * Copy the **Access Key ID** and **Secret Access Key**, and save them securely.

### STS credentials

To create your STS credentials:

1. Log in to the AWS Management Console and go to the **IAM** (Identity and Access Management) service.
1. Click **Roles**, and then click **Create role**.
1. Under **Trusted entity type**, select the AWS account.
1. Select **Another AWS account** and enter the Tealium account ID: `757913464184`.
1. (Optional) Select the **Require external ID** checkbox and specify the external ID that you want to use. External IDs can be up to 256 characters long and can include alphanumeric characters (`A-Z`, `a-z`, `0-9`) and symbols, such as hyphens (`-`), underscores (`_`), and periods (`.`).
1. Enter a name for the role. The role name must start with `TealiumBedrock`. For example: `TealiumBedrock-RoleName`.
1. Attach policies to the role. For more information, see [Attach policies](#attach-policies).
1. Create a trust policy.
    * Go to the **Trust relationships** tab and click **Edit trust relationship**.
    * Ensure that the trust policy allows the specific external ID to use the role you created and that the Tealium production account ID is `757913464184`.
    * Set the `EXTERNAL_ID` value for the connection to Tealium. The ID can be up to 256 characters long and can include alphanumeric characters (`A-Z`, `a-z`, `0-9`) and symbols, such as hyphens (`-`), underscores (`_`), and periods (`.`).

```json
    {
      &#34;Version&#34;: &#34;2012-10-17&#34;,
      &#34;Statement&#34;: [
        {
          &#34;Effect&#34;: &#34;Allow&#34;,
          &#34;Principal&#34;: {
            &#34;AWS&#34;: &#34;arn:aws:iam::757913464184:root&#34;
          },
          &#34;Action&#34;: &#34;sts:AssumeRole&#34;,
          &#34;Condition&#34;: {
            &#34;StringEquals&#34;: {
              &#34;sts:ExternalId&#34;: &#34;EXTERNAL_ID&#34;
            }
          }
        }
      ]
    }
```

### Attach policies

In the AWS Management Console, enter the necessary policies for the connector actions you are using. The following policies are required for each connector action:

We recommend that you limit permissions to the specific ARNs of flows and Lambda functions you require.




```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;ListModels&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:ListFoundationModels&#34;
      ],
      &#34;Resource&#34;: &#34;*&#34;
    },
    {
      &#34;Sid&#34;: &#34;InvokeModel&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:InvokeModel&#34;
      ],
      &#34;Resource&#34;: &#34;*&#34;
    }
  ]
}
```



```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;RenderManagedPrompt&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:RenderPrompt&#34;
      ],
      &#34;Resource&#34;: &#34;*&#34;
    }
  ]
}

```



If you are using Lambda:

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;BedrockFlowInvoke&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:InvokeFlow&#34;
      ],
      &#34;Resource&#34;: &#34;arn:aws:bedrock:&lt;REGION&gt;:&lt;ACCOUNT_ID&gt;:flow/&lt;flow_id&gt;/alias/&lt;alias_name&gt;&#34;
    },
    {
      &#34;Sid&#34;: &#34;LambdaInvokeFunction&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;lambda:InvokeFunction&#34;
      ],
      &#34;Resource&#34;: &#34;arn:aws:lambda:&lt;REGION&gt;:&lt;ACCOUNT_ID&gt;:function:&lt;FUNCTION_NAME&gt;&#34;
    }
  ]
}
```

If you are not using Lambda:

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;BedrockFlowInvoke&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;bedrock:InvokeFlow&#34;
      ],
      &#34;Resource&#34;: &#34;arn:aws:bedrock:&lt;REGION&gt;:&lt;ACCOUNT_ID&gt;:flow/&lt;flow_id&gt;/alias/&lt;alias_name&gt;&#34;
    }
  ]
}
```



To enter and attach the policies:

1. In the AWS console, go to **IAM &gt; Policies** and click **Create policy**.
1. In the policy editor, select the **JSON** tab, paste the policy for your connector action, resolve any validation warnings, and click **Next**.
1. Enter a policy name (for example, `TealiumCustomAccessPolicy`) and optional description, then click **Create policy**.
1. Go to **IAM &gt; Roles** and select the role you want to modify.
1. On the **Permissions** tab, click **Add permissions &gt; Attach policies**.
1. Search for your custom policy, select it, and click **Attach policies**.

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Authentication Type**: (Required) The type of authentication to use.
    * **Access Key**
        * **Access Key**: (Required) Provide your IAM user&#39;s access key. The associated IAM policy (for either IAM user or Assumed Role) must grant `bedrock:PutRecord` permission along with streams you want to send data to.
        * **Secret Key**: (Required) Provide your IAM user&#39;s secret key.
    * **STS**
        * **STS - Assume Role: ARN**: (Required) An Amazon Resource Name assigned to the role to assume. For more information, see: [AWS: Switching to an IAM Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).
        * **STS - Assume Role: Session Name**: (Required) A unique identifier of the assumed role session.
        * **STS - Assume Role: External ID**: (Optional) A unique identifier used by third parties when assuming roles in their customers&#39; accounts. For more information, see: [AWS: Access to AWS accounts owned by third parties](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html).
* **Region**: (Required) Select a region.


## Prompt information

A Bedrock AI prompt, whether sent from Tealium, managed within Amazon Bedrock, or used in a flow, must be authored to return only valid JSON for Tealium to correctly process the response. Use the following guidelines:

* Use double curly braces to reference mapped parameters, for example: `{{tealium_account}}`, `{{tealium_profile}}`, `{{tealium_visitor_id}}`, `{{visitor_json}}`.
* Clearly instruct the model to return only valid JSON with no explanations, no markdown, no code fences, and no extra text before or after the JSON.
* Define the exact JSON structure you expect (field names, required keys, and value types) so the output can be parsed safely.
* Instruct the model to return Tealium fields explicitly (for example, `tealium_account`, `tealium_profile`, `tealium_visitor_id`, `tealium_event`).
* If you need to reference a specific attribute in the prompt, map that attribute to a vendor parameter. For example, map `Last product viewed` to `last_product_viewed` and reference it in the prompt as `{{last_product_viewed}}`.
* Avoid vague instructions. Write deterministic prompts so that repeated calls produce the same JSON schema.
* For best results, include a line such as: &#34;Return a single JSON object only, with no prose, no backticks, and no additional formatting.&#34;

### Prompt example

```none
You are an AI assistant that must return only valid JSON.
Do not include explanations, markdown, code fences, or any text outside the JSON object.

Using the visitor data below, calculate a numeric score between 0 and 100 that represents
the visitor&#39;s likelihood to convert in this session.

Return a single JSON object only, with this exact structure:

{
  &#34;tealium_account&#34;: &#34;{{tealium_account}}&#34;,
  &#34;tealium_profile&#34;: &#34;{{tealium_profile}}&#34;,
  &#34;tealium_visitor_id&#34;: &#34;{{tealium_visitor_id}}&#34;,
  &#34;tealium_event&#34;: &#34;bedrock_ai_insight&#34;,
  &#34;visitor_score&#34;: &lt;integer between 0 and 100&gt;
}

Visitor data:
{{visitor_json}}

Pay particular attention to the value of {{last_product_viewed}}.

```

The response will resemble the following:

```json
{
    &#34;metrics&#34;: {
        &#34;latencyMs&#34;: 1272
    },
    &#34;output&#34;: {
        &#34;message&#34;: {
            &#34;content&#34;: [
                {
                    &#34;text&#34;: &#34;{\&#34;tealium_account\&#34;:\&#34;your-account\&#34;,\&#34;tealium_profile\&#34;:\&#34;main\&#34;,\&#34;tealium_visitor_id\&#34;:\&#34;__your-account_main__5574_438850__\&#34;,\&#34;tealium_event\&#34;:\&#34;bedrock_ai_insight\&#34;,\&#34;visitor_score\&#34;:85}&#34;
                }
            ],
            &#34;role&#34;: &#34;assistant&#34;
        }
    },
    &#34;stopReason&#34;: &#34;end_turn&#34;,
    &#34;usage&#34;: {
        &#34;inputTokens&#34;: 8811,
        &#34;outputTokens&#34;: 65,
        &#34;serverToolUsage&#34;: {},
        &#34;totalTokens&#34;: 8876
    }
}
```

The connector accepts the response and sends the JSON event object to the Tealium Collect API endpoint.

## Amazon Bedrock Flows

Amazon Bedrock Flows are multi-step AI orchestrations that combine prompts, knowledge bases, Lambda functions, conditional logic, and external data into a single reusable workflow. A flow defines how input data moves through prompts, enrichment steps, business logic, and final output to turn complex AI decisioning into a single API endpoint.

To use the **Send Data to Bedrock Flow** action, create a flow in Amazon Bedrock that accepts input from Tealium, processes it through your AI steps, and sends the results back to Tealium through a Lambda function.

The sections below describe the required and optional components of a flow.

### Step 1 - Define the flow input

Every flow begins with an input node. This node represents the JSON document Tealium sends to the flow.

Tealium sends your mapped attributes in the following format similar to the following example:

```json
&#34;document&#34;: {
    &#34;tealium_account&#34;: &#34;services-example&#34;,
    &#34;tealium_profile&#34;: &#34;ai&#34;,
    &#34;tealium_visitor_id&#34;: &#34;1234567890abc&#34;,
    &#34;visitor_profile&#34;: {
        &#34;lifetime_value&#34;: &#34;1200&#34;,
        &#34;total_orders&#34;: 5,
        ...
        }
}
```

Inside your flow, reference fields using `$.data.attribute_name`. Based on the previous example:

| Tealium Attribute | Bedrock Reference | Example |
| -----| ----- | ----- |
| `tealium_account` | `$.data.tealium_account` or `{{tealium_account}}` | `services-example` |
| `tealium_profile` | `$.data.tealium_profile` or `{{tealium_profile}}` | `ai` |
| `tealium_visitor_id` | `$.data.tealium_visitor_id` or `{{tealium_visitor_id}}` | `1234567890abc` |
| `visitor_profile` | `$.data.visitor_profile` |  `&#34;visitor_profile&#34;: {&#34;lifetime_value&#34;: &#34;1200&#34;,&#34;total_orders&#34;: 5,...}` |

### Step 2 - Map data into a prompt node (Required)

Next, add a prompt node to generate AI output (such as a score, recommendation, or decision).

Inside the prompt node:

1. Set your prompt text.
1. Insert variables using the `{{fieldname}}` format. For example, `{{tealium_account}}`.
1. Choose a Bedrock model.
1. Return valid JSON as the output of the prompt.

For an example, see the [Prompt example](#prompt-example) section above.

### Step 3 - (Optional) Add knowledge base retrieval

Amazon Bedrock Knowledge Bases let you connect your AI workflows to external data sources, such as Amazon S3, Amazon Redshift, or Amazon OpenSearch Service. A knowledge base stores and indexes your documents, making them available for retrieval and grounding during prompt execution. When you add a knowledge base node to your flow, the model can use relevant information from your data to generate more accurate and context-aware responses. This step is optional, but it is valuable for personalization, recommendations, or contextual decisioning.

After you connect the knowledge base, you can pass knowledge base results into your prompt using fields like `{{$.kbResults}}`.

For more information on knowledge bases, see [Amazon Bedrock: Retrieve data and generate AI responses with Amazon Bedrock Knowledge Bases](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html).

For more information on creating a knowledge base, see [Amazon Bedrock: Create a knowledge base by connecting to a data source in Amazon Bedrock Knowledge Bases](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-create.html).

### Step 4 - Add a Lambda node to send results back to Tealium (Required for Tealium Integration)

After your prompt produces structured JSON, you must send that result back into Tealium for profile enrichment.

Add a Lambda node that:

* Receives the prompt output (`$.data` from your prompt node).
* Parses the JSON.
* Posts it to Tealium Collect: `POST https://collect.tealiumiq.com/event`.
* Includes the following:
  * `tealium_account`
  * `tealium_profile`
  * `tealium_visitor_id`
  * `tealium_event` (user-defined)
  * Your AI output fields (for example, `visitor_score`)

Use [our provided Lambda example](#lambda-example) or build your own.

### Step 5 - Add a flow output node

Although Tealium does not process the flow’s API response, an output node is required to complete the flow.

Connecting your Lambda output to the `FlowOutputNode` doesn’t affect Tealium processing, but helps you verify that the flow works with the following tools:

* Debug in the Bedrock console.
* View errors from the Lambda function.
* Inspect final JSON results for validation.
* View output in Tealium using Trace.

#### Lambda example

The following is a Lambda example for accepting prompt output, parsing the JSON, and sending that data to the Tealium Collect endpoint for enrichment and activation in Tealium. It includes fallbacks to account for various data structures. Rewrite yours as needed.

The account and profile must be configured to accept server-side events with the specified data source.

This example requires Node.js version 18.x or later as the runtime environment.


```js
const COLLECT_URL = process.env.COLLECT_URL || &#34;https://collect.tealiumiq.com/event&#34;;
function extractInputByName(event, name) {
  const arr = event?.node?.inputs;
  if (Array.isArray(arr)) {
    const hit = arr.find(i =&gt; i?.name === name);
    if (hit &amp;&amp; typeof hit.value === &#34;string&#34;) return hit.value;
    if (hit &amp;&amp; typeof hit.value === &#34;object&#34;) return JSON.stringify(hit.value);
  }
  return undefined;
}
function extractJsonStringFromEvent(event) {
  const fromStandardPin = extractInputByName(event, &#34;codeHookInput&#34;);
  if (typeof fromStandardPin === &#34;string&#34;) return fromStandardPin;
  const anyString = event?.node?.inputs?.find?.(i =&gt; typeof i?.value === &#34;string&#34;)?.value;
  if (typeof anyString === &#34;string&#34;) return anyString;
  if (typeof event?.codeHookInput === &#34;string&#34;) return event.codeHookInput;
  if (typeof event?.document === &#34;string&#34;) return event.document;
  const doc = event?.fields?.[0]?.content?.document;
  if (typeof doc === &#34;string&#34;) return doc;
  if (typeof event === &#34;string&#34;) return event;
  throw new Error(&#34;Could not find JSON string in event&#34;);
}
export const handler = async (event) =&gt; {
  try {
    const jsonStr = extractJsonStringFromEvent(event);
    const obj = JSON.parse(jsonStr);  // Fixed: store parsed result
    const required = [&#34;tealium_account&#34;, &#34;tealium_profile&#34;, &#34;tealium_visitor_id&#34;];
    for (const key of required) {
      if (!Object.prototype.hasOwnProperty.call(obj, key)) {
        throw new Error(`Missing required field &#39;${key}&#39; in model output`);
      }
    }
    const r = await fetch(COLLECT_URL, {
      method: &#34;POST&#34;,
      headers: { &#34;Content-Type&#34;: &#34;application/json&#34; },
      body: jsonStr
    });
    if (!r.ok) {
      const txt = await r.text().catch(() =&gt; &#34;&#34;);
      throw new Error(`Collect failed ${r.status}: ${txt}`);
    }
    return jsonStr;
  } catch (err) {
    console.error(&#34;Shim error:&#34;, err);
    return JSON.stringify({ ok: false, error: String(err.message || err) });
  }
};
```


## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Prompt to Bedrock AI Model | ✓ | ✓ |
| Send Data to Bedrock AI Managed Prompt | ✓ | ✓ |
| Send Data to Bedrock AI Workflow | ✓ | ✓ |


### Send Prompt to Bedrock AI Model

Use **Send Prompt to Bedrock AI Model** when you need a simple, single-model call that returns a response synchronously through the connector.

#### Parameters

| Parameter | Description |
| --- | --- |
| Model ID or Inference Profile ARN | Select an Amazon Bedrock model to use on-demand inference, or manually enter a Provisioned Throughput model ARN or inference profile ARN.&lt;br&gt;Only models that support on-demand inference and text input/output are shown.&lt;br&gt;If the model you want does not appear, verify that the model is enabled in your AWS account and region and that it supports on-demand inference.&lt;br&gt;&lt;br&gt;&lt;br&gt;If using Provisioned Throughput, enter the full model ARN (for example: `arn:aws:bedrock:region:account-id:provisioned-model/...`).&lt;br&gt;Inference profile ARNs may also be used if configured in your AWS account.&lt;br&gt;Model availability and supported inference types are determined by your AWS account permissions and region configuration.|
| Prompt Parameters | Map parameters to a placeholder to replace in the prompt. By default, the connector has access to `{{tealium_account}}`, `{{tealium_profile}}`, and `{{tealium_visitor_id}}`. These can be overwritten with mapping. |
| Add Visitor Profile | (Only audience actions) Whether to allow the visitor profile for use in the prompt template as the variable `{{visitor_profile}}`. |
| Add Current Visit | (Only audience actions) Whether to include current visit data in the `{{visitor_profile}}` object. |
| Add Event Payload | (Only event actions) Whether to allow the event payload for use in the prompt template as the variable `{{event_payload}}`. |
| Prompt | &lt;ul&gt;&lt;li&gt;Use double curly braces to reference mapped parameters, for example: `{{tealium_account}}`, `{{visitor_id}}`, `{{event_value}}`.&lt;/li&gt;&lt;li&gt;Use `{{visitor_profile}}` to include the visitor profile in the prompt.&lt;br&gt;Clearly instruct the model to return only valid JSON, with no explanations, markdown, code fences, or extra text.&lt;/li&gt;&lt;li&gt;Define the exact JSON structure expected (for example, field names, required keys, value formats).&lt;/li&gt;&lt;li&gt;If Tealium fields must be included, specify them explicitly in the prompt.&lt;br&gt;Avoid ambiguous phrasing. Write deterministic prompts.&lt;/li&gt;&lt;li&gt;Include direct instructions such as: &#34;Return a single JSON object only, with no prose, no backticks, and no extra formatting.&#34;&lt;/li&gt;&lt;/ul&gt; |
| Debug Mode | When debug mode is enabled, the connector accepts the raw Bedrock response without sending it to Tealium Collect. Use Trace to validate the response format before enabling full processing. |

#### Inference Parameters

For more information, see [Amazon Bedrock API Reference: InferenceConfiguration](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_agent_InferenceConfiguration.html).

| Parameter | Description |
| --- | --- |
| `maxTokens` | Maximum number of tokens the model may generate in its response. Lower values produce shorter outputs and help reduce latency, cost, and throttling risk. |
| `temperature` | Controls randomness in the output. Lower values (such as `0.2`) make responses more deterministic and higher values (such as `0.8`) produce more creative and varied results. |
| `topP` | Nucleus sampling parameter that limits token selection to the smallest set whose cumulative probability exceeds this value. Lower values make output more focused; higher values allow more diversity. |
| `stopSequences` | One or more strings that cause the model to stop generating when encountered. Useful for truncating responses or enforcing structured output boundaries. |

### Send Data to Bedrock AI Managed Prompt

Use **Send Data to Bedrock AI Managed Prompt** when you want a reusable, versioned call to a prompt that returns a response synchronously through the connector.

| Parameter | Description |
| --- | --- |
| Prompt ARN | (Required) Provide the ARN of a Bedrock Prompt Management template. The prompt ARN can be found in the **Overview** section of the prompt details in Bedrock. |
| Prompt Data | &lt;ul&gt;&lt;li&gt;Tealium passes mapped attributes into the prompt when invoking it.&lt;/li&gt;&lt;li&gt;The connector includes the variables `tealium_account`, `tealium_profile`, and `tealium_visitor_id` in the prompt. These can be overwritten with mapping.&lt;/li&gt;&lt;li&gt;Write the prompt to clearly instruct the model to return only valid JSON, with no explanations, no markdown, no code fences, and no additional text before or after the JSON.&lt;/li&gt;&lt;li&gt;You must author the prompt to include instructions for the model to return `tealium_account`, `tealium_profile`, and `tealium_visitor_id` in the JSON.&lt;/li&gt;&lt;li&gt;Avoid ambiguous phrasing. Write deterministic prompts so the output can be parsed reliably.&lt;/li&gt;&lt;li&gt;For best results, include a direct instruction such as: &#34;Return a single JSON object only, with no prose, no backticks, and no extra formatting.&#34;&lt;/li&gt;&lt;/ul&gt; |
| Add Visitor Profile | (Only audience actions) Whether to allow the visitor profile for use in the prompt template as the variable `{{visitor_profile}}`. |
| Add Current Visit | (Only audience actions) Whether to include current visit data in the `{{visitor_profile}}` object. |
| Add Event Payload | (Only event actions) Whether to allow the event payload for use in the prompt template as the variable `{{event_payload}}`. |
| Debug Mode | When debug mode is enabled, the connector accepts the raw Bedrock response without sending it to Tealium Collect. Use Trace to validate the response format before enabling full processing. |

### Send Data to Bedrock AI Workflow

Use **Send Data to Bedrock AI Workflow** when you need multi-step orchestration or knowledge base retrieval that runs asynchronously through Lambda.

| Parameter | Description |
| --- | --- |
| Bedrock Flow Alias ARN | (Required) Enter the ARN of the Bedrock Flow Alias you want this action to invoke. We recommend creating an alias such as `live` and using that ARN here. |
| Flow Data | &lt;ul&gt;&lt;li&gt;Change which Flow Version that alias points to in AWS without updating this connector.&lt;/li&gt;&lt;li&gt;The connector sends your mapped fields to the Flow as a JSON object named document.&lt;/li&gt;&lt;li&gt;Inside your Flow, reference these fields using `$.data.&lt;fieldName&gt;` in Prompt, Lambda, or other nodes.&lt;/li&gt;&lt;li&gt;By default, `tealium_account`, `tealium_profile`, and `tealium_visitor_id` are included automatically, and can be overwritten through field mappings if needed.&lt;/li&gt;&lt;li&gt;Your flow must include a `FlowOutputNode`, but Tealium does not use its output.&lt;/li&gt;&lt;li&gt;Use Lambda to send data back into Tealium through the Collect endpoint.&lt;/li&gt;&lt;li&gt;We recommend wiring the Lambda output into the `FlowOutputNode` to see success/error information when testing the flow in the Bedrock console.&lt;/li&gt;&lt;/ul&gt; |
| Add Visitor Profile | (Only audience actions) Whether to include the full visitor profile in the Flow input as a `visitor_profile` JSON object. |
| Add Current Visit | (Only audience actions) Whether to include the current visit data in the `visitor_profile` JSON object. |
| Add Event Payload | (Only event actions) Whether to include the event payload in the Flow input as the `event_payload` JSON object. | 

## Common errors and troubleshooting

The following are common error codes and resolutions:

### Common AWS error codes:

* **`AccessDeniedException` or `NotAuthorized`**   
Your IAM user or role doesn’t have the required permissions (for example, `bedrock:InvokeModel`, `bedrock:RenderPrompt`, `bedrock:InvokeFlow`, `bedrock:ListFoundationModels`).  
To solve this, update the IAM policy attached to the role or access keys to include the needed Bedrock actions on the correct resources.

* **`InvalidClientTokenId`, `UnrecognizedClientException`, or `ExpiredTokenException`**  
The configured access keys or STS session are invalid or expired.  
To solve this, rotate and re‑enter credentials in the connector, or verify the STS role and external ID are correct and not expired.

* **`OptInRequired` or `FTUFormNotFilled`**  
The AWS account is not fully enabled for Bedrock or for a specific model (for example, Anthropic).  
To solve this, complete the required Bedrock enablement steps and any model‑specific forms or Marketplace subscriptions in the AWS console.

If you see any of these errors, resolve the IAM or account setup in AWS first. Retrying the connector action alone will not succeed until permissions are corrected.

### Common errors from Bedrock API calls

The following errors mean the request reached Bedrock, but the service or model could not complete it successfully.

* **`ValidationException` or `ValidationError`**  
The request body or parameters are invalid for the target model or API (for example, wrong model ID, unsupported parameters, input too large).  
To solve this, verify the model ID / prompt ARN / flow ARN, ensure the request body matches the model’s expected schema, and reduce prompt size or max tokens if needed.

* **`ResourceNotFound` or `ResourceNotFoundException`**   
The specified model, prompt version, or Flow alias ARN does not exist or is not available in that region.  
To solve this, double‑check ARNs and region in the connector configuration against the values shown in the Bedrock console.

* **`ThrottlingException` or `ServiceQuotaExceededException`**  
Your calls exceed Bedrock quotas (for example, TPS or token limits).  
To solve this, reduce call frequency or request a quota increase in AWS.

* **`ServiceUnavailable`, `InternalFailure`, or `InternalServerException`**  
Temporary or internal errors within Bedrock.  
To solve this, if errors persist, check the AWS Service Health Dashboard or open an AWS Support case.

* **`ModelErrorException`, `ModelNotReadyException`, or `ModelTimeoutException`** (prompt or managed prompt flows)  
The model failed, is still warming up, or took too long to respond.  
To solve this, wait and retry, simplify the prompt or reduce token usage, and confirm the model or provisioned throughput is fully active.

For all of these errors, Tealium displays the original AWS error message from Bedrock so you can match it against AWS documentation when you are troubleshooting.
