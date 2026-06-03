---
title: SSO configuration with Okta IdP
description: This article describes how to configure Okta to access and download a metadata file for creating a new Tealium SSO connection.
url: https://docs.tealium.com/administration/security-access/single-sign-on/okta/
---
After you download the Tealium metadata file in [Set up your SSO: Step 1](), complete the following steps to configure Okta for use with Tealium SSO:

1. Locate the Tealium `metadata.xml` you downloaded and open the file locally. You will need to refer to this file in the Okta configuration.  
2. Log in to your Okta account and navigate to **Applications &gt; Applications** and click **Create App Integration**.
![](/images/iq-tag-management/administration/security/okta-applications.png)
3. Select the **SAML 2.0** sign-in method.
![](/images/iq-tag-management/administration/security/okta-new-app-integration.png)
4. In the **Create SAML Integration** screen, enter the integration name in the **App name** field. Click **Next**.
![](/images/iq-tag-management/administration/security/okta-create-saml-integration.png)
5. In the **Configure SAML** screen, enter the following values as listed in the Tealium metadata file you downloaded:
    * **Single sign-on URL**: In `AssertionConsumerService`, use the `Location` value: `https://prod-federation.auth.us-west-1.amazoncognito.com/saml2/idpresponse`.
    * **Audience URI (SP Entity ID)**: In `EntityDescription`, use the `entityID` value: `urn:amazon:cognito:sp:us-west-1_FGJFGdCYT`.
6. Configure the following additional settings:
    * **Name ID format**: `EmailAddress`
    * **Application username**: `Email`
    * **Update application username on**: `Create and update`
![](/images/iq-tag-management/administration/security/okta-saml-settings.png)
7. In the **Attributes Statements (Optional)** section, add an attribute statement with the following settings:
    * **Name**: `email`
    * **Name format**: **Unspecified**
    * **Value**: `user.email`
![](/images/iq-tag-management/administration/security/okta-attribute-settings.png)
8. (Optional) Select the business purpose for your Okta configuration. Providing Okta with background information about your app configuration allows the IdP to provide relevant support for your SAML integration.
![](/images/iq-tag-management/administration/security/okta-feedback.png)
9. Click **Finish**.
10. In the **Sign On** tab, copy the **Metadata URL**.
![](/images/iq-tag-management/administration/security/okta-metadata-details.png)
12. Save this file to your computer. You will use this file to complete the [Tealium SSO configuration]().
