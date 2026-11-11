---
title: Teads Tag Setup Guide
description: This article describes how to set up the Teads tag.
url: https://docs.tealium.com/client-side-tags/teads-tag/
---
## Tag tips

* Use mapping to override standard configuration values and set additional options.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

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

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

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
