---
title: Manage First-Party Domains
description: This article provides information about adding domains to a certificate, removing domains, and viewing contact information for domains.
url: https://docs.tealium.com/iq-tag-management/administration/first-party-domains/manage/
---
## Configure first-party domains


<blockquote>
For server-side data collection, the domain certificates are configured and stored in the Tealium endpoint in the region you select during configuration. If the selected region is different from the region for the profile, the event and visitor data is collected in the first-party domain region and forwarded to the region configured for the profile.
</blockquote>


Use the following steps to configure first-party domains:

1. In the admin menu, click **First-Party Domains**.
1. Under **Server-Side Data Collection/DLE** or **Client-Side Delivery**, click **Configure Certificate**.
1. Select the region in which most of your data collection occurs.
1. Select one of the following:
    * **Tealium-managed**: Tealium generates and manages the certificates.
    * **Self-managed**: Provide your own certificate files. For information about the requirements and format for certificate files, see [Self-managed certificates](https://docs.tealium.com/about-first-party-domains/#self-managed-certificates).
1. If you selected **Self-managed**, upload the following files:
    * Certificate (Required)
    * Private Key (Required)
    * Certificate Chain (Optional)
1. Select one of the following methods to validate domain ownership:
    * **DNS Validation**
    * **Email Validation**
1. In the **Add Domains** section, enter a subdomain name, omitting `https://` and the ending slash. 
    For example, `collect.example.com` or `cdp.example.com`.
1. To add another domain, click **+ Add Domain**.  
First-party domains apply to all profiles in your account. Enter a subdomain for each site managed by this account.

### Validation confirmation

Click **I Agree** to give Tealium permission to manage certificates for the provided domains and to certify you own and manage these domains, then click **Save**.

----

#### **DNS validation**

The following message appears when you choose DNS validation:

> Pending validation. Add the required DNS records for each domain, then wait for DNS to propagate.

The temporary A or CNAME records (one for each domain) used for validation are displayed. Add these temporary A or CNAME records to your DNS configuration.

After you add the validation A or CNAME records to your DNS configuration and the validation process is completed (this can take several hours), the permanent A or CNAME records for your domains are displayed. Add these permanent A or CNAME records to your DNS configuration.


<blockquote>
Your final DNS configuration must include the validation and permanent A or CNAME records. The validation records are used when you add domains to a certificate and for auto-renewal of the certificate.
</blockquote>


----

#### **Email validation**

The following message appears when you choose email validation:  

> Pending validation. Confirm the validation email sent for each domain, or resend the email if needed.

You will receive an email from Amazon Web Services (one message for each domain) containing a validation token that expires in 72 hours. To complete the validation process, you must respond to the email message for each domain. If you did not receive the email or if the token has expired, a separate **Resend Email** button is available.

----

When the domain status in the **First-Party Domains Overview** changes to **Issued**, your domains are ready to use.

Validation must occur within 72 hours. If the validation period expires, request a new certificate for the same subdomain. The DNS validation records are the same for subsequent requests of the same subdomain.

After the domain status changes to **Issued**, you must update your endpoint configuration to use first-party domains with Tealium iQ Tag Management. For more information, see [Update endpoint configurations]().

### Validation failure

If validation fails, the domain status changes to **Failed** and a message appears with details about the failure:

> We couldn’t create your certificate because your domains do not include Amazon as a certificate authority in DNS. Add Amazon in CAA records in DNS, then Retry. See affected domains in Manage Domains.

If you see this message, add Amazon in CAA records in your DNS configuration, then click **Retry** to validate the domain and generate the certificate again.

For more information, see [About first-party domains](https://docs.tealium.com/about-first-party-domains/#tealium-managed-certificates).

## Add a domain to a certificate

To add domains to a certificate, use the following steps:

1. In the admin menu, click **First-Party Domains**, then select a domain.
1. Click **Manage Domains**, then click **Edit Domains**.
1. Click **+ Add Domain**.  
An empty row is added to the list of domains. When the maximum number of domains for the account is reached, **+ Add Domain** is disabled.  
    ![](https://docs.tealium.com/images/iq-tag-management/empty-domain-row-added.png)
1. Enter the URL for the new domain and click **Save**.  
When the certificate has been updated, the response varies depending on the validation method and the domain type (client-side or server-side).  
    * **DNS Validation**:  
    ![](https://docs.tealium.com/images/iq-tag-management/domains-updated.png)  
    * **Email Validation**:  
    ![](https://docs.tealium.com/images/iq-tag-management/domains-updated-email-validation.png)  
    When the domain status changes to **Issued**, your domains are ready to use.

## Remove a domain

Use the following steps to remove a domain:

1. In the admin menu, click **First-Party Domains**, then select a domain.
1. Click **Manage Domains**, then click **Edit Domains**.
1. Click the remove icon for the domain.  

## View contact information for a domain

To view the contact information for a domain, go to **First-Party Domains**, click a domain, then click **View Contact Info**.

## Certificate expiration

### Self-managed

When a self-managed certificate is nearing expiration or has expired, a message appears with details about the expiration:

> Certificate expiring soon. Renew this certificate with your certificate authority, then upload the new certificate and private key before the expiration date.

> Certificate expired. Renew this certificate with your certificate authority, then upload the new certificate and private key to restore First‑Party Domains.

To avoid service disruption, you must request a new certificate for the same subdomain before the expiration date. The DNS validation records are the same for subsequent requests of the same subdomain.

In the message, click **Provide Certificate** to upload the certificate. The new certificate replaces the previous one. If the previous certificate has not expired, there should be no downtime. If the previous certificate has expired, there may be a few hours delay while the certificate propagates to DNS servers.

### Tealium-managed

Usually when a Tealium-managed certificate expires, it is immediately replaced with a new certificate. However, you may see the following message:

> Certificate expired. Auto‑renewal failed because DNS records changed. Restore the validation records for each domain (see View DNS Records), then Retry to issue a new certificate.

This message appears because the DNS records for the domain were changed, which caused the auto-renewal process to fail. To resolve this issue, restore the validation records for each domain, then click **Retry** to issue a new certificate.