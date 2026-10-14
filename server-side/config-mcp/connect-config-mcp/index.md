---
title: Connect to Tealium Configuration MCP
description: Configure Tealium Configuration MCP for your organization and connect an AI client to a server-side profile.
url: https://docs.tealium.com/server-side/config-mcp/connect-config-mcp/
---

<blockquote>
Tealium Configuration MCP is only available to select customers. If you are interested in trying this feature, [contact support](https://docs.tealium.com/support/).
</blockquote>


Setting up Tealium Configuration MCP involves steps for both admins and end users. Complete Steps 1–3 in the Tealium UI before configuring your AI client in Step 4. Skipping these steps causes authentication errors.

## Step 1: Enable Tealium Configuration MCP in Tealium AI Settings (admin)

Enable Tealium Configuration MCP at both the account level and the profile level in the Tealium UI.

1. In Tealium, click your initials in the upper-right corner and click **AI Settings**.
1. Set the **MCP Server** toggle to **On** for the account.
1. Switch to each profile where you want to enable Tealium Configuration MCP and repeat: set the **MCP Server** toggle to **On** at the profile level.

You can disable Tealium Configuration MCP for a specific profile at any time by returning to AI Settings and setting the toggle to **Off**.

![](https://docs.tealium.com/images/server-side/config-mcp-setup-ai-settings-toggle.png)

## Step 2: Enable Tealium Configuration MCP access delegation (admin)

Grant users permission to connect to Tealium profiles through Tealium Configuration MCP. The steps depend on whether your account uses legacy permissions or platform permissions.

### If your account uses legacy permissions

Set the required profile-level permissions for each user who needs Tealium Configuration MCP access.

1. In Tealium, go to **Manage Users**.
1. Select a user to open the **Edit Users** screen.
1. Click **Next** to go to the **Profile Permissions** screen.
1. Under **Profile Permissions**, find each profile you want to grant Tealium Configuration MCP access to and set one of the following access levels:
   * **Reader:** Read-only. Tealium Configuration MCP can explore and explain the profile but cannot create, modify, or delete entities.
   * **Editor** or **Publisher:** Read and write. Tealium Configuration MCP can explore, create, modify, and delete supported entities.
1. Click **Save**.

Repeat for each user who needs Tealium Configuration MCP access.

### If your account uses platform permissions

Grant users permission to connect to Tealium profiles through Tealium Configuration MCP by creating a user group with the appropriate access level.

1. In Tealium, go to **Manage Permissions**.
1. Click **+New Group**.
1. Enter a name for the group and click **Next**.
1. Under **AI Access**, locate **MCP Server** and select one of the following access levels. Click **Next** when you are done.
    * **Viewer:** Read-only. Tealium Configuration MCP can explore and explain the profile but cannot create, modify, or delete entities.
    * **Editor:** Read and write. Tealium Configuration MCP can explore, create, modify, and delete supported entities.
     ![](https://docs.tealium.com/images/server-side/config-mcp-setup-user-group-access.png)
1. There are no additional feature permissions for Tealium Configuration MCP. Click **Next** to skip this step.
1. Add the profiles that need Tealium Configuration MCP access to the group and click **Next**.
1. Add the users who need Tealium Configuration MCP access to the group and click **Save**.

You can create separate groups for view and edit access to serve users with different needs.


<blockquote>
Tealium may adjust individual product component permissions to match the minimum required for Tealium Configuration MCP access.
</blockquote>


## Step 3: Select a profile in user preferences (user)

Each user selects the default Tealium profile for Tealium Configuration MCP to use.

1. In the server-side Tealium UI, click your initials in the upper-right corner and select **Edit/View User Settings**.
1. Under **Tealium Configuration MCP**, select the **Account** and **Profile** to use as the default.
1. Click **Apply Configuration**.

To use a different profile, return to this screen, select the profile, and click **Apply Configuration**.


<blockquote>
After changing the profile, disconnect and reconnect Tealium Configuration MCP in your AI client, then start a new chat. The previous session is no longer valid.
</blockquote>


## Step 4: Connect your AI client (admin and user)

Connect your AI client to Tealium Configuration MCP. Follow the instructions for your client.

### Connect Claude Desktop

**Before you begin**

Confirm the following before starting:

* You have a Claude Pro, Max, Team, or Enterprise plan. Free plans cannot add custom connectors.
* You have Claude Desktop installed, or access to [claude.ai](https://claude.ai).
* Tealium Configuration MCP is enabled for your account. To request access, [contact support](https://docs.tealium.com/support/).

**Add the connector**

1. Sign in to [claude.ai](https://claude.ai) as an admin.
1. Click your profile icon and select **Settings**.
1. Select **Connectors**.
1. Scroll to the bottom of the page and click **Add custom connector**.
1. If a warning appears about connecting to trusted services, review and confirm to continue.
1. Enter the following connector details:

   * **Name:** `Tealium Configuration MCP`
   * **Remote MCP server URL:** `https://us-west-1.prod.developer.tealiumapis.com/2026-09/mcp/dcp`

1. Leave **Advanced settings** blank.
1. Click **Add**. The connector appears in your Connectors list.

![](https://docs.tealium.com/images/server-side/config-mcp-setup-add-connector.png)

**Authenticate and connect**

1. In Claude, go to **Settings > Connectors**.
1. Click **Connect** next to **Tealium Configuration MCP**.
1. Complete the Tealium sign-in steps in [Step 5: Authenticate](#step-5-authenticate-user).
1. After authentication is complete, the connector status shows as connected.

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-connected.png)

To disconnect the connector at any time, go to **Settings > Connectors** in Claude, locate **Tealium Configuration MCP**, and select **Disconnect**.

**Enable the connector in a chat**

1. Open a new chat in Claude.
1. Click the **+** icon in the message composer.
1. Toggle **Tealium Configuration MCP** on.

![](https://docs.tealium.com/images/server-side/config-mcp-setup-enable-in-chat.png)

### Connect Claude Code CLI

**Before you begin**

Confirm the following before starting:

* Claude Code is installed and authenticated.
* A terminal is open in any project directory. Any directory works, including an empty one.

**Register Tealium Configuration MCP**

Before starting a Claude session, run the following command in your terminal:

```bash
claude mcp add --transport http tealium-configuration-mcp https://us-west-1.prod.developer.tealiumapis.com/2026-09/mcp/dcp
```

Verify the server was added:

```bash
claude mcp list
```

**Authenticate and connect**

1. Start a Claude session by running `claude`.
1. List configured MCP servers by running `/mcp`.
1. Locate `tealium-configuration-mcp`. It shows as **needs authentication**.
1. Select the **Authenticate** action. Claude Code opens your default browser with the Tealium login screen.
1. Complete the Tealium sign-in steps in [Step 5: Authenticate](#step-5-authenticate-user).
1. After authentication is complete, the server status updates to connected.

To disconnect at any time, within a Claude session go to `/mcp`, locate `tealium-configuration-mcp`, and select **Disable**.

## Step 5: Authenticate (user)

Complete the Tealium sign-in challenge to activate the Tealium Configuration MCP connection. These steps apply to both Claude Desktop and Claude Code CLI.

1. A Tealium sign-in window opens. Enter your account name and click **Sign In**. If your organization uses SSO, enter your SSO account name. If you don't know it, contact your account administrator.

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-signin-account.png)

1. Sign in with your Tealium credentials:
   * **Without SSO:** Enter your username or email and password and click **Sign In**.

     ![](https://docs.tealium.com/images/server-side/config-mcp-setup-signin-credentials.png)

   * **With SSO:** Your identity provider redirects you to sign in. Enter your SSO credentials.

1. When prompted, select **Yes** to grant the AI client access to your Tealium profile.

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-grant-access.png)

1. After the window closes, return to your AI client. The connector status shows as connected.

If you see an error such as "Your account was authorized, but Tealium MCP Early Access returned an error when connecting," verify the following in the Tealium UI before contacting support:

* The **MCP Server** toggle is set to **On** for both the account and the profile in AI Settings.
* Your user permissions are configured correctly for Tealium Configuration MCP access (see [Step 2](#step-2-enable-tealium-configuration-mcp-access-delegation-admin)).
* You have selected a default account and profile under **Edit/View User Settings** (see [Step 3](#step-3-select-a-profile-in-user-preferences-user)).

The connector is now active. For more information on running a session, see [Manage Tealium Configuration MCP](https://docs.tealium.com/manage-config-mcp/).
