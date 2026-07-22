---
title: Azure IdPとのSSO構成
description: この記事では、新しいTealium SSO接続を作成するためのメタデータファイルにアクセスしてダウンロードするためにAzureを構成する方法について説明します。
url: https://docs.tealium.com/ja/administration/security-access/single-sign-on/azure/
---
[SSOの構成：ステップ1](https://docs.tealium.com/set-up-single-sign-on/#step-1-configure-your-idp)でTealiumのメタデータファイルをダウンロードした後、以下の手順でAzureをTealium SSOで使用するように構成します：

1. Azureアカウントにログインし、**Identity > Applications > Enterprise applications > All applications**に移動します。
1. **+ New Application**をクリックします。
1. **+ Create your own application**をクリックします。
1. アプリケーション名を入力します。他のユーザーがその目的を理解できるような名前を付けることをお勧めします。例えば、`tealium`, `tealium-iq-user-federation`などです。
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-application-name.png)
1. **Integrate any other application you don't find in the gallery (Non-gallery)**が選択されていることを確認します。
1. **Create**をクリックします。
1. **Manage > Single sign-on**に移動します。
1. SAMLサインオン方法を選択します。
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-saml.png)
1. **Set up Single Sign-On with SAML**画面で、**Upload metadata file**をクリックします。[SSOの構成：ステップ1](https://docs.tealium.com/set-up-single-sign-on/#step-1-configure-your-idp)でダウンロードしたメタデータファイルをアップロードします。
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-metadata.png)
1. Tealiumのメタデータファイルをアップロードすると、アップロードされたファイルから基本的なSAML構成情報が表示されます。これらの構成を変更する必要はありません。
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-saml-configuration.png)
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-attributes-claims.png)
1. **Save**をクリックします。
1. **Test single sign-on**ウィンドウで、**No, I'll test later**をクリックします。
1. **Set up Single Sign-On with SAML**画面で、**Attributes & Claims**セクションに移動し、編集アイコンをクリックします。
1. **+ Add new claim**をクリックし、以下の構成で新しいクレームを追加します：
    * **Claim name**: `email`
    * **Type**: `SAML`
    * **Value**: `user.mail`
1. **Set up Single Sign-On with SAML**画面で、**SAML Certificates**セクションに移動し、**Federation Metadata XML**ファイルをダウンロードします。
![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-download-metadata.png)
1. このファイルをコンピュータに保存します。このファイルを使用して、[Tealium SSO構成](https://docs.tealium.com/set-up-single-sign-on/#step-2-connect-to-your-idp)を完了します。

以下の例は、動作する構成を示しています：

![](https://docs.tealium.com/images/iq-tag-management/administration/security/azure-attributes-and-claims.png)