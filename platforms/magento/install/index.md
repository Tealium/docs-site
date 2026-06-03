---
title: Install
description: This article shows how to install Tealium in your Magento® 2 system using the Tealium iQ Tag Management extension from the Magento Marketplace.
url: https://docs.tealium.com/platforms/magento/install/
---
## Requirements

The following items are required:

* An active Tealium iQ Tag Management account
* Your Tealium account ID
* Your Tealium profile name
* The Tealium environment to use (prod, qa, dev, or custom)

## How it Works

The Tealium for Magento extension provides a robust implementation of minimal boilerplate code to implement and extend universal data objects (UDOs) across various page types. Leveraging Magento&#39;s prescribed dependency injection and layout systems, the module simplifies the process of creating and extending UDOs.

The extension includes a simple script that scaffolds out boilerplate code when creating a new UDO. It lets you specify any UDOs that it may extend and which pages of the site the new UDO should appear on. When finished, you will have a scaffolded template that needs to be filled in with any data-specific logic for your particular use case.

For more information about Magento, see [Magento Documentation](http://devdocs.magento.com/).

## Install

 The following prodecure uses commands for an Ubuntu server environment. For other server environments, adjust the commands accordingly. 

To install Tealium in your Magneto system:

1. **Enable maintenance mode**: Enable maintenance mode before installing the extension to avoid any user issues. To enable maintenance mode, run the following command:
   ```
   php bin/magento maintenance:enable
   ```
1. **Copy the Tealium folder**: Copy the Tealium folder from [GitHub](https://github.com/Tealium/integration-magento2/tree/DependencyUpdates) to `app/code/Tealium/Tags` within your Magento folder. If `app/code/Tealium/Tags` doesn’t exist, create it.
1. **Update changes**: Run the following commands to update changes:
   ```
   php bin/magento setup:upgrade
   php bin/magento setup:di:compile
   php bin/magento setup:static-content:deploy -f
   php bin/magento cache:flush
   ```
1. **Disable maintenance mode**: After the installation is complete, disable maintenance mode to allow users to access the site. To disable maintenance mode, run the following command:
   ```
   php bin/magento maintenance:disable
   ```

## Configure

To configure Magento 2, perform the following steps:

1. In the admin panel, go to **Stores &gt; Configuration &gt; Tealium &gt; Tag Management**.
1. Enable the extension and enter your Tealium iQ account, profile, and environment.
1. If you are using a first-party domain, enter your client domain in the **First Party Domain** field.
1. To allow plain text customer email addresses, select **No** under the **Allow plain text customer email** drop-down list. Otherwise, email addresses will be encrypted using a SHA-256 hash.

## Tests

To test your Tealium and Magento configuration to ensure that they are working properly together, use the following tests:

* [Code Sniffer](https://developer.adobe.com/commerce/marketplace/guides/sellers/code-sniffer/)
* [Installation and Varnish Tests](https://developer.adobe.com/commerce/marketplace/guides/sellers/installation-and-varnish-tests/)
* [MFTF Commerce-supplied Tests](https://developer.adobe.com/commerce/marketplace/guides/sellers/mftf-magento/)
