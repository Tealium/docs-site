---
title: About the Explicit Consent Prompt Manager
description: The Explicit Consent Prompt Manager makes it easy to deploy a prompt to your website to allow users to opt-in or opt-out of tracking.
url: https://docs.tealium.com/consent/client-side/consent-management/explicit-consent-prompt/about/
---
This tool offers full access to customize the code behind the prompt as well as the option to use translated content for global customers. This feature replaces the functionality previously offered by the Privacy Manager extension and is part of our consent management features designed to help you stay compliant with [Opt-in model regulations](https://docs.tealium.com/glossary/#opt-in-model-consent) like GDPR.

## How it works

The Explicit Consent Prompt Manager works together with the [Consent Preferences Manager]() to present tracking options to your customers. A consent prompt notifies your customers about you wanting to track their activity on your digital property and to acquire their consent. Explicit consent is a proactive approach in encouraging your customers to opt-in or opt-out by forcing a pop-up prompt until a selection is made.

* If a customer opts-out, the website suppresses all tracking activity and cookie storage that is not directly relevant to the digital experience.
* If the customer opts-in, the website can track the user behavior (commonly using third-party services).

Explicit Consent Prompt example:

![](https://docs.tealium.com/images/iq-tag-management/example-consent-prompt.png)

The Explicit Consent Prompt Manager in iQ Tag Management makes it easy to create and deploy a consent prompt to your website using your existing installation. This feature can be used with the [Consent Preferences Manager]() to offer your customers more granular control over how they are tracked.

The Explicit Consent Prompt satisfies a requirement of the General Data Protection Regulation that a data subject (EU residents) must give explicit consent before activity can be tracked.

## Visitor experience

After you deploy to your website using the standard iQ JavaScript container ( `utag.js` ), the consent prompt operates automatically – no additional coding is needed for the consent prompt to function. The prompt behavior is based on the configured load rule and the presence of a consent cookie. The prompt is triggered automatically on pages matching the load rule if that cookie is not detected. After a response to the prompt is submitted (for example, the visitor selects **Opt-in** or **Opt-out**), the consent cookie is created and subsequent page views do not trigger the consent prompt.


<blockquote>
The consent prompt can be displayed programmatically [using the JavaScript helper functions](https://docs.tealium.com/iq-tag-management/consent-management/explicit-consent-prompt/manage/#javascript-helper-functions).
</blockquote>


## Features

The Explicit Consent Prompt in Tealium iQ offers the following features:

* Display Templates
* Customizable Style and Layout
* Multi-Language Support
* Configurable Display Condition
* Global Settings for Enterprise Rollout
* Consent Logging (requires DataAccess or EventStream)

This feature does not require additional code on your site. All of the configuration is bundled with your existing installation of our JavaScript library (`utag.js`).


<blockquote>
After you configure and activate the consent prompt, the changes are released in your next publish.
</blockquote>


## Steps

The Explicit Consent Prompt is set up using the following screens:

* **Content** 
Use this screen to enter the message displayed to your customers, add multiple language translations, and provide your company's logo URL and privacy policy link.
* **Customization** 
Customize the design and layout of your prompt by editing the CSS, HTML, and JavaScript used to display your prompt.
* **Enforcement Rule**
Use your data layer to create a load rule that determines when to display the consent prompt.
* **Options**
Adjust additional options, such as logging consent changes using DataAccess or marking non-tracking tags that are not governed by consent management, such as chat widget.
* **Default Consent Categories (JavaScript Code Extension when Consent Preferences is disabled)**  
If you do not use the **Consent Preferences Dialog** and have a server-side product enabled (EventStream, AudienceStream, or DataAccess), then this JavaScript Code extension is required to set the default consent categories.  

<blockquote>
If you skip this step, incoming events might be ignored.
</blockquote>


## Global settings

The **Explicit Consent Prompt** can be configured for multiple profiles simultaneously when using the global parameters setting. This lets you configure your consent prompt at the account level and have each profile inherit that configuration.

To learn more, see [Managing Global Consent Content]().