---
title: Manage opt-out privacy banner & popup
description: This article explains how to manage settings in the opt-out Model privacy banner and popup.
url: https://docs.tealium.com/consent/client-side/consent-management/privacy-banner-and-popup/manage/
---
## Getting started

Use the following steps to begin setting up the opt-out consent manager:

1. In the left sidebar, go to **Client-Side Tools &gt; Consent Management**.  
If the opt-out model banner and popup is already set up, you can toggle it on or off from this screen.
1. In the **Opt-Out Model** section, click **Get Started** to launch the configuration modal.

### User experience

To get started, choose the user experience option that matches your site:

* **Banner and Popup (Recommended)** 
This option adds a cookie banner to be displayed on the page. You set the message and links and the consent manager takes care of the rest, displaying the banner on the page based on your configured settings. The banner contains a link that opens the popup where users set their **Do Not Sell** preferences.
    ![](/images/iq-tag-management/ccpa-banner-popup.png)

* **Popup Only**  
Select this option if you already display a cookie banner on your site. This option makes the popup available using a JavaScript method that you add to a link in your banner.
    ![](/images/iq-tag-management/ccpa-popup.png)

### Content

On the **Content** screen, customize the text displayed in the banner and popup, add languages for translated content, and define custom parameters.

#### Content parameters

The consent manager uses parameters to construct the final text that displays on your site. It uses templates so that custom content can be easily added. Parameters are referenced in the templates in the format `{{parameter_name}}`.

The standard built-in content parameters are:

#### Banner Parameters

* **Title** `{{title}}`  
The main heading of the banner or popup.
* **Message** `{{message}}`  
Your message to customers to inform them about your tracking intentions and links to other resources such as a privacy policy or contact form.
* **Do Not Sell Details Button** `{{details_button}}`  
The label on the submission button.
* **Continue to Site Button** `{{continue_button}}`  
URL of the logo to display.
* **Privacy Policy URL** `{{privacy_policy_url}}`  
The URL to your Do Not Sell page.
* **Privacy Policy Text** `{{privacy_policy_text}}`  
The text of the link to your Do Not Sell page.
* **Cookie Statement URL** `{{cookie_statement_url}}`  
The URL to your cookie policy page.
* **Cookie Statement Text**`{{cookie_statement_text}}`  
The text of the link to your cookie policy page.

#### Popup Parameters

* **Title** `{{title}}`  
The main heading of the popup.
* **Message** `{{message}}`  
Your message to customers to inform them about your tracking intentions.
* **Do Not Sell Description** `{{do_not_sell_description}}`  
Description of what opt-out of selling of personal information means.
* **Confirmation Button** `{{confirmation_button}}`  
The label on the submission button.
* **Company Logo URL** `{{company_logo_url}}`  
The URL of the logo to display.

To edit the content of the standard parameters, modify the text fields and click **Finish**.

Sample HTML code with parameters:

```html
&lt;div class=&#34;privacy_prompt consent_doNotSell&#34;&gt;
  &lt;div class=&#34;privacy_prompt_content&#34;&gt;
    &lt;h1&gt;{{title}}&lt;/h1&gt;
    &lt;img src=&#34;{{company_logo_url}}&#34; class=&#34;logo&#34;&gt;
    &lt;p&gt;{{message}}&lt;/p&gt;
    &lt;input id=&#39;consent_doNotSell_checkbox&#39; type=&#39;checkbox&#39; /&gt;
    {{do_not_sell_description}}
  &lt;/div&gt;
  &lt;div class=&#34;privacy_prompt_footer&#34;&gt;
    &lt;div class=&#34;button right&#34; id=&#34;consent_doNotSell_submit&#34;&gt;{{confirmation_button}}&lt;/div&gt;
  &lt;/div&gt;
  &lt;div class=&#34;close_btn_thick&#34;&gt;&lt;/div&gt;
&lt;/div&gt;
```

#### Custom parameters

Custom parameters can be added to further customize the consent manager. These parameters can be referenced within the standard parameters or in the templates.

Best Practice: Avoid putting translatable text directly in the HTML or JavaScript. Instead, construct the code with `{{parameters}}` and define the values using custom parameters.

To add a custom parameter:

1. Scroll down to the Custom Parameters section and click **&#43; Add Parameter**.  
The **Custom Parameter** dialog appears.
1. Enter a name for the parameter.
1. Click **Apply**.  
The new custom parameter displays in the list.
1. Enter a value for the new parameter.  
This value is substituted where the parameter is referenced.
1. Click **Finish**.

#### Languages

The consent manager is built with automatic language detection. The banner and popup detects the language setting in the browser (two-character language code) and presents the corresponding version if that language has been configured. The prompt is configured in English (`en`) by default.

##### Language overrides

You can optionally override the language with a value provided in the data layer if it is in the ISO format.

To override a language, use a preloader extension to set the `gdprDLRef` override:

```js
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
window.utag_cfg_ovrd.gdprDLRef = utag_data.site_language;
```

##### Adding a language

To add a language:

1. In the **Language** side panel, click **&#43; Add**.  
The **Add Language** dialog appears.
1. Select the language and click **Apply**.  
The new language displays in the side panel.
1. Click the new language to configure the content.
1. Enter the translated values in the standard parameter boxes (**Title**, **Message**, and **Confirmation Button**).
1. Click **Finish**.

##### Setting the default language

The default language is used to display the consent manager when the user&#39;s detected browser language does not have a matching language configured.

To set a default language, select the **Make Default Language** checkbox located in the language title bar.  
    ![](/images/iq-tag-management/consent-prompt-content-make-default.png)

### Customization (CSS, HTML, JavaScript)

The **Customization** screen displays the code behind the banner and popup – the CSS, HTML, and JavaScript. This code can be edited to adjust the look and design of the banner and popup to match your website and customer needs.

The JavaScript code is minified before it is published into the utag.js file. If the minification process fails for any reason (such as a syntax error), the publish process halts and returns a warning message in Tealium iQ. Upon successful publish, when `utag.js` executes on the page, the consent manager JavaScript code is injected into the `&lt;head&gt;` of the page.

### Affected tags

On the **Affected Tags** screen, you select the tags that are governed by your Do Not Sell policy--that is, tags that are blocked if the user opts out of **Do Not Sell**.

To select tags affected by your Do Not Sell policy:

1. Select a category from the sidebar.  
The list of tags appears in the main panel.
1. Tick the checkbox next to each affected tag or tick the checkbox at the top to select all tags displayed.
1. Click **Finish**.

### Enforcement rule

On the **Enforcement Rule** screen, select the load rule to determine when to enforce consent. You can select an existing load rule or create one to satisfy your legal criteria. For more information, see [Load rules]().

### Consent cookie

The prompt relies on a cookie named `CONSENTMGR`. The presence of this cookie and the values it contains determine the behavior of the prompt and reflect the state of the visitor&#39;s choice. The key-value pairs are delimited by the pipe (&#34;|&#34;) character.

The `CONSENTMGR` cookie stores the following key-value pairs related to the Do Not Sell Prompt:

* **dns** – a boolean value that reflects the **Do Not Sell** choice of the visitor:  
    * `true` – the visitor opted-in to **Do Not Sell**
    * `false` – the visitor opted-out of **Do Not Sell**

* **ts** – the timestamp of the last state change

Example value of the `CONSENTMGR` cookie: `ts:1525369619|dns:true`

This cookie has a default expiry of 13 months from the time it is set or changed.


## JavaScript functions

After the Opt-out banner and popup are enabled and published, JavaScript utility functions are available in the `utag` namespace to allow you to integrate additional functionality. The namespace `utag.gdpr` contains all of the consent management utility functions.

### utag.gdpr.showDoNotSellBanner()

Displays the [Opt-out](/glossary/#opt-out-model-consent) Model banner. By default, this function is called when the display rule evaluates to `true`.

Optionally set the language as a parameter when calling the function. This overrides all other language detection logic.

```js
utag.gdpr.showDoNotSellBanner(&#34;EN&#34;);
```

### utag.gdpr.showDoNotSellPrompt()

Displays the Opt-out Model popup. If you are not using the banner, integrate this function into your site banner to provide visitors a way to change their consent setting.

Optionally set the language as a parameter when calling the function. This overrides all other language detection logic.

Example:

```html
&lt;a href=&#34;javascript: utag.gdpr.showDoNotSellPrompt(&#39;EN&#39;)&#34;&gt;Change Consent&lt;/a&gt;
```

### utag.gdpr.dns.getDnsState()

Returns the value of the `dns` consent cookie.

Example:

```js
utag.gdpr.dns.getDnsState()
true
```

### utag.gdpr.dns.setDnsState()

Set the value of the `dns` consent cookie. Recognized values: `true`, `false`, `1`, `0`, `&#34;true&#34;`, `&#34;false&#34;`.

Example:

```js
utag.gdpr.dns.setDnsState(true);

```

### utag.gdpr.getCookieValues()

Returns an object of key-value pairs from the `CONSENTMGR` cookie, accessible in the data layer object as `utag.data[&#39;cp.CONSENTMGR&#39;]`.

Example of consent declined:

```js
utag.gdpr.getCookieValues()
{
  ts: &#34;1525369619&#34;,
  consent: &#34;true&#34;,
  dns: &#34;false&#34;
}
```