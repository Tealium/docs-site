---
title: Neustar (Real User Measurement) tag
description: This article describes how to configure the Neustar (Real User Measurement) tag.
url: https://docs.tealium.com/client-side-tags/neustar-real-user-measurement-tag/
---
Neustar (RUM), Inc. is a trusted, neutral provider of real-time information and analysis to the internet, telecommunications, information services, financial services, retail, media and advertising sectors.

## Tag tips

* Add the following code to a PreLoader extension for more accurate metrics:
```
window.t_pagestart = new Date().getTime();
```
* Recommended that this tag runs first (move to top of tags list)
* This tag should be set to `Wait=Yes` (default)
* No tag configuration needed

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Account ID**: The account ID.
* **Time Out Value**: Set the amount of time before the tag times out.
* **Run Init at Tag load**: Run init process when the tag loads. Cannot be mapped.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Description |Variable  |
|:---------|:------------|
|  `account` | Account ID |
|  `time_out` | Perceived load timeout  |