---
title: Neustar PageAdvisor Tag Setup Guide
description: This article describes how to configure the Neustar PageAdvisor tag.
url: https://docs.tealium.com/client-side-tags/neustar-pageadvisor-tag/
---
## Tag tips

* Use mapping to override the standard configuration values dynamically.
* Use custom variables to assign dynamic values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Service ID (sid)**: A 10-digit numeric value that allows Neustar to identify the client (for example, `9876543210`).
* **Page Reference (page)**: A reference used by the client to indicate which page a user is on (for example, `http://www.neustar.biz`).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
|   `service_id` | Service ID |
|   `page_ref` | Page reference |
|   `cv1` | Custom variable |
