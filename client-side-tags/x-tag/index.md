---
title: X (formerly Twitter) Tag Setup Guide
description: This article describes how to set up the X (formerly Twitter) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/x-tag/
---
X is a real-time information network that connects you to the latest stories, ideas, opinions, and news about what you find interesting.

## Tag Tips
*   Use the Content Modification Extension to add a new div if necessary
*   The contents of the Div ID specified will be overwritten with the X button (button is just a link)

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Button Type**: `Share` (Post), `Follow`, `mention`, or `hashtag`.
* **Language**: Select a language from the drop-down list.
* **Div ID**: Div ID where the X link (button) is to be added.  Overwrites contents of div.  Leave blank if your page already has a link defined.
* **Size**: `Standard` or `Large`.
* **Show Count**: `None`, `Horizontal`, or `Vertical`.
* **Follow**: X account (do not include the `@`)
* **Link Text**: Leave blank to use default text.
* **Message to Post**: Message to send for the Share button
* **Share URL**: Leave blank to use current URL. For example: http://www.tealium.com
* **Add Query String**: (Optional) Added to query string after `/share?`. For example: utm_source=website in http://x.com/share?utm_source=website

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `type` |  | Type of button |
| `divid` | Div ID |
| `lang` | Language |
| `size` | Size |
| `count` | Count box location |
| `follow` | Follow |
| `text` | Text |
| `url` | URL |
| `post` | Post text |
| `dnt` | Opt out tailoring |

### Post

| Variable | Description |
|:---------|:-----|:------------|
| `via` | Screen name |
| `related` | Related accounts |
| `counturl` | Long URL |
| `hashtags` | String or array of hashtags |

### Follow

| Variable | Description |
|:---------|:------------|
| `width` | Width |
| `align` | Align |
| `screen_name` | Screen name |
| `show-screen-name` | Show screen name |
| `show-count` | Show count box |