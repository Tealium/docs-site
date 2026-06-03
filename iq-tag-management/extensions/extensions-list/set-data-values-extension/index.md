---
title: Set Data Values Extension
description: The Set Data Values extension sets the value of a data layer variable using text, another data layer variable, or JavaScript code.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/set-data-values-extension/
---
## Prerequisites

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* Familiarize yourself with [how extensions work]().

## How it works

Use this extension to set the value of a data layer variable using text, another data layer variable, or JavaScript code. The data layer variable is specified in the **Set** configuration option, and the new value assigned is specified in the **To** text box. Multiple variables can be assigned in one instance of the extension. An optional condition may be added to control when the value is assigned.

## Using the extension

Once the extension is added, the following configuration options are available:

* **Set**: The data layer variable you want to assign a value to. Select from a drop-down list of variables or create a new variable by clicking the **&#43; Add Variable** button.
* **To**: The value to assign to the variable. Click the **&#43;** button to set another variable, or the **-** button to remove a variable from the extension.  
The value can be one of these options:  
    * **Text**: Set the value to a text value that you type.
    * **Variable**: Set to the value of another data layer variable.
    * **JS Code**: Set to the value of a JavaScript code statement.

* **Condition**: (Optional) A condition is added to control when variables are assigned. If a condition is added, it must evaluate to `true` for the variables to be assigned new values.

## Examples

### Set a text value

This example shows how to set a variable to a text value. In this scenario, a condition is used to detect if a query string parameter named `q` is populated, then the data layer variable `page_type` is set to the text value `search` to indicate that this is a search results page.

1. Add the **Set Data Values** extension.
1. Set **Title** to `Set search as the page type`.
1. Select the variable `page_type` from the drop-down menu.
1. Set the value type to **Text**.
1. In the text box, enter `search`.
1. Click **Add Condition** and set the following:
    * Select the variable `q (js)`.
    * Set the condition to `is defined`.

![](/images/iq-tag-management/setdatavalues-1.png)

### Set a variable value

This example shows how to set a variable to the value of another variable. In this scenario, if the variable `page_name` does not have a value it is set to the value of the `document.title` variable.

1. Add the Set Data Values extension.
1. Set **Title** to `Set page_name`.
1. Select the variable `page_name` from the drop-down menu.
1. Set the value type to **Variable**. A variable drop-down list appears.
1. Select `Document Title` from the drop-down menu.
1. Click **Add Condition** and set the following:
    * Select the variable `page_name`.
    * Set the condition to `is not defined`.
    * Click **&#43;** outside of the **Condition** box to add an **Or** condition.
    * Select the variable `page_name`.
    * Set the condition to `is defined`.
    * Click **&#43;** next to the `is defined` text box to add an **And** condition.
    * Select the variable `page_name`.
    * Set the condition to` is not populated`.

![](/images/iq-tag-management/setdatavalues-2.png)

### Set a JavaScript code value

This example shows how to set a variable to the value returned by a JavaScript statement. In this scenario, the number of search results on a search page is determined by using jQuery to select the number of search result link elements on the page. The variable `search_results` is set to the value returned by the JavaScript code.

1. Add the Set Data Values extension.
1. Set **Title** to `Determine number of search results`.
1. Select the variable **search_results** from the drop-down menu.
1. Set the value type to **JS Code**.
1. In the text box, enter JavaScript code, exactly how it would appear in the page (or a browser console). This example uses a simple jQuery selector and the `.length` property: `$(&#39;.search-results a&#39;).length;`.
1. Click **Add Condition** and set the following:
    * Select the variable `page_type`.
    * Set the condition to `equals` and enter `search` in the text box.

![](/images/iq-tag-management/setdatavalues-3.png)
