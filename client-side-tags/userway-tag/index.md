---
title: UserWay Tag Setup
description: This article describes how to set up the UserWay tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/userway-tag/
---

UserWay creates advanced website accessibility solutions that help ensure ADA compliance without refactoring your website's existing code. With UserWay's RaaS™ and Tealium users can effortlessly increase compliance with WCAG 2.1, ADA, ATAG 2.0, EN 301-549, and Section 508 regulations as required by US & international governmental & regulatory bodies.

## Tag tips

* Use mappings to override or dynamically set the tag configurations.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following setting:

* **Data-account**: Single-text field

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Common

|Variable| Description|
|---| ---|
|Get UserWay API version.| `(getVersion)`|
|Show UserWay accessibility menu icon.| `(iconVisibilityOn)`|
|Hide UserWay accessibility menu icon.| `(iconVisibilityOff)`|
|Toggle UserWay accessibility icon's visibility.| `(iconVisibilityToggle)`|

### Widget methods

|Variable| Description|
|---| ---|
|Open or close widget menu.| `(widgetToggle)`|
|Open widget menu.| `(widgetOpen)`|
|Close widget menu.| `(widgetClose)`|
|Reset all widget features.| `(resetAll)`|

### Keyboard navigation

|Variable| Description|
|---| ---|
|Enable or disable keyboard navigation.| `(keyboardNavToggle)`|
|Enable keyboard navigation.| `(keyboardNavEnable)`|
|Disable keyboard navigation.| `(keyboardNavDisable)`|

### Big Cursor

|Variable| Description|
|---| ---|
|Enable or disable big cursor.| `(bigCursorToggle)`|
|Enable big cursor.| `(bigCursorEnable)`|
|Disable big cursor.| `(bigCursorDisable)`|

### Reading Guide

|Variable| Description|
|---| ---|
|Enable or disable reading guide.| `(readingGuideToggle)`|
|Enable reading guide.| `(readingGuideEnable)`|
|Disable reading guide.| `(readingGuideDisable)`|

### Contrast feature

|Variable| Description|
|---| ---|
|Enable or disable contrast feature.| `(contrastToggle)`|
|Enable contrast feature, integer value from `1` to `4` or empty.| `(contrastEnable)`|
|Disable contrast feature.| `(contrastDisable)`|

### Big text

|Variable| Description|
|---| ---|
|Enable or disable big text feature.| `(bigTextToggle)`|
|Enable big text feature, integer value from `1` to `4` or empty.| `(bigTextEnable)`|
|Disable big text feature| `(bigTextDisable)`|

### Highlight feature

|Variable| Description|
|---| ---|
|Enable or disable highlight feature.| `(highlightToggle)`|
|Enable highlight feature.| `(highlightEnable)`|
|Disable highlight feature.| `(highlightDisable)`|

### Legible fonts

|Variable| Description|
|---| ---|
|Enable or disable legible fonts feature.| `(legibleFontsToggle)`|
|Enable legible fonts feature.| `(legibleFontsEnable)`|
|Disable legible fonts feature.| `(legibleFontsDisable)`|

### Text spacing

|Variable| Description|
|---| ---|
|Enable or disable text spacing feature.| `(textSpacingToggle)`|
|Enable text spacing feature, integer value from `1` to `3` or empty.| `(textSpacingEnable)`|
|Disable text spacing feature.| `(textSpacingDisable)`|

### ReadPage

|Variable| Description|
|---| ---|
|Enable, disable or change reading speed of the **Read Page** feature.| `(readPageToggle)`|
|Enable read page feature.| `(readPageEnable)`|
|Disable read page feature.| `(readPageDisable)`|

### PageStructure

|Variable| Description|
|---| ---|
|Enable page structure view with predefined **headers** tab.| `(pageStructureHeaders)`|
|Enable page structure view with predefined **landmarks** tab.| `(pageStructureLandmarks)`|
|Enable page structure view with predefined **links** tab.| `(pageStructureLinks)`|
|Disable page structure function.| `(pageStructureDisable)`|

### Tooltips

|Variable| Description|
|---| ---|
|Enable or disable tooltips feature.| `(tooltipsToggle)`|
|Enable tooltips feature.| `(tooltipsEnable)`|
|Disable tooltips feature.| `(tooltipsDisable)`|

### Stop Animations

|Variable| Description|
|---| ---|
|Enable or disable stop animations feature.| `(stopAnimationToggle)`|
|Enable stop animations feature.| `(stopAnimationEnable)`|
|Disable stop animations feature.| `(stopAnimationDisable)`|

### Quick Accessibility Menu

|Variable| Description|
|---| ---|
|Opens quick accessibility menu| `(openQuickAccessibilityMenu)`|

### Widget Settings

|Variable| Description|
|---| ---|
|Updates widget language dynamically. No page refresh required.| `(changeWidgetLanguage)`|
