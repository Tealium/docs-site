---
title: Use AI with Tealium
description: Learn how Tealium gives AI agents customer context, enriches data with AI models, sends data to AI services, and helps you configure Tealium with AI.
url: https://docs.tealium.com/get-started/use-ai-with-tealium/
---
AI agents and models make better decisions with current customer data. Tealium supplies that data to the AI systems you choose, adds AI output to visitor profiles, and includes AI assistants that help your teams configure Tealium.

## Give AI agents customer context

AI agents need current context about the customer they serve. The Context API MCP server gives agents that context through the Model Context Protocol (MCP), a standard way for AI agents to call tools. Agents receive the same visitor profile data that your apps request, such as audiences, badges, and attributes.

For example, an AI support agent loads a visitor's recent activity and audience memberships when a conversation starts.


![](https://docs.tealium.com/images/icons/icon-moments-api.svg)

#### Context API MCP server

Give AI agents real-time access to visitor profile data through MCP.


## Enrich data with AI

AI enrichments run large language model (LLM) processing on event or visitor data as part of the Tealium data pipeline. For example, an AI enrichment can classify the sentiment of a product review or infer a visitor's shopping intent from recent browsing. The output returns to Tealium as a new event, so audiences and connectors can act on it.


![](https://docs.tealium.com/images/icons/icon-star.svg)

#### AI enrichments

Send customer data to an LLM and return the output to Tealium.


## Send data to AI services

AI connectors send event and visitor data to AI platforms, such as Amazon Bedrock, Google Vertex AI, and OpenAI, for prompt-based inference. Model responses return to Tealium as events, and enrichments write the results to visitor profiles.


![](https://docs.tealium.com/images/icons/icon-connector.svg)

#### AI connectors

Learn how AI connectors send customer data to AI platforms.


## Configure Tealium with AI

AI features in the Tealium interface help you build and maintain your configuration:

* **AI Assistant**: Answers questions about configuring and using Tealium.
* **AI audience recommendations**: Suggests audiences based on your attributes and visitor data.
* **Functions writer**: Generates function code, trigger rules, and test payloads.
* **Note generation**: Writes descriptions for configuration items.
* **SQL writer**: Generates queries for cloud data sources.

Tealium Studio is an AI chat interface for questions about your server-side configuration, such as how a component is configured or which components depend on each other.

The Configuration MCP server connects external AI clients, such as Claude, to your server-side profile, so you can explore and change your configuration in natural language.


![](https://docs.tealium.com/images/icons/icon-star.svg)

#### AI features

Learn about the AI features in the Tealium interface and how to turn them on.



![](https://docs.tealium.com/images/icons/icon-audience.svg)

#### AI audience recommendations

Get AI-generated suggestions for new audiences.



![](https://docs.tealium.com/images/icons/icon-code.svg)

#### Functions writer

Generate and debug function code with AI.



![](https://docs.tealium.com/images/icons/icon-cube.svg)

#### Tealium Studio

Ask natural-language questions about your server-side configuration.



![](https://docs.tealium.com/images/icons/icon-gear.svg)

#### Configuration MCP server

Explore and change your server-side configuration from an AI client.



![](https://docs.tealium.com/images/icons/icon-book-solid.svg)

#### Documentation for AI agents

Use Tealium documentation with AI agents and LLMs.

