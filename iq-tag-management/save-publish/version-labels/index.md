---
title: Version labels
description: Version labels help you organize your publish version history.
url: https://docs.tealium.com/iq-tag-management/save-publish/version-labels/
---
Use labels to identify versions that are safe to roll back to or to mark versions that should never be published. When viewing the **Versions** tab, you can select any of the version labels to view only those versions that are labeled.

Version labels are organized at the account level. This means that any changes to your version labels in one profile will propagate to all of the other profiles in your account.

## Requirements

* Manage labels: [Manage Account permission]()
* All users can apply a label to a version.

## Managing version labels

There are three version labels initially available for any profile: **Waiting to Verify**, **Verified Success**, and **Verified Failure**. You may delete these at your convenience. Keep in mind that deleting a label automatically removes it from any versions you&#39;ve applied it to. To manage your version labels, click the **Manage** link in the **Version Labels** area.

![](/images/iq-tag-management/no-title-1652ic6bbb75313e91a90.png)

### Adding labels

Adding a new label is a simple process:

1. From the **Manage Version Labels** modal, click on the swatch drop-down to select the color you want to assign to your new label. **Note:** You can reuse a color for multiple labels.
1. Enter the name of your new label. **Note:** The label&#39;s name cannot exceed 40 characters or contain special characters, nor can you use the same name twice.
1. Click the **Save** button.

![](/images/iq-tag-management/no-title-1653i7c507566c876a5c8.png)

Once you&#39;ve created a label, all other users in the account can use it. Note that they will not necessarily be able to edit, add, or delete these labels though.

### Removing labels

To remove labels:

1. From the **Manage Versions Labels** modal, click the **X** next to the label you want to remove. The label&#39;s name will appear in red.

    ![](/images/iq-tag-management/no-title-1654i309f77c9d2aff410.png)

1. Click **Save**.

The label that you deleted will disappear, and it will be removed from any versions you applied it to.

## Applying labels

Any user can apply a version label to a version.

To apply a label:

1. In Tealium iQ, navigate to the **Versions** tab.
1. Click the version you want to apply the label to. The version detail view will expand.
1. Click **Add Label**.
1. Select the labels you want to apply or, if you want to create a new label, enter the name of your new label and click **Enter**.
1. When you are finished applying labels, click outside of the **Version** Labels window to close it.

Managing and applying labels does not require you to save the profile.
