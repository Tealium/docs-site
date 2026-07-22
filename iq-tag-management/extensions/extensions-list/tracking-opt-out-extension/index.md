---
title: Tracking Opt Out Extension
description: Use this extension to enable Tracking Opt Out. You will be provided an Opt Out link to put on your web site to allow customers to select the Opt Out option.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/tracking-opt-out-extension/
---

<blockquote>
This extension supports legacy implementations. See [consent manager]() for a more comprehensive and up-to-date solution.
</blockquote>


## How it works

Due to the fact that some browsers may not support [DNT (Do Not Track)](http://en.wikipedia.org/wiki/Do_Not_Track) technology, Tealium offers this extension as a secondary measure by providing users with the ability to opt out of tracking by Tealium-managed tags.

When a user chooses to opt out, Tealium sets a first-party cookie that informs our service of this selection. That cookie is read immediately on the next page, and instructs our services not to execute the `utag.js` file or load any third-party libraries. If the user chooses to opt in later, the cookie is reset with their new selection, and the `utag.js` file and third-party libraries load as normal.

## Using the extension

Before you begin, familiarize yourself with [how extensions work]().

The Tracking Opt Out extension's scope is automatically set to Pre Loader to provide the user with the option to opt out of tracking before the other tags load.

Once the extension is added, the following configuration options are available:

* **Opt In**: `<a href='javascript:utag_trackingOptIn()'>Tracking Opt In</a>`
* **Opt Out**: `<a href='javascript:utag_trackingOptOut()'>Tracking Opt Out</a>`

​Add these links to the site in which you offer visitors the ability to opt in/out of tracking.


<blockquote>
This extension only needs to be added once and must be activated for these links to work.​
</blockquote>

