---
title: Moments API managed MCP server
description: Learn about the Moments API managed MCP server.
url: https://docs.tealium.com/server-side/moments-api/managed-mcp-server/
---
## Overview
The Moments API managed MCP server enables secure, real-time access to visitor profile data using the Model Context Protocol (MCP). AI systems connect to this server to retrieve customer context for instant personalization, analytics, and automation. Tealium MCP services are part of our managed native AI protocol support, which currently includes Agent-to-Agent (A2A) protocol support.

## Requirements

* **Moments API engine**: You must have at least one active [Moments API engine]().
* **API Key**: Access to the managed MCP server requires an API key dedicated to this feature. Contact Tealium Support to request a key.

## How it works

The managed MCP server operates by exposing tools that can be triggered through specific instructions and parameters. These tools allow you to query visitor profile data in real-time, enabling personalized responses and insights.

To interact with the managed MCP server, you need to provide clear and concise instructions to the Large Language Model (LLM). These instructions should include:

* **Context**: Explain the purpose of the interaction and what information you expect to receive.
* **Parameters**: Clearly mention the required parameters for the tool, such as `account`, `profile`, `engineId`, and any visitor-specific identifiers.

### Instructions and prompt

This section outlines the key concepts for writing effective instructions and prompts when interacting with the MCP server.

1. **Instructions: Use static parameters**  
   The instructions define the static parameters required by the MCP tool, such as the `account`, `profile`, and `engineId`. These parameters remain constant for a given configuration and ensure that the MCP tool knows which account, profile, and engine to use when processing requests. For example:  
   ```none
   Use the Tealium MCP tools to answer the questions.
   Use the following required parameters:
   * Tealium Account: my_account
   * Tealium Profile: my_profile
   * Tealium Engine ID: engine_001
   ```

2. **Prompt: Use dynamic parameters**  
   The prompt specifies the dynamic parameters required by the MCP tool, such as visitor-specific values required by each tool. These parameters vary depending on the specific visitor or use case being queried. By referencing dynamic parameters in the prompt, the MCP tool can retrieve data tailored to the current context. For example:  
   ```none
   Is the anonymous visitor {anon_visitor_id} part of the VIP Audience?
   ```

3. **Response data: Reference specific properties**  
   The prompt should include references to the specific properties of the response data that are expected, such as `audiences`, `attributes`, or `badges`. This ensures that the MCP tool returns only the relevant data needed for the use case, improving clarity and reducing unnecessary output. For example:  
   ```none
   Here is the visitor&#39;s list of audiences: {response.audiences}
   ```  
   This guides the MCP tool to focus on the `audiences` property in the response, ensuring the output aligns with the requirements of the prompt. For more information, see [Moments API: Objects]().  

By combining static parameters in the instructions, dynamic parameters in the prompt, and specific response properties, you can create precise and effective queries for the MCP server.

## Best practices

To achieve the best results from this solution, we strongly recommend the following:

**Use attribute names** (Strongly recommended)  
By default, the Moments API engine returns numeric attribute IDs, which lack context for LLMs. For best results, configure the engine to return attribute names instead. Attribute names are descriptive and help LLMs interpret and respond accurately. If your account uses acronyms or abbreviations that are not widely recognized, the LLM may have difficulty interpreting them. Consider reviewing and updating attribute names to ensure they are descriptive and easily understood by both humans and AI systems.

Using attribute names is the only viable approach for leveraging the managed MCP server with LLM-based solutions. For more information, see [Moments API: Objects]().

**Dedicated Moments API engine**  
Do not reuse existing Moments API engines created for other purposes. Create a separate engine for each managed MCP server use case, configured only with the attributes, badges, and audiences needed for that scenario. This ensures:

* Only relevant data is exposed and precise context is provided.
* Reduced complexity and easier maintenance.
* Simpler auditing and updates as requirements change.

**Use specific visitor data**  
Avoid exposing large sets of visitor data in your Moments API engine that is unrelated to the use case. Only include attributes, badges, and audiences essential to your specific use case. Supplying unnecessary data can overwhelm the LLM and reduce response accuracy. A focused set of relevant data improves clarity and response quality.

## Available tools

All tools support the following parameters:

| Parameter | Description |
| --------- | ----------- |
| `account` | (Required) The name of your Tealium account. |
| `profile` | (Required) The name of the profile within your Tealium account. |
| `engineId` | (Required) The engine ID of the Moments API endpoint. |
| `Origin` | (Required) The origin that initiated the request. |
| `Referer` | (Required) The absolute or partial address that initiated the request. |
| `suppressNotFound` | Determines the response type returned when a visitor record is not found.&lt;br&gt;`false` (default): Returns the HTTP status code `404 Not Found`.&lt;br&gt;`true`: Returns the HTTP status code `200 OK` with an empty response body. |


The Moments API managed MCP server includes the following tools:

### `getPersonalizationContentByAnonymousId`

Retrieve visitor data using the Tealium anonymous ID. For more information, see .

| Parameter | Description |
| --------- | ----------- |
| `visitorId` | (Required) A unique and anonymous value assigned to a visitor on each visit to a site or each use of an app. The anonymous ID tracks a visitor over multiple visits from the same browser or app, but not across different browsers or devices. |

To use this tool, format your prompt specifically to mention the anonymous ID, for example:

```none
What is anonymous visitor {visitor_id} interested in?
```

### `getPersonalizationContentByVisitorId`

Retrieve visitor data using a visitor ID attribute, by specifying the attribute ID and attribute lookup value. For more information, see .

| Parameter | Description |
| --------- | ----------- |
| `attributeId` | (Required) The numeric UID representing a [visitor ID attribute](). |
| `attributeValue` | (Required) The value of the attribute to look up. |

To use this tool, format your prompt specifically to mention the attribute ID and value to search, for example:

```none
What is visitor attribute id {visitor_attribute_id} with value {visitor_attribute_value} interested in?
```

## OpenAI Agent SDK solution

The following sample code demonstrates how to connect to the Moments API managed MCP server with the OpenAI Agent for Python and ask a question about the visitor. The agent instructions specify the static parameters related to the request. The prompt assumes the visitor&#39;s anonymous ID is known.

For more information, see [OpenAI Agents SDK: Model context protocol (MCP)](https://openai.github.io/openai-agents-python/mcp/).



```python
import asyncio
import os

from agents import Agent, HostedMCPTool, Runner

async def main() -&gt; None:
    agent = Agent(
        name=&#34;Assistant&#34;,
        instructions=f&#34;&#34;&#34;
                Use the Tealium MCP tools to answer the questions.
                Tealium Account: my_account
                Tealium Profile: my_profile
                Tealium Engine Id: engine_001
                &#34;&#34;&#34;,
        tools=[
            HostedMCPTool(
                tool_config={
                    &#34;type&#34;: &#34;mcp&#34;,
                    &#34;server_label&#34;: &#34;tealium_personalization_mcp&#34;,
                    &#34;server_url&#34;: &#34;https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp&#34;,
                    &#34;require_approval&#34;: &#34;never&#34;,
                    &#34;headers&#34;: {
                        &#34;X-Tealium-Api-Key&#34;: os.getenv(&#39;TEALIUM_API_KEY&#39;),
                        &#34;Origin&#34;: &#34;https://example.com&#34;,
                        &#34;Referer&#34;: &#34;https://example.com&#34;
                    }
                }
            )
        ],
    )

    anon_visitor_id = &#39;1234567&#39;
    query = f&#39;&#39;&#39;
    Is the anonymous visitor {anon_visitor_id} part of the VIP Audience? Here is the visitor&#39;s list of audiences: {response.audiences}
    &#39;&#39;&#39;
    result = await Runner.run(agent, query)
    print(result.final_output)

if __name__ == &#34;__main__&#34;:
    asyncio.run(main())
```



```python
import asyncio
import os

from agents import Agent, Runner
from agents.mcp import MCPServerStreamableHttp
from agents.model_settings import ModelSettings

async def main() -&gt; None:
    api_key = os.environ[&#34;TEALIUM_API_KEY&#34;]

    async with MCPServerStreamableHttp(
            name=&#34;Tealium MCP Streamable HTTP Server&#34;,
            params={
                &#34;url&#34;: &#34;https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp&#34;,
                &#34;headers&#34;: {
                    &#34;X-Tealium-Api-Key&#34;: api_key,
                    &#34;Origin&#34;: &#34;https://example.com&#34;,
                    &#34;Referer&#34;: &#34;https://example.com&#34;
                },
                &#34;timeout&#34;: 10,
            },
            max_retry_attempts=3
    ) as server:
        agent = Agent(
            name=&#34;Assistant&#34;,
            instructions=f&#34;&#34;&#34;
                Use the Tealium MCP tools to answer the questions.
                Tealium Account: my_account
                Tealium Profile: my_profile
                Tealium Engine ID: engine_001
                &#34;&#34;&#34;,
            mcp_servers=[server],
            model_settings=ModelSettings(tool_choice=&#34;required&#34;),
        )

        anon_visitor_id = &#39;1234567&#39;
        query = f&#39;&#39;&#39;
        Is the anonymous visitor {anon_visitor_id} part of the VIP Audience? Here is the visitor&#39;s list of audiences: {response.audiences}
        &#39;&#39;&#39;
        result = await Runner.run(agent, query)
        print(result.final_output)

if __name__ == &#34;__main__&#34;:
    asyncio.run(main())
```



## Test the MCP server with MCP Inspector

We suggest that you use a tool such as the open-source MCP Inspector to connect to the MCP server.

Use the MCP Inspector to:

* Verify server connectivity.
* Review available tools and their parameters.
* Troubleshoot authentication or configuration issues.
* Speed up development of MCP-based integrations.

For more information, see [Model Context Protocol &gt; Getting started](https://modelcontextprotocol.io/docs/tools/inspector#getting-started).

To run MCP Inspector and test the MCP server:

1. Open a terminal and run:  
    ```
    npx @modelcontextprotocol/inspector
    ```
    This installs MCP Inspector and opens the tool in a browser window.
1. Set **Transport Type** to `Streamable HTTP`.
1. Set the **URL** to `https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp`. The region must match the region of your Moments API engine.
1. Under **Custom Headers**, add the `X-Tealium-Api-Key` key and your MCP server API key. The MCP API key is a dedicated API key for MCP server access and must be requested from Tealium Support.

![](/images/server-side/moments-api/moments-mcp-server-inspector-config.png)

Click **Connect** and the status updates to **Connected** and the **List Tools** button appears.

To run a tool on the server:

1. Click **List Tools** to inspect available tools.
1. Click a tool to see its definition.
1. Enter values for the required parameters.
1. Click **Run Tool**.
1. Under **Tool Result**,  the `Success` message and Moments API result appears.
