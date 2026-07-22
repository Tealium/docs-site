---
title: Publishing best practices
description: This article presents a procedure for developing, testing, and publishing updates to a Tealium iQ Tag Management profile.
url: https://docs.tealium.com/iq-tag-management/save-publish/publishing-best-practices/
---
Tealium iQ supports a robust development effort and approval process:

* **Multiple concurrent projects**  
  Developers can work on separate versions of a profile and then merge changes from one version into another. When one developer finishes their project, they publish their version to production. Other developers can merge the updates into their own still-in-development version. If multiple developers are working on the same profile, the platform notifies the developers of published changes. Developers can load the new version or merge the new version into their current work so they can keep working.

  For more information, see [Concurrent Users](https://docs.tealium.com/concurrent-users/).
* **Branching, merging, and iteration**  
  Developers can use the following methods to save their changes:

  * **Save As** branches a new version off of their current version.
  * **Merging** pulls changes from one version into another.
  * **Save/Overwrite** replaces the current version when they save their changes.

  For more information, see [About Saving](https://docs.tealium.com/about-saving/) and [merging-versions](https://docs.tealium.com/merging-versions/).
* **Merge conflict resolution**  
  When multiple developers modify the same object in a profile, publishers are able to choose the preferred version before publishing, thereby avoiding the publication of incorrect versions.

  For more information, see [Resolving merge conflicts](https://docs.tealium.com/merging-versions/#resolving-merge-conflicts).

* **Development and testing environments**

  By default, Tealium iQ offers Development, QA testing, and Production environments. Developers and testers can switch environments to test site performance, user experience, and data collection. Custom environments can be created as needed to support multiple development projects in progress.

  For more information, see [Publish environments](https://docs.tealium.com/about-publishing/#publish-environments).
* **Testing tools**  
  Tealium provides a set of testing tools that let developers and testers confirm that tags and events fire as expected, the data layer object contains the data you need, and data is processed correctly. If there's a problem, the tools help them diagnose the issue so it can be resolved before the version goes into production.

  For more information, see [Tealium Tools](https://docs.tealium.com/iq-tag-management/tealium-tools/).
* **Approval structure**  
  The Account Administrator can set up permission levels and workflows on the account. These grant Developers, QA Testers, and Product Managers the access and permissions they need to perform their roles, but prevent users from performing tasks they shouldn't. For example, a developer shouldn't be allowed to publish directly to a production environment without QA testing and project manager approval.

  For more information, see [Publishing Workflow](https://docs.tealium.com/publish-workflow-management/).
* **Version tracking map**  
  The version tracking map displays all of the versions in the Development, QA testing, and Production environments. Users can quickly see how versions branch from each other, compare the versions with a diff tool, and merge changes from one version to another.

  For more information, see [Version History](https://docs.tealium.com/client-side-versions/).

## Publish procedure

![](https://docs.tealium.com/images/iq-tag-management/save-publish/publishingbestpractices2.png)

The following steps summarize a simplified workflow for managing updates to a Tealium IQ profile:

1. Configure the publishing environments, permissions, and workflows on the account.
1. Load the **Prod** version.
1. **Save As** a new version and publish it to **Dev**.
1. Make your changes, save the version, and publish the version to **Dev**.
    * **Save As** if you want to create a new version so you can roll back to the previous version if necessary.
    * **Save/Overwrite** changes to the new version, and publish to **Dev** to test it.
    * If other developers update the **Prod** version, merge those changes into the new version.
1. When ready to test, publish the new version to **QA**.
1. Perform QA tests.
1. When the version passes tests, request publish to **Prod**.
1. Project manager approves publish to **Prod**.

## Example

### Configure the account

Before any development begins, the account administrator configures the account's publishing workflow and configuration.

1. Enable and configure **Workflow Management** to control who can submit changes to the **Prod** environment and who can approve those changes for publishing.
1. Enable **Publish Notify Email** so users and developers know when a new version is published while not logged in to Tealium iQ.
1. If multiple projects are developed and tested concurrently, set up **Custom Publish Environments** so the developers can load extra environments and configurations on websites through the **Web Companion** and **Environment Switcher** tools.

For more information, see:
* [Publish Configuration](https://docs.tealium.com/publish-configuration/)
* [Publish Workflow Management](https://docs.tealium.com/publish-workflow-management/)
* [Custom Publish Environments](https://docs.tealium.com/custom-publish-environments/)

### Create a new version based on Prod

Developer #1 gets a new task: configure a new tag on the profile. The first thing the developer does is create a version as a workspace to make changes. Doing this ensures that they have a clean development environment with the most recent updates from production, and that their work can merge back into production cleanly.

By default, Tealium iQ loads the most current version of a profile, so the developer needs to switch to the version that is currently published as **Prod**:

1. The developer loads the **Prod** version of the profile.
1. The developer performs a **Save As** a new version, and gives the new version a meaningful **Title** and description in the **Note** field: `New Tag For 2023 1Q`
    * Every time the developer overwrites the new version, they also publish it to the **Dev** environment.

For more information, see:
* [About Saving](https://docs.tealium.com/about-saving/)
* [About Publishing](https://docs.tealium.com/about-publishing/).

If the development team requires multiple development environments, the account administrator can create custom environments named *DEV A*, *DEV B*, etc. For more information, see, [Custom Publish Environments](https://docs.tealium.com/custom-publish-environments/).

So, if another developer is working on cleaning up load rules on the profile (let's call it version `Load Rule Cleanup For 2023 1Q`), that developer can ask for a custom **Dev** environment to avoid conflicting with the first developer.

### Develop changes

The developer works on changes in the new version and overwrites that version with each change:

1. The developer makes changes to the profile.
1. The developer uses **Save** with the **Overwrite existing version** option to save changes to the version. The version is still named `New Tag For 2023 1Q`.
    * If the developer wants to make changes that can be rolled back, they can **Save As** a new version (for example, `New Tag For 2023 1Q - B`)

Some helpful development tips:

* Give objects meaningful and descriptive names and notes, which identifies what has changed in a version and track those changes.
* Add labels to tags, variables, events, and extensions to group them by publish environment, geographic location, or campaign. This helps organize changes and identify objects that need to be checked during QA testing.
* Save changes often.

For more information, see:
* [About labels](https://docs.tealium.com/about-labels/) 
* [About saving](https://docs.tealium.com/about-saving/).

#### Developer tests

While working on changes in the new version, the developer can test a new version in a **Dev** environment or create a custom environment for testing. Testing ensures that the new version works as expected and doesn't impact site performance.

Tealium provides many tools to assist with this effort, which include:

* [Tealium Tools - Web Companion](https://docs.tealium.com/web-companion/): Use this browser app to inspect and validate tags that load on your web pages. It contains multiple tools to help you diagnose problems.
* [Universal Tag Debugger](https://docs.tealium.com/universal-tag-debugger/): Use this tool to validate the UDO and event tracking data. 
* [Version diff tool](https://docs.tealium.com/version-diff-tool/): Use this tool to compare your development version to another version so you can see how your changes impact the distributed universal tag files.
* [Tealium Tools - Environment Switcher](https://docs.tealium.com/environment-switcher/): Use this tool to switch to the **Dev** environment to check site performance.
    * The Environment Switcher also lets a developer use custom environments on a website.

You can also use your browser's development console to inspect page elements, network calls, and more.

For more information, see [Troubleshooting](https://docs.tealium.com/iq-tag-management/troubleshooting).

### Merge Prod updates into the development version

Sometimes, while a developer is working on a new version, another developer changes the version that is currently published to **Prod**:

* Concurrent development efforts (the other developer finishes `Load Rule Cleanup For 2023 1Q` before the first developer is done with `New Tag For 2023 1Q`).
* Quick bug fixes to a **Prod** version (the other developer is fixing the first developer's past mistakes).

Developers need to merge the changes that were made to the **Prod** version to all otheer versions in development. This ensures that developers are working with the latest version of the main profile and have identified any potential conflicts or incompatibilities earlier in the development process.

In this example, if the other developer's project finishes before the first developer's, the first developer needs to merge the second developer's changes to **Prod** into the `New Tag For 2023 1Q` version.

The following diagram represents the development process with two developers working on separate versions:

![](https://docs.tealium.com/images/iq-tag-management/save-publish/publishingbestpractices1.png)

To merge changes in the **Prod** version to a version in development:

1. In the [profile switcher]( ), select the **Dev** version and click **Load Version**.
1. Navigate to **Client-Side Versions**.
1. From the **Merge changes into current session** drop-down list, select the **Prod** version and click **Merge**.
1. Confirm that all of the changes need to be added to the development version. 
1. Publish the new version to **Dev**.

If multiple developers are working on the same version, the platform notifies them of published changes and allows them to quickly load the new version or merge changes in the new version into their current work so they can keep working. There are also communication tools that allow the group to communicate with each other over the platform.

For more information, see:
* [Merging Versions](https://docs.tealium.com/merging-versions/): How to bring changes from an old version to the currently published version.
* [Version diff tool](https://docs.tealium.com/version-diff-tool/): Compare the versions published in your file and inspect the distribution files. This lets you determine which configurations were added, removed, or unmodified between versions.
* [Merging changes between concurrent users](https://docs.tealium.com/merging-changes-between-concurrent-users/): How to bring in changes from concurrent users of the same profile version.
* [Concurrent Users](https://docs.tealium.com/concurrent-users/): Concurrent user communication tools and several example collaboration workflow scenarios.

### QA Testing

After the developer finishes testing, they publish the version to **QA** and notifies their testing staff. If there is no dedicated testing department, other developers can peer review the version to ensure that it follows coding standards, doesn't impact site performance, and functions as expected.

1. The developer publishes the `New Tag For 2023 1Q` version to **QA**.
    * If the version fails testing, the tester returns it to the developer to fix.
    * If the version passes testing, the tester saves it as new version (`New Tag For 2023 1Q - Passed Tests`) and requests publishing it to **Prod**. The platform notifies the appropriate users that a version is waiting for approval.

For more information about testing, see [Troubleshooting](https://docs.tealium.com/iq-tag-management/troubleshooting).

We recommend that the testing staff consolidate all development versions into a single version for testing. This allows the testing staff to test all of the pending changes in a single staging environment, which reveals any conflicts between the developer's efforts before submitting them for publishing to **Prod**.

The following diagram represents the development process with two developers working on separate versions and a consolidated testing environment:

![](https://docs.tealium.com/images/iq-tag-management/save-publish/publishingbestpractices3.png)

### Approval for Prod publish

When a version is queued up for publishing to **Prod**, the product manager is notified of a publish request. The product manager can publish the version to coincide with advertising campaigns or promotions. When the publish is approved, the version is published to **Prod**.

For more information about how to set up an approval workflow, see [Publish Workflow Management](https://docs.tealium.com/publish-workflow-management/).

For more information about updating the remaining development versions with the new changes to **Prod**, see [Merging changes between concurrent users](https://docs.tealium.com/merging-changes-between-concurrent-users/).