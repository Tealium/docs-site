---
title: Do Not Track Extension
description: The Do Not Track extension creates an easy way to detect DNT and to control your tags based on that value.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/do-not-track-extension/
---
### What is Do Not Track?

Do Not Track (DNT) is a browser setting which gives the visitor a choice to opt out of third-party tracking. When a visitor enables the DNT setting, the browser instructs websites, applications, and advertisers to refrain from tracking the visitor&#39;s page views, clicks and other browsing behavior by populating a property accessible from one of the following native browser objects:

* `navigator.doNotTrack`
* `navigator.msDoNotTrack`

This setting is `Off` by default in most browsers.

For example, here is the DNT preferences setting in Chrome:

![](/images/iq-tag-management/chrome-do-not-track.png)

## How it works

The Do Not Track extension creates an easy way to detect DNT and to control your tags based on the value. The extension adds a variable to the data layer named `do_not_track`. If the DNT setting is detected in the browser then `do_not_track` is set to &#34;yes&#34;, otherwise it remains empty. The extension is capable of being configured to automatically prevent all tags from loading based on DNT.

The extension runs in the Pre Loader scope. This cannot be changed, which ensures that the DNT setting is enforced before any other extensions or tags run.

## Using the extension

Before you begin, familiarize yourself with [how extensions work]().

Once the extension is added, the following configuration option is available:

* **Halt Load**: Prevent any tags from loading based on the visitor&#39;s Do Not Track preference

Use this extension to detect if a visitor has enabled Do Not Track in the browser. The visitor&#39;s Do Not Track selection is placed in the `do_not_track` variable, which is used in load rules.

### Block all tags

To halt the loading of all the tags based on the DNT setting, click the checkbox named **Halt Load**. When **Halt Load** is on and a visitor has enabled Do Not Track, the entire functionality of the Universal Tag (`utag.js`) is disabled.

### Block some tags

To halt only certain tags, [use a load rule]() to check the value of the `do_not_track` variable. You only want tags to load if `do_not_track` is not set, so the load rule should use the **is not populated** condition, like this:

![](/images/iq-tag-management/do-not-track-load-rule.png)

Include this load rule on any tags that should honor the DNT setting, like this:

![](/images/iq-tag-management/do-not-track-load-rule-tag.png)
