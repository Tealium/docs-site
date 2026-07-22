---
title: Google Publisher Tag Setup Guide and Mapping
description: This article describes how to set up the Google Publisher tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-publisher-tag/
---The Google Publisher tag, primarily an ad tag, lets you define ad slots and the criteria or audience you'd like to target through the ad. You may enable this tag to display a single ad or multiple ads by suitably configuring the tag.

## Requirements

* DFP Account
* Network Code
* Ad unit
* Ad slot creative size

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Title**: Enter a descriptive title to identify the tag instance. Or you can choose the default **Google Publisher Tag(GPT)**.
* **NC+TAU**: Enter the Network Code (NC) and the Targeted Ad Unit (TAU) of the ad slot. These values are available in your DFP account. For example, in `/1234/travel/asia/food`, NC = `1234` and Targeted Ad Unit = `/travel/asia/food`
* Enter the **Width** and **Height** of the ad slot.
* **Div ID**: Enter the ID of the `<div>` container for the ad slot. The general format is `div-gpt-ad-#########-#`. 
For example: `div-gpt-ad-123456789-0`.
* **Collapse Empty Div's**: Choose whether or not you want the slot to collapse in the event it is not filled by an ad. The default value is set to **Yes**. Toggling to **No** will display empty slots.
* **Library**: Select where you want the `gpt.js` library code to load from:
  * **Google**: (default) Loads the library code from Google's servers.
  * **Tealium**: (Recommended) Loads the library code through Tealium's code on your webpage. This setting is recommended since it reduces the number of network requests leading to faster page load.


<blockquote>
You have the option to configure these settings from the Mapping Toolbox.
</blockquote>


## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

**Best Practice**: Load this tag on any page that contains the target ad slot.


## Data mappings

Mapping is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The destination variables for this tag are available in the Data Mapping toolbox.

For instructions on how to map to a tag destination, see [Mapping Data Sources](https://docs.tealium.com/about-data-mappings/#mapping_data_sources).


|Destination Name| Destination Variable| Description|
|---| ---| ---|
|Network Code| `networkcode`| This code is available in the Admin tab of your DFP account|
|Targeted Ad Unit| `adunit`| This is the target Ad Unit.|
|Height| `height`| Height of the ad slot,|
|Width| `weight`| Width of the ad slot.|
|Set Slot-level Targeting| `setTargeting_slot`| Sets the `key:value` parameters for the target ad slot.<br> Example: `.setTargeting("interests", "sports");`|
|Set Page-level targeting| `myvar`| Sets the `key:value` parameters of all ad slots on a page.<br> Note: Replace "myvar" with your custom targeting parameter name.<br> Example: `googletag.pubads().setTargeting("topic","sports");`|
|Multiple Slot Configs| `gptSlots`| Define an array of slots for a single page ([more details below](#multiple_slots)).<br> Note: Make sure the data source being mapped from contains an array.|
|Collapse Empty DIVs| `collapseEmptyDivs`| Collapses ad slots that do not get filled.<br> Note: Make sure the data source value contains either `true` or `false`.|
| Publisher Provided ID | `publisherProvidedId` | Sets values for publisher-provided ID for use in frequency capping and other audience-based activities. |

## Configuring the Tag for multiple ad slots

Adding and configuring the GPT for a single ad slot is very simple and straightforward. Employing the same process to configure multiple ad slots becomes tedious because you would have to to add an instance of GPT for all the ads you want to display. A faster alternative is to store all slot configurations in an array then map the array to the **Multiple Slot Configs** destination in the GPT instance. To create such an array, you can use the [JavaScript Code Extension](https://docs.tealium.com/javascript-code-extension/). Make sure to define the slot configurations for every ad in this order:

Network Code + Targeted Ad Unit, Eligible Creative Size(s), Ad Container DIV ID, Slot-Level Targeting Name/Value Pairs

### Using the JavaScript code extension

Write a JavaScript code that uses the `googletag.cmd.push` function to define an array of slot configurations for all the ads you want to display on a page.

1. Navigate to the Extensions tab and add the [JavaScript Code Extension](https://docs.tealium.com/javascript-code-extension/) from the Extensions marketplace.
1. Scope the extension to **Google Publisher Tag(GPT)**.
1. Write the JavaScript code as you would in any editor. Do not include the `<script>` tags around the code.

Here's a sample code for configuring three ad slots using a single GPT:

```js
googletag.cmd.push(function() {
   googletag.defineSlot("/111/example.com/electronics", [700, 200], "div-gpt-ad-987654321-0").addService(googletag.pubads()).setTargeting("slot_var", "tv");
   googletag.defineSlot("/222/example.com/electronics", [250, 170], "div-gpt-ad-987654321-1").addService(googletag.pubads()).setTargeting("slot_var", "dvd player");
   googletag.defineSlot("/333/example.com/electronics", [300, 100], "div-gpt-ad-987654321-2").addService(googletag.pubads()).setTargeting("slot_var", "smartphone");
   googletag.pubads().enableSingleRequest();
   googletag.pubads().enableSyncRendering();
   googletag.enableServices();
});
```


<blockquote>
You may choose to use the `u.gptSlots.push()` method instead of `googletag.cmd.push` and reference the NC+TAU value from a data source.<br>
For example, `u.gptSlots.push([b.GPT_SlotID, [[728, 90]], 'div-gpt-ad-987654321-0', {"place":"london","theme":"sports"}]);`
</blockquote>


## Vendor documentation

* [Overview of GPT](https://support.google.com/admanager/answer/181073?hl=en)
* [Setting targeting and sizes with GPT ](https://support.google.com/dfp_sb/answer/1698183?hl=en)
* [Collapsing empty div elements](https://support.google.com/dfp_sb/answer/3419382?hl=en&ref_topic=4409240)
* [Tag Samples ](https://support.google.com/dfp_sb/answer/1651549?hl=en&ref_topic=4409240)
