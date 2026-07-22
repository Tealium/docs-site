---
title: Tealium Tool Optimizely Helper
url: https://docs.tealium.com/server-side/connectors/optimizely-helper/
---### Installing Tealium Tools

Make sure you have the latest version of Tealium Tools installed. This Google Chrome extension provides a variety of tools, including the Optimizely Helper. For more information, see [Tealium Tools Browser Extension](https://docs.tealium.com/tealium-tools-browser-extension/).

### Connecting Your Optimizely Account

After you have installed Tealium Tools, use these steps, along with the API Token and the Project ID from Optimizely, to connect AudienceStream and Optimizely:

1. In Optimizely, navigate to **Account Settings** and click **View Tokens** under the API Tokens section.
1. Create a new API Token and copy the new token to your clipboard.
1. Open **Tealium Tools** by clicking the Tealium icon in the top-right corner of Google Chrome.
1. Select **Optimizely Helper**.
1. Paste the API Token into the **Token** field.
1. Navigate to the project in which you'd like to map AudienceStream audiences and copy the Project ID. The Project ID is available from the **Project Code** drop-down menu in the top-right corner of the Project page.  
    ![](https://docs.tealium.com/images/server-side/optimizely-helper-project-id.png)
1. In the Optimizely Helper, paste the Project ID into the **Project ID** field.
1. Enter the name of the Tealium account and profile you would like to associate with this Optimizely project.
1. Click **Import Audience Data**.

The Optimizely Helper now contains a list of audiences and badges that you can map to new or existing audiences in Optimizely.

### Mapping Audiences to an Optimizely Project

1. In the Optimizely Helper, select the AudienceStream audience or badge to add to Optimizely.
1. On the Optimizely Audience drop-down menu, select an existing Optimizely Audience or create a new one. If you create a new Optimizely Audience, the name is the same as the name of the AudienceStream badge or audience you selected.
1. Click **Create Audience** to confirm.
1. To create additional audience mappings, repeat the steps above.

After you have mapped audiences, click **Generate Code Snippet**. This code needs to be added to the utag.sync.js file.<br>
![](https://docs.tealium.com/images/server-side/optimizely-helper-code-snippet.png)

To add the code to the utag.sync.js template, click **Copy Code Snippet to Clipboard**. For more information, see [Using the utag.sync.js Script](https://docs.tealium.com/utag-sync/).

### Create Audience-based Experiments

Your project now has the mapped AudienceStream badges and audiences available for targeting. To select a new target audience:

1. Create a new experiment or edit an existing experiment and click **Audience Targeting**.
1. Click **Add a Saved Audience** and select an AudienceStream badge or audience.
    ![](https://docs.tealium.com/images/server-side/audiencebasedexperiments.png)
1. Save your experiment.

For more information on targeting audiences in Optimizely, refer to the [Optimizely knowledge base article.](https://help.optimizely.com/hc/en-us/articles/200039685#changes)
