---
title: Flicker Free Test & Target
description: This article explains the problem of flicker in constent display and how to configure Tealium to reduce it.
url: https://docs.tealium.com/client-side-tags/flicker-free-test-and-target/
---
## What is flicker?

Flicker is the occurrence of default content being momentarily displayed to the visitor before it is replaced with the content you intended to show the visitor, making it seem to the visitor that the content flickered. Visitors can sometimes interpret flicker as a problem with the site, potentially causing the visitor to lose confidence in the site or brand. Flicker can also cause visitor dissatisfaction if, for example, they see a discount they like &#34;flicker away&#34; to be replaced with a lesser discount. Flicker is a symptom of encountering a delay in loading the content displayed, also called &#34;tests&#34;, asynchronously.

## Synchronous vs. Asynchronous

You can load Test &amp; Target, a popular solution for A/B and Multivariate testing, either synchronously or asynchronously. Both methods provide benefits and issues, and it is important to understand each to make an informed decision.

### Synchronous loading

If you choose to load your tests synchronously, you will not see flicker occur. However, loading content synchronously means that the entire page must wait to receive that content before it parses and displays the rest of the page. If the content the page is trying to load is unavailable, the page will &#34;hang&#34;, meaning it will appear to stop loading. If the delay is too long, the page becomes unavailable to visitors completely, resulting in lost traffic, conversions, et cetera.

### Asynchronous loading

Asynchronous loading circumvents the issue of unavailable content halting page load because the browser continues to load the rest of the page while it waits for the pending content. However, if there is a long enough delay between the browser encountering the offer on the page and retrieving the offer&#39;s content, visitors may briefly see the default content. This is the flicker phenomenon.

## Tealium&#39;s new approach

### Before you begin: utag.footer.js is deprecated

Going forward, `utag.footer.js` is officially deprecated and no longer an option. Older implementations that are using `utag.footer.js` will continue to function as before. You will not have to change the scope for your old Content Modification Extensions. The old Content Modifications Extensions originally scoped to **Footer** will appear to be scoped to **DOM Ready**, but they will still publish to the `utag.footer.js` file.

### Introducing utag.sync.js

The `utag.sync.js` file replaces the functionality of the old `utag.footer.js` file. When you use the `utag.sync.js`, make sure you include its file reference within the head tags at the top of the page&#39;s code. You must include `utag.sync.js` on your page if you want to use Flicker Free Test &amp; Target.

### How it works

1.  When the page loads, the browser will encounter the `utag.sync.js` file which sets the CSS visibility property off to `hidden`. The content is not removed, but the browser will not render it. The layout dimensions of the hidden content are preserved, so the layout of your page is not deformed. To a visitor it will appear as though the section where the content would be displayed is blank instead. There is no flicker.
1.  When the `utag.js` file loads, it calls the Test &amp; Target Tag which in turn shows the hidden nodes.

 If a load rule does not allow the Test &amp; Target Tag to load, then the `utag.js` file will show the hidden nodes and display the default content instead. 

## Using the Flicker Free Test &amp; Target extension

We&#39;ve updated the Test &amp; Target Extension to handle our Flicker Free solution. Before you begin using the Flicker Free TnT Extension:

### Include utag.sync.js on Your Page

Include `utag.sync.js` within the head tag of your page&#39;s code. You cannot use the Flicker Free functionality without this.

### Enable the Flicker Free Publish Setting

First, you need to enable the appropriate Publish Setting:

1. In the admin menu, click **Configure Publish Settings**=. The **Publish Configuration** dialog appears.
1. Toggle **Flicker-Free Support for Adobe Target** to On and click **Apply**.

### Remove Old Test &amp; Target Tag Template

You must delete the old Tag Template for Test &amp; Target.

1.  In the admin menu, click **Manage Templates**.
1.  Select the **Adobe Text &amp; Target Tag** template. the **Tag Config** window will appear.
1.  Click the trash icon in the upper-right corner to delete the current template.
1.  Click **Close**.
1.  Save/Publish the profile. When you log back into the profile, it will automatically pull in the new Tag template.

## Setting up the Test &amp; Target extension

Setting up the Extension to use Flicker free is as simple as checking the &#39;Flicker Free&#39; box in the Extension settings. Be aware that if you use Flicker Free, you must select **Replace Node Content (leave default)** for the **Mod Position** selection. All other configurations remain as they were before, as described in the [Test &amp; Target article.](/client-side-tags/adobe-test-target-tag/)

### Important Notes

*   The mBox DIV ID cannot be the same as the element identifier. If they&#39;re the same, then the `utag.sync.js` file will hide all elements with that identifier as well.
*   If you have an mBox that isn&#39;t in a campaign, then you must make certain you remove that mBox from the Test and Target Content Modification extension. Otherwise the `utag.sync.js` file will hide the content for the duration you entered in the timeout field of the [Test &amp; Target Tag](/client-side-tags/adobe-test-target-tag/) configurations before finally displaying the default content. Removing the mBox allows the default content to display immediately.