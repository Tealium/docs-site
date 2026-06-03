---
title: How do I log in to the Tealium platform?
description: This article describes how to log into the Tealium platform.
url: https://docs.tealium.com/iq-tag-management/frequently-asked-questions/faq-login/
---
The main Tealium login page is located at [https://my.tealiumiq.com](https://my.tealiumiq.com).

## Email and password

To log in to an account with an email username and password:

1. In the **Email** field, enter your email address.
1. In the **Password** field, enter your password.
    &#43; If you do not remember your password, click **Forgot Password?** For more information, see [How do I reset my password?]()
1. Click **Login**.

### Multi-factor authentication

Multi-factor authentication (MFA) is a security method that requires a second method of authentication to log in, such as a smartphone or browser app. Your account administrator may require that you use MFA to log in to the account.

To log in to an account with MFA enabled, see [Multifactor Authentication]().

### No access to log in

If you see a message that says **&#34;You do not have access to Client-Side for this profile. Contact your account administrator for access.&#34;**, the most likely reason is that you are not a member of any [permission groups](). Your account administrator needs to add you to a permission group with access to at least one profile.

## Single-sign on

Single-sign on (SSO) is a secure way of using one identity management solution to gain access to multiple applications. You can log in to the SSO provider of your primary account, which then grants you access to all of your accounts on the Tealium platform.

Your [organization&#39;s identity management solution for SSO]() can either use a third-party provider or a self-hosted authentication system.

Most of Tealium SSO users log in through their organization&#39;s identity management solution first, but you can still log in to Tealium&#39;s platform directly with SSO, as follows:

1. Navigate to one of the following login pages:
    * The main Tealium login page at [https://my.tealiumiq.com](https://my.tealiumiq.com) and click **SSO Login**.
    * The SSO login page at [https://my.tealiumiq.com/login/sso/?ssoMethod=accountNameSSO](https://my.tealiumiq.com/login/sso/?ssoMethod=accountNameSSO).
1. If you remember your primary account name, enter your primary account name in the **Account Name** field and click **Next**.
    - If you are not currently authenticated with the SSO service, you will be redirected to their login screen.
1. If you do not remember your primary account name:
     1. Click **Forgot Account Name**.
     1. In the **Email** field, enter your email address.
     1. Click **Submit**.
     1. The system will send an email with the primary account name.