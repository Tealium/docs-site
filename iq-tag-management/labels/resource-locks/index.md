---
title: Resource locks
description: Resource locks are labels that you apply to restrict access to those elements.
url: https://docs.tealium.com/iq-tag-management/labels/resource-locks/
---
## About resource locks

When an element has a resource lock applied to it, only users added to that label may edit the element. However, that element is still available for use by others. For example, if a load rule has a resource lock applied to it, users can still apply that load rule to a tag without being a member of that load rule&#39;s resource lock.

### Required permissions

Any user with the **Manage Users** permission prior to the implementation of the resource lock feature automatically has the **Manage Resource Locks**. To grant a user the **Manage Resource Locks** permission, a user who already has that permission must grant it through **Manage User Permissions**. For more information, see [Managing User Permissions]().

## Creating a resource lock

Since a resource lock is also a label, you have the following two options for creating one:

* Create a new label as a resource lock.
* Edit an existing label to convert it into a resource lock.

### Create a resource lock

1. In the admin menu, click **Manage Labels**.
1. In the **Add New Label** screen, enter a **Name** for the label.  
You may want to use a naming convention to indicate this label is a resource lock, to differentiate it from regular labels.
1. Select a color for the label.
1. Set the **Enable as Resource Lock** toggle to **Yes**.
1. Select the users you want to assign to this resource lock.  
    ![](/images/iq-tag-management/resource-lock-select-users.png)
1. Click **Save Changes**.  
To create another resource lock, click **Save &amp; Add Another**.

Your new resource lock appears in the list of labels, and you can now apply it to elements. The icon for resource locks contains a lock to differentiate resource locks from labels. You may apply more than one resource lock to an element, but a user only needs to be assigned to one of the resource locks to edit the element.

If you convert a resource lock back into a regular label, you will lose the list of users you assigned to it.

### Copying and inheriting resource locks

* Labels are not inherited from a [profile library]().

* During the [profile creation process](), any resource locks applied to the elements you are copying are copied as well. Unassigned resource locks are not copied.
