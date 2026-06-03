---
title: Event trigger variables
description: This article explains how to add or customize event trigger variables.
url: https://docs.tealium.com/iq-tag-management/events/variables/
---
Event trigger variables are the values sent in the tracking call. You can edit existing trigger variables or add custom variables to collect extra data with the event.

1. From the event&#39;s **Configuration** page, select the variable from the list, or click **&#43; New Variable** to create a new variable.
    1. Select the **Type** of variable to set.
    1. Enter the **Source** for this variable. Use the variable name that your site&#39;s source code uses.
    1. (Optional) Enter an **Alias** to identify the variable.
    1. (Optional) Enter any **Notes** for this variable.
    1. Click **Apply** to set the new variable.
1. Select an option from the list.
    * **Text** – Set a value for the variable in the text box.
    * **Variable** – Select another variable to set this variable to.
      - Use `event` to reference the event object. To reference a property of the event, use dot or bracket notation (for example, `event.property`).
      - Use `element` to reference the DOM element. To reference a property of the DOM element, use dot or bracket notation (for example, `element.property`).
    * **JavaScript** – Enter the JavaScript code to evaluate for this variable&#39;s value. Write the code without a trailing semicolon. A trailing semicolon is injected into the surrounding code in `utag.js` and causes it to fail to load.
    * **Data Layer Value** – Send the variable as-is from the utag data to the data layer.

If the event scope is set to **Pre Loader**, you can&#39;t select **Data Layer Value** or **Variable** because `utag.data` doesn&#39;t exist in that scope.

To add another row to the list, click the plus symbol ( **&#43;** ).

To delete a row from the list, click the minus symbol ( **-** )
