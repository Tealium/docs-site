---
title: About linking to GitHub
description: This article describes how to create a secure link between your GitHub account and your iQ Tag Management account using an access token.
url: https://docs.tealium.com/iq-tag-management/administration/linking-to-github/about/
---
Once linked, use the [Advanced JavaScript Code extension]() to reference and synchronize files from a GitHub repository. Your code remains safely stored in GitHub, but is available to publish in your iQ Tag Management configuration.

## Requirements

#### GitHub requirements

* A GitHub account:
  * With at least one public repository, which can be empty.
  * With a [GitHub personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). For GitHub Enterprise Server, use a fine-grained personal access token authorized by your organization.
  * Hosted at `github.com` or a self-hosted GitHub Enterprise Server.
* Working knowledge of GitHub and experience working with GitHub repositories.

 If you do not use GitHub or do not have a public repository, we recommend that you use the  instead of linking to GitHub. 

#### Tealium requirements

* The Manage Account permission in your Tealium account.

## How it works

The GitHub integration creates a seamless workflow between your code management process in GitHub and publishing in iQ Tag Management. Use your GitHub username and [personal access token](https://github.com/settings/tokens) to create a link to your GitHub account. Only one link is needed for all the profiles in your Tealium account.

Your GitHub account must have at least one public or private repository for the link to succeed.

Once the account is linked, the JavaScript files in your repositories are available to be referenced in your iQ Tag Management configuration. When a file from your GitHub repository is referenced it remains safely in your GitHub repository, but the code is now available to publish as part of your iQ Tag Management configuration.

As you commit changes to the referenced files in your GitHub repository, you must synchronize those files in iQ Tag Management to get the latest versions. When you synchronize the referenced files, you will have unsaved changes that must be saved and published.

## Supported features

The following features support the GitHub integration:

* [Advanced JavaScript Code extension]()
