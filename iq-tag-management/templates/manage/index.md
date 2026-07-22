---
title: Manage templates
description: This document explains how to manage iQ Tag Management templates.
url: https://docs.tealium.com/iq-tag-management/templates/manage/
---
A template contains JavaScript code that integrates the vendor code snippet with Tealium iQ Tag Management or a component of the consent manager. Templates can be modified for advanced customization or updated to get the latest version of a tag.

To get the latest version of a tag, see the [template status checker](https://docs.tealium.com/template-status-checker/).

## Update a template

Updating a template replaces the current template with the latest system version. If a template has been customized, this action will overwrite those changes.

To update a template:

1. Use a method to access the template:
    * In the admin menu, click **Manage Templates** and select the template you want to update from the drop-down list.
    * Go to **Tag Management > Tags** and click **Run Tag Template Status Checker**. For more information, see [Template Status Checker](https://docs.tealium.com/template-status-checker/).
    * Go to **Tag Management > Tags**, click the tag, click **Edit**, and click **Edit Template**.
1. Click **Update**. A confirmation dialog appears.
1. Click **Update** to confirm and replace the template with the latest system version of the template.
1. If you have customized this template, make any necessary customizations to the template.
1. Click **Apply**.

You must save the profile to preserve the changes to the template.

### Update the utag.js template

Tealium releases new versions of the `utag.js` template to improve performance, extend functionality, and resolve bugs. 

Updating the `utag.js` template works the same as updating any other template, but because the `utag.js` template is so important, we recommend that you follow additional steps to ensure a successful update.

* For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* For more information about recent updates to the `utag.js` template, see [Tealium Universal Tag (utag.js) release notes](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2014-01-01).

## Edit a template


<blockquote>
Editing templates is only recommended for advanced users with working knowledge of JavaScript.
</blockquote>


There are two ways to access templates for edits: through the admin menu or the tag configuration screen.

### Admin Menu

Follow these steps to edit a template:

1. In the admin menu, click **Manage Templates**.
1. Select the template you want to edit from the drop-down list and make changes.

This method lets you browse all templates in the profile and quickly access them from a drop-down list.

### **Tag Configuration**

To edit a tag template:

1. Click the tag you want to edit.
1. In the **Tag Configuration** panel, click **Edit**.
1. Scroll down to **Advanced Settings** and expand the section. Click **Edit Templates**.  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-tagconfiguration-edittemplates.png)
1. Make your changes and click **Apply**.
1. Save the profile.

## Revert a template

Reverting a template discards any changes that have been made since the last time the profile was saved. If a template has been updated or edited, this action will undo those changes.

To revert a template:

1. Use a method to access the template.
1. Click **Revert**. A confirmation dialog appears.
1. Click **Revert** to confirm and revert to the last saved version of the template.
1. Click **Apply**.

## Edit template workflow

When you edit or update a template, you must apply your changes and then save the profile. If a tag template is changed, the tag will be marked as **Updated**. If you change a template and don't save the profile, the changes are discarded.

### Template merge behavior

Tag templates do not follow standard merge behavior. When merging one version into another, the tag templates in the active version take priority. Any tag template changes from the merged version will be discarded. If you want to merge in tag templates from another version, switch to that version and then merge the tag templates into your original version.

For more information about merging versions, see [merging-versions](https://docs.tealium.com/merging-versions/).