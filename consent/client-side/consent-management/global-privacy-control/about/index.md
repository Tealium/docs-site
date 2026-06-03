---
title: About Global Privacy Control (GPC)
description: This article describes the Global Privacy Control (GPC), a proposed browser standard that allows users to indicate that they generally do not consent to the sale or sharing of their personal data.
url: https://docs.tealium.com/consent/client-side/consent-management/global-privacy-control/about/
---
[Global Privacy Control](https://globalprivacycontrol.org/) (GPC) is a proposed browser standard that allows users to indicate across domains that they generally do not consent to the sale or sharing of their personal data.

In many ways, GPC is similar to [Do Not Track](https://en.wikipedia.org/wiki/Do_Not_Track). Both are browser-level Boolean settings designed to save users from having to manually opt out of each website they visit. The [key difference](https://iapp.org/news/a/is-gpc-the-new-do-not-track/) between Do Not Track and GPC signals is that the California Attorney General has clearly indicated that GPC must be respected by businesses covered by CCPA or CPRA.

## Why does it exist?

GPC intends to provide a durable, cross-site signal to indicate that a consumer generally objects to the sale and sharing of their personal data. The proposed standard hopes to save users from needing to repeatedly object to the sale of their data on each site they visit. From the [specification](https://privacycg.github.io/gpc-spec/#introduction): 

&gt; Several legal frameworks exist — and more are on the way — within which people have the right to request that their privacy be protected, including requests that their data not be sold or shared beyond the business with which they intend to interact. Requiring that people manually express their rights for each and every site they visit is, however, impractical.

The California Attorney General has been [explicit](https://oag.ca.gov/sites/all/files/agweb/pdfs/privacy/ccpa-fsor.pdf) in his support for a signal like GPC - it&#39;s clear that companies are expected to respect the signal as an opt-out:

&gt; Given the ease and frequency by which personal information is collected and sold when a consumer visits a website, consumers should have a similarly easy ability to request to opt-out globally. This regulation offers consumers a global choice to opt-out of the sale of personal information, as opposed to going website by website to make individual requests with each business each time they use a new browser or a new device.

For more information, see the [GPC specification proposal](https://privacycg.github.io/gpc-spec/#introduction).


## How should the GPC signal be interpreted?

The California Attorney General and the [Sephora settlement](https://oag.ca.gov/news/press-releases/attorney-general-bonta-announces-settlement-sephora-part-ongoing-enforcement) have made it clear that companies subject to California regulations are expected to enforce the GPC signal as an opt-out for purposes of CCPA/CPRA.

The appropriate interpretation of the GPC signal for GDPR / ePrivacy isn&#39;t as clear, but we expect more clarity with the upcoming ePrivacy regulation, which is now undergoing final negotiations. It is not certain whether and in what form it will be legally binding, but there is already [a standard](https://noyb.eu/en/new-browser-signal-could-make-cookie-banners-obsolete) proposed for that purpose.

Ultimately, it&#39;s up to your business to decide which interpretation of the applicable regulations is best for you.

## How can I respect the GPC signal with Tealium?

The needs and requirements of our customers vary widely, so we intend to provide a flexible foundation for our customers to build upon, across our platform.

For more information on Tealium&#39;s support for GPC, see [Client-side Global Privacy Control]() and [Server-side Global Privacy Control]().

## How is the signal exposed?

To enable GPC, [supporting browsers](https://globalprivacycontrol.org/orgs) expose a global boolean (`true` for an opt-out) in the DOM:

```javascript
navigator.globalPrivacyControl // will be true for opt-outs
```
 
and sets a header on all outgoing requests (`1` for an opt-out):

```
Sec-GPC: 1
``` 

## How can I indicate GPC support?

Websites can explicitly signal that they support GPC by using a [mechanism](https://privacycg.github.io/gpc-spec/#gpc-support-resource) provided by the proposed standard.

&gt; A website MAY produce a resource at a `.well-known` URL to indicate that it supports GPC. The purpose of a GPC support resource is for a site to communicate its support for Global Privacy Control. By default, an origin&#39;s support is unknown.

This file may be hosted by the site owner, Tealium does not provide any related services or hosting.