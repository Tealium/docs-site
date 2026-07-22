---
title: Crazy Egg Tag Setup Guide
description: This article describes how to set up the Crazy Egg tag.
url: https://docs.tealium.com/client-side-tags/crazy-egg-tag/
---
## Tag Specifications and Requirements

### Specifications

**Name**: Crazy Egg

**Vendor**: Crazy Egg

**Type**: Miscellaneous: Heat mapping

##### Required

**Services**: Crazy Egg Account

**Configurations**:

* Account

## Tag Configuration in Tealium iQ

### Add the Tag

Tealium iQ's Tag marketplace offers a wide variety of tags. Click [here](https://docs.tealium.com/manage-tags/) to learn how to add a tag to your profile.

### Configure the Tag

Here's a list of tag configurations essential to load the Crazy Egg Tag:

1. **Title**: (Required) Enter a descriptive title to identify the tag.
1. **Account**: (Required) Enter your Crazy Egg account number.

**Tip**: Place this tag near the top of the list in the **Tags** tab to ensure that it loads as soon as possible. The sooner the tag loads, the sooner it captures visitors' activity.

### Apply Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag. The **Display on All Pages** rule is the default load rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

**Note**: We recommend creating load rules to load this tag only on those pages you are trying to generate a heat map for.

### Setting up Mappings

[Mapping](https://docs.tealium.com/about-data-mappings/) is the process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag.

For Crazy Egg, mappings are not supported in Tealium iQ. By default Crazy Egg's library captures data and sends it to your Crazy Egg report. To use custom User Vars 1 through 5, you must pass the following method definition into a callback function:

```
window.CE_READY = function CE_READY() {
CE2.set(1, 'some string');
CE2.set(2, 'another value');
CE2.set(3, 'yet another value');
CE2.set(4, 'more');
CE2.set(5, 'and more');
}
```

----

## Vendor Documentation

* [Crazy Egg Support](http://support.crazyegg.com/)
