---
title: Manage Tealium Configuration MCP
description: Learn how to run a Tealium Configuration MCP session, explore and modify your server-side profile using natural language, and review your changes before publishing.
url: https://docs.tealium.com/server-side/config-mcp/manage-config-mcp/
---
Before using Tealium Configuration MCP, complete the setup steps in [Connect to Tealium Configuration MCP](https://docs.tealium.com/connect-config-mcp/).

## Start a session

Each new chat in Claude Desktop, claude.ai, or Claude Code CLI starts a fresh Tealium Configuration MCP session with its own profile draft.

1. Start a new chat in Claude with the **Tealium Configuration MCP** connector enabled.
1. The agent asks which profile version to work against. Select one of the following:
   * **Latest Published:** The most recently published profile version.
   * **Latest Saved:** The most recently saved version, including unpublished drafts.
   * A specific revision by name or number.
1. Tealium Configuration MCP creates a temporary draft based on the selected version. All changes during the session apply to that draft. Optionally, provide a name for the draft version when prompted.
1. The agent pre-fills the message box with the selected version. Send the message to start the session.

## Explore and make changes

Ask questions about the profile or describe a change you want to make. For questions, the agent responds directly. For changes, Tealium Configuration MCP creates a plan, the agent presents it, and you confirm before anything is applied.


<blockquote>
Before editing an existing audience, verify that it has been published in the current Audiences UI. If Tealium Configuration MCP can read the audience but cannot apply a condition change, open the audience in **Activate > Audiences**, make no changes, and save and publish it, then start a new MCP session and retry the operation.
</blockquote>


```wrap
Add a condition to the 'High Value Customers' audience so that only visitors who have made a purchase in the last 30 days are included.
```

After you confirm, Tealium Configuration MCP applies changes to the draft in sequential patches and validates the profile integrity after each patch. If Tealium Configuration MCP detects a conflict, it attempts to resolve it automatically and the agent describes what it did.

For specific tasks and example prompts, see [Use cases](https://docs.tealium.com/about-config-mcp/#use-cases).

## Commit and review

When you are done making changes, ask the agent to commit, or type `commit`.

The agent provides a summary of all changes made during the session. Review the summary, then confirm to proceed.

After committing:

1. In the Tealium UI, go to the profile.
1. Go to **Version History** and locate the new saved version.
1. Review the changes.
1. Publish manually after completing your organization's approval process.


<blockquote>
Committing creates a new saved version but does not publish changes. The profile continues to run on the previously published version until you publish the new one manually.
</blockquote>


Commit your changes before ending a long session. Sessions expire after 4 days of inactivity and uncommitted changes are lost. After the session expires, start a new chat and select the committed version as **Latest Saved** to continue.

## Best practices

* **Use the minimum required effort level.** Using a lower effort level than recommended leads to worse results and more incorrect outputs. The minimum effort levels are: Sonnet (4.6, 5) at **High**, and Opus (4.6, 4.7, 4.8, 5) at **Medium**.
* **Be precise and explicit.** Clear instructions produce more accurate results. Specify entity names, conditions, and values directly rather than describing them in general terms.
* **Review before confirming.** Read the agent's plan carefully before approving each step. Adjust the plan or clarify your request if the proposed changes are not what you intended.
* **Start a new chat for each new task.** For a new use case or when switching to a different profile version, start a new chat to reset the session context.

For help resolving common issues, see [Troubleshooting](https://docs.tealium.com/troubleshoot-config-mcp/).
