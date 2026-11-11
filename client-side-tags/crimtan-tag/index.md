---
title: Crimtan Tag Setup Guide
description: This article describes how to set up the Crimtan tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/crimtan-tag/
---
Crimtan is a fully programmatic, data-driven, digital marketing company based in 12 countries around the world. Crimtan turns consumer data into valuable insights and creative display advertising campaigns, helping businesses increase brand awareness, find new customers, and better maintain customer relationships.

## Tag tips

*   Use mapping to dynamically override the standard config values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

*   **Container ID**
*   **Silent Mode**

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
| --- | --- |
| Container ID | (`containerId`) |
| Silent Mode | (`silentMode`) |
| Consent Status | (`consentStatus`) |