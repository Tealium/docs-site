---
title: SSO configuration with ADFS (Active Directory) IdP
description: This article describes how to configure ADFS (Active Directory) to access and download a metadata file for creating a new Tealium SSO connection.
url: https://docs.tealium.com/administration/security-access/single-sign-on/adfs/
---
After you download the Tealium metadata file in [Set up your SSO: Step 1](), complete the following steps to configure ADFS (Active Directory) for use with Tealium SSO:

1. Launch the ADFS console.
1. Expand the **Trust Relationships** folder and select **Relying Party Trust**. In the **Relying Party Trusts** screen, click **Add Relying Party Trust**. 
![](/images/iq-tag-management/administration/security/adfs-console.png)
1. In the **Select Data Source** step, select **Import data about the relying party from a file** and upload the metadata file that you downloaded in [Set up your SSO: Step 1]().
1. In the **Specify Display Name** step, enter a descriptive name for your connection. For example, `Tealium`.![](/images/iq-tag-management/administration/security/adfs-name-trust.png)
1. In the **Choose Issuance Authorization Rules** screen, select **Permit all users to access this relying party**.
![](/images/iq-tag-management/administration/security/adfs-issuance-rules.png)
1. Click **Next** to view a summary of your configuration.
1. Click **Next**. In the **Finish** step, ensure the **Open the Edit Claim Rules dialog for this relying party trust when the wizard closes** is checked.
![](/images/iq-tag-management/administration/security/adfs-edit-claim-rules.png)
1. After you close the setup wizard, the **Edit Claim Rules** configuration window will open. Click **Add Rule**.
![](/images/iq-tag-management/administration/security/adfs-edit-claim-rules-utility.png)
1. In the **Choose Rule Type** step, select the **Send LDAP Attributes as Claims** claim rule template. This setting will gather only claims from the Active Directory. Click **Next**.
![](/images/iq-tag-management/administration/security/adfs-choose-rule-type.png)
1. In the **Configure Claim Rule** step with the following settings:
    * **Claim rule name**: `AD Attributes`
    * **Attribute store**: `Active Directory`
    * **E-mail-Addresses**: `email`
    * **SAM-Account-Name**: `Name ID`
![](/images/iq-tag-management/administration/security/adfs-edit-rule.png)
1. Click **OK**.
1. After you complete configuring your claim rule, you will return to the **Relying Party Trust** screen. Right-click the connection you just created to view the connection properties.
1. Click the **Encryption** tab and click **Remove** to download the encryption certificate.
![](/images/iq-tag-management/administration/security/adfs-connection-properties.png)
1. Download the SAML metadata document for your ADFS federation server. You will use this file to complete the [Tealium SSO configuration](). The following is an example metadata URL:
`https://&lt;yourservername&gt;/FederationMetadata/2007-06/FederationMetadata.xml`