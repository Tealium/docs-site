---
title: About server-side saving and publishing
description: This article describes the concepts of saving and publishing on the server-side.
url: https://docs.tealium.com/server-side/save-publish/about/
---
## How it works

In Tealium, a version represents a distinct configuration of your server-side profile. Users create new versions to manage changes without affecting the current production environment, ensuring stability and preventing unintended disruptions.

The system doesn’t save changes automatically. Any unsaved changes are discarded if you sign out or close your browser.

Saving a version preserves your configuration for future sessions, enabling you or other team members to continue working from the same point. However, saving a version does not activate changes in production. To activate changes in production, you must publish the version.

## Saving new versions and revisions

When you save changes, you have the option to save your changes to the existing version as a revision or create a new version:

* **Save**: Create a revision of the profile version. 
* **Save As**: Create a new version of the profile.

When starting a new project or creating a dedicated team workspace, we recommend that you **Save As** to branch off to a new version to keep your version history organized. You should **Save** incremental development within that new version to create a series of revisions.


<blockquote>
Using **Save As** instead of **Save** to create multiple new versions during development on a branch will result in confusion when it is time to reconcile your changes to the published version and then publish them.
</blockquote>


If you need to undo changes in a version that you saved as a revision, you can revert to a previous save using the [version history](https://docs.tealium.com/ss-version-history/) screen.

For more information, see [ss-save-and-publish](https://docs.tealium.com/ss-save-and-publish/).

## Published version

The relationship between each version and the published version is the core concept of managing server-side versions. The platform displays your version’s relationship to the published version in the version status. The status lets you and other users know if the published version contains changes that do not exist in their currently loaded versions.

Users need to integrate newly published changes from other users into their own versions to keep them current. This process helps ensure that the latest updates are always included in other active versions and prevents conflicts during concurrent activity.

### Deletion

To permanently delete an item, delete it from the published version. If you delete an item from a version that is not the published version and then save and publish, the platform will restore the deleted item during publishing. This is to prevent accidental removal of dependencies, such as attributes required by audiences.

### Version status

The version status label compares your current version to the latest published version. It lets you know if the published version has changes that do not exist in your current version. Tracking these changes helps ensure that you incorporate published updates from other users.

The [profile switcher](https://docs.tealium.com/ss-profile-switcher/) and the [Save/Publish window](https://docs.tealium.com/ss-save-and-publish/) display your version's status. 

![](https://docs.tealium.com/images/server-side/save-publish/server-side-profile-switcher-status.png)

The version statuses are:

* **You are up to date**: Your current version matches the latest published version, indicating no changes have been made since the last publish. For example, if you recently published a version and no further edits have been made, your version will display this status.
* **You are ahead of the published version**: Your version includes unpublished changes. Once published, other users will be notified so they can integrate your changes into their versions. This helps them keep up with and build upon your published changes.
* **You are behind the published version**: Another user has published updates that do not appear in your version. To stay current, integrate these updates. This status message has precedence over the other status messages so you always know when there are changes in the published version that you need to integrate into your version.

## Concurrent users

The server-side platform supports managing changes from concurrent users who are logged into the server-side platform at the same time. 

The platform displays an in-app notification when other users make changes or publish. When one user publishes their version, other logged-in users must integrate those published changes to avoid conflicts and ensure continuity. The platform also displays your version's relationship to the published version in the version status.

To prevent conflicts, follow a clear publishing strategy and the recommended [best practices](https://docs.tealium.com/ss-save-publish-best-practices/) to avoid overwriting or omitting changes made by other users.

For more information, see [Concurrent users](https://docs.tealium.com/concurrent-user-management/).

## Permissions

Profile and publishing permissions determine the available actions in the **Save/Publish** interface:

* Edit permissions for a feature allow profile changes to be saved.
* Server-side publishing permissions allow profile versions to be published.

## Save and publish exceptions

Some areas of the platform do not require you to save the profile to preserve your changes. In these areas of the platform, when you click **Save** for the item, it is saved to the profile configuration immediately.

The following areas of the platform can be edited and saved directly without needing to save the profile:

* Segments (only segments not used in an audience)
* Moments API
* First-party domains
* Users and permission groups
* DataAccess credentials
* Insights (third-party platform)
* Data Connect (third-party platform)