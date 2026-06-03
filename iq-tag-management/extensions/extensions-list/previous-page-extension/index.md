---
title: Previous Page Extension
description: The Previous Page extension is used to persist the name of the previous page for use on the subsequent page.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/previous-page-extension/
---
## Prerequisites

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* [How extensions work]()

## How it works

The Previous Page extension adds a variable to the data layer named `previous_page_name`. The value of this variable is set to the value of a data layer variable from the previous page. You specify which data layer variable to use as the page name and the extension will save this value in a cookie so that it can be used on subsequent pages.

Here is a simple example where `page_name` is used. It shows what value to expect in `previous_page_name` as a visitor navigates through a series of pages. Notice that `previous_page_name` is not set on the first page in the session.

|**Page**| `page_name` | `previous_page_name`|
|---| ---| ---|
|Home Page| `Home - Welcome` | (not set)|
|Search Page| `Search for iPhone` | `Home - Welcome` |
|Product Page| `iPhone 10 Product Details` | `Search for iPhone` |

## Using the extension

Once the extension is added, the following configuration option is available:

* **Page Value**: Select the data layer variable that contains the page&#39;s name.

The extension automatically saves the value of this variable and sets it to `previous_page_name` on the next page view.
