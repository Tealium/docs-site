---
title: Tag marketplace policy
description: The tag marketplace policy lets you control which vendor tags are available in your tag marketplace to your users.
url: https://docs.tealium.com/iq-tag-management/tags/tag-marketplace/tag-marketplace-policy/
---
You can use the policy to restrict and safeguard your account so that only a limited selection of pre-approved vendor tags can be added to your account. This is particularly useful for large organizations where multiple users have permission to add tags and publish. By limiting the tags available in the tag marketplace, you can prevent unapproved tags from being added to your site.

## Prerequisites

* The [Manage Account permission level]() is required to access this feature.

## How it works

The tag marketplace contains every vendor integration that Tealium iQ offers. This means that any user with permission to add tags and publish can add one of these tags to your configuration (and to your site).

When the tag marketplace policy is enabled, the policy hides all vendors by default. Select the vendors that you want to approve for your site. Limiting the tags available provides an additional security to your account and prevents unapproved tags from being released to your site.

To access the tag marketplace policy, click **Manage Tag Marketplace Policy** in the admin menu.

![](https://docs.tealium.com/images/iq-tag-management/tags/tag-marketplace-policy/manage-tag-marketplace-policy.png)

### Manage tags

To manage tags in the tag marketplace:

1. Click the **Enable Tag Marketplace Policy** checkbox.
1. From the **Marketplace Tags** column, scroll down to a tag you want to hide and click **Hide**.  
1. From the **Hidden Tags** column, scroll down to a tag you want to show and click **Show**.  
    * To show all tags, click **Show All**.
    * To hide all tags, click **Hide All**.
1. Click **Save** to confirm.

You do not need to save and publish after this step, the changes go into effect immediately.

For example, if you show only tags that begin with "Tealium":

![](https://docs.tealium.com/images/iq-tag-management/tags/tag-marketplace-policy/manage-tag-marketplace-policy-tealium-only.png)

The tag marketplace now only offers the "Tealium" tags and a banner is displayed indicating that the tag marketplace policy is enabled:

![](https://docs.tealium.com/images/iq-tag-management/tags/tag-marketplace-policy/manage-tag-marketplace-policy-tealium-list.png)

### Reset the policy

Clicking **Reset** cancels any show or hide actions prior to saving and restores the two columns to their original state prior to saving.