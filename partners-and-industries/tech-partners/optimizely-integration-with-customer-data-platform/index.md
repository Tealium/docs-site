---
title: Customer Data Platform (CDP) CDP + Optimizely X
description: Integrate Optimizely with CDP to use audiences to build targeted experiments in Optimizely Classic or Optimizely X.
url: https://docs.tealium.com/partners-and-industries/tech-partners/optimizely-integration-with-customer-data-platform/
---
## Requirements

Set **Data Enrichment for the Tealium Collect tag** to **Frequent**. For more information, see the [Tealium Collect Setup Guide](https://docs.tealium.com/tealium-collect-tag/).

After you complete the integration, audiences are automatically sent to Optimizely with data layer enrichment.

## Integrate Optimizely Classic with CDP

There are two steps to integrate Optimizely Classic with CDP:

1. Add `utag.sync.js` to your site.
1. Connect CDP and Optimizely by using the Tealium Tool: Optimizely Helper.

### Add utag.sync.js to your site

You need to include `utag.sync.js` in all HTML pages that need to use Optimizely. For consistency, you may want to include it in all pages.

For details on setting up `utag.sync.js`, see [Using the utag.sync.js Script](https://docs.tealium.com/utag-sync/).

### Connect CDP and Optimizely

To use audiences in Optimizely, you need to connect CDP and Optimizely and then map audiences to your Optimizely project. Use the Tealium Tool: Optimizely Helper to complete both of these tasks.

For more information, see [Tealium Tool: Optimizely Helper](https://docs.tealium.com/optimizely-helper/).

## Integrate Optimizely X with CDP

Use the Optimizely Dashboard to integrate Optimizely X with CDP.

1. After creating your Audiences in CDP, log into Optimizely and click **Integrations**.
1. Set Tealium to **On**.
1. Enter your Tealium account ID.
1. Select the **Overview** tab, then click **Audiences**.
1. Under Conditions, click **Tealium**.
1. Drag **Tealium Audience** or **Tealium Badge** to create an Optimizely Audience condition based on a Tealium audience.  
    ![](https://docs.tealium.com/images/tech-partners/createaudience1.png)  
    ![](https://docs.tealium.com/images/tech-partners/createaudience2.png)
1. Click **Save Audience**.

## Create audience-based experiments

After Optimizely is integrated with CDP, the mapped audiences are available for your project and you can create audience-based experiments.

To select a new target audience for an experiment:

1. Create a new experiment, or edit an existing experiment, and click **Audiences**.
1. Click **Add a Saved Audience** and select the audience to target.
1. Save your experiment.
