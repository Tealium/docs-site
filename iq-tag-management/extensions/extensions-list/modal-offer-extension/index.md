---
title: Modal Offer Extension
description: The Modal Offer extension enables the insertion of a modal overlay on any pages to alert the user of promotions, call to actions, or offers.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/modal-offer-extension/
---
## Prerequisites

* [About Extensions]()

## How it works

The Modal Offer extension generates a modal pop-up window on the page. The content and appearance of the pop-up is configured based on the **Modal Publish Mode** selected:

* **Standard**: Content is set by entering text in to three fields: **header**, **body**, and **footer**. The height and width may also be specified.
* **Custom**: Content is coded by editing the CSS and HTML directly.

The popup is launched based on the condition applied to the extension.

![](https://docs.tealium.com/images/iq-tag-management/modal-popup-extension-example.jpg)

The extension runs in the DOM-Ready scope on every page, but only runs when the defined condition evaluates to `true`.

## Using the extension

To begin setting up the Modal Offer extension, be sure to have the content of the modal prepared so that you're ready to enter it into the configuration.

Once the extension is added, the following configuration options are available:

* **Modal Publish Mode**: Set the content of the modal pop-up using the Modal Publish Modes
    * **Standard**: (Default) Uses a simple template where you type in the content of the modal and adjust the height and width. In standard mode the window appearance follows these rules:
        * The modal is always centered.
        * The font style of the modal is inherited from the `<body>` element.
        * The CSS of the modal is a set of Tealium defaults.
        * A dark `div` element is added to block out the rest of the page while the modal is up.
        * The size of the header, body, and footer elements are a percentage of the window height and width.
    * **Custom**: Lets you edit the CSS and HTML of the modal pop-up directly for a custom behavior.  
        ![](https://docs.tealium.com/images/iq-tag-management/modal-extension-custom-mode.png)
        * To configure the modal pop-up in custom mode edit the CSS code for modal window styling definitions, and the HTML code for the modal window template.
        * The CSS and HTML contain placeholders in the form of `##VALUE##` that reference the settings from the standard publish mode. For example, `##MDLWIDTH##` refers to the **Window Width** setting. Replace these placeholders with your own custom values or leave them intact to be populated by the values from the standard settings.  
            
<blockquote>
If you customize the `_tealiumModalClose` button, be sure you keep the `onclick="utag.extn.mdlW.dismiss()` function.
</blockquote>

        * Click **Reset** at the bottom of the extension to return all of the code to its default state.
* **Modal Header** - The text to appear at the top of the window.
* **Modal Body** - The text to appear in the middle of the window.
* **Modal Footer** - The text to appear at the bottom of the window, after the line separator.
* **Window Height** - (Default: 200) The height of the window in pixels (px).
* **Window Width** - (Default: 300) The width of the window in pixels (px).
* Click **Add Condition** to control when this modal pops up.
      * Click the **+** button inside the **Condition** box to add an AND condition.
      * Click the **+** button outside the **Condition** box to add an OR condition.
      * Click the **-** button inside the **Condition** box to remove an AND condition.
      * Click the **-** button outside the **Condition** box removes an OR condition.  
    ![](https://docs.tealium.com/images/iq-tag-management/modal-extension-condition.png)  

<blockquote>
If you do not set a condition the modal pops up on every page.
</blockquote>


## Launch the modal directly

By default, the modal runs at DOM Ready and pops up if the applied condition is `true`. To launch the modal window at a different time, or based on custom  logic, apply the following changes:

* **Block the default modal launch**: Apply a condition that always evaluates to `false` to block the modal from launching.
* **Launch the modal directly**: Find the UID of your modal offer extension on the **Extensions** screen):  
    ![](https://docs.tealium.com/images/iq-tag-management/modal-extension-uid.png)
* Use the following JavaScript code to launch the modal window, replacing `{UID}` with the UID from above:  
    ```js
          // Replace {UID} with the UID of the Modal Offer extension to trigger
          // For example "utag.modalExt_72.js"
          utag.ut.loader({
              src: utag.cfg.path + 'utag.modalExt_{UID}.js?utv=' + utag.cfg.v,
              cb: function() {
                  utag.extn.mdlW.load();
              }
          });
    ```

Use this code anywhere in your iQ configuration to launch the modal offer. By using this code in a [JavaScript Code extension]() or a [jQuery onHandler extension](), you can customize the launch behavior of the modal offer window.

Additional reading: [Triggering the modal offer extension (Use Cases)](https://support.tealiumiq.com/en/support/solutions/articles/36000363394-triggering-the-modal-offer-extension-use-cases-)

## FAQ

#### Can I add multiple modal offer extensions to my profile?

Yes, but only one modal offer is displayed on a web page at a time. If you add multiple instances of the modal offer extension be sure that each one has a different condition.
