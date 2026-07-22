---
title: PII Permissions and Server-Side Account Level Roles (Early Access)
description: PII Permissions with server-side account level roles is an Early Access feature that introduces data privacy controls for server-side products.
url: https://docs.tealium.com/administration/early-access/administration/platform-permissions/pii-account-roles/
---

<blockquote>
This feature is in Early Access and is only available to select customers. However, we are in the process of converting customers to the [Platform Permissions feature](https://docs.tealium.com/about-platform-permissions/), which manages access to products and features through permission groups and manages PII permissions through the Privacy Admin role and individual user settings. For more information, see [Platform Permissions](https://docs.tealium.com/about-platform-permissions/). <br><br>When all accounts have migrated from legacy permissions to platform permissions, this Early Access feature will be deprecated.
</blockquote>


## About permissions and restricted data

Today, PII data can be viewed throughout all the products and features in the server-side platform, such as Live Events, Trace, Visitor Sampler, and the Visitor Lookup Tool. Some users need to view PII so they can validate incoming event data and test data, but not all users require this level of permissions. If you allow more users to see PII data than necessary, your business is at risk because private customer data will be seen by users who shouldn't see it.

The **Restricted Data** property on attributes controls where sensitive data can flow through the data supply chain, but it does not limit who can view the values of those attributes.

In addition, access to the server-side products can only be granted at the profile-level with a single role: **Reader**, **Editor**, or **Publisher**. PII data is still exposed throughout the application and can only be hidden from a user by restricting access to the entire profile. Also, the role of **Editor** often is not sufficient to serve the growing needs of large businesses that have many active users with various duties.

## What's new

PII permissions and server-side account level permission roles provide an easier way to manage user permissions and control who can access PII data.

The new permission roles serve two main purposes:

* Integrate with the **Restricted Data** property of attributes so that PII data values are only exposed to users that require that access.
* To provide finer control over who can edit the profile configuration.

With PII Permissions enabled, you can grant access to select users to view PII if they have a legal basis for collecting, viewing, and using this data. This helps you reduce unnecessary exposure of sensitive customer data and helps you adhere to data privacy and compliance regulations.

With more granular permission roles, you can protect your most critical configuration components while granting broader access to the core functionality that is used on daily basis.

### New account permission roles

This feature introduces four permission roles related to PII and profile editing. Account permission roles are cumulative and can be combined to expand a user's access to the platform.

New account-level roles provide the following abilities:

* Control who can edit the **Restricted Data** property of attributes.
* Control who has the ability to view restricted data (PII) values.
* Control who can define, transform, and send restricted data outside of the Tealium Customer Data Hub (using connector integrations).
* Offer separate permission roles to access core components such as connector configuration and attributes, and more common components such as audiences.

These new abilities help minimize the chance of exposing sensitive PII data and support the integrity of your core configuration components by limiting access to only your most trusted and trained users.

The new account permission roles are:

* **PII Admin**  
Users assigned to this role can set the **Restricted Data** property for event, visit, or visitor attributes. These users cannot view PII data values unless also they are additionally granted the **PII Viewer** role.
* **PII Viewer**  
Users assigned to this role can view PII data values within the interface for profiles and areas of the product where they have access. These users cannot set the **Restricted Data** property unless they are additionally granted the **PII Admin** permission. 
<blockquote>
A user without the **PII Viewer** role cannot view restricted data values in the application.
</blockquote>

* **Configuration Admin**  
Users assigned to this role have access to edit the configuration of the profile, including the ability to create and edit attributes, enrichments, and rules.
* **Data Warehouse Admin**  
Users assigned to this role have access to DataAccess product features.![](https://docs.tealium.com/images/early-access/screen-shot-2021-06-27-at-10.11.15-pm.png) 


<blockquote>
The new roles applies to all users, including server-side admins and users with access to the **Manage Users** menu for server-side products. User Admins must assign account-level roles to themselves to have the wider privileges throughout the application.
</blockquote>


### What is a Standard User?

A **standard user** is a term introduced with this feature to describe the default level of access that new users receive at the account level.

Permissions are granted to standard users using the "principle of least privilege" with a new, minimal set of permissions that limits access to specific parts of the product. This is particularly important for features related to the setup and configuration of critical components in your profile.

By default, standard users have access to do the following:

* View data sources, attributes, enrichments, and rules
* Create audiences
* Use existing connectors
* Access testing and validation tools (Trace)

Standard users cannot do the following:

* See PII data or restricted data anywhere within the application
* Create connectors
* Create or edit attributes, nor set the **Restricted Data** property
* View connector error log details or download sample data
* Use the DataAccess product or DataAccess features (if enabled)

### Profile permission roles

No changes were made to profile permissions. PII Permissions are additive and complimentary to profile roles. Profile Level permission roles remain valid and applicable to user access rights at the profile level.

Users permissions can be set for one or more profiles within an account and access can be granted to one of the following four available roles:

* **No Access**  
The profile is not accessible to the user.
* **Viewer**  
View-only access for all features is available to all areas of the product to which the user has been granted access, as defined by account-level roles.
* **Editor**  
Edit access to areas of the product to which the user has been granted access, as defined by account-level roles.
* **Publisher**  
Edit access to areas of the product to which the user has been granted access, as defined by account-level roles, and the ability to publish changes to the profile.

### Masked data

Masked data is a way to protect confidential data from unintended exposure. A restricted data attribute will appear throughout the platform as a string of asterisks (\*\*\*\*) in place of the real value. Only users with the **PII Viewer** permission role will see the real value.

Data is masked in the back-end, before it is passed to the user interface, so the real values cannot be viewed using browser inspection tools. The masking format is not configurable.

## Activation and setup

This section describes the steps to activate and set up PII Permissions.

### Step 1: Request early access

Request access to this feature by sending a message to your Customer Success Manager.

When the feature is enabled, an in-product announcement displays with a summary of the new feature. A persistent alert bar displays throughout all server-side screens until enforcement of the feature is enabled.

### Step 2: Assign and configure user permissions

With the feature enabled you can configure user permissions and enable the enforcement of the roles. This allows you time to update user permissions and double-check the configuration without disrupting user access unintentionally.

To assign and configure account-level permissions for your users:

1. In the admin menu, click **Manage Users**.
1. Click the user to update.
1. Go to **Account Permissions**. ![](https://docs.tealium.com/images/early-access/screen-shot-2021-06-27-at-10.30.25-pm.png)
1. Select the roles that are appropriate for the user’s job function.
1. Click **Save**.  
Users in the account are not impacted until enforcement is enabled in the next step.

### Step 3: Enable enforcement

After you assign permission roles to your users and are satisfied that the proper permissions are in place, click the enforcement toggle to the ON position.

![](https://docs.tealium.com/images/early-access/screen-shot-2021-06-27-at-10.14.03-pm.png)

Enforcement is immediate and cascades to all account users. The persistent alert bar no longer displays and users in the account are now governed by the new permissions.

### Disable enforcement

If your new permission settings are not working as expected, or if you just need to revert the permissions, simply toggle off the **PII Permission Enforcement**. This reverts all user permissions back to their level prior to enabling enforcement.

The new account level permission configurations are maintained, but are not enforced. The alert bar will reappear (only visible to user admins) and remain persistent until you enable enforcement.

## Additional information

* [About Restricted Data](https://docs.tealium.com/about-restricted-data/)
* [Managing Server-Side User Permissions](https://docs.tealium.com/about-managing-server-side-user-permissions/)
