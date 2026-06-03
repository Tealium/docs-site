---
title: Debugging
description: Learn the basics of debugging tracking calls.
url: https://docs.tealium.com/platforms/javascript/debugging/
---
The functions `utag.view()` and `utag.link()` are used to track page views and events, respectively. This article shows how to debug these functions to see how and when they are being called and what data is being processed.

## Debug mode

To enable debug mode, open the developer console in your browser and run the following command:

```js
document.cookie=&#34;utagdb=true; path=/&#34;;
```

This cookie turns on debug mode which generates useful output to the console.

![](/images/platforms/javascript/console-output.png)

When debug mode is enabled, log statements appear in the console when tracking calls occur. Look in the console output for these statements:

```none
trigger: view
trigger: link
```

The following example demonstrates how this looks in the console after an event is tracked:

![](/images/platforms/javascript/debugging-console-utag-link.png)

Click the line after `trigger:view` or `trigger:link` to expand and collapse the event data object.

## Breakpoints

For more in-depth debugging, it is useful to set breakpoints in `utag.js` to pause the code when calls tracking calls occur. Use breakpoints to inspect the tracking data object or to inspect the stack trace to see where the call originated. 

To use Chrome DevTools to set a breakpoint:

1. Open DevTools and go to the **Sources** tab, then open the file `utag.js`.
1. Find the line with `return this.track(` and click the line number to set a breakpoint:  
      ![](/images/platforms/javascript/debugging-utag-code.png)
4. Return to the main window and perform an action to trigger a tracking call. When the tracking call runs, the code will pause on the breakpoint.
5.  In the right panel, expand the **Watch** pane and click the **&#43;** sign to add a watch expression. Type `a` and click **Enter** to add a watch expression for this variable.
6.  Expand the object that is contained in parameter `a` to show the data that was passed to the tracking call. This data is available in extensions, load rules and data mappings. 
7. In the right panel, expand the **Call Stack** pane to see where the tracking call originated.

The following is an example of where to look for the location of a `utag.link()` call:

![](/images/platforms/javascript/utag-link-call-stack.png)

This example shows the breakpoint in `utag.js` that was placed to debug the `utag.link()` call. Item (2), when clicked, shows the `utag.link()` call that is made within the source code (to the left). 

You have now successfully been able to debug three things:

*   Did the breakpoint get hit? If yes, then the function is set up to be triggered correctly.
*   Since the breakpoint was hit, you were able to see what data was sent when `utag.view()` or `utag.link()` was called. 
*   You were able to view the actual configuration of the `utag.view()` or `utag.link()` call. 

This is helpful when you are not seeing the correct data passed when certain events are triggered. It is likely that the data being sent in the function is incorrect.

For more information, see [Chrome DevTools: JavaScript debugging](https://developer.chrome.com/docs/devtools/javascript/reference/).

## Console output

This following table describes some of the important debug statements that appear in the console. The debug output on your site might vary slightly based on your version of `utag.js` or your specific settings.

| Debug statement | Description |
| ------------- | ----------- |
| `Pre-INIT` | Extensions scoped to **Pre Loader** run. |
| `PINIT` | Extensions scoped to **Before Load Rules** run, load rules are evaluated, and tags are loaded. |
| `utag.loader.RD` |  Data layer variables are read from the page (see [data layer variable types](). |
| `utag.loader.INIT`| Extensions scoped to **After Load Rules** run and tags are loaded.  |
| `All Tags EXTENSIONS`| Extensions scoped to **After Load Rules** run. |
| `utag.loader.INIT: waiting &lt;UID&gt;` | The tag (UID) is set to load at DOM Ready and is added to the queue.  |
| `READY:utag.cfg.readywait` | DOM Ready occurs and `PINIT` runs. |
| `READY:utag.cfg.wq` | DOM Ready occurs and queued tags are processed. |
| `WQ: #` | The number of tags in the queue to wait for DOM Ready. |
| `Attach to head` | Tag script is added into the source code.|
| `utag.loader.LOAD &lt;UID&gt;` | The tag (UID) has loaded on the page. |
| `Sending: &lt;UID&gt;` | The tag (UID) is triggering the call to the vendor. |
| `trigger:view` | `utag.view()` was called. |
| `trigger:link` | `utag.link()` was called. |
| `trigger:called before tags loaded` | A tracking call occurred before the tags loaded on the page. The tracking call is queued and will run after the tags load.|
| `utag.handler.INIT` | Queued tags are triggered. |
