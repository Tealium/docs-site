---
title: About Tealium Configuration MCP
description: Tealium Configuration MCP is an AI-native interface for exploring and configuring server-side profiles using natural language.
url: https://docs.tealium.com/server-side/config-mcp/about-config-mcp/
---

<blockquote>
Tealium Configuration MCP is only available to select customers. If you are interested in trying this feature, [contact support](https://docs.tealium.com/support/).
</blockquote>


Tealium Configuration MCP connects AI clients to your server-side profile so you can explore configuration, make changes, and commit new versions using natural language instead of navigating the Tealium UI.

Describe a business goal, such as creating an audience, understanding dependencies, or identifying unused configuration, and the MCP server translates that goal into the required profile configuration.

The MCP server stages AI-generated changes as draft profile revisions. Publishing requires a separate review and action in the Tealium UI.

## Requirements

This feature requires the following:

* **Tealium Platform Permissions:** Your account must use Tealium Platform Permissions. Legacy permissions are not supported.
* **Paid Claude plan:** You must have a Claude Pro, Max, Team, or Enterprise plan. Free plans cannot add custom connectors.

Tealium Configuration MCP is not available for private cloud accounts.

To enable Tealium Configuration MCP for your account, [contact support](https://docs.tealium.com/support/).

## How it works

Tealium Configuration MCP works as a guided, stateful session rather than a collection of independent commands. The MCP server manages session state, maintains a profile draft, and controls when changes are validated and applied. Ask questions or describe the changes you want to make, and the MCP server executes the required steps.

Each session uses the following workflow:

1. **Select a version.** At the start of a chat session, the agent asks which profile version to work against: **Latest Published**, **Latest Saved**, or a specific revision. A temporary draft copy is created. All changes during the session apply to that draft.
1. **Explore.** Ask questions about the profile or request changes. The agent can explain existing configuration, trace dependencies, and create a plan for any changes you want to make. Review the plan before the MCP server proceeds.
1. **Apply patch.** After you confirm the plan, the MCP server applies changes to the draft in sequential patches and continuously validates the profile integrity, attempting to resolve conflicts automatically.
1. **Commit.** After all changes are complete, the agent provides a summary. Confirm the summary to commit.
1. **Review in UI.** Open the new saved version in the Tealium UI, review the changes, and publish manually after completing your organization's approval process.


<blockquote>
Tealium Configuration MCP never publishes profile changes. All changes are saved as a new saved version that requires a manual publish in the Tealium UI.
</blockquote>


## Use cases

Tealium Configuration MCP supports most configuration tasks you would normally complete through the Tealium UI, within the scope of [supported objects](#supported-objects). Common use cases include the following:

**Explore existing configuration**

Summarize a profile, find entities, explain rules and logic, and inspect how configuration is connected.

```wrap
Provide a summary of attributes available in my Tealium profile. Group them by their scope (event/visit/visitor).
```

```wrap
Summarize the rules behind audience A, so I better understand when a user joins or leaves.
```

```wrap
Which connectors are being used most across my configured actions, and what use cases do they support?
```

**Trace dependencies and lineage**

Identify upstream and downstream references for an entity, for example, which enrichments, audiences, rules, connectors, or actions reference a given attribute.

```wrap
Are attributes used by audience A used by any other audiences?
```

```wrap
What is the downstream impact if I change the enrichment of attribute X?
```

```wrap
Which of my active audiences are not wired to any actions or connectors?
```

**Create individual entities**

Add supported profile objects such as attributes, audiences, rules, event specifications, or other available entities.

```wrap
Create a new basic webhook action for the VIP audience. The webhook URL is https://webhook.site/a1b2c3d4-1234-5678-abcd-ef1234567890. The method is POST. Include the entire visitor payload. Trigger when visitors join the audience.
```

```wrap
Create a visitor tally that counts how many different product IDs the user purchases, when tealium_event is 'purchase'.
```

**Create interconnected workflows**

Describe a business use case and create the related set of entities and references needed to implement it.

```wrap
Develop a use case in Tealium to understand the intent of a user who is browsing the e-commerce site attached to the profile. Add users into five distinct audiences that can be targeted in paid media.
```

```wrap
As a <industry> company, recommend additional use cases to configure in my Tealium profile.
```

**Modify configuration**

Update the logic, conditions, or relationships in a supported workflow using natural language.

```wrap
Add a condition to the 'High Value Customers' audience so that only visitors who have made a purchase in the last 30 days are included.
```

```wrap
Exclude visitors who have already converted from the 'Prospecting' audience.
```

```wrap
Change the frequency cap on the Send Campaign Message Braze action from once per day to once per week.
```

**Maintain profile health**

Find orphaned or unused entities and identify candidates for cleanup or deletion.

```wrap
Which of my attributes are currently unused, not referenced in any audience rules or enrichments?
```

```wrap
Give me an overall health summary of my Tealium profile, covering audiences, attributes, and connectors.
```

```wrap
What are the top three gaps or improvements you'd recommend based on my current profile configuration?
```

## Supported objects

Tealium Configuration MCP supports the following profile objects.

**Data sources**

* Tealium iQ, Android, iOS, HTTP API, HTTP API - Advanced, file import

**Events**

* Event feeds, event specifications, event attributes (universal data object only), event attribute enrichments

**Visitors and audiences**

* Visitor attributes, visit attributes, visitor/visit attribute enrichments, audiences (without segments)

**Connectors**

* Adobe Campaign Classic, AudienceStore, Braze, Facebook Audiences, Facebook Conversions, Google Ads Customer Match (Tealium-Provided Credentials), Google Ads Enhanced Conversions for Web, Google Analytics 4 Measurement Protocol, Google Display & Video 360 Customer Match, Google Cloud Pub/Sub (Service Account), Google Sheets, Pinterest Conversions, Reddit Conversions, Snowflake Streaming, Adobe Analytics 1.4, Snapchat Conversions, TikTok Events, Webhook, Databricks

**Server-side tools**

* Rules, labels

**Not supported**

The following are not supported in Tealium Configuration MCP:

* Cloud data sources, CloudStream, segments, audiences with segments, fill an audience, audience discovery, audience sizing, audience jobs
* Tealium Insights, Context API, Functions, DataAccess, Data Connect, Predict
* Tealium iQ (client-side), consent orchestration

## Limitations

**One profile per session:** Each session connects to one profile. To switch profiles, update your User Preferences and reconnect to Tealium Configuration MCP. The current session becomes invalid when the profile changes.

**No credential creation for connectors:** The MCP server cannot create outbound connector credentials. You can re-use existing connectors and create new connector actions against them. Alternatively, create a new connector in an incomplete state and add the credentials manually in the Tealium UI.

**Secrets not accessible:** Credentials stored in the profile, such as access tokens and passwords, are filtered before reaching the agent. The MCP server cannot retrieve or display them.

**No publishing:** Tealium Configuration MCP never publishes profile changes. Updates made through MCP are saved as a new saved version in Tealium, available for review, and require a manual publish.

**Concurrency:** If a new version is published in the Tealium UI while your session is active, the agent notifies you. You can continue the session and resolve any merge conflicts manually later, or discard the current session and start a new one from the latest published version.

**Session expiry:** Sessions expire after 4 days of inactivity. Commit your changes before leaving a session for an extended period. After returning, start a new session and load the committed version as `Latest Saved`.

**Token usage:** Large or complex profiles require more tokens per session. A Claude Pro, Max, Team, or Enterprise plan is required.

**Platform Permissions only:** Accounts using Legacy permissions are not supported.

**Supported AI client:** Tealium Configuration MCP works with Claude (claude.ai and Claude Desktop). 