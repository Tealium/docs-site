---
title: How to add support for utag.link to a tag template
description: This article describes how to add support for utag.link to a tag template.
url: https://docs.tealium.com/iq-tag-management/frequently-asked-questions/how-to-add-support-for-utaglink-to-a-tag-template/
---## Symptoms

A tag is firing on utag.view (pageview) events, but not responding to utag.link (user interaction/click) events.

## Diagnosis

Each tag template is set up by default to respond to either:

* utag.view
* utag.view AND utag.link

Generally, this is based on the implementation guide the tag vendor provided, so if the vendor only specified code for a page view, then only utag.view support will be present in the template.

## Solution

Sometimes you might want to add utag.link support to a tag that by default only supports utag.view. To begin, follow this document for instructions on how to edit a tag template: [Edit a tag template](https://docs.tealium.com/manage-templates/).

Once you are editing the template, look for the line that starts with the following:

```js
u.ev= {'view': 1};
```

![](https://docs.tealium.com/images/iq-tag-management/viewonly.png)

Edit this line to read:

```js
u.ev = {'view' : 1, 'link': 1};
```

![](https://docs.tealium.com/images/iq-tag-management/view-link.png)

Save the tag template and re-publish the profile. Your tag will now respond to both utag.view and utag.link events.
