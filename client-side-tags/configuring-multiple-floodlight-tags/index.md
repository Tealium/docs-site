---
title: Configuring Multiple Floodlight Tags
description: This articles describes how to set up multiple Floodlight tags in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/configuring-multiple-floodlight-tags/
---If you have many Floodlight tags, all with a slightly different configuration, but based on the same load criteria, for example, different paths in the URL, rather than setting up several similar instances of the Floodlight tag, each with different load rules and configuration values, you can combine them into one instance of the Floodlight tag using some additional configuration.


<blockquote>
Google recommends migrating to the Google global site tag by implementing the [Floodlight tag](https://docs.tealium.com/client-side-tags/floodlight-gtagjs-tag/).
</blockquote>


## How it works

This multi-tag solution uses data mappings to set the Floodlight parameters dynamically and a lookup table to set the Floodlight values based on a data layer variable. The lookup table creates a delimited string containing multiple values per entry which can then be separated into individual Floodlight parameters using a JavaScript Code extension.

## New data layer variables

You will need the following variables for the data mappings in the Floodlight tag and for the lookup table extension. The "dc_" prefix is a best practice to remind you that these variables are used for the Floodlight configuration.

Create the following:

* **dc\_advertiserId** (mapping)
* **dc\_type** (mapping)
* **dc\_category** (mapping)
* **dc\_counterType** (mapping)
* **dc\_settings** (lookup table extension)

## Data mapping

In this multi-tag solution the Floodlight parameters will be set dynamically based on the output of the lookup table extension, so the values must be set in the tag configuration using data mappings.

Set the following data mappings:

* `dc_advertiserId` set to `src`
* `dc_counterType` set to `countertype`
* `dc_type` set to `type`
* `dc_category` set to `cat`

Once completed the mappings will look like this:

![](https://docs.tealium.com/images/client-side-tags/doubleclick-multi-tag-data-mappings.png)

## Extensions

This solutions uses three extensions to construct all of the Floodlight tags we intend to fire. The following extensions will be added and must be ordered as they appear here:

* **Lookup Table**  
This sets a delimited string based on the selection criteria (in this case we will be using the URL pathname).
* **Set Data Values**  
This converts the delimited string from the lookup table into the separate Floodlight variables.
* **JavaScript Code**  
This verifies that a value exists for the tag to fire, otherwise it suppresses the tag.

### Lookup table extension

This extension will be used to set a delimited string based on a criteria variable. In this example, the criteria variable is the `pathname` variable and the delimited string is the `dc_settings` variable set in the following format:

```
ADVERTISER ID|TYPE|CATEGORY|COUNTERTYPE
```

To add this extension:

1. Add a [Lookup Table extension](https://docs.tealium.com/lookup-table-extension/).
1. Set the **Title**. For example, "DC Settings".
1. Set **Scope** to the Floodlight tag you just added.
1. Set **Lookup Value In**: `pathname`
1. Set **Destination**: `dc_settings`
1. Set **Variable Type**: String
1. Set **Match Type**: Contains

Each lookup table entry will contain a URL pathname and a delimited string value. This example uses the following entries:

|**Pathname**| **Output**|
|---| ---|
|/test1/test| 321123|Testing|Test001|standard|
|/test2/test/something.htm| 321123|Testing|Test002|standard|
|/test1/docs| 321123|Docs|Test003|standard|

The Lookup Table extension should appear as follows:

![](https://docs.tealium.com/images/client-side-tags/doubleclick-multi-tag-lookup-table.png)


<blockquote>
Use the **Import from CSV...** option to manage long lists.
</blockquote>


### Set data layer extension

This extension will separate the delimited string into separate Floodlight variables.

To add this extension:

1. Add a [Set Data Values extension](https://docs.tealium.com/set-data-values-extension/).
1. Set the **Title**. For example: "Floodlight Parameters".
1. Set **Scope** to the Floodlight tag you just added.
1. Set a variable for each of the Floodlight parameters: 

|**Set Variable**| **Value Type**| **Value**|
| --- | --- | --- |
|dc\_advertiserId| JS Code| **b['dc_settings'].split("&#124;")[0]** |
| dc\_type| JS Code| **b['dc_settings'].split("&#124;")[1]**|
| dc\_category| JS Code| **b['dc_settings'].split("&#124;")[2]**|
| dc\_counterType| JS Code| **b['dc_settings'].split("&#124;")[3]**|

The extension should appear as follows:

![](https://docs.tealium.com/images/client-side-tags/doubleclick-multi-tag-set-data.png)


<blockquote>
Use the **Add Condition** to test that `dc_settings` is populated to ensure this will only run when there is a value.
</blockquote>


### JavaScript code

This extension will suppress the Floodlight tag if the lookup table extension did not output a value, for instance, there is no tag to fire. This means that you can keep the "All Pages" load rule set on the Floodlight tag and it will not fire if there is no configuration for the current page.

To add this extension:

1. Add a [JavaScript Code extension](https://docs.tealium.com/advanced-javascript-code-extension/).
1. Set the **Title**. For example: "Check Value".
1. Set **Scope** to the Floodlight tag you just added.
1. Enter this code:  
```
if(b['dc_settings']===''){
    return false;
}
```

1. Publish your changes for testing.
