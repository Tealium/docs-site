---
title: Teads Tag Setup Guide
description: This article describes how to set up the Teads tag.
url: https://docs.tealium.com/client-side-tags/teads-tag/
---
## Tag Tips

* Use mapping to override standard configuration values and set additional options.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Teads tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **pid**
  * Your Teads-supplied PID

* **lang**
  * Language.
  * Default value is English ( `en`).

* **Slot**
  * The selector for placing the Ad.
  * Example: `.article .article_body &gt; p`

* **Format**
* **minSlot**
* **Mobile**
* **css**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable   | Description               |
|:-----------|:--------------------------|
| Pid        |                           |
| Lang       |                           |
| Slot       |                           |
| Format     |                           |
| minSlot    |                           |
| mobile     | <ul><li>Boolean</li></ul> |
| Skip delay |                           |
| Mute delay |                           |
| CSS        |                           |
| BTF        | <ul><li>Boolean</li></ul> |
| Mutable    | <ul><li>Boolean</li></ul> |
| AdBreaks   |                           |
| avoidSlot  |                           |
