---
title: jQuery clickHandler (jQuery v1.6 and below) Extension
description: Use the jQuery clickHandler extension to trigger tracking events when elements are clicked for versions 1.6 and below of jQuery.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/jquery-clickhandler-extension/
---
 The built-in event listener system provides a no-code solution that does not require jQuery to listen for and trigger tracking events. For more information, see . 

## Requirements

This extension requires the following:

* jQuery version 1.6 and earlier

## How it works

Use the jQuery clickHandler extension works by selecting a jQuery selector identifier to be tracked, and then selecting the type of trigger action event. Links clicked by a visitor, page views, or any custom event may be tracked by providing custom JavaScript code.

You can trigger a `utag.view()`, `utag.link()`, or your own custom code. The variables you set in the extension are automatically passed to `utag.view` and `utag.link` as the event data.

## Using the extension

Once the extension is added, the following configuration options are available:

* **jQuery Selector**: The jQuery identifier of the element being tracked.
    To determine the jQuery Selector of an element, use Web Companion&#39;s [On-page Element Selector]() tool.

* **Trigger On**: Select from the drop-down menu the event you want to trigger this extension.
    * **click**: (Default) The button is pressed down and released while the pointer is over the element.
    * **mousedown**: (Recommended) The button is pressed down on the element.
    * **mouseup**: The button is released while the pointer is over the element.
    * **mouseover**: The pointer is held over the element.
    * **change**: A change occurs in the value of the `&lt;input&gt;` element or the `&lt;select&gt;` element.
    * **blur**: The element loses focus when the mouse is clicked away from it or the **Tab** key is pressed.
    * **focus**: The element gains focus when it is selected by a mouse click or the **Tab** key.

* **Tracking Event**: Select from the drop-down menu the event you want to track.
    * **link**: (Default) Triggers a call to `utag.link()`.
    * **view**: Triggers a call to `utag.view()`.
    * **custom**: Triggers custom JavaScript code. Enter your custom code in the built-in editor that appears when this option is selected.

* **Set**: Select the variables you want to set.
* **To**: Select the type of value you want to assign to the variable. In the adjacent text field, enter the new value. If you want to set more variables, click the **&#43;** button at the end of the text box.

* **Condition**: (Optional) A condition can be added to control if the extension should run at all.