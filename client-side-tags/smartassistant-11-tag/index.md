---
title: SMARTASSISTANT 1.1 Tag Setup Guide
description: This article describes how to set up the SMARTASSISTANT 1.1 tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/smartassistant-11-tag/
---
With SMARTASSISTANT, businesses can create Guided Selling solutions to share their expert advice much quicker and shoppers can receive helpful and immediate support to make more confident and smarter purchase decisions.

## Tag tips

Use mapping to dynamically override the standard config values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Advisor Code**: Your SMARTASSISTANT supplied Advisor Code.
* **Subdomain**: The first part of your advisor context path.  
For example: `//{subdomain}.smartassistant.com/advisor-fe-web`
* **Div ID**: This is the Div ID on your page where the `advisor-container` div will be added.
* **Advisor Container Div ID**: This is the integration container on your page where your advisor will go.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable                 | Description      |
|:-------------------------|:-----------------|
| Advisor Code             | (`advisorCode`)  |
| Subdomain                | (`subdomain`)    |
| Div ID                   | (`divId`)        |
| Advisor Container Div ID | (`advisorDivId`) |
