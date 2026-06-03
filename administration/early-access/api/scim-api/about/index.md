---
title: About SCIM API
description: Learn how to use SCIM provisioning to sync users from your identity provider to your Tealium account.
url: https://docs.tealium.com/administration/early-access/api/scim-api/about/
---
## How it works

System for Cross-domain Identity Management (SCIM) is a standard that automates and simplifies creating, updating, and removing user accounts across cloud apps.

Use SCIM provisioning to automatically sync users from your identity provider (IdP) to Tealium. SCIM creates users with appropriate access during onboarding and removes Tealium access when users are deprovisioned in the identity provider, ensuring consistent offboarding and preventing unauthorized access.

Use a SCIM provisioning connector in your IdP or invoke the SCIM API directly.

## Authentication

The Tealium SCIM integration uses a long-lived bearer token to authenticate with applications. Use this bearer token as the OAuth bearer token when you configure your user provisioning application.

All SCIM API calls are authenticated with this bearer token.

The API key and bearer token are linked to the user who generates them. Use a dedicated service user with the required Tealium permissions. A service user is a user account not linked to a person that is used to manage resources. This approach prevents access issues if a regular user account becomes unavailable.

To generate the bearer token:

1. Log in to Tealium as a dedicated service user. 
1. Generate an [API key]().
1. Call the long-lived token endpoint to generate a long-lived bearer token using the following cURL command. Replace the placeholders with your account name, profile name, dedicated username, and the API key:  

```bash
curl --location &#39;https://developer.tealiumapis.com/v1/auth-long-lived/token&#39; \
--header &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;account={ACCOUNT}&#39; \
--data-urlencode &#39;profile=main&#39; \
--data-urlencode &#39;username={USERNAME@EXAMPLE.COM}&#39; \
--data-urlencode &#39;key={API_KEY}&#39;
```

The token should resemble the following example:

```json
{
  &#34;access_token&#34;:&#34;eyJhbG...53UHg&#34;,
  &#34;expires_in&#34;:35999,
  &#34;refresh_expires_in&#34;:0,
  &#34;token_type&#34;:&#34;Bearer&#34;,
  &#34;not-before-policy&#34;:0,
  &#34;scope&#34;:&#34;profile email&#34;
}
```

The token expires after 90 days. Regenerate the token as needed.

If you need assistance generating a token or have questions about permissions, contact Tealium Support.

## Endpoints and permissions

The Tealium implementation of SCIM supports the following HTTP methods:

| Method | Description                          | Tealium permissions |
| ------ | ------------------------------------ | --------------------------- |
| `POST`   | Create a user or group.              | User admin or account admin |
| `GET`    | Retrieve user details, group details, or list users or groups. | All account users |
| `PUT`    | Replace a user or group.                      | User admin or account admin |
| `DELETE` | Delete a user or group.                       | User admin or account admin |
| `PATCH`  | Partially update a user or group.             | User admin or account admin |

## Built-in groups

The SCIM API exposes built-in groups that align with the [Tealium system admin roles]().

The following built-in groups are available with the SCIM `/Groups` endpoint:

| Group name | Description |
| --- | --- |
| Account Admins | Full account administration privileges |
| User Admins | User management privileges |
| Privacy Admins | Privacy and consent management privileges |
| Technical Admins | Technical and integration privileges |
| Profile Admins | Profile-level administration privileges |
| Standard User | Basic read-only access (alias for Account Viewers) |

The `Standard User` group is an alias for the internal `Account Viewers` group. Both groups share the same UUID. Filtering on `displayName eq &#34;Standard User&#34;` matches this group, but filtering on `Account Viewers` returns zero results.

### Inherited groups

Adding a user to certain admin groups automatically grants membership in inherited groups:

| Add to Group | Automatically Added To |
| --- | --- |
| Account Admins | User Admins, Privacy Admins, Technical Admins, Profile Admins &#43; PII access |
| User Admins | Technical Admins &#43; PII access |
| Privacy Admins | User Admins, Technical Admins and PII access |
| Technical Admins | (none) |
| Profile Admins | (none) |
| Standard User | (none) |

Membership in Account Admins, User Admins, or Privacy Admins automatically grants membership in internal PII groups (PII Admins/PII Viewers). For security purposes, these internal groups are not visible with the SCIM API.

### Group removal behavior

Removing a user from an admin group automatically removes them from inherited groups:

* **Account Admins**: Removes from User Admins, Privacy Admins, Technical Admins, Profile Admins, and revokes PII access
* **User Admins**: Removes from Technical Admins and revokes PII access
* **Privacy Admins**: Removes from User Admins, Technical Admins, and revokes PII access
* **Technical Admins**: No automatic removal
* **Profile Admins**: No automatic removal

### Built-in group protection

Built-in groups have the following restrictions:

* Cannot be renamed with SCIM PATCH operations.
* Cannot be deleted with SCIM DELETE operations.

Creating or updating a custom group with a `displayName` that matches a built-in group returns an HTTP 400 error. 

