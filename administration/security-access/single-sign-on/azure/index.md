---
title: SSO configuration with Azure IdP
description: This article describes how to configure Azure to access and download a metadata file for creating a new Tealium SSO connection.
url: https://docs.tealium.com/administration/security-access/single-sign-on/azure/
---
After you download the Tealium metadata file in [Set up your SSO: Step 1](https://docs.tealium.com/set-up-single-sign-on/#step-1-configure-your-idp), complete the following steps to configure Azure for use with Tealium SSO:

1. Log in to your Azure account and go to **Identity > Applications > Enterprise applications > All applications**.
1. Click **+ New Application**.
1. Click **+ Create your own application**.
1. Enter an application name. We recommend giving your application a name that lets others know what it was created for. For example, `tealium`, `tealium-iq-user-federation`, etc.
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-application-name.png)
1. Ensure that **Integrate any other application you don't find in the gallery (Non-gallery)** is selected.
1. Click **Create**.
1. Go to **Manage > Single sign-on**.
1. Select the SAML sign-on method. 
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-saml.png)
1. In the **Set up Single Sign-On with SAML** screen, click **Upload metadata file**. Upload the metadata file that you downloaded in [Set up your SSO: Step 1](https://docs.tealium.com/set-up-single-sign-on/#step-1-configure-your-idp).
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-metadata.png)
1. After you upload the Tealium metadata file, the basic SAML configuration information from the uploaded file is displayed. You do not need to change these settings.
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-saml-configuration.png)
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-attributes-claims.png)
1. Click **Save**.
1. In the **Test single sign-on** window, click **No, I'll test later**.
1. In the **Set up Single Sign-On with SAML** screen, go to the **Attributes & Claims** section and click the edit icon.
1. Click **+ Add new claim** and add a new claim with the following settings:
    * **Claim name**: `email`
    * **Type**: `SAML`
    * **Value**: `user.mail`
1. In the **Set up Single Sign-On with SAML** screen, go to the **SAML Certificates** section and download the **Federation Metadata XML** file.
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-download-metadata.png)
1. Save this file to your computer. Use this file to complete the [Tealium SSO configuration](https://docs.tealium.com/set-up-single-sign-on/#step-2-connect-to-your-idp).

The following example shows a working configuration:

![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-attributes-and-claims.png)