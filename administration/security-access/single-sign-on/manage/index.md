---
title: Manage Single Sign-On (SSO) Connections
description: This article describes how to manage SSO connections.
url: https://docs.tealium.com/administration/security-access/single-sign-on/manage/
---
After successfully connecting to your IdP, you can manage the following SSO settings from the **Manage SSO** screen: 

* Switch the authentication mode from **Test** to **On**
* Update the IdP administration email
* Upload a new signing certificate
* Check the status of your signing certificate

## Deactivate SP-Initiated SSO

Complete the following steps to deactivate SP-initiated SSO:

1. From the **Manage SSO** screen, switch the **Authentication Mode** to **Test**. Switching the authentication mode to **Test** forces all users through the Tealium-initiated login. Users need to reset their Tealium login credentials before they can access their accounts.
1. A confirmation dialog appears. Click **Deactivate**.
1. Click **Save**.

## Reset SSO

To reset the SSO configuration, you first must switch the authentication mode to **Test** so that your users can use the Tealium-initiated login. 

Resetting the SSO configuration deletes all current SSO settings and forces all users through the Tealium-initiated login. After you reset the SSO configuration, all affected users need to reset their Tealium login credentials before they can access their accounts.

To reset the SSO configuration, complete the following steps:

1. Go to **Admin menu > Manage SSO** and click **Reset**. 
<blockquote>
Reset is available only when the **Authentication Mode** is switched to **Test**.
</blockquote>

2. The **Reset SSO?** dialog appears. Enter `RESET` in the confirmation field and click **Reset** to confirm the SSO reset.
3. The **Configure IdP** screen appears. Follow the steps in the **Setting up your SSO** section.


<blockquote>
If your company changes its email address domain or IdP, you must reset the SSO.
</blockquote>
