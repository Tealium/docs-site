---
title: Account organization
description: This document explains how accounts are organized into profiles, versions, and permissions. Use this hierarchy to help organize your Tealium account to match your business needs and implement a smooth development workflow.
url: https://docs.tealium.com/administration/account-org/account-organization/
---
## Accounts

The account is at the top level of the Tealium platform, and each customer has one account with Tealium. Accounts contain the following:

* Global settings for the account.
* Profiles, which are configuration sets for either server-side or client-side products and features.
* Permission groups of users.
* Admin roles for delegating management of the account.

![](/images/administration/account-organization/account.png)

At the account level, you manage the following:

* Admin roles for users to delegate management of the account.
* Permission groups.
* Single sign-on access management.

### Multiple accounts

Each person who logs into Tealium has a user account. A user can have access to multiple accounts, but their security settings (Single Sign-On, Multi-Factor Authentication, etc.) are determined by their primary account. The primary account is the first account the user was added to.

![](/images/administration/account-organization/multiple-accounts.png)

User 2 exists in Account 1 and Account 2, and its primary account is Account 1.

## Profiles

A profile contains configuration sets and data for a website, a mobile application, a region, or a brand. A profile can exist on either the client-side or the server-side:

* **Client-side** profiles manage tags and configurations in iQ Tag Management for a website or app.
* **Server-side** profiles collect data from all your sites and apps into your Customer Data Hub to build a comprehensive view of your customers and visitors, and then action that data through vendor integrations.

![](/images/administration/account-organization/profiles.png)

At the profile level, you manage the following:

* User permissions for the platform’s products, features, and data.
* Consent management.

For more information about profiles, see [About Profiles]().

 Only client-side profiles can be created through the platform. To create a server-side profile, contact Tealium Support.

### Multiple profiles

Set up multiple profiles to represent your business needs based on organizational structure, brands, and sources of data collection:

* **Websites**: If you have multiple websites and apps, set up separate profiles to manage development specific to each website.
    * **Brands**: If you have multiple brands for products or services, set up separate profiles for each of your brands to facilitate brand-specific management and development.
    * **Regions**: If you have websites and apps based in different regions, set up separate profiles for each region. For example, you could have separate profiles for each of your regional domains, such as `example.com`, `example.ca`,` example.fr`, etc.
* **Mobile platforms**: If you have websites and apps based on different mobile devices, set up separate profiles for each mobile environment. For example, set up profiles for iOS and Android so you can configure the tags to use each platform’s specific privacy and visitor identification methods.
* **Legal requirements**: If you have compliance or internal policies that require customer data to be stored in a specific region or subsidiaries with legal requirements not to share data, set up separate profiles to store data appropriately. For example, set up a separate server-side profile to store EU customer data in an EU data center (Dublin or Frankfurt) for GDPR compliance.

The following diagram demonstrates possible sets of profiles:

![](/images/administration/account-organization/multiple-profiles.png)

Multiple client-side profiles can send data to a single server-side profile for a unified view of your visitors. From there, you can create audiences of visitors, segment those audiences to power personalized experiences, and use that data across your digital marketing stack.

![](/images/administration/account-organization/client-to-server.png)

Server-Side Profile 1 receives data from Client-Side Profile 1, Profile 2, and Profile 3.

### Profile libraries

Using multiple profiles may cause you to duplicate effort configuring tags and other features. It also increases the amount of testing needed to ensure the tags, extensions, and other configurations in each profile run properly. Tealium provides client-side profile libraries to simplify this process.

A profile library contains all the features of a client-side profile and is designed to be imported into one or more profiles. Libraries are used to standardize configurations across profiles to avoid repeating the same configuration. For example, if you have two profiles that use the same tag and extensions, you could configure the profiles to inherit the tag and extensions from a common library.

For more information about profile libraries, see [Profile Libraries]().

The following diagram demonstrates a simple profile library relationship:

![](/images/administration/account-organization/profile-libraries.png)

Profile 1, Profile 2, and Profile 3 all import settings from Profile Library 1.

### Profile versions

A profile version is a saved set of changes to a profile. You can use one of the following save options on a profile version:

* **Save As**: Use this option to branch off of the current version to create a new version, preserving a copy of the previous version. This option provides the ability to roll back changes and retrieve previous versions.
* **Overwrite**: Use this option to overwrite the current version. You will not be able to revert your changes to the version.

![](/images/administration/account-organization/profile-versions.png)

### Client-side workflow

The client-side workflow offers the following collaborative tools:

* Multiple concurrent versions in development.
* Merges between versions.
* Multiple publishing environments for development, testing, and publishing to test functionality and appearance on a site without disrupting the production environment.
* Reverting the version in production to an earlier version to diagnose the errors in a test environment.

For more information about saving profile versions and merging changes between versions, see [Client-side Versions]().

The following diagram demonstrates a simple client-side workflow:

![](/images/administration/account-organization/cs-workflow.png)

The developer performs a Save As to create Version 2 and publishes it to Dev. After the developer works on Version 2, they publish it to the QA environment for testing. Finally, Version 2 can be published to the Prod environment.

### Server-side workflow

Server-side offers save, save as, and the option to publish a profile. You can use badges, rules, test users, and Trace to test new server-side functionality without disrupting the production environment.

For more information, see [About testing]() and [Trace: Test with Trace]().

The following diagram demonstrates a simple server-side workflow:

![](/images/administration/account-organization/ss-workflow.png)

The developer performs a Save As to create Version 2. After the developer works on Version 2, they add a test badge, rule, and user before publishing the profile. The profile is tested with Trace, then the test badge, rule, and user are removed before the profile is published to the Prod environment.

## Permissions

As stated before, each person who requires access to your Tealium account needs a user account. Users can be granted two types of account-level permissions:

* **Admin Roles**: Admin roles delegate administrative responsibilities on the account for tasks, such as managing account users or profile configurations. For more information about admin roles, see [Admin Roles]().
* **Permission Groups**: These groups are sets of permissions to specified profiles and features in the products that you grant to users. The structure of your permission groups should mirror how your business is organized, whether you divide up responsibilities by regional offices or brands or some other structure. For more information about permission groups, see [Permission Groups]().

Users can also be granted **PII (Personally Identifiable Information)** permission, which controls whether a user is allowed to see or edit PII data. This permission is set on a per-user basis. For more information, see [Users]().

The Customer Data Hub provides a unified interface for managing admin roles, groups, and users. For an example of the process of setting up profile access for permission groups, see [Permissions System Migration Guide]().
