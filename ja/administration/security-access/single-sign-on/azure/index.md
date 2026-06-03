---
title: Azure IdPとのSSO構成
description: この記事では、新しいTealium SSO接続を作成するためのメタデータファイルにアクセスしてダウンロードするためにAzureを構成する方法について説明します。
url: https://docs.tealium.com/ja/administration/security-access/single-sign-on/azure/
---
[SSOの構成：ステップ1]()でTealiumのメタデータファイルをダウンロードした後、以下の手順でAzureをTealium SSOで使用するように構成します：

1. Azureアカウントにログインし、**Identity &gt; Applications &gt; Enterprise applications &gt; All applications**に移動します。
1. **&#43; New Application**をクリックします。
1. **&#43; Create your own application**をクリックします。
1. アプリケーション名を入力します。他のユーザーがその目的を理解できるような名前を付けることをお勧めします。例えば、`tealium`, `tealium-iq-user-federation`などです。
![](/images/iq-tag-management/administration/security/azure-application-name.png)
1. **Integrate any other application you don&#39;t find in the gallery (Non-gallery)**が選択されていることを確認します。
1. **Create**をクリックします。
1. **Manage &gt; Single sign-on**に移動します。
1. SAMLサインオン方法を選択します。
![](/images/iq-tag-management/administration/security/azure-saml.png)
1. **Set up Single Sign-On with SAML**画面で、**Upload metadata file**をクリックします。[SSOの構成：ステップ1]()でダウンロードしたメタデータファイルをアップロードします。
![](/images/iq-tag-management/administration/security/azure-metadata.png)
1. Tealiumのメタデータファイルをアップロードすると、アップロードされたファイルから基本的なSAML構成情報が表示されます。これらの構成を変更する必要はありません。
![](/images/iq-tag-management/administration/security/azure-saml-configuration.png)
![](/images/iq-tag-management/administration/security/azure-attributes-claims.png)
1. **Save**をクリックします。
1. **Test single sign-on**ウィンドウで、**No, I&#39;ll test later**をクリックします。
1. **Set up Single Sign-On with SAML**画面で、**Attributes &amp; Claims**セクションに移動し、編集アイコンをクリックします。
1. **&#43; Add new claim**をクリックし、以下の構成で新しいクレームを追加します：
    * **Claim name**: `email`
    * **Type**: `SAML`
    * **Value**: `user.mail`
1. **Set up Single Sign-On with SAML**画面で、**SAML Certificates**セクションに移動し、**Federation Metadata XML**ファイルをダウンロードします。
![](/images/iq-tag-management/administration/security/azure-download-metadata.png)
1. このファイルをコンピュータに保存します。このファイルを使用して、[Tealium SSO構成]()を完了します。

以下の例は、動作する構成を示しています：

![](/images/iq-tag-management/administration/security/azure-attributes-and-claims.png)