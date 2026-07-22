---
title: Password policy
description: A password policy is a set of rules designed to improve security by establishing strict password requirements for your users. These rules are enforced on all users in your account.
url: https://docs.tealium.com/administration/security-access/password-policy/
---
## Password policy settings

Password policy controls password settings for all users on your account. You can configure the following password settings:

* Minimum password length
* Minimum uppercase characters
* Minimum numeric characters
* Minimum special characters  
Valid special characters: **@ # $ % ^ &amp; \* ( ) - \_ = + ' " [ ] \{ \} | ; : &lt; &gt; , . / ? !**
* Password history restriction - Prevents users from entering previously used passwords when updating their passwords.
* Password expiration - The number of days before a password expires and a new one must be set.

The following two password policies cannot be changed or disabled:

* Does not match the username
* Does not appear in compromised password database

Tealium hashes the password and checks a portion of the hash against a third-party database of compromised passwords. This method is secure and does not reveal the actual password.

For more information about password requirements and why each is necessary, see [Digital Identity Guidelines by NIST](https://csrc.nist.gov/pubs/sp/800/63/3/upd2/final).

### Default policy

The default password policy contains the following requirements:

* Minimum eight characters in length
* Minimum one number character
* Minimum one uppercase character
* Minimum one special character
* One password history restriction
* Password never expires
* Does not match the username
* Does not appear in database of compromised passwords

### Recommended policy

For your convenience, we offer a recommended policy. This is a stricter policy than the default policy and uses the following settings:

* Minimum 12 characters in length
* Minimum two number characters
* Minimum two uppercase characters
* Minimum one special character
* Two password history restrictions
* Password never expires
* Does not match the username
* Does not appear in database of compromised passwords

### Custom policy

Select this option to configure your own password policy. The strength indicator will update as you adjust each policy setting. We strongly recommend using a policy with a minium strength of **Strong**.

## Manage the password policy

Managing the password policy requires the [Manage Accounts]() permission. Only an account admin has the permissions required to modify this setting.

Use the following steps to manage the password policy for your account:

1. Log in to iQ Tag Management.
1. In the admin menu, click **Manage Password Policy**.
1. Modify the password settings and click on **Update Password Settings**.

The changes take effect immediately.

### Password expiration

Tealium account passwords do not expire by default. However, depending on your security requirements, you can configure how long a password can be valid before needing to be reset.

To configure the password expiration time for your account, set the expiration time to a number of days greater than zero.

### Change to a stricter password policy

If you set a stricter password policy, you may break some users’ current passwords. This forces those users to reset their passwords if they don't satisfy the new password requirements. As an admin, you cannot change passwords for other users.

## Failed logins

Note that after five unsuccessful login attempts, your account is temporarily locked for five minutes.