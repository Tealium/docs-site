---
title: Universal Tag Debugger
description: The Universal Tag (UTAG) Debugger is a tool used for validating the Universal Data Object and tracking calls.
url: https://docs.tealium.com/iq-tag-management/tealium-tools/utag-debugger/
---
## How it works

The Universal Tag (UTAG) Debugger tool displays the [Universal Data Object]() and event tracking callstriggered by `utag.js` on a site.

![](/images/iq-tag-management/utag-debugger.png)

## Install

### Tealium Tools

To install UTAG Debugger as a Tealium Tool, first install the [Tealium Tools Browser Extension]().

After you install the extension, follow these steps to add the custom tool:

1. Click the Tealium icon in the upper-right of your browser to open Tealium Tools.
1. Go to the **Custom Tools** tab and click the square for **&#43; Custom Tools**, then click **Add Custom Tools**.
1. Next, copy and paste the following JSON code in the field for **Add by JSON Definition** then click **Add Custom Tool**:  
    ```json
    {
        &#34;id&#34; : &#34;teal.sol.debug&#34;,
        &#34;title&#34; : &#34;UTAG Debugger&#34;,
        &#34;description&#34; : &#34;Universal Tag Debugger&#34;,
        &#34;no_ui&#34; : true,
        &#34;scripts&#34; : {
            &#34;utag_monitor&#34; : {
                &#34;js&#34; : &#34;void(window.open(\&#34;\&#34;,\&#34;utagmon\&#34;,\&#34;width=700,height=600,location=0,menubar=0,status=1,toolbar=0,resizable=1,scrollbars=1\&#34;).document.write(\&#34;&lt;script language=&#39;JavaScript&#39; id=&#39;utagmon&#39; src=&#39;//tags.tiqcdn.com/utag/tealium-solutions/main/prod/utag.4.js?opt_show_enrich=0&amp;opt_show_meta=0&amp;opt_show_query=0&amp;opt_show_jspage=0&amp;opt_show_tiq=1&amp;opt_show_cookie=0&amp;_cb=\&#34;&#43;Math.random()&#43;\&#34;&#39;&gt;&lt;/\&#34;&#43;\&#34;script&gt;\&#34;));&#34;,
                &#34;auto_inject&#34; : true
            }
        }
    }
    ```
1. When complete, a new button with the tool name appears on the **Custom Tools** tab.

### Bookmarklet

To install UTAG Debugger as a bookmark, copy the following code into the URL of a new bookmark:
```js
javascript:void(window.open(&#34;&#34;,&#34;utagmon&#34;,&#34;width=700,height=600,location=0,menubar=0,status=1,toolbar=0,
resizable=1,scrollbars=1&#34;).document.write(&#34;&lt;script language=&#39;JavaScript&#39; id=&#39;utagmon&#39;
src=&#39;//tags.tiqcdn.com/utag/tealium-solutions/main/prod/utag.4.js?
opt_show_enrich=0&amp;opt_show_meta=0&amp;opt_show_tiq=1&amp;opt_show_dom=0&amp;opt_show_jspage=0&amp;opt_show_cookie=0&amp;_cb=&#34;
&#43;Math.random() &#43;&#34;&#39;&gt;&lt;/&#34;&#43;&#34;script&gt;&#34;))
```

## Use UTAG Debugger

To launch UTAG Debugger, follow these steps:

1. Navigate to your site.
1. For Tealium Tools, open Tealium Tools and click **UTag Debugger**. 
1. For the bookmarklet, click the bookmark in your browser toolbar.
    ![](/images/iq-tag-management/utag-debugger-bookmarklet.png) 

### Version and display options

When UTAG Debugger is open, the top section displays the `utag.js` file detected on the page with the following information:

* The `account/profile/environment` of the `utag.js` file on the page.
* The version of the `utag.js` file on the page.

![](/images/iq-tag-management/utag-debugger-options.png)

Use the following features:

* **Bookmarklet** – Save your preferred display options by dragging the link to your browser&#39;s toolbar.
* **Events** – The tracking events detected on the page are either `view` events or `link` events. Toggle these checkboxes to filter the display.
* **Scope** - Select the scope of the UDO data to display. The default is **Before load rules**.
    The UDO variables displayed in the tool are captured after extensions scoped to **All Tags - Before Load Rules** and after extensions scoped to **All Tags - After Load Rules**. Learn more about [order of operations]().
* **Show Data** – Select the variable types to display. The UDO variables are always displayed.


### Variable types

The following variable types are available:

* **iQ** – Built-in data collected by `utag.js`, including DOM attributes and variables prefixed with `ut.` (for example: `ut.profile`).
* **Cookie** – All first-party cookies available in the page.
* **JS Page** – JavaScript page variables defined in your data layer (variables other than `utag_data`).
* **Querystring** – Query string variables found in the URL.
* **Meta** – All meta data values available in the page.
* **AudienceStream** – Variables populated by data layer enrichment.
* **Local storage** – Local storage variables defined in your data layer.
* **Session storage** – Session storage variables defined in your data layer.

For more information, see [Data layer variable types]().

### Events

The data display area automatically updates as you navigate or trigger events. New pages are listed as `utag_view` events and in-page events are listed as `utag_link` events.

The following example shows two pages visited and one event triggered. The result is two `utag_view` entries and one `utag_link` entry. The most recent activity always appears at the top.

![](/images/iq-tag-management/utagmon-event-display.jpg)
