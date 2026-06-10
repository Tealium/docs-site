---
title: Managing server-side user permissions FAQ
description: This article describes how to manage server-side users and permission roles for the Tealium Customer Data Hub.
url: https://docs.tealium.com/server-side/settings/user-permissions/faq/
---
## Frequently Asked Questions

#### If a user is removed from the client-side profile, is the user also removed from the server-side profile? 
No. When a user exists in both client-side and server-side, removing the user from one does not impact the other.

#### Can I grant a user access to a server-side profile without allowing access to a client-side profile?
Yes. If a user already exists in the account and has been granted permission to a profile on the server-side, go to **Tag Management &gt; Manage Users** and remove that user from the client-side interface. For more information, see Add a server-side only user above.

#### How does the &#34;All current and future profiles&#34; option impact server-side permissions?
There is no impact to server-side users. All server-side users have the default permission role of **No Access** to all new server-side profiles.

#### What happens if a user has access to only one profile on the server-side and no profile access on the client-side?
If the user selects server-side at the login screen, they are automatically loaded into the account/profile accordingly. If the user attempts to log in to the client-side, a modal displays a denied access message.

#### Can a server-side admin change their own permissions for server-side profiles? 
Yes. A server-side admin user (granted by the **Manage Account** permission) can change permissions for all server-side users, including their own.

#### Can a server-side admin update manage permissions for all server-side profiles?
Yes. A server-side admin user&#39;s access is granted by the **Manage Account** permission, which is an account-level permission. Users with this permission level have access to the **Manage Users** screen in the server-side interface where they can manage user permissions for all profiles.

#### How do the new server-side permissions affect the Omnichannel File Status API?
Access control to the [Omichannel File Status API]() will change upon final release of the server-side permissions feature. In addition to the standard requirement of needing [an API key to authenticate with the API](), users must have read access to the relevant Customer Data Hub account. Users using the [v1 API]() only need read access to the Customer Data Hub account.

#### Can a server-side admin add new users to an account?
No. The **Manage Account** permission does not grant access to add new users or delete users from an account. While they can remove access to profiles, only users who have the **Manage Users** permission assigned in the iQ Tag Management workflow can invite a new user to an account or completely delete a user from an account.

#### Does this feature change the way user management access is granted or controlled within TiQ?
No. The **Manage Users** permission in iQ Tag Management remains the permission that grants a user access to add or remove users from a business account. Users with only the **Manage Users** permission do not have access to manage permissions on the server-side.
