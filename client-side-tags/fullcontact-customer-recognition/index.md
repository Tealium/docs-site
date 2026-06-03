---
title: FullContact Customer Recognition Tag Setup Guide
description: This article describes how to set up the FullContact Customer Recognition tag.
url: https://docs.tealium.com/client-side-tags/fullcontact-customer-recognition/
---
FullContact is a privacy-safe Identity Resolution company building trust between people and brands. Delivering the capabilities needed to create tailored customer experiences by unifying data and applying insights in the moments that matter.

## Tag tips

* Use mapping to override the standard config values dynamically.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **FullContact Key**: The FullContact Tag Recognition key.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `fullContactKey`  | String | FullContact Key |
|  `base_url`  | String | Base URL |
|  `forceCallback`  | Boolean | Force Callback |
|  `fc_cb`  | Function | FullContact Callback |
