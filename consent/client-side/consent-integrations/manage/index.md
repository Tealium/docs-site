---
title: Manage consent integrations and purpose groups
description: This article explains how to manage client-side consent integrations and purpose groups.
url: https://docs.tealium.com/consent/client-side/consent-integrations/manage/
---
In the Tealium iQ Tag Management dashboard, the consent integrations screen provides the ability to add and configure consent integrations.

## Add an integration

Follow the steps below to add an integration:

1. Go to **Tag Management &gt; Consent Integrations**.
1. Click **&#43; Add Integration** to open the integration configuration screen.

### Step 1: Configure integrations

1. In the **Configure Integrations** slideout, enter a descriptive name for your integration.
1. Select a vendor from the **Vendor** list. Depending on your vendor selection, additional fields may be required, usually an identifier for the CMP configuration you want to integrate with.
1. (Optional) To configure your integration with the default vendor categories, select **Create new Purpose Group with {Vendor} Default Categories**.
1. Enter a description.
1. Click **Next**.

### Step 2: Enforcement rules

Use the drop-down list to create a new rule, or select an existing rule. This rule determines when to enforce a consent integration.

To create a new rule:
1. Click **&#43; New Rule**.
1. In the **Add Rule** slideout, add a **Title** for the load rule, and optional **Notes** if needed.
1. Use the drop-down lists to select a **Variable** and an **Operator**, then enter a **Value**.
1. To add another condition using AND logic, do one of the following:
    * Click **&#43;** next to the default conditional statement.
    * To create a copy of a conditional statement using AND logic by clicking the row menu and selecting **Duplicate Row**.  
    The duplicate conditional statement can be edited as needed.
1. To add another condition using OR logic, do one of the following:
    * Click **&#43;OR**.
    * Create a copy of a condition using OR logic by clicking the condition menu and selecting **Duplicate**.  The duplicate condition can be edited to create a new condition.
1. To remove a conditional statement from a condition, click the row menu and select **Remove Row**.
1. Click **Done.**

### Step 3: Publish locations

1. Select the environments where you want this integration&#39;s enforcement to apply.
1. Click **Next**.

### Step 4: Purpose group

1. Select a purpose group for your integration from the **Purpose Group** drop-down list.
    * If you opted to configure your integration with the default vendor categories in step 1, complete the following steps and proceed to save your integration:
        1. Select **&amp;lt;Vendor&amp;gt; Default** from the list.
    * If you did not opt to configure your integration with the default vendor categories in step 4:
        1. Select **&#43; New Purpose Group** from the drop-down list.
        1. In the **New Purpose Group** dialog, click **Create Purpose Group**. You will be redirected to the **New Purpose Group** screen. Your progress in the **Add Integration** wizard is saved and you will be redirected back after configuring your purpose group.
        1. In the **Purpose Group** dialog, complete the steps in the [Add a purpose group](#add-a-purpose-group) section to add a purpose group.
        1. In the **Add Integration** wizard, select your purpose group from the **Purpose Group** drop-down list.
        You will be redirected back to the **Add Integration** wizard to finish setting up your integration.
1. Click **Save** to create your new integration.

If you are using OneTrust default vendor categories for the first time, after creating your integration, follow the steps in [edit purpose group](#edit-a-purpose-group) to assign tags to the **Default** purpose group.

## Manage purpose groups

To manage your purpose groups, go to **iQ Tag Management &gt; Consent Integrations &gt; Purpose Groups** tab.

### Add a purpose group

Follow the steps below to add a purpose group:

1. Go to **Tag Management &gt; Consent Integrations**.
1. Click **&#43; Add Purpose Group** to open the purpose group configuration modals.

#### Step 1: Purpose group

1. Enter a name and description.
1. Click **Next**.

#### Step 2: Purposes

1. Enter purpose name and description. Each purpose name must match the name of a consent category for the vendor you are integrating with.
1. You can create multiple purposes in a purpose group. To add more purposes to your purpose group, click **&#43; Add Purpose**.
1. Click **Next**.

#### Step 3: Tealium iQ purpose

1. Select a purpose to map to Tealium iQ from the **Tealium Tag Purpose**. Tealium iQ controls all tag operations and must be mapped to a purpose for any tags to function.
1. Click **Next**.

#### Step 4: Map tags

All tags must be mapped to a purpose before they can be triggered.

1. To map your tags to the newly created purposes, for each tag, click **Assign/Map** and select the purpose you want to map that tag with from the drop-down list.
1. To enable or disable tag refire for each tag, toggle the **OFF/ON** button under the **Tag Refire** column. For more information about tag refire, [Tag refire]().
1. Click **Save** to create your new purpose group.

### Edit a purpose group

Follow the steps below to edit a purpose group:

1. Click the options icon beside the purpose group you want to edit.
1. Click **Edit** to open the purpose group configuration.
1. Click the tab for the section you want to edit. To map tags to a new default purpose group, click **Map Tags**.
1. Click **Save** to save your changes.

For a step-by-step example of how to set up a supported vendor integration with Tealium iQ tag management, see [consent integration guide]().