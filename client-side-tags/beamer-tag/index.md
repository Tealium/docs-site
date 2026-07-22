---
title: Beamer Tag Setup Guide
description: This article describes how to set up the Beamer tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/beamer-tag/
---
## How it works

Beamer is a notification center and changelog plugin that lets you send announcements to users and site visitors for important news, latest products, special offers, and more.

## Tag Tips

* Widget configurations are set with mappings.
* If you do not add an Element ID by default, Beamer will display a notification icon in the bottom-right corner of your page.
* You can call the `callback`, `onclick`, `onopen`, and `onclose` functions by providing by mapping either the name of the function as a string or a reference to the functions. If you provide the name of the function, the function must be defined at the window level.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Beamer tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Product ID**  
The Product ID is the unique identification code that appears in the top bar of your Beamer dashboard.
* **Selector**  
HTML identifier for the DOM element to be used as a trigger to show the panel.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable           | Description    |
|:-------------------|:---------------|
| Beamer Customer ID | (`product_id`) |

### Widget Configurations

| Variable                              | Description                   |
|:--------------------------------------|:------------------------------|
| Selector ID                           | (`selector`)                  |
| Display Mode                          | (`display`)                   |
| Display Position                      | (`display_position`)          |
| Top Offset                            | (`top`)                       |
| Right Offset                          | (`right`)                     |
| Bottom Offset                         | (`bottom`)                    |
| Left Offset                           | (`left`)                      |
| Embed Toggle [`true`/`false`]         | (`embed`)                     |
| Button Toggle [`true`/`false`]        | (`button`)                    |
| Button Position                       | (`button_position`)           |
| Icon                                  | (`icon`)                      |
| Bounce Toggle [`true`/`false`]        | (`bounce`)                    |
| Notification Prompt                   | (`notification_prompt`)       |
| Notification Prompt Delay             | (`notification_prompt_delay`) |
| Language                              | (`language`)                  |
| Filter                                | (`filter`)                    |
| Filter By URL Toggle [`true`/`false`] | (`filter_by_url`)             |
| Mobile Toggle [`true`/`false`]        | (`mobile`)                    |
| Lazy Toggle [`true`/`false`]          | (`lazy`)                      |
| Alert Toggle [`true`/`false`]         | (`alert`)                     |
| Delay                                 | (`delay`)                     |
| Callback Function                     | (`callback`)                  |
| Onclick Function                      | (`onclick`)                   |
| Onopen Function                       | (`onopen`)                    |
| Onclose Function                      | (`onclose`)                   |

### User Data

| Variable        | Description        |
|:----------------|:-------------------|
| User First Name | (`user_firstname`) |
| User Last Name  | (`user_lastname`)  |
| User Email      |                    |
| User ID         | (`user_id`)        |

### Button Position

| Variable                      | Description    |
|:------------------------------|:---------------|
| Bottom Left (`bottom-left`)   | `bottom-left`  |
| Bottom Right (`bottom-right`) | `bottom-right` |
| Top Left (`top-left`)         | `top-left`     |
| Top Right (`top-right`)       | `top-right`    |

### Display

| Variable          | Description |
|:------------------|:------------|
| Left (`left`)     | `left`      |
| Right (`right`)   | `right`     |
| In-app (`in-app`) | `in-app`    |
| Popup (`popup`)   | `popup`     |

### Display Position

| Variable                      | Description    |
|:------------------------------|:---------------|
| Bottom (`bottom`)             | `bottom`       |
| Bottom Left (`bottom-left`)   | `bottom-left`  |
| Bottom Right (`bottom-right`) | `bottom-right` |
| Left (`left`)                 | `left`         |
| Left Bottom (`left-bottom`)   | `left-bottom`  |
| Left Top (`left-top`)         | `left-top`     |
| Right (`right`)               | `right`        |
| Right Bottom (`right-bottom`) | `right-bottom` |
| Right Top (`right-top`)       | `right-top`    |
| Top (`top`)                   | `top`          |
| Top Left (`top-left`)         | `top-left`     |
| Top Right (`top-right`)       | `top-right`    |

### Icon

| Variable                      | Description    |
|:------------------------------|:---------------|
| Bell Full (`bell_full`)       | `bell_full`    |
| Bell Lines (`bell_lines`)     | `bell_lines`   |
| Flame (`flame`)               | `flame`        |
| Flame Alt (`flame_alt`)       | `flame_alt`    |
| Alert Bubble (`alert_bubble`) | `alert_bubble` |
| Alert Circle (`alert_circle`) | `alert_circle` |
| Bullhorn (`bullhorn`)         | `bullhorn`     |
| Thumbtack (`thumbtack`)       | `thumbtack`    |

### Notification Prompt

| Variable            | Description |
|:--------------------|:------------|
| Popup (`popup`)     | `popup`     |
| Sidebar (`sidebar`) | `sidebar`   |
