---
title: Detect a tag from code
description: This article explains how to detect a tag on your site from its code and add it to your Tealium profile.
url: https://docs.tealium.com/iq-tag-management/tags/tag-marketplace/detect-a-tag-from-code/
---
Adding a tag to your profile involves multiple steps: search for your tag, add it, configure it, then save and publish. If you want to simplify this process, use the **Detect Tag from Code** tool. This tool extracts the tag parameters from your vendor code snippet and automatically configures the tag for you.

Use the following steps to add a tag using the **Detect Tag from Code** tool:

1. Click **Detect Tag From Code** to display a text box.  
    ![](/images/iq-tag-management/manage_tags/tag_marketplace_detect_from_code.png)
1. Paste the code provided to you by your tag vendor.
1. Click **Detect Configuration**.  
The platform will parse the tag snippet and extract its parameters.
1. Upon detecting a match for the code snippet, the tag and its configurations are displayed below your code snippet.
1. Select the tag and click **Continue** to add the tag to your profile.

If the tool fails to detect the vendor code snippet, search for and [add a tag using conventional methods]().  
If the required tag is not available in the tag marketplace, use a Tealium custom container to add the tag.

Hiding tags with the [Tag Marketplace Policy]() prevents the tool from detecting the matching code snippet.