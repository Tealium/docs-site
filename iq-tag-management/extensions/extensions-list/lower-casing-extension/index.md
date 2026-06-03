---
title: Lower-Casing Extension
description: The Lower-Casing extension sets data layer values to lower-case. This is a best practice for data consistency.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/lower-casing-extension/
---
## Prerequisites

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* [About Extensions]().

## How it works

This extension uses the JavaScript method [`String.toLowerCase()`](https://www.w3schools.com/jsref/jsref_tolowercase.asp) to convert data layer values to lower-case. The extension can be applied to all data layer variables or specific ones.

## Using the extension

Once the extension is added, the following configuration options are available:

* **All Variables to Lower Case**: (Default: Yes)
    * **Yes** (default): sets all variables to lower-case.
    * **No**: only set specific variables to lower-case.  
  
Select a variable from the drop-down.  
Click the **&#43;** button to add more variables, or the **-** button to remove variables.

## Example

In this example, lower-casing is performed on a specific variable, `search_keyword`. This is a common practice to ensure that that all tracked searches are case-insensitive.

Step to configure:

1. Add the Lower-Casing extension.
1. Set a title.
1. Set **All Variables to Lower Case** to **No**.
1. From the variable drop-down, select **Search Keyword**.

![](/images/iq-tag-management/lowercasing.png)
