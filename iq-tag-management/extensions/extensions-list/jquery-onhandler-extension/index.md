---
title: jQuery onHandler (jQuery 1.7 and up) Extension
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/jquery-onhandler-extension/
---

<blockquote>
The built-in event listener system provides a no-code solution that does not require jQuery to listen for and trigger tracking events. For more information, see [about-events](https://docs.tealium.com/about-events/).
</blockquote>


## Requirements

This extension requires the following:

* jQuery version 1.7 and later

## How it works

The jQuery onHandler extension works by selecting a jQuery selector identifier to be tracked, and then selecting the type of trigger action event. Standard on-page events, such as click, mouse down, focus, and others may be tracked by providing custom JavaScript code.

## Using the extension

Before you begin, familiarize yourself with [how extensions work]().

Once the extension is added, it has several configuration options. If you are familiar with the [jQuery on() method](http://api.jquery.com/on/), then these settings will be familiar.

* **jQuery Selector**: A selector string to filter the elements from the primary selected elements that trigger the event.
* **Primary Selector**: (Default: `body`) A parent selector string for the elements to target.
* **Trigger On**: The event type that will trigger the action.  
    * **show**: When a hidden element appears on the page.
    * **hide**: When a displayed element is hidden from the page.
    * **click**: When the mouse pointer is over the element and the mouse button is pressed and released.
    * **mousedown**: When the mouse pointer is over the element, and the mouse button is pressed.
    * **mouseup**: When the mouse pointer is over the element, and the mouse button is released.
    * **mouseover**: When the mouse pointer enters the element.
    * **change**: When the value changes within `<input>`, `<select>`, and `<textarea>` elements
    * **blur**: When an element loses focus, such as when the mouse is clicked away from it or the tab key is pressed.
    * **focus**: When an element gains focus, such as when it is selected by a mouse click or the tab key.

* **Tracking Event**: The action to take when the event is triggered.
    * **link**: Calls `utag.link()`
    * **view**: Calls `utag.view()`
    * **custom**: Runs the code that you provide

* **Set**: Select the variables you want to set.
* **To**: Select the type of value you want to assign to the variable. In the adjacent text field, enter the new value. If you want to set more variables, click the **+** button at the end of the text box.
* **Condition**: (Optional) A condition can be added to control if the extension should run at all.

### Generated code

The generated JavaScript code for this extension will vary depending on the settings for **Tracking Event** and **Set To**. The settings will generate code in the following form:

```js
$( "**Primary Selector**" ).on( "**Trigger On**", "**jQuery Selector**", function() {
    // ------------------
    // Tracking Event: link (or view)
    // utag.link({
    //  Variables from Set To
    //      "variable1" : "value1",
    //      "variable2" : "value2"
    //  });

    // ------------------
    // Tracking Event: custom
    // Your code here

});
```

You can see that when the **Tracking Event** is set to `link` or `view`, the code that executes is simply a call to the corresponding utag tracking call, `utag.link() `or `utag.view()`. If you use the **Set To** options to set data layer variables, then those will appear as an inline object passed to the tracking method.

If you set **Tracking Event** to **custom**, then the code that you provide in the text box is that code that will run.

### Determining the selector

There are many ways to determine the selector of a page element. Read more about this in the article [How to Determine the CSS Selector of an Element](https://support.tealiumiq.com/en/support/solutions/articles/36000363465-how-to-determine-the-css-selector-of-an-element).

### Order of operations

It's important to note that this extension always runs at DOM Ready. This means it runs once on page load and out of band from the All Tags extensions. Learn more about [Order of Operations]().

### Working with the data layer

It's common to need to reference variables in your data layer in this extension, either to create conditions or to set values in the tracking call. It's important to know how this works so that you can ensure that the extension is doing what you expect.

### Conditions

If you add a condition to this extension, the values will be referenced in the object `utag.data` . This is the data object that gets created as the Universal Tag runs in the page.

### Set variables

If you trigger a view or link event, then you will likely also be setting data layer variables as part of the tracking event. If you don't set any variables, then an empty tracking call is made:

```js
utag.link(); // or utag.view()
```

If you do set variables, then they will be set and passed in an anonymous data object to the tracking call, like this:

```js
utag.link({
    "variable1" : "value1",
    "variable2" : "value2"
});
```

The values set can use the standard options:

* **Text**: The values are passed just as you type them.
* **Variable**: The values will be fetched from the `utag.data`.
* **JS Code**: Lets you reference the `$(this)` object to access dynamic values based on the event item.

### Example

Let's say we have a feedback form on the page and we want to track when it gets submitted by tracking clicks on the submit button. In the tracking call we want to collect the comment that was typed and the visitor's logged in username. The tracking call we want to call might look like this:

```js
utag.link({
    "tealium_event": 'feedback_submitted',
    "feedback_message": '',
    "username": ''
})
```

To configure this event in the jQuery extension, we need the selector for the submit button and three data layer variables. The name of the event will be hard-coded and the username is already populated in the page UDO, but the feedback message has to be retrieved dynamically from the form. In this example our feedback form has an ID of `feedbackForm`.

Let's see how this will look in the extension:

![](https://docs.tealium.com/images/iq-tag-management/jquery-extension-example.png)

In this example we had to determine the selector for the button: `input.submit-action`.

Since there might be more than one submit button on a page, we also set the **Primary Selector** to narrow the selector down to only the feedback form.

We fetch the feedback text dynamically using jQuery to select the value of the `textarea` input in the form. Also, since the `username` variable is already set in the UDO, we can reuse that value to include it in the tracking call. This extension will result in the following code on your page:

```js
jQuery('#feedbackForm').on('mousedown', 'input.submit-action', function(e) {
    utag.link({
        "tealium_event"     : 'feedback_submitted',
        "feedback_message"  : $('#feedbackForm textarea').val(),
        "username"          : utag.data['username']
    })
});
```
