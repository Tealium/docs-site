---
title: ADFS（アクティブディレクトリ）IdPとのSSO設定
description: この記事では、新しいTealium SSO接続を作成するためのメタデータファイルにアクセスし、ダウンロードするためのADFS（アクティブディレクトリ）の設定方法について説明します。
url: https://docs.tealium.com/ja/administration/security-access/single-sign-on/adfs/
---
[SSOの設定：ステップ1]()でTealiumのメタデータファイルをダウンロードした後、以下の手順を完了してADFS（アクティブディレクトリ）をTealium SSOで使用するように設定します：

1. ADFSコンソールを起動します。
1. **Trust Relationships**フォルダを展開し、**Relying Party Trust**を選択します。**Relying Party Trusts**画面で、**Add Relying Party Trust**をクリックします。 
![](/images/iq-tag-management/administration/security/adfs-console.png)
1. **Select Data Source**ステップで、**Import data about the relying party from a file**を選択し、[SSOの設定：ステップ1]()でダウンロードしたメタデータファイルをアップロードします。
1. **Specify Display Name**ステップで、接続の説明的な名前を入力します。例えば、`Tealium`。![](/images/iq-tag-management/administration/security/adfs-name-trust.png)
1. **Choose Issuance Authorization Rules**画面で、**Permit all users to access this relying party**を選択します。
![](/images/iq-tag-management/administration/security/adfs-issuance-rules.png)
1. **Next**をクリックして設定の概要を表示します。
1. **Next**をクリックします。**Finish**ステップで、**Open the Edit Claim Rules dialog for this relying party trust when the wizard closes**がチェックされていることを確認します。
![](/images/iq-tag-management/administration/security/adfs-edit-claim-rules.png)
1. セットアップウィザードを閉じると、**Edit Claim Rules**設定ウィンドウが開きます。**Add Rule**をクリックします。
![](/images/iq-tag-management/administration/security/adfs-edit-claim-rules-utility.png)
1. **Choose Rule Type**ステップで、**Send LDAP Attributes as Claims**クレームルールテンプレートを選択します。この設定では、アクティブディレクトリからのクレームのみが収集されます。**Next**をクリックします。
![](/images/iq-tag-management/administration/security/adfs-choose-rule-type.png)
1. 以下の設定で**Configure Claim Rule**ステップを進めます：
    * **Claim rule name**: `AD Attributes`
    * **Attribute store**: `Active Directory`
    * **E-mail-Addresses**: `email`
    * **SAM-Account-Name**: `Name ID`
![](/images/iq-tag-management/administration/security/adfs-edit-rule.png)
1. **OK**をクリックします。
1. クレームルールの設定が完了したら、**Relying Party Trust**画面に戻ります。作成したばかりの接続を右クリックして接続プロパティを表示します。
1. **Encryption**タブをクリックし、**Remove**をクリックして暗号化証明書をダウンロードします。
![](/images/iq-tag-management/administration/security/adfs-connection-properties.png)
1. ADFS連携サーバーのSAMLメタデータドキュメントをダウンロードします。このファイルを使用して、[Tealium SSO設定]()を完了します。以下はメタデータURLの例です：
`https://&lt;yourservername&gt;/FederationMetadata/2007-06/FederationMetadata.xml`
