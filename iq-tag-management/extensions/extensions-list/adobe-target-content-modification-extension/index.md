---
title: Adobe Target Content Modification Extension
description: Use the Adobe Target Content Modification extension along with the Adobe Target tag or Adobe Experience Platform Web SDK tag to change the content of an HTML element.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/adobe-target-content-modification-extension/
---
## Prerequisites

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* [Using Global Mbox with utag.sync.js](https://docs.tealium.com/adobe-target-using-global-mbox-with-utagsyncjs/)

## How it works

The Adobe Target Content Modification extension along with the Adobe Target tag or Adobe Experience Platform Web SDK tag  tag is used to change the content of an HTML element. This is used to show A/B content based on a condition. In order for this extension to work, it needs to be scoped to the [Adobe Target tag](https://docs.tealium.com/adobe-test-target-tag/) or [Adobe Experience Platform Web SDK tag ](https://docs.tealium.com/adobe-experience-platform-web-sdk-tag/).

This extension requires initialization code. This must be done by placing the `utag.sync.js` snippet in the `<head>` section of your page. Learn more about [using utag.sync.js]().

### Using the extension

Before you begin, familiarize yourself with [how extensions work]().

You must set the scope of this extension to the tag Adobe Target or Adobe Experience Platform Web SDK.

Once the extension is added, if you require an additional mbox besides the global mbox, configure the extension by clicking the **Add mbox** button. The following configuration options are available:

* **Element Type**: We recommend using DOM ID to identify an element, as the XPath identifier changes if the content of a page changes significantly.
    * Select **DOM ID** or **XPath**.

* **DOM ID**: Enter the element's DOM ID or XPath identifier value.
* **Mod Position**: Specify where you want the new content to go in relation to the element you identified:
    * **Before Node**: Place the content before the element you identified.
    * **After Node**: Place the content after the element you identified.
    * **Beginning of Node**: Place the content at the beginning of the element you identified.
    * **End of Node**: Place the content at the end of the element you identified.
    * **Replace Node Content**: Replace the element's content.
    * **Replace Node**: Replace the entire element.
    * **Replace Node Content (leave default)**: Replace the element's content, but if Adobe's Target service is temporarily unavailable, the default content displays instead of the test content. If you want to use the Flicker Free functionality, you must select **this Mod Position**.

* **mBox Div ID**: (Provided by Adobe) Enter the mBox ID of your test.
* **Static Params** (Optional) Add static parameters in this field in query string format, which means you delimit them with an ampersand (`&`) character.
* **Timeout**: The amount of time (in milliseconds) to wait for Adobe to respond before displaying default content on the page. This feature allows the page to finish rendering if Adobe Target tag or Adobe Experience Platform Web SDK tag personalization data is not available due to a communication issue or consent settings.

Click **Add Condition** to create the logic statement that determines when and where the extension modifies content. To add more content modification entries, click the **+** button in the upper right corner of the extension settings. Another option is to duplicate the extension for each entry instead, but keeping multiple entries in the one extension is a cleaner implementation, as all entries in this extension share the load condition for the extension.
