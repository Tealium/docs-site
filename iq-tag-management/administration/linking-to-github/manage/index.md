---
title: Manage linking to GitHub
description: This article explains how to manage linking to GitHub.
url: https://docs.tealium.com/iq-tag-management/administration/linking-to-github/manage/
---
 If you do not use GitHub or do not have a public GitHub repository, we recommend that you use the  instead of linking to GitHub. 

## Link a GitHub account

To link a GitHub account hosted at `github.com`, you need your GitHub username and a [personal access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token). For GitHub Enterprise Server, use a fine-grained personal access token authorized by your organization. Linking your GitHub account creates a secure connection to your iQ Tag Management account that allows repository files to be referenced in your iQ Tag Management configuration.

For the link to succeed, your GitHub account must have at least one public repository.

#### Personal access tokens and repo scope

You must have a personal access token to link your GitHub account. This token is used instead of a password to create a more secure connection. When you create a personal access token in GitHub, you define the scope of access for the token. If you want to reference files from a private repository, you must select the **repo** scope when you create your access token.

![](/images/iq-tag-management/new-personal-access-token-2021-06-08-13-13-33.png)

To link to your GitHub account:

1. Log in to your Tealium iQ Tag Management account.
1. In the admin menu, click **Manage GitHub Account**.
1. Enter your **GitHub Username**.  
This is the username or email address you use to sign in to GitHub.
1. Enter your **Access Token**.  
This is the token used to authenticate your account with third-party applications.  
        Locate your access token in GitHub by going to **User &gt; Settings &gt; Developer Settings &gt; Personal Access Tokens**. Ensure that you store the token securely and do not share it with others to maintain account security.
1. Click **Link Account**.  
        ![](/images/iq-tag-management/manage-github-account-new.jpg)
1. Click **Save Changes**.

### Troubleshoot invalid authorization messages

If you receive an invalid authorization message when attempting to link your GitHub account, check the following:

* Check the [github.com status page](https://www.githubstatus.com/) to confirm that the service is up. There is nothing you can do until the service is up again. You can keep using the extension as normal but you will not be able to get the latest code from GitHub. If this is the case, a message with a timestamp is displayed that the system is unable to connect until GitHub is back up.
* The URL being used to retrieve the file no longer is valid. For example, the file was renamed or deleted on GitHub. You can delete the snippet if it is no longer needed and replace it with a new snippet containing the new URL.
* There are too many snippets trying to be synced (more than 10). Delete any unnecessary snippets.
* The personal access token was revoked or the GitHub account was deleted. Contact your GitHub account manager or contact GitHub support. In some cases, support may need to unlink your account and relink it with a new access token.
* Ensure that your GitHub account has at least one public repository.

If the issue persists, consider using  instead of linking to GitHub.

## Unlink a GitHub account

Remove access to the GitHub account by removing the link. When you remove the link to the GitHub account, any files referenced in your configuration remain unchanged, but they are no longer synchronized. If the account is relinked later, the referenced files reconnect to the repository and synchronization resumes.

To unlink your GitHub account:

1. Log in to your Tealium iQ Tag Management account.
1. In the admin menu, click **Manage GitHub Account**.
1. Click **Unlink Account**.

If you unlink your GitHub account, the referenced files remain unchanged in your configuration, but are now disconnected from the GitHub repository and can no longer be synchronized.

If the account is unlinked and then linked again, the referenced files reconnect to the repository and can be synchronized again.
