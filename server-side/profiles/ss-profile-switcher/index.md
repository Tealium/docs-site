---
title: Profile switcher
description: This article explains how to use the server-side profile switcher.
url: https://docs.tealium.com/server-side/profiles/ss-profile-switcher/
---
## How it works

Each account can contain several profiles. The profile switcher lets you quickly switch accounts, profiles, and profile versions.

![](/images/server-side/save-publish/ea-server-side-profile-switcher.png)

 When you switch to the server-side platform from a client-side profile, the most recently saved version of the profile is loaded. It might not be the same version you had been working on previously. 

### Version status messages

When you select a version in the profile switcher, it displays one of the following messages that compares your version&#39;s changes to the currently published version:

* **You are ahead of the published version**  
Your current version includes changes that are not in the currently published version.
* **You are up to date**  
Your current version and the currently published version match.
* **You are behind the published version**  
The currently published version includes changes that are not in your current version. To view those changes, click **View latest published changes**.

For more about these status messages and how to use them, see [About Server-Side Saving and Publishing]().

## Switch profiles and versions

Use the following steps to switch to another profile:

1. Click the profile drop-down menu.
1. From the **Profile** drop-down menu, select the profile you want to switch to.
1. From the **Version** drop-down menu, select the version of the profile to switch to.
1. When you select a version, the profile switcher compares the currently selected version, including any changes you have made to it, to the currently published version.
1. Click **Load Version**.

You can also use the **Load this Version** option in [Version History]() to switch versions.