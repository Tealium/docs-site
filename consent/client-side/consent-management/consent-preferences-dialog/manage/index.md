---
title: Manage consent preferences
description: This article explains how to manage settings in the Consent Preferences Manager.
url: https://docs.tealium.com/consent/client-side/consent-management/consent-preferences-dialog/manage/
---
The Consent Preferences Manager is configured using the following tabs:

![](https://docs.tealium.com/images/iq-tag-management/consent-manager-consent-preferences-dialog.jpg)

* **Content**  
This tab is used to enter the message displayed to your customers, add multiple language translations, and provide your company's logo URL and privacy policy link.
* **Customization**  
From this tab, customize the design and layout of your prompt by editing the CSS, HTML, and JavaScript used to display the pop-up.
* **Categories**  
In this tab, group your tags into categories based on their purpose or function.
* **Options**  
This tab lets you adjust additional options, such as logging consent changes using DataAccess or marking non-tracking tags that are not governed by consent management, for example, a chat widget.


## Setup

Use the following steps to begin setting up the Consent Preferences Manager:

1. In the left sidebar, go to **Client-Side Tools > Consent Management**. In the **Consent Preferences Dialog** section, click **Get Started** to launch the configuration modal.  
    ![](https://docs.tealium.com/images/iq-tag-management/consent-manager-consent-preferences-dialog-get-started.jpg)  
    If your prompt is already set up, toggle it on or off from this screen.

### Content

Use the **Content** screen to customize the message displayed in the **Preferences** popup, add languages for translated content, and define custom parameters.

The popup is templatized so that the content is separated from the code. The code uses parameters to substitute content using placeholder parameters. Parameters are referenced using the format: `{{parameter_name}}`.

The standard built-in content parameters are:

* **Title** `{{title}}`  
The main heading of the consent prompt.
* **Message** `{{message}}`  
Your message to customers to inform them about your tracking intentions and links to other resources such as a privacy policy or contact form.
* **Opt-in/Opt-out** `{{opt_in}} / {{opt_out}}`  
The two options available: **opt-in - grant consent**, **opt-out - deny consent**.
* **Confirmation Button** `{{confirmation_button}}`  
The label on the submission button.

To edit the content of the standard parameters, modify the text fields and click **Finish**.

Sample HTML code with parameters:

``` html
<div class="example_body">
  <div class="privacy_prompt">
    <div class="privacy_prompt_content">
      <h1>{{title}}</h1>
      <p>{{message}}</p>
    </div>
    <div class="privacy_prompt_footer">
      <div class="button right">{{confirmation_button}}</div>
    </div>
    <div class="close_btn_thick"></div>
  </div>
</div>
```

### Custom parameters

Add custom parameters to further customize the popup. Custom parameters are referenced within the standard parameters or in the CSS/HTML/JavaScript code.


<blockquote>
Best Practice: Avoid putting translatable text directly in the HTML or JavaScript. Instead, construct the code with `{{parameters}}` and define the values using custom parameters.
</blockquote>


To add a custom parameter:

1. Click **+ Add Parameter**.  
The **Custom Parameter** dialog appears.
1. Enter a name for the parameter.
1. Click **Apply**.  
The new custom parameter displays in the list.
1. Enter a value for the new parameter.  
This value is substituted any place that the parameter is referenced.
1. Click **Finish**.

### Languages

The preferences popup is built with automatic language detection. The browser's language setting of the browser is detected (two-character language code, for example `de` for German) and the pop-up presents the corresponding version of the content (if that language has been configured). The preferences pop-up is configured in English (`en`) as the default.

You are able to override the language with a value provided in the data layer (provided it is in the ISO format). Add this code as a preloader extension. This tells the consent which variable to use to switch the language. This affects the language shown for both explicit and preferences manager.

```
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
window.utag_cfg_ovrd.gdprDLRef = "<some data layer var, for example: meta.lang/page_lang>";
```

Use the following steps to add a language:

1. In the **Language** side panel, click **+ Add**.  
The **Add Language** dialog appears.
1. Select the language and click **Apply**.  
The new language displays in the **Language** side panel.
1. Click the new language to configure its content.
1. Enter the translated values in the standard parameter boxes (**Title**, **Message**, and **Confirmation** button).
1. Click **Finish**.

Set a default language by checking the box named **Make Default Language** located in the language title bar. The default language is used to display the preferences pop-up when the customer's detected browser language does not have a matching language configured in the consent prompt manager.

![](https://docs.tealium.com/images/iq-tag-management/consent-prompt-content-make-default.png)

## Customization (CSS, HTML, JavaScript)

On the **Customization** screen, the code appears behind the consent prompt – the CSS, HTML, and JavaScript that runs the prompt. This code is editable to adjust the look and design of the popup to match your website.

## Categories

When a user opts out of a category, tags in that category are suppressed automatically by the consent preferences manager. Customers can access their preference selections by clicking a link that you provide using the consent preferences JavaScript.

On the **Categories** screen, you can adjust the categories that tags are grouped into.

Use the following steps to adjust a tag category:

1. Select a category from the sidebar.  
The list of tags appears in the main panel.
1. Click the drop-down list and select a new category for the tag.
1. Click **Finish**.

To omit a category from displaying in the pop-up list that displays to the customer, toggle the switch to **Off**. To display a category in the customer's pop-up display, toggle the switch to **On**.


## Options

On the **Options** screen, configure the Tealium cookie behavior and tags to omit.

### Cookie preferences

Select whether or not to retain the Tealium cookie. This setting overrides any other preferences that disable tracking. The Tealium cookie is used for visitor, session and timestamp information. In addition, it is used with the [Persist Data Values extension]() to store custom values.

### Default state for categories

This setting applies to two scenarios where a default state for the categories is needed:

* Explicit consent prompt is active but the customer ignores it  
When the consent preferences modal is shown the default state for categories is used.
    * **On**  
    Categories are enabled by default in the preferences modal until the customer makes changes, but tracking follows the consent prompt policy until the customer gives consent.
    * **Off**  
    Categories are disabled by default in the preferences modal until the customer makes changes, but tracking follows the consent prompt policy until the customer gives consent.

* Explicit consent prompt is inactive and the customer has not set preferences  
The default state for categories determines if tags should fire.
    * **On**  
    Tracking occurs until preference categories are disabled
    * **Off**  
    Tracking is suppressed until preference categories are enabled

### Tag to omit

Not all tags deployed by iQ Tag Management are for tracking or data collection. Tags and extensions are also used to serve site functionality, such as popup modals, product feedback, site support, or chat clients. Use the Tags to Omit setting to create a list of tags to be exempted from the consent preferences popup.

## JavaScript code

After enabled and published, the consent preferences pop-up introduces a JavaScript function into the `utag` namespace for integrating additional functionality.

Use the following function to launch the consent preference dialog:

```js
utag.gdpr.showConsentPreferences()
```

Displays the consent preferences popup. Integrate this function into your site to provide visitors a way to change their consent preferences.

Example:

```html
<a href="#" onClick="utag.gdpr.showConsentPreferences()">Consent Preferences</a>
```

To set the language dynamically, pass a language code value to the function. This overrides both the `window.utag_cfg_ovrd.gdprDLRef` configuration and the browser detection logic.

Examples:

```js
utag.gdpr.showConsentPreferences('de-DE'); // German/Germany
utag.gdpr.showConsentPreferences('fr');    // French
```