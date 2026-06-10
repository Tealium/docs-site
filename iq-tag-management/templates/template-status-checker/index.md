---
title: Template Status Checker
description: This article describes how to use the Template Status Checker to scan your templates and display version information and modification status.
url: https://docs.tealium.com/iq-tag-management/templates/template-status-checker/
---
## Requirements

**Manage Templates** permission.

## How it works

The **Template Status Checker** tool compares each of your templates to the latest system version available. After running the tool, a status for each template is displayed based on its version and modification status. The status report lets you quickly determine if updates are needed.

### Summary window

After completing the scan, a detailed report displays the following columns:

* **Status**  
The status or characteristics of the template in color-coded icons. The number that displays next to an icon is the number of templates detected with that status.
* **Tag Name**  
The name of the tag.
* **Latest Version**  
The latest version available to the tag template marked by the version number or the date.
* **Version**  
The version detected by the tool, displays as **Latest** or **Old**.
* **UID**  
The unique identifier (UID) for the template.

### Status symbol definitions

The following statuses are reported. Note that a template may have more than one status.

| Symbol | Status| Description |
|:------:|:------|:------------|
| ![](/images/iq-tag-management/tag-status-new-version-available.png) | New Version Available | Indicates that a newer version of the template is available.|
| ![](/images/iq-tag-management/tag-status-latest-version.png)        | Latest Versions       | Indicates that this template matches the latest system version available.|
| ![](/images/iq-tag-management/tag-status-not-customized.png)        | Not Customized        | Indicates that the template has not been modified from its original state when it was added.|
| ![](/images/iq-tag-management/tag-status-customized.png)            | Customized            | Indicates that the template has been edited from its original state by a user.|
| ![](/images/iq-tag-management/tag-status-deprecated.png)            | Deprecated            | Indicates that this version of the template is no longer supported or offered. It is likely that a new version of the template has been released to replace this one. |
| ![](/images/iq-tag-management/tag-status-version-mismatch.png)      | Version Mismatch      | Indicates that the template does not match the currently selected version of the tag in the tag configuration settings.|
| ![](/images/iq-tag-management/tag-status-unknown.png)               | Unknown               | Indicates that the system is unable to determine the current state of the template.|
| ![](/images/iq-tag-management/template-status-unsaved.png)          | Unsaved Changes       | Indicates that this template has pending changes that have not been saved in the profile.|

## Using the Template Status Checker

There are two ways to access the template status checker:

* **From the Tags screen**  
Click the **Run Template Status Checker** button that appears at the top of the list view.
* **From the Admin menu**  
From the **Admin** menu, click **Template Status Checker**.

### From the Tags screen

Use the following steps to check the status of your templates from the **Tags** screen:

1. Go to **Tag Management &gt; Tags**.
1. In the header toolbar, click **Run Template Status Checker**.
1. The **Status** column displays in the list of tags with a colored indicator for the status of each template.  
    ![](/images/iq-tag-management/template-status-checker-column.png)

### From the Admin menu

Use the following steps to check the status of your templates from the **Admin** menu:

1. In the admin menu, click **Template Status Checker**.
1. Select the type of scan to run.  
    * **Full Scan**  
    Scans all active and inactive templates in your profile.
    * **Active templates**  
    Scans only active templates in your profile.
    * **Specific template**  
    Scans only the template you specify. Enter the name of the tag or consent manager component in the text field.

1. Click **Scan**.  
The **Template Status Checker** window displays the results.  
    ![](/images/iq-tag-management/template-status-checker-report.png)
1. Click a table row to view that template.

### Filter by status

After the template status checker runs, use the status results to filter the tag list by template status.

Use the following steps to filter the tag list by template status:

1. Select the **Template Status** drop-down list and click a status.  
    ![](/images/iq-tag-management/template-status-filter.png)  
    The list of tags adjusts accordingly.
1. (Optional) Click **Re-Run** to run the tool again.