---
title: Optimizely Synchronous Implementation
description: This post outlines the steps to load Optimizely Synchronous with the utag.sync.js container. The utag.sync.js runs early in the page load when it is included in the &lt;head&gt;&lt;/head&gt; section of the page's HTML. To current users of the [Optimizely Sync Tag](/client-side-tags/optimizely-sync-tag/)  we highly recommend switching to this form of implementation as the tag has been deprecated. Only existing tag instances are supported.
url: https://docs.tealium.com/client-side-tags/optimizely-synchronous-implementation/
---

<blockquote>
Tealium's best practice is to load all tags Asynchronously.
</blockquote>


**IMPORTANT**: **Optimizely Tool is unable to detect `utag.sync.js`**

At the time of writing, Optimizely's tool is NOT able to detect their Synchronous script when served through a Tag Management System. Running the tool on a page where Tealium iQ is serving the script causes it to display an error message. Optimizely is working quickly to resolve this issue, until which point it is safe to ignore the error message. Our recommendation would be to use the Ghostery tool to verify whether or not Optimizely Synchronous is loading on the page as expected.

## Loading Optimizely Sync using utag.sync.js container (RECOMMENDED)

This method assumes the `utag.js` file is coded Asynchronously on the page.

### STEP 1: Enable utag.sync.js file creation

1. In the admin menu, click **Configure Publish Settings** . The **Publish Configuration** dialog appears.
1. Scroll down to the **Implementation** listing and enable the **Generate utag.sync.js** toggle.
1. Click **Save** to apply the setting.  

### STEP 2: Add the utag.sync.js script to all pages where tests will be performed. Here's how to access the script:

1. In the admin menu, click **Code Center**. The **Code Center** dialog appears.
1. In the left panel of the **Code Center** dialog, select the environment of your choice. The corresponding code is displayed in the right panel.
1. Select the **Sample HTML** tab and copy the `utag.sync.js` script.
1. Copy the script and add it to the &lt;head&gt;&lt;/head&gt; section of your page's HTML.  

### STEP 3: Configure Optimizely Project number

1. In the admin menu, click **Manage Templates**.  
1. Drop down the template listing and select **uTag Sync (Profile)**.
1. Paste the below block of code in the text editor.  
```
document.write('&lt;script type="text/javascript" src="//[cdn.optimizely.com/js/12345678.js](http://cdn.optimizely.com/js/12345678.js)"&gt;&lt;/scr'+'ipt&gt;');
```

1. Replace `12345678` with the project number provided to you by Optimizely.
1. Click **Save Profile Template** and close the template window.

### STEP 4: Save/Publish your profile.

Now, on the page, the `utag.sync.js` file will load at the very top because it is inserted in the &lt;head&gt;&lt;/head&gt; of the HTML. This will synchronously load the Optimizely JavaScript file very early in the page load and the A/B tests will be initiated very early as well. Then, later in the page load process, the `utag.js` file will load and the rest of your tags will load asynchronously.
