---
title: Profile retention policy
description: This document explains our account profile retention policy.
url: https://docs.tealium.com/administration/resources/profile-retention-policy/
---
## How it works

The following policy is applicable to the profile configuration data.

Profile configuration is the data and metadata stored by Tealium to control how each customer’s account profile operates. Customers control what is included in these configurations every time they save or publish their profile. The data does not contain any user event information. It only includes the Tealium system configuration for how the data should be collected and activated.

Examples of what may be included in the profile configuration are names and rules of configured attributes or when and with what data to fire a tag or connector.

## Versions

In Tealium, the profile configuration is referred to as a version. You can find a list of versions in the Client-Side and Server-Side profile switcher:

| Client-Side | Server-Side |
| --- | --- |
| ![](https://docs.tealium.com/images/administration/profile-retention-client-side-version.png) | ![](https://docs.tealium.com/images/administration/profile-retention-server-side-version.png) |

## Retention scope

Tealium retains the following configuration versions for both Tealium iQ (Client-Side) and Server-Side by default:

* The currently published version, regardless of when it was published.
* The previous published version, regardless of when it was published.
* Any other versions saved or published within the past 13 months.
* The original version from which the branch was created from for any of the previously mentioned versions.

In addition, Tealium retains the following additional items for Tealium iQ (Client-Side):

* All libraries
* 13 months of publish history

All retained versions and libraries are available to load in the Tealium user interface, and any version available in the user interface can be merged into any other available version.