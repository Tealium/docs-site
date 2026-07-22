---
title: Tealium Currency Converter Tag
description: This article describes how to set up the Tealium Currency Converter tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/tealium-currency-converter-tag/
---
## How it works

There are two components related to implementing currency conversion:

* Tealium Currency Converter Tag
* Currency Converter Extension ([Learn more](https://docs.tealium.com/currency-converter-extension/))

## Tealium Currency Converter Tag

Once per day, the exchange rates from [Open Exchange Rates](https://openexchangerates.org) are synced to Tealium. When the Currency Converter Tag runs on your site, it fetches the exchange rate information from Tealium and makes it available to the extension. It also defines a utility JavaScript function so that you can perform conversions manually in your code.

The currency exchange rates are stored in this file:

`https://tags.tiqcdn.com/utag/tiqapp/utag.currency.js`


<blockquote>
This is a blocking tag so, while it is still loaded asynchronously, it will prevent other Tealium tags from loading until it is loaded.
</blockquote>


## Currency Converter Extension

This extension makes it easy to configure the currency conversion to store a converted value in a data layer variable. Learn more about the [Currency Converter extension](https://docs.tealium.com/currency-converter-extension/).

## Add the Tag

Use the following steps to add the Tealium Currency Converter tag:

1. Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).
1. Using the Tag wizard, give the Tag a specific title, enter any notes, and proceed to the load rules tab.
1. Select any load rules you want to apply, then click **Finish**.![](https://docs.tealium.com/images/client-side-tags/no-title-1602i561ebcf8f19811c5.png)

## Currency Convert Function

When the Currency Converter tag is loaded on the page, the following utility function is available for use:

`tealiumiq_currency.convert(amount, source_currency, converted_currency)`

|Parameter| Description|
|---| ---|
|`amount`| The currency amount to convert, either as a string/number or an array of values. For example, `100` or `[100, 200, 300]`|
|`source_currency`| The three-character currency code representing the value in amount. For example, `USD`|
|`converted_currency`| The three-character currency code to convert the amount to. For example, `GBP`|

Example:

```
var order_total_uk = tealiumiq_currency.convert(100, "USD", "GBP");
```
