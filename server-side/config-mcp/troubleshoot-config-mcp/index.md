---
title: Troubleshooting
description: Resolve common issues with Tealium Configuration MCP, including connection failures, unexpected agent behavior, and session errors.
url: https://docs.tealium.com/server-side/config-mcp/troubleshoot-config-mcp/
---
## MCP cannot connect to my Tealium profile

Confirm that the Tealium Configuration MCP connector is enabled for the current conversation. Disconnect and reconnect the connector, then sign in again if the authentication session has expired.

Verify the following in the Tealium UI:

* The account and profile selection is correct under your server-side User Preferences.
* You have the required Platform Permissions and MCP access to the profile.
* The profile has at least one published revision.

If the issue continues, contact your admin to verify the MCP setup for your organization.

## MCP takes unexpected actions

If the agent behaves unexpectedly, generate a diagnostic report using the built-in feedback prompt in Claude Desktop or claude.ai: 

1. In the message composer, click the **+** icon.
1. Select **Add from Tealium Configuration MCP**.
1. Select **Mcp-feedback** and follow the prompts.

![](https://docs.tealium.com/images/server-side/config-mcp-feedback-prompt.png)

Share the exported report with [Tealium support](https://docs.tealium.com/support/) for analysis.

## MCP creates a version that does not load in the Tealium UI

Do not publish the version. If the version was already published, use [Version Management](https://docs.tealium.com/ss-version-history/) to roll back to the previous published version. [Contact support](https://docs.tealium.com/support/) and provide details about what the agent was doing when the issue occurred.

## A requested entity or action is unavailable

Check the [supported objects](https://docs.tealium.com/about-config-mcp/#supported-objects) list to confirm that the entity and operation are supported. Review your prompt and rephrase with more explicit instructions if the MCP server cannot complete the task.

## Changes are not visible after committing

Confirm that the commit completed successfully. If needed, type `commit` to force a commit. Then open **Version History** in the Tealium UI and locate the new saved version. Committing does not publish. The new version requires a separate publish action in the Tealium UI.

## Running out of tokens

Upgrade your Claude plan. If a specific activity or prompt seems to consume an unexpectedly high number of tokens, contact [Tealium support](https://docs.tealium.com/support/) with details about the prompt and task. Sharing these details helps Tealium investigate and optimize further.
