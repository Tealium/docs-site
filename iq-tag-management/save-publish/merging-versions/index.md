---
title: Merge versions
description: The merge feature is useful when you have to bring changes from another version into the currently-published version.
url: https://docs.tealium.com/iq-tag-management/save-publish/merging-versions/
---
For example, you could be testing a version in Dev or QA environments and it is finally ready to be merged into the Prod environment. Using this built-in feature, you can pick changes from the Dev or QA version, merge them in the current version, and continue to save and publish as usual.

![](https://docs.tealium.com/images/iq-tag-management/merge-version-dropdown.png)

## Show version relationship

The **Show version relationship** checkbox in the **Versions** tab, which is checked by default, highlights the origin path. This feature shows how each version is related to the other versions in the publish history. This is important because the origin path is your visual guide for determining which versions you can or cannot merge.

![](https://docs.tealium.com/images/iq-tag-management/show-relationship.png)

## How it works

Two versions can be merged **only** if they have branched away from the same origin or ancestor. What does this mean? Take a moment to trace the path of publish history in your profile. You will notice that saved (overwritten) versions have lined up in the same origin path, whereas saved-as versions have branched away into distinct paths. Merging is possible **only** when the versions -- current and incoming -- are present in distinct paths.

Here's a sample publish history with the 2 as the current version.

![](https://docs.tealium.com/images/iq-tag-management/example-screenshots.png)

As you can see:

* Version 1 is NOT in the same path as version 2, which means they can be merged. This is also true for version 1.1.
* Version 2 and the initial publish are lined up in the same path, which is why they cannot be merged.

### Tag templates

Tag templates do not follow standard merge behavior. When merging one version into another, the tag templates in the active version take priority. Any tag template changes from the merged version will be discarded. If you want to merge in tag templates from another version, switch to that version and then merge the tag templates into your original version.

For more information about tag templates, see [about-templates](https://docs.tealium.com/about-templates/).

## Merging changes into current session

To merge changes from one version into the current version:

1. From the **Merge Changes into Current Session** drop-down list, select the version you want to merge into this session.
    
<blockquote>
Make sure that the incoming and current versions are in distinct origin paths.
</blockquote>

1. In the next window, select the changes you want to add, update, or remove in the current version.  
    ![](https://docs.tealium.com/images/iq-tag-management/incoming-changes-merge-versions.png)
1. Review and confirm the changes. Then click the **Merge** button to complete the merge.
1. **Save/Publish** the current version. You have the option to save as a new version (Save As) or overwrite the existing version (Save).

The following video tutorial demonstrates how to merge changes between versions:



## Resolving merge conflicts

Conflicts arise if the versions contain two distinct instances of the same Tealium iQ element. For example, a certain load rule condition with a date range in the incoming version will conflict and collide with same load rule condition without a date range in the current version. Merging them is not possible unless you accept one instance of the element and discard the other.

To resolve a conflict from the **Merge Changes** window,

1. Click the eye icon to reveal the conflicting changes.
    ![](https://docs.tealium.com/images/iq-tag-management/use-this-slider.png)  

1. Read the configurations and determine which instance you want to keep.
1. Click the **Use this** bar to move the change you want into the **Accepted** column. Unaccepted changes will be discarded before merging.
    ![](https://docs.tealium.com/images/iq-tag-management/accepted-column.png)  

1. Click **Next** and review the final changes before merging.
1. Click **Merge** and proceed to Save/Publish your version.

## Resolving merge errors

The following are common errors, and their solutions:

### Alert message: "Version cannot be merged"

This message informs you that the version cannot be merged because the changes in the incoming version are already a part of this version. This situation is due to the fact that the two versions exist in the same origin path.

**Solution**: If you need to remove any changes, remove any components from previous or incoming versions.

### Alert message: "Permissions"

This alert informs you that the merge operation has failed due to permissions issues. Here are the possibilities:

#### Alert Message: "You do not have the permission to edit JavaScript Extensions"

This alert indicates certain changes contain one or more JavaScript extensions that you are not permitted to access or edit. This error may occur when merging between versions or between concurrent users.

**Solution**: Make sure your account admin grants you **Manage Javascript Code Extension** permissions.

#### Alert Message: Sorry you don't have the required permission to perform this action...

**Solution**: Contact your Account Manager for further assistance.

#### Alert Message: "You do not have permissions to resource locks."

This alert indicates that certain changes are secured by resource locks. You cannot perform the merge operation unless you have the permission to access or edit resource locks. This error may occur when merging between versions or between concurrent users.

**Solution**: Make sure your account admin grants you the **Manage Resource Locks** permission.

![](https://docs.tealium.com/images/iq-tag-management/labels-perm-missing.png)

### Alert Message: "You have pending changes"

This alert indicates that there are pending changes on one or more of the versions that you are trying to merge.

**Solution**: Save all pending changes on both of the versions you are trying to merge.

### Alert Message: "Your libraries are mismatched"

This alert informs you that when you try to merge profile versions that are linked to libraries, the incoming profile version must be linked to every library that the current profile version is linked to, and those library versions must match.

**Solution**: Link each profile version to the same library versions as the other profile versions.

#### Example: Older library version

If Version A is linked to Library 1 and Version B is linked to an older version of Library 1, the merge between Version A and Version B will fail. To resolve this, navigate to Version B and either overwrite Version B with the updates from Library 1 or save as a new version (Version C) with the updates from Library 1. The merge will now succeed because each profile version is linked to the same library version.

![](https://docs.tealium.com/images/iq-tag-management/save-publish/merge-libraries-diagram-1.png)

#### Example: Missing library link

If Version A is linked to Library 1 and Library 2 and Version B is only linked to Library 1, the merge between Version A and Version B will fail. To resolve this, navigate to Version B and link it to Library 2. Then overwrite Version B or save as a new version (Version C) with the links to Library 1 and Library 2. The merge will now succeed because each profile version is linked to the same library versions as the other profile versions.

![](https://docs.tealium.com/images/iq-tag-management/save-publish/merge-libraries-diagram-2.png)


