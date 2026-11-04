---
title: AI audience recommendations
description: Discover new audience opportunities using AI-generated recommendations.
url: https://docs.tealium.com/server-side/audiences/ai-audience-recommendations/
---

<blockquote>
This feature is only available to select customers. If you are interested in trying this feature, [contact support](https://docs.tealium.com/support/).
</blockquote>


AI audience recommendations analyzes your business context, profile attributes, and visitor data to suggest audiences you can create. It uses an industry-specific knowledge base to generate recommendations.

Each recommendation includes suggested audience conditions, an explanation of the recommendation, suggested next best actions, and an estimated audience size. You can create audiences from recommendations or reject recommendations you don't want to use.

Attributes marked as **Restricted Data** are never sent to the AI.

## Requirements

This feature requires the following:

* An active server-side profile.
* **AI Recommendations** enabled at both the account and profile levels in **AI Settings** by an account admin. For more information, see [Tealium AI features](https://docs.tealium.com/ai-features/).

To access **AI Settings**, click your profile icon and select **AI Settings**.

When enabled, the **AI Recommendations** tab appears on the **Audiences** page (**Activate > Audiences**). Use this tab to generate recommendations, review AI-suggested audiences and their conditions, and create audiences from recommendations.

## Set up AI audience recommendations

When you open the **AI Recommendations** tab for the first time, a setup screen appears. The settings icon and **Refresh** button become available after setup is complete.

To set up AI audience recommendations:

1. Go to **Activate > Audiences** and click the **AI Recommendations** tab.
1. Click **Set Up Recommendations**.
1. In the **Tell us about your business** step, enter your company name, the websites or apps that send data to the profile, and your audience goals in the **Business Context** field.
1. Click **Run Research**.

   To skip research and configure settings manually, click **Set Up Manually**, select a **Vertical**, enter your **Business Context**, and click **Generate recommendations**. Click **Back** to return to the research step.

A progress indicator appears while setup runs. Setup continues in the background if you leave the page.

If research fails, an error message appears on the tab. Retry the research or click **Set Up Manually** to configure settings manually.

After the AI generates the initial recommendations, the recommendations list appears, along with the settings icon and **Refresh** button.

## Configure recommendation settings

Use **Audience Recommendation Settings** to provide business context and instructions that help the AI generate relevant recommendations.

To configure recommendation settings:

1. Go to **Activate > Audiences** and click the **AI Recommendations** tab.
1. Click the settings icon to open **Audience Recommendation Settings**.
1. Configure the following settings:
   * **Vertical**: Your company's industry. The AI uses this setting to apply industry-specific marketing patterns when generating recommendations. Tealium supports major industry verticals and continues to add more.
   * **Business Context**: Information about your company and the current profile. Include your company name, products or services, and the markets or regions covered by the profile.
   * **Recommendation Instructions**: Instructions that apply to every recommendation refresh for the profile. These instructions take priority over the goal entered for an individual refresh.
1. Click **Save**.

Changes to recommendation settings take effect without publishing.

![](https://docs.tealium.com/images/server-side/audiences/ai-recommendations-settings.png)

### Use the research agent

The research agent analyzes publicly available information about your company to populate the **Vertical** and **Business Context** fields.

The research agent runs during [initial setup](#set-up-ai-audience-recommendations) when you click **Run Research**. You can also run it again after setup is complete.

To run the research agent after setup:

1. On the **AI Recommendations** tab, click the settings icon.
1. In **Audience Recommendation Settings**, click **Run Research**.
1. In the confirmation dialog, enter your company name and links to official resources in the **Research Prompt** field.
1. Click **Run Research** to confirm.

While research runs, the **Vertical** and **Business Context** fields are read-only. When research completes, both fields are populated and saved automatically.

You can edit either field after research completes. The timestamp of the last completed research appears next to **Run Research**.

## Generate recommendations

The AI generates recommendations on demand. There is no scheduled refresh.

**Refreshing replaces the current list of recommendations**. Create any audiences you want to keep before refreshing.

To generate recommendations:

1. Go to **Activate > Audiences** and click the **AI Recommendations** tab.
1. Click **Refresh**.
1. In the confirmation dialog, optionally enter a goal in the **Marketing Goal** field. The goal applies only to the current refresh. The field is prefilled with the goal from your previous refresh.
1. Click **Refresh** to confirm.

Generating recommendations may take a few minutes. The tab is read-only while the AI generates recommendations.

When generation completes, the updated recommendations appear with the total number of results and the last refreshed timestamp.

Profiles with more attributes and visitor history generally produce higher-quality recommendations. Refreshing without changes to the underlying profile data may produce similar results.

### Refresh limits

Each profile has a monthly refresh limit. The default is 15 refreshes per month, but the limit may vary by account.

When three or fewer refreshes remain, a warning appears in the confirmation dialog.

When no refreshes remain, the **Refresh** button is disabled. To request additional refreshes, [contact support](https://docs.tealium.com/support/).

## Review recommendations

After generating recommendations, the **AI Recommendations** tab displays the suggested audiences for your profile.

Each recommendation card includes:

* An audience name and a description of its marketing purpose.
* Suggested next best actions.
* Conditions that define the audience.
* An estimated audience size.
* A similarity score indicating how closely the recommendation matches existing audiences in the profile.

### View recommendation details

To view alternative audience names and estimated sizes, click **Variations (N)** on a recommendation card. Click it again to collapse the list.

To view an AI-generated explanation of an attribute used in the recommendation, click the info icon next to **Conditions**.

### Filter recommendations

Use the following controls to filter recommendations:

* **Search**: Enter a keyword to filter recommendations.
* **Similarity Score**: Select one or more similarity levels to filter recommendations based on their similarity to existing audiences. Options include **Completely Unique**, **Mid-match**, and **Almost Identical**.
* **Audience Size**: Enter a minimum audience size, a maximum audience size, or both, then click **Apply**.

A warning icon appears on the tab if profile changes have been published since the last refresh. This indicates that the recommendations may not reflect the current profile.

![](https://docs.tealium.com/images/server-side/audiences/ai-recommendations-tab.png)

## Create an audience from a recommendation

To create an audience from a recommendation:

1. On the **AI Recommendations** tab, find the recommendation you want to use.
1. Click **Create Audience**.
1. In the **New Audience** slideout, review the prefilled conditions and modify them as needed.
1. Click **Done**.
1. Save and publish your changes to activate the audience.

The new audience appears on the **Audiences** tab with the **AI Recommended** label. The recommendation is removed from the **AI Recommendations** tab.

## Reject a recommendation

Reject a recommendation to remove it from the current results. Rejected recommendations may appear again when you generate new recommendations.

To reject a recommendation:

1. On the **AI Recommendations** tab, find the recommendation you want to remove.
1. Click the **X** icon in the upper-right corner of the recommendation card.
1. In the confirmation dialog, click **Reject**.
