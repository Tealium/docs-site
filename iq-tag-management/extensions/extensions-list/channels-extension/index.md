---
title: Channels Extension
description: The Channels extension is used to get a view of your customer's journey across multiple channels.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/channels-extension/
---
For example, you may be running across many ad channels, and want to know what the channel life cycle is for customers. Are people looking at one or many ads? Which ads are they looking at first or last? For those that do buy, what is the flow before they purchased?
 
This extension also provides you with the ability to set the Channel Conversion Credit for your Originator, Influencer, and Closer affiliates.

## Prerequisites

* Before you start, see [About Extensions]().

## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## Using the extension

Once the extension is added, the following configuration options are available:

### Channels

* **Channel Name**: The name of the channel
* **Category**: Select the Category that the channel belongs from the drop-down menu
* **Condition**: Apply a condition to determine when to set this channel. Click the **&#43;** button to add new conditions, or the **-** button to remove conditions.

Click the **Add Channel** button to add and configure an additional channel, as needed.

![](/images/iq-tag-management/no-title-176icaa0d1be9b890a0e.png)

### Attribution period and population

Choose on which pages you want to populate the Output data sources. We recommend you only populate these data sources on a conversion-type page, such as a cart page or order confirmation page.

Navigate to the **Attribution Period/Population** tab. From this tab you set how long you want to attribute conversions to certain channels and on what pages you want this to happen.

* **Attribution Period:** Enter an integer, and select the units from the drop-down menu
    * **Session**: lasts for the duration of user&#39;s visit to the website. It displays a &#39;0&#39; in the cookie.
    * **Visitor**: The max value is set to 365 days, and displays a timestamp.
    * **Days**: This value is the number of days to keep the data, and displays a timestamp.

* **Data Sources:** (Default: All Pages) Select a load rule to determine when and where you want the Channels extension to run. We recommend you use the default value.
* **Clear Persisted Values on Data Source Population**: Selecting the checkbox clears the data from all output data source on each page load.
    * Check the box if you want to track the current channel only, or check the box if you are not interested in lifetime channel behavior beyond a single conversion.
    * Do not check the box for sites that have multiple conversions.

![](/images/iq-tag-management/no-title-175i03abcc3041938f48.png)

### Conversion

To determine the commission amount to give to a channel depending on how it contributed to a conversion:

* **Conversion Value Source**: This is the data source that contains the numeric conversion amount that credit is based on. This is often the subtotal amount of a conversion.
* **Originator Credit**: This is the percentage of the conversion value source to be attributed to the originator of a conversion.
* **Influencer Credit**: This is the combined percentage of the conversion value source attributed to any influencer or influencers of a conversion.
    * By checking **Allow Repeat Channel Responses** you enable a Channel to appear as an Influencer more than once. If you leave this value unchecked, each unique influencer is only listed once.

* **Closer Credit**: This is the percentage of the conversion value source attributed to the closer of a conversion.

![](/images/iq-tag-management/no-title-174icc0c5df949e4995c.png)

## Cookie data formatting

Data from this extension is saved in a cookie called `channelflow`. The cookie data provides the full channel flow from beginning to end. Each channel has three values: the channel name, the category, and the attribution period. Each value is saved as a string delimited by a bar &#39;`|`&#39;. Each individual channel is separated by a comma. The following is an example:

```
Channel1 Name|Category|Attribution Period, Channel2 Name|Category|Attribution Period
```

If the attribution period is set to `Same Session`, then its value in the cookie is `0`. If the attribution period is set to either `Visitor` or `Days`, then the attribution period value is a number greater than zero.

So, if we had three channels (`channel1`, `channel2`, and `channel3`) with categories set to `affiliate`, `display ads`, and `sponsorship`, respectively and the attribution period for all of them set to `Same Session`, the data will resemble the following:

```
channel1|affiliate|0,channel2|displayads|0,channel3|sponsorship|0
```

The same channels and categories with their attribution period set to `Visitor` or `Days` will resemble the following:

```
channel1|affiliate|1358975968083,channel2|displayads|1358975970419,channel3|sponsorship|1358975973256
```

### Read the cookie data

Cookie data provides the full channel flow from beginning to end. The cookie is read from left (beginning) to right (end).

* The cookie and page variables are made up of channels, categories, and expiration dates.
* The cookie examples above read as `channel|category|expiration`
    * **Channel**: the name of the channel, such as `PepperJam`.
    * **Category**: the category of the channel, for `PepperJam choose Affiliate`.
    * **Expiration**: keeps track of the lifecycle of the channel flow for the duration assigned (based on the attribution period).

* When determining who the credit for the sale/conversion goes to, credit goes to the last visited channel, which in our example is channel `SF`.

## Channel variables

When you use the Channels extension, the data persisted by the extension are saved in new data layer variables that are readily available for use in load rules, extensions, and data mappings. These variables provide more detailed information by splitting out channels from categories, and by providing the first, last, and all visited channels and categories.

The following variables are created:

| Variable                      | Description                                                                                                                                                                                                                                                                         |
|:------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `channel_category_originator` | The first Category visited.                                                                                                                                                                                                                                                         |
| `channel_originator`          | The first channel visited.                                                                                                                                                                                                                                                          |
| `channel_category_influencer` | The list of categories visited, not including the closer.                                                                                                                                                                                                                           |
| `channel_influencer`          | The list of channels visited, not including the closer.                                                                                                                                                                                                                             |
| `channel_category_closer`     | The last category visited.                                                                                                                                                                                                                                                          |
| `channel_closer`              | The last channel visited.                                                                                                                                                                                                                                                           |
| `channel_category_path`       | All categories visited                                                                                                                                                                                                                                                              |
| `channel_path`                | All channels visited.                                                                                                                                                                                                                                                               |
| `channel_originator_credit`   | Displays the amount credited to the originator based on the percentage of the conversion value.                                                                                                                                                                                     |
| `channel_influencer_credit`   | The amount credited to each influencer based on the percentage of the conversion value. This is calculated by taking the Influencer Credit percentage multiplied by the Conversion Variable value and divided by the number of Channels listed in the `channel_influencer` variable |
| `channel_closer_credit`       | The amount credited to the closer based on the percentage of the conversion value.                                                                                                                                                                                                  |

If you only want to pass channel information to a vendor tag on certain pages, follow these steps:

1. Create a new data layer variable.
1. Configure a Set Data Values extension to set the value of the new data source to the channel closer, for example, on certain pages.
1. Open the vendor tag settings and map the new variable, instead of `channel_closer`, to the appropriate tag destination.

### Read the channel variables

To see how the variables change with each page visit, imagine the scenario above where the customer views the PJ, then EM, then SF Channels. Notice how the variables change as follows:

1. First Channel Flow:
    * `channel_category_originator: affiliate`
    * `channel_originator: PJ`
    * `channel_category_path: affiliate`
    * `channel_path: PJ`
    * `channel_category_closer: affiliate`
    * `channel_closer: PJ`

1. Second Channel Flow:
    * `channel_category_originator: affiliate`
    * `channel_originator: PJ`
    * `channel_category_path: affiliate,displayads`
    * `channel_path: PJ,EM`
    * `channel_category_closer: displayads`
    * `channel_closer: EM`

1. Third Channel Flow:
    * `channel_category_originator: affiliate`
    * `channel_originator: PJ`
    * `channel_category_path: affiliate,displayads,sponsorships`
    * `channel_path: PJ,EM,SF`
    * `channel_category_closer: sponsorships`
    * `channel_closer: SF`

## Custom handling - advanced

The custom handling code is run at the end of the extension, so any calculations and assignments are completed when this code is invoked.

The container object is named `obj` and it contains the following attributes for any custom handling:

* `channel_originator`
* `channel_influencer`
* `channel_closer`
* `channel_category_originator`
* `channel_category_influencer`
* `channel_category_closer`
* `channel_path`
* `channel_category_path`
* `channel_originator_credit`
* `channel_influencer_credit`
* `channel_closer_credit`

The following is a custom handler example:

```
  // Custom Handler Example
  // if commisionjunction is the originator
  // it is also the closer
  if(obj.channel_originator==&#39;commisionjunction&#39;){
    obj.channel_closer=&#39;commission junction&#39;;
  }
```

## Testing

Complete testing after the Channels extension is published to your environment.

Make note of the page URLs where the different Channels reside, and navigate to each of the URLs so that the data is captured.

Using Chrome debugging tools, or Firefox tools such as [HTTPFox](https://addons.mozilla.org/en-us/firefox/addon/httpfox/) and [Firebug](http://getfirebug.com) allow you to see page variables and cookie states. These tools help you to debug any issues and validate that the Channel Flow tracking is working, as needed.
