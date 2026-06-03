---
title: Single Sign-On (SSO) Certificate Status
description: This article describes how to view the status of a SAML 2.0 signing certificate.
url: https://docs.tealium.com/administration/security-access/single-sign-on/certificates/
---
## Certificate Status

From the **Manage SSO** screen, you can verify the status of your SAML 2.0 signing certificate under **Certificate Details**.

### Valid Status

After you upload a current metadata file or separate signing certificate, the **Certificate Expiration Date** is automatically populated and the **Certificate Status** is set to **Valid**. The **Certificate Status** automatically updates to indicate when the certificate has expired.

### Expired Status

When the certificate expires, the **Certificate Status** is set to **Expired** and the SSO login is unavailable until you upload a new signing certificate or an updated metadata file with a valid expiration date and save the configuration. 

To allow your users to access their accounts using the Tealium-initiated login, switch the **Authentication Mode** to **Test**. After you switch authentication modes, users must reset their Tealium login credentials before they can access their accounts.
