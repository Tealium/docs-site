---
title: Install
description: This article shows how to install Tealium in your Magento® 1 system using the Tealium iQ Tag Management Extension from the Magento Connect Extension Marketplace..
url: https://docs.tealium.com/platforms/magento-v1/install/
---
 This procedure is compatible for Magento versions 1.5 - 1.14.  For version 2.9&#43;, see [Tealium for Magento 2](/platforms/magento/install/) 

To add and enable the Tealium Extension in Magento Connect:

1. Log in to the Magento Extension Marketplace with your Magento account.
2. Search the marketplace for &#34;Tealium&#34;, then click **Tealium Tag Management** extension.
![](/images/platforms/magento-v1/magento1-1.png)
3. Click **Install Now**
![](/images/platforms/magento-v1/magento1-2.png)
4. Select the **Extension license terms** checkbox to agree to the terms, then click **Get Extension Key**.
![](/images/platforms/magento-v1/magento1-3.png)
5. The **Extension Key** will appear in the key field. Copy the Extension Key.
![](/images/platforms/magento-v1/magento1-4.png)
6. Navigate to **Magento Admin Panel &gt; System &gt; Magento Connect &gt; Magento Connect Manager**.
![](/images/platforms/magento-v1/magento1-5.png)
7. Under **Install New Extensions**, paste the Extension key you copied from the Magento Extension marketplace into the empty field and click **Install**.
![](/images/platforms/magento-v1/magento1-6.png)
8. Under **Extension dependencies**, click **Proceed**.
![](/images/platforms/magento-v1/magento1-7.png)
9. Wait for the following message to appear beneath the console: `Procedure completed. Please check the output frame for useful information and refresh the page to see the changes.`, then click **Return to Admin**.
![](/images/platforms/magento-v1/magento1-8.png)
10. Navigate to **Magento Admin Panel &gt; System &gt; Configuration**.
11. In the left-side navigation, under the **Tealium** heading, click **Tag Management**
![](/images/platforms/magento-v1/magento1-9.png)
12. Update the configuration settings with your account information:
    * **Enable**: `Yes`
    * **Account**: Your Tealium account
    * **Profile**: Your Tealium profile (default is `main`)
    * **Environment**: Your Tealium publish environment (`dev`, `qa`, or `prod`)
13. Click **Save Config**.
![](/images/platforms/magento-v1/magento1-10.png)
Congratulations! You have now installed Tealium into your Magento implementation. Be sure to [validate your installation](/platforms/javascript/install/#validate-installation).