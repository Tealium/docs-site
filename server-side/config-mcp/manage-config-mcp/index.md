---
title: Manage Tealium Configuration MCP
description: Learn how to run a Tealium Configuration MCP session, explore and modify your server-side profile using natural language, and review your changes before publishing.
url: https://docs.tealium.com/server-side/config-mcp/manage-config-mcp/
---
Before using Tealium Configuration MCP, complete the setup steps in [Connect to Tealium Configuration MCP](https://docs.tealium.com/connect-config-mcp/).

## Start a session

Each new chat in Claude Desktop or claude.ai starts a fresh Tealium Configuration MCP session with its own profile draft.

1. Start a new chat in Claude with the **Tealium Configuration MCP** connector enabled.
1. The agent asks which profile version to work against. Select one of the following:
   * **Latest Published:** The most recently published profile version.
   * **Latest Saved:** The most recently saved version, including unpublished drafts.
   * A specific revision by name or number.
1. The MCP server creates a temporary draft based on the selected version. All changes during the session apply to that draft. Optionally, provide a name for the draft version when prompted.
1. The agent pre-fills the message box with the selected version. Send the message to start the session.

## Explore and make changes

Ask questions about the profile or describe a change you want to make. For questions, the agent responds directly. For changes, the MCP server creates a plan, the agent presents it, and you confirm before anything is applied.

```wrap
Add a condition to the 'High Value Customers' audience so that only visitors who have made a purchase in the last 30 days are included.
```

After you confirm, the MCP server applies changes to the draft in sequential patches and validates the profile integrity after each patch. If the MCP server detects a conflict, it attempts to resolve it automatically and the agent describes what it did.

For specific tasks and example prompts, see [Use cases](https://docs.tealium.com/about-config-mcp/#use-cases).

## Commit and review

When you are done making changes, ask the agent to commit, or type `commit`.

The agent provides a summary of all changes made during the session. Review the summary, then confirm to proceed.

After committing:

1. Open the Tealium UI and navigate to the profile.
1. Go to **Version History** and locate the new saved version.
1. Review the changes.
1. Publish manually after completing your organization's approval process.


<blockquote>
Committing creates a new saved version but does not publish changes. The profile continues to run on the previously published version until you publish the new one manually.
</blockquote>


Commit your changes before ending a long session. Sessions expire after 4 days of inactivity and uncommitted changes are lost. After the session expires, start a new chat and select the committed version as **Latest Saved** to continue.

## Best practices

* **Match the model to the task.** We recommend starting with Claude Opus for most tasks. Its deeper reasoning handles exploration, targeted entity creation, and simple modifications well. For complex tasks such as whole use case implementation or creating large numbers of entities at once, Claude Sonnet is more efficient. Opus can over-generate plans for bulk operations and slow down the session.
* **Be precise and explicit.** Clear instructions produce more accurate results. Specify entity names, conditions, and values directly rather than describing them in general terms.
* **Review before confirming.** Read the agent's plan carefully before approving each step. Adjust the plan or clarify your request if the proposed changes are not what you intended.
* **Start a new chat for each new task.** For a new use case or when switching to a different profile version, start a new chat to reset the session context.

For help resolving common issues, see [Troubleshooting](https://docs.tealium.com/troubleshoot-config-mcp/).
