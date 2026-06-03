---
title: Manage explicit consent prompt
description: This article explains how to manage settings in the Explicit Consent Prompt.
url: https://docs.tealium.com/consent/client-side/consent-management/explicit-consent-prompt/manage/
---
## Getting started

Use the following steps to begin setting up the explicit consent prompt:

1. In the left sidebar, go to **Client-Side Tools &gt; Consent Management**.
1. In the **Explicit Consent Prompt** section, click **Get Started** to launch the configuration.  
If the **Explicit Consent Prompt** is already set up, you can toggle it on or off from this screen.

### Content

On the **Content** screen, customize the message displayed in the consent prompt, add languages for translated content, define custom parameters, and view a preview of the prompt you created.

![](/images/guides/iq/consent-manager-explicit-consent-prompt.png)

#### Content parameters

The **Explicit Consent Prompt** uses parameters to construct the final prompt that displays on your site. The prompt is templatized so that the values of the parameters can be easily substituted. Parameters are referenced using the format: `{{parameter_name}}`.

The standard built-in content parameters are:

* **Title** `{{title}}`  
The main heading of the consent prompt.
* **Message** `{{message}}`  
Your message to customers to inform them about your tracking intentions and links to other resources such as a privacy policy or contact form.
* **Opt-in/Opt-out** `{{opt_in}} / {{opt_out}}`  
The two options available:
    * `opt-in - grant consent`
    * `opt-out - deny consent`

* **Confirmation Button** `{{confirmation_button}}`  
The label on the submission button.

To edit the content of the standard parameters, modify the text fields and click **Finish**.

Sample HTML code with parameters:

``` html
&lt;div class=&#34;example_body&#34;&gt;
  &lt;div class=&#34;privacy_prompt&#34;&gt;
    &lt;div class=&#34;privacy_prompt_content&#34;&gt;
      &lt;h1&gt;{{title}}&lt;/h1&gt;
      &lt;p&gt;{{message}}&lt;/p&gt;
    &lt;/div&gt;
    &lt;div class=&#34;privacy_prompt_footer&#34;&gt;
      &lt;div class=&#34;button right&#34;&gt;{{confirmation_button}}&lt;/div&gt;
    &lt;/div&gt;
    &lt;div class=&#34;close_btn_thick&#34;&gt;&lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;
```

#### Custom parameters

Custom parameters can be added to further customize the prompt. These parameters can be referenced within the standard parameters or in the CSS/HTML/JavaScript code.

Best Practice: Avoid putting translatable text directly in the HTML or JavaScript. Instead, construct the code with `{{parameters}}` and define the values using custom parameters.

Use the following steps to add a custom parameter:

1. Scroll down to the **Custom Parameters** section and click **&#43; Add Parameter**.  
The Custom Parameter dialog appears.
1. Enter a name for the parameter.
1. Click **Apply**.  
The new custom parameter displays in the list.
1. Enter a value for the new parameter.  
This value are substituted where the parameter is referenced.
1. Click **Finish**.

### Languages

The consent prompt can be displayed in multiple languages. For each language you add you must provide the translations for each content parameter and custom parameter.

The consent prompt detects the language setting in the visitor&#39;s browser (two-character language code) and displays the corresponding version. If the detected language is not configured, the default language is displayed.

#### Add a language

To add a language:

1. In the **Language** side panel, click **&#43; Add**.  
    ![](/images/iq-tag-management/consent-manager-consent-preferences-dialog-add-language.jpg)

1. Select the language and click **Apply**.  
The new language displays in the side panel.

Click the new language to enter translated text for all content parameters and custom parameters.

#### Set the default language

The default language is used to display the consent prompt when the user&#39;s detected browser language is not configured.

To set a default language:

1. Check the **Make Default Language** box located in the language title bar.  
    ![](/images/iq-tag-management/consent-prompt-content-make-default.png)
1. Click **Preview** to view your language configuration.

#### Override the language

You can override the consent manager language setting with a data layer variable by using the [Universal Tag settings override object](/platforms/javascript/settings/). Specify the name of the data layer variable which stores the language to be used in the consent manager.

For example, if your data layer contains a variable named `site_language`:

```
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {}
window.utag_cfg_ovrd.gdprDLRef = &#34;site_language&#34;;
```

Do not set the two-character language code directly. This override setting expects a variable name, not a language code value.

On the **Customization** screen, the code is behind the consent prompt – the CSS, HTML, and the JavaScript that runs the prompt. This code can be edited to adjust the look and design of the prompt to match your website.

The JavaScript code is minified before it is published into the utag.js file. If the minification process fails for any reason (such as a syntax error), the publish process halt and return a warning message in iQ. Upon successful publish, when utag.js executes on the page, the consent prompt JavaScript code is injected into the `&lt;head&gt;` of the page.

### Enforcement rule

On the **Enforcement Rule** screen, select the load rule that determines when to show the consent prompt to customers. If the rule evaluates to false, the consent manager does not enforce any consent, and tags fire normally. To comply with GDPR, you must present the consent prompt to data subjects residing in the European Union (EU). You can select an existing load rule or create one to satisfy that criteria. If you&#39;re unsure how to create a suitable load rule, see [About load rules]().

## Options

From the **Options** screen, you can enable event logging and tags to omit.

### Event logging

The event logging option requires DataAccess (EventStore or EventDB) or EventStream and logs every consent action taken by your visitors. These consent actions can then be logged to EventStore, EventDB, or EventStream. Each time a visitor grants or revokes consent using the consent prompt, the action is logged for auditing purposes.

This option is offered to help you comply with Recital 42 of the GDPR, which requires that proof of consent be available for auditing purposes. In addition, the event logging option provides you with the data needed to enable you to analyze the volumes and percentages of visitors that opt in or opt out of consent and the types of cookies each visitor is opting in or out of as a result of your efforts.

Learn more about [Event logging for consent management]().

### Tags to omit

Not all tags deployed by iQ Tag Management are for tracking or data collection. Tags and extensions can also be used to serve site functionality, such as pop-up modals, product feedback, site support, or chat clients. Use the **Tags to Omit** setting to create a list of tags to be exempted from the tracking restrictions.

### Consent cookie

The consent prompt uses a cookie named `CONSENTMGR`. The presence of this cookie and the values it contains determine the behavior of the prompt and reflect the state of the visitor&#39;s consent. The key-value pairs are delimited by the pipe (&#34;`|`&#34;) character.

The `CONSENTMGR` cookie stores the following key-value pairs related to the consent and preferences prompts:

* **c1..N** – integer value `1` or  indicating the tag category consent status where `1..N `is the category number. `1`=allowed, `0`=not allowed (for use with the Consent Preferences prompt)
* **consent** – a Boolean value that reflects the consent state of the visitor:  
    * **true** – consent was given using the opt-in option
    * **false** – consent was declined using the opt-out option

* **ts** – the timestamp of the last consent state change

Example value of the `CONSENTMGR` cookie:
```
ts:1525369619|consent:true|c1:0|c2:0|c3:0|c4:0|c5:0|c6:0|c7:1|c8:0|c9:1|c10:0|c11:0|c12:1|c13:0|c14:0|c15:0
```

If you have multiple profiles that share a domain name, we strongly recommend that you give a unique name to the consent cookie for each profile. Using unique cookie names prevents conflicts and security issues between the cookies.

For more information, see [Consent management cookie name](/platforms/javascript/settings/#cmcookiens).

### Default consent categories (JavaScript Code Extension)

This step is only needed if the Consent Preferences Dialog is disabled and if you have a server-side product (EventStream, AudienceStream, DataAccess) enabled. This step uses the JavaScript Code extension to add the default consent categories to the data layer to ensure that server-side events continue to be processed.

To add the default consent categories:

1. Add a [JavaScript Code extension]().
1. Add this line of code to set the default list of consent categories:
    ```
    b[&#34;consent_categories&#34;] = [&#34;analytics&#34;, &#34;affiliates&#34;, &#34;display_ads&#34;, &#34;search&#34;, &#34;email&#34;, &#34;personalization&#34;, &#34;social&#34;, &#34;big_data&#34;, &#34;misc&#34;, &#34;cookiematch&#34;, &#34;cdp&#34;, &#34;mobile&#34;, &#34;engagement&#34;, &#34;monitoring&#34;, &#34;crm&#34;];
    ```
1. Scope the extension to the Tealium Collect tag.


## JavaScript helper functions

After enabled and published, the consent prompt introduces JavaScript utility functions into the utag namespace to allow you to integrate additional functionality. The namespace `utag.gdpr` contains all of the consent management utility functions.

### utag.gdpr.showExplicitConsent()

Displays the explicit consent prompt. Integrate this function into your site to provide visitors a way to change their consent setting. To set the language dynamically, you can send the language as a parameter when calling the function. This overrides both the `window.utag_cfg_ovrd.gdprDLRef` defined above and the browser detection logic.

Example:

```html
&lt;a href=&#34;javascript:utag.gdpr.showExplicitConsent(&#39;EN&#39;)&#34;&gt;Change Consent&lt;/a&gt;
```

### utag.gdpr.getCookieValues()

Returns an object of key-value pairs from the `CONSENTMGR` cookie (mentioned above). The values are retrieved from `utag.data[&#39;cp.CONSENTMGR&#39;]`.

Example of consent declined:

```js
utag.gdpr.getCookieValues()
{
  ts: &#34;1525369619&#34;,
  consent: &#34;false&#34;
}
```

Example of partial consent has been given for categories `7`, `9`, and `12`:

```js
utag.gdpr.getCookieValues()
{
  ts: &#34;1525369619&#34;,
  consent: &#34;true&#34;,
  c1: 0,
  c2: 0,
  c3: 0,
  c4: 0,
  c5: 0,
  c6: 0,
  c7: 1,
  c8: 0,
  c9: 1,
  c10: 0,
  c11: 0,
  c12: 1,
  c13: 0,
  c14: 0,
  c15: 0
}
```
