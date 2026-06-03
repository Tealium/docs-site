---
title: Okta IdPとのSSO設定
description: この記事では、新しいTealium SSO接続を作成するためのメタデータファイルにアクセスし、ダウンロードするためのOktaの設定方法について説明します。
url: https://docs.tealium.com/ja/administration/security-access/single-sign-on/okta/
---
[SSOの設定: ステップ1]()でTealiumのメタデータファイルをダウンロードした後、以下の手順を完了してTealium SSOでのOktaの使用を設定します：

1. ダウンロードしたTealiumの `metadata.xml` を探し、ローカルでファイルを開きます。このファイルはOktaの設定で参照する必要があります。
2. Oktaアカウントにログインし、**Applications &gt; Applications**に移動して**Create App Integration**をクリックします。
![](/images/iq-tag-management/administration/security/okta-applications.png)
3. **SAML 2.0**のサインイン方法を選択します。
![](/images/iq-tag-management/administration/security/okta-new-app-integration.png)
4. **Create SAML Integration**画面で、**App name**フィールドに統合名を入力します。**Next**をクリックします。
![](/images/iq-tag-management/administration/security/okta-create-saml-integration.png)
5. **Configure SAML**画面で、ダウンロードしたTealiumのメタデータファイルに記載されている値を以下のように入力します：
    * **Single sign-on URL**: `AssertionConsumerService`で、`Location`の値を使用します：`https://prod-federation.auth.us-west-1.amazoncognito.com/saml2/idpresponse`。
    * **Audience URI (SP Entity ID)**: `EntityDescription`で、`entityID`の値を使用します：`urn:amazon:cognito:sp:us-west-1_FGJFGdCYT`。
6. 以下の追加設定を行います：
    * **Name ID format**: `EmailAddress`
    * **Application username**: `Email`
    * **Update application username on**: `Create and update`
![](/images/iq-tag-management/administration/security/okta-saml-settings.png)
7. **Attributes Statements (optional)**セクションで、以下の設定を持つ属性ステートメントを追加します：
    * **Name**: `email`
    * **Name format**: **Unspecified**
    * **Value**: `user.email`
![](/images/iq-tag-management/administration/security/okta-attribute-settings.png)
8. (オプション) Okta設定のビジネス目的を選択します。アプリ設定に関する背景情報をOktaに提供することで、IdPはSAML統合に関する関連サポートを提供することができます。
![](/images/iq-tag-management/administration/security/okta-feedback.png)
9. **Finish**をクリックします。
10. **Sign On**タブで、**Metadata URL**をコピーします。
![](/images/iq-tag-management/administration/security/okta-metadata-details.png)
12. このファイルをコンピュータに保存します。このファイルは、[Tealium SSO設定]()を完了するために使用します。

