---
title: Concurrency best practices
description: This article explains best practices for team collaboration.
url: https://docs.tealium.com/server-side/save-publish/best-practices/
---
## General guidelines

We recommend that you follow these best practices for team collaboration:

* **Only create a separate version for new long-term projects**:  
If you're performing a quick fix, you should use the **Save** option to save a revision of the current version. Do not use the **Save As** option for minor changes. Only use **Save As** to create a separate version based on the published version when starting development of new, long-term projects.
* **Save revisions to your current version frequently, and avoid multiple versions for the same project**:  
Save your changes frequently to a new project's version with the **Save** option, not **Save As**. Creating multiple new versions during development causes confusion when reconciling your changes to the published version and publishing them. Only users logged into that version receive update notifications.
* **Make small changes, publish often**:  
Keep your development version changes small and publish often to reduce the impact on your peers. This will make it easier to troubleshoot any errors and revert changes.
* **Your changes supersede the changes of others**:  
If your changes and the latest published version modify the same item and the system cannot reconcile those changes automatically, publishing your version overwrites the existing items in the published version with yours.
* **Compare only with the published version**:  
Compare and integrate your version with the published version, because you cannot compare and integrate your version with other versions.
* **Coordinate with your team**:  
Communicate your plans between your teams. Identify any potential issues of overlap early to prevent teams from inadvertently saving over each other's changes to common elements.
* **Integrate the published version**:  
Any time your current version is behind the published version, integrate the published version into your version. This makes it easier to publish your changes later. The profile switcher and the **Save/Publish** dialog contain a status message that you can use to compare your version's changes to the currently published version:
    * **You are ahead of the published version**  
    Your current version includes changes that are not in the currently published version.
    * **You are up to date**  
    Your current version and the currently published version match.
    * **You are behind the published version**  
    The currently published version includes changes that are not in your current version. To view those changes, click **View latest published changes**. For more about these status messages and how to use them, see [About Server-Side Saving and Publishing](https://docs.tealium.com/about-save-publish/).
* **Delete items only from the published version**:  
To permanently delete an item, delete it from the published version. If you delete an item from a version that is not the published version and then save and publish, the platform will restore the deleted item during publishing. This is to prevent accidental removal of dependencies, such as attributes required by audiences.

## Example workflows

In the following examples, an organization has two users working on the server-side platform. **User 1** is working on a connector while **User 2** is working on a data source.

### Concurrent saves to same version

In the following example, both users are working together on the same version.

![](https://docs.tealium.com/images/server-side/save-publish/collaboration-workflow-two-users2.png)

The diagram shows each action performed.

1. We begin with a single version **A1** currently published. When visitors go to the site or app, they use version **A1**.
1. **User 1** adds a connector.
1. **User 2** adds a data source.
1. **User 1** saves changes as a revision to version **A1**. **User 2** receives a notification that **User 1** has updated this version.
1. **User 2** saves changes as a revision to version **A1**, integrating **User 1**'s changes (the new connector). **User 1** receives a notification that **User 2** has updated this version.
1. **User 1** loads version **A1** and receives **User 2**'s changes (the new data source).
1. **User 1** publishes version **A1**. **User 2** receives a notification that **User 1** has published this version. User 1 and User 2 are up to date.
1. When visitors go to the site or app, they use version **A1** with the new connector and data source.

### Concurrent saves to multiple versions

In the following example, each user is working on their long-term projects in their own separate version.

![](https://docs.tealium.com/images/server-side/save-publish/collaboration-workflow-two-projects2.png)

The diagram shows each action performed.

1. We begin with a single version **Start** currently published. When visitors go to the site or app, they use version **Start**.
    * **Start**: You are up to date.
1. **User 1** creates a new version of **Start** named **Project 1**. 
    * **Project 1**: You are up to date.
1. **User 2** creates a new version of **Start** named **Project 2**.
    * **Project 2**: You are up to date.
1. **User One** adds a connector to version **Project 1** and saves a revision.
    * **Project 1**: You are ahead of the published version.
1. **User 2** adds a data source to version **Project 2** and and saves a revision.
    * **Project 2**: You are ahead of the published version.
1. **User 1** publishes version **Project 1** and receives a notification that version **Project 1** has been published. When visitors go to the site or app, they use version **Project 1** with the new connector.
    * **Project 1**: You are up to date.
    * **Project 2**: You are behind the published version.
1. **Project 1** is complete.
1. **User 2** saves changes to version **Project 2** and saves a revision, using the **Include latest published changes** option to integrate changes from version **Project 1** (the new connector).
    * **Project 2**: You are ahead of the published version.
1. **User 2** publishes version **Project 2**. When visitors go to the site or app, they use version **Project 2** with the new connector and the new data source.
    * **Project 1**: You are behind the published version.
    * **Project 2**: You are up to date.
1. **Project 2** is complete.