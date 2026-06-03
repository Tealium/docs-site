---
title: SSO configuration with Azure IdP
description: This article describes how to configure Azure to access and download a metadata file for creating a new Tealium SSO connection.
url: https://docs.tealium.com/administration/security-access/single-sign-on/azure/
---
After you download the Tealium metadata file in [Set up your SSO: Step 1](), complete the following steps to configure Azure for use with Tealium SSO:

1. Log in to your Azure account and go to **Identity &gt; Applications &gt; Enterprise applications &gt; All applications**.
1. Click **&#43; New Application**.
1. Click **&#43; Create your own application**.
1. Enter an application name. We recommend giving your application a name that lets others know what it was created for. For example, `tealium`, `tealium-iq-user-federation`, etc.
![](/images/iq-tag-management/administration/security/azure-application-name.png)
1. Ensure that **Integrate any other application you don&#39;t find in the gallery (Non-gallery)** is selected.
1. Click **Create**.
1. Go to **Manage &gt; Single sign-on**.
1. Select the SAML sign-on method. 
![](/images/iq-tag-management/administration/security/azure-saml.png)
1. In the **Set up Single Sign-On with SAML** screen, click **Upload metadata file**. Upload the metadata file that you downloaded in [Set up your SSO: Step 1]().
![](/images/iq-tag-management/administration/security/azure-metadata.png)
1. After you upload the Tealium metadata file, the basic SAML configuration information from the uploaded file is displayed. You do not need to change these settings.
![](/images/iq-tag-management/administration/security/azure-saml-configuration.png)
![](/images/iq-tag-management/administration/security/azure-attributes-claims.png)
1. Click **Save**.
1. In the **Test single sign-on** window, click **No, I&#39;ll test later**.
1. In the **Set up Single Sign-On with SAML** screen, go to the **Attributes &amp; Claims** section and click the edit icon.
1. Click **&#43; Add new claim** and add a new claim with the following settings:
    * **Claim name**: `email`
    * **Type**: `SAML`
    * **Value**: `user.mail`
1. In the **Set up Single Sign-On with SAML** screen, go to the **SAML Certificates** section and download the **Federation Metadata XML** file.
![](/images/iq-tag-management/administration/security/azure-download-metadata.png)
1. Save this file to your computer. Use this file to complete the [Tealium SSO configuration]().

The following example shows a working configuration:

![](/images/iq-tag-management/administration/security/azure-attributes-and-claims.png)