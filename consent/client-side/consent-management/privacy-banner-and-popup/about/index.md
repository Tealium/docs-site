---
title: About the Opt-out Privacy Banner and Popup
description: The opt-out consent manager makes it easy to allow users to opt-out of the sale of personal information and set preferences for the sale of personal information.
url: https://docs.tealium.com/consent/client-side/consent-management/privacy-banner-and-popup/about/
---This tool adds the ability to add a privacy banner and popup to your site to inform your visitors about your sale of personal information policy and to provide opt-out options. The [opt-out](https://docs.tealium.com/glossary/#opt-out-model-consent) consent manager can be fully customized to match your site requirements and it supports translated content for your global visitors.

## How it works

The opt-out consent manager notifies your users of your policy for processing personal information and allows them to opt-out of the sale of their personal information or control how their personal information is sold. This solution can be deployed to your site either as a privacy banner and popup or just as a popup to integrate with your existing banner.

The banner informs your users about your policy and provides a link to your **Do Not Sell My Information** page required opt-out models such as CCPA. The popup is triggered from the banner and allows a visitor to opt-out of the sale of personal information or set preferences for the sale of their personal information.

This feature is integrated with your Tealium iQ Tag Management account to make it easy to configure and categorize vendor tags that might be governed by CCPA. The tags that you identify as selling information can be categorized as **Dot Not Sell** and presented to your users in the popup.

## Visitor experience

After the opt-out consent manager is deployed to your website using the Universal Tag (`utag.js`), it operates automatically – no additional coding is needed for it to function. The banner and popup is displayed based on the configured load rule and the presence of a `do_not_sell` cookie. When the cookie is not set, the Opt-out model is triggered automatically on pages that match the load rule. After a preference is set, the cookie is created and subsequent page views do not trigger the banner or popup.


<blockquote>
The Opt-out modal can be displayed programmatically using the JavaScript helper functions.
</blockquote>


## Features

The Opt-out Model offers the following features:

* Display Templates
* Customizable Style and Layout
* Multi-Language Support
* Configurable Display Condition
* Global Settings for Enterprise Rollout

## Steps

The Opt-out Model is set up using the following screens:

* **User Experience**
Select how it is displayed on your site: either as a banner and popup or just a popup. We recommend selecting the banner and popup as the most complete solution. However, if you already display a cookie banner on your site, the popup option is best.
* **Content**
Use this screen to enter the message displayed to your customers on the banner and popup, add multiple language translations, and provide your company's logo URL and privacy policy link.
* **Customization**
Customize the design and layout of your prompt by editing the CSS, HTML, and JavaScript used to display your prompt.
* **Enforcement Rule**
Use your data layer to create a load rule that determines when the banner should be displayed.

This feature does not require additional code on your site. All of the configuration is bundled with your existing installation of the Universal Tag (`utag.js`).


<blockquote>
After you activate and configure the opt-out consent manager, the changes are included in your next publish.
</blockquote>


## Global parameters

The parameters used in the Opt-out Model can be set globally at the account level. This lets you set the titles, messages, and labels once and have each profile inherit those values.

To learn more, see [Managing Global Consent Content Parameters]().
