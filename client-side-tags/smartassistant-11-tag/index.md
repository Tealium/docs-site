---
title: SMARTASSISTANT 1.1 Tag Setup Guide
description: This article describes how to set up the SMARTASSISTANT 1.1 tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/smartassistant-11-tag/
---
With SMARTASSISTANT, businesses can create Guided Selling solutions to share their expert advice much quicker and shoppers can receive helpful and immediate support to make more confident and smarter purchase decisions.

## Tag Tips

Use mapping to dynamically override the standard config values.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the SMARTASSISTANT 1.1 tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Advisor Code**: Your SMARTASSISTANT supplied Advisor Code.
* **Subdomain**: The first part of your advisor context path.  
For example: `//{subdomain}.smartassistant.com/advisor-fe-web`
* **Div ID**: This is the Div ID on your page where the `advisor-container` div will be added.
* **Advisor Container Div ID**: This is the integration container on your page where your advisor will go.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable                 | Description      |
|:-------------------------|:-----------------|
| Advisor Code             | (`advisorCode`)  |
| Subdomain                | (`subdomain`)    |
| Div ID                   | (`divId`)        |
| Advisor Container Div ID | (`advisorDivId`) |
