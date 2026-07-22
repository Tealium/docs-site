---
title: Server-side version history
description: This article explains how to use the version history to display and compare server-side versions and revisions.
url: https://docs.tealium.com/server-side/save-publish/version-history/
---
## How it works

In the sidebar, click **Server-Side Versions** to view the version history.

![](https://docs.tealium.com/images/server-side/versions/server-side-versions-table.png)

The **Latest Publish** box displays the currently published server-side version. The versions table lists all publish and save actions on versions and revisions of the current profile.

## Versions table

The versions table lists the following information about each action:

* **Version**: The name of the version or revision, who performed the action, and the date of the action. A revision is an incremental **Save** of a version.
* **Status**: Whether the version or revision was saved or published.
* **Notes**: The user notes at the time of the action.
* **Details**: View the details about the action in the [**Revision Details**](#revision-details) window.

Additional actions include:

* **Load this version**: Switch to the selected revision.
* **Revert to this Revision**: Duplicates the selected revision and publishes it. The table will refresh with the new information. If the revision was published within the past three months and you have publishing permissions, you can revert to the selected revision.

The table also displays the branching relationship between the revision that you select and the other revisions in the table.

* **Save**: Creates a revision of the profile version. 
* **Save As**: Creates a new version of the profile.

Darker lines represent activity that appears in the selected version, while lighter lines represent progress since the selected version.

### Dashboard filters

To select a new date range for the version table, click **Date Range** and select the start and end dates. You can also filter by version status and the user who last saved a revision.

## Revision details

To view revision details, click **Details**. The **Revision Details** window is displayed:

![](https://docs.tealium.com/images/server-side/versions/server-side-version-details.png)

The top of the **Revision Details** window displays the account, profile, and version name. It also displays the following information:

* **Status**: Whether the version was saved or published.
* **By**: Who performed the action.
* **Date**: The date of the action.
* **Notes**: The user notes at the time of the action.

The table lists the changes made in the save or publish.

* If the action was a publish, the table lists changes since the previous publish.
* If the action was a save, the table lists changes since the previous save.

You can filter the displayed changes by the type of item or by the action performed.

* **Type**: The type of item that was changed.
* **Name**: The name of the item that was changed.
* **Action**: The action performed on the item (Created, Updated, Deleted).
* **User**: The user who performed the change.

<blockquote>
If historical data for a change does not exist, the system displays **System** as the user who made the change.
</blockquote>


### Revert revision

The **Revert to this Revision** option is available for users with [publishing rights to the profile](https://docs.tealium.com/permission-groups/#publishing-permissions) when the selected revision was published less than three months ago. Click **Revert to this Revision** to duplicate the selected revision and publish it. The table will refresh with the new information.

### Compare revisions

Select two revisions from the table, then click **Compare** to see differences between them.

![](https://docs.tealium.com/images/server-side/versions/server-side-versions-table-compare.png)

The **Compare Revisions** window is displayed, and it displays the differences, if any:

* **Type**: The type of item that was changed.
* **Name**: The name of the item that was changed.
* **Action**: The action performed on the item (Added, Not Included, Updated).

![](https://docs.tealium.com/images/server-side/versions/server-side-versions-diff.png)

The **Compare Revisions** window is read-only. You cannot make changes on this window.