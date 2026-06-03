---
title: Currency Converter Extension
description: The Currency Converter extension coverts the value of a data layer variable in one currency into a different currency.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/currency-converter-extension/
---
## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* [Tealium Currency Converter Tag]() (can be scoped to All Tags or any specific tag)

## How it works

The Currency Converter extension works with the Tealium Currency Converter tag, which makes the exchange rates available to the extension. The extension coverts the value of a data layer variable in one currency into a different currency. The extension may be configured to convert many data layer variables. Each conversion is controlled by a load rule to help run the conversion only when needed.

## Using the extension

Before you begin, familiarize yourself with [how extensions work]().

Once the extension is added, click **Add Currency Conversion** to add a new conversion, then set the following fields (repeat this step as needed):

* **Convert**: The data layer variable containing the value to convert.
* **On Condition**: The load rule used to trigger the conversion.
* **From Currency**: The currency of the current value.
* **To Currency:** The currency of the new, converted value.

### Example

On your site, customers can make purchases in any currency, but one tag vendor always expects amounts to be sent as USD values. Here are the components needs to convert a data layer variable from many currencies into USD:

* **Currency Load Rules**: Create a load rule for each currency that a customer might use, such as:

  
  [
    [
      {
        &#34;input&#34;: &#34;site_currency&#34;,
        &#34;operator&#34;: &#34;equals (ignore case)&#34;,
        &#34;filter&#34;: &#34;GBP&#34;
      }
    ]
  ]
  
    
* **Currency Converter Extension**: Add a currency conversion for each currency that your site supports and for each data layer variable that needs to be converted. Notice how this example is scoped to the specific tag that requires all values be sent in USD.  
    ![](/images/iq-tag-management/iq-currency-extension.jpg)
