---
title: Crimtan Tag Setup Guide
description: This article describes how to set up the Crimtan tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/crimtan-tag/
---
Crimtan is a fully programmatic, data-driven, digital marketing company based in 12 countries around the world. Crimtan turns consumer data into valuable insights and creative display advertising campaigns, helping businesses increase brand awareness, find new customers, and better maintain customer relationships.

## Tag Tips

*   Use mapping to dynamically override the standard config values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

*   **Container ID**
*   **Silent Mode**

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
| --- | --- |
| Container ID | (`containerId`) |
| Silent Mode | (`silentMode`) |
| Consent Status | (`consentStatus`) |