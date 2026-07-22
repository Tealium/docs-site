---
title: Tealiumアカウントのシングルサインオンの構成
description: この記事では、アカウントのシングルサインオン（SSO）を構成する方法について説明します。
url: https://docs.tealium.com/ja/administration/security-access/single-sign-on/sso/
---
## 要件

* **アイデンティティプロバイダー**: SAML 2.0のサポート
* **Tealium**: アカウント管理者およびユーザー管理者の権限


<blockquote>
複数のTealiumアカウントにアクセスできる場合、SSOは主アカウントでのみ有効になります。
</blockquote>


## 仕組み

SSOは、一つの認証システムを使用して複数のアプリケーションにアクセスする安全な方法です。Tealiumは、SSOを実装するためにSecurity Assertion Markup Language（SAML）2.0をサポートし、あなたのIdentity Provider（IdP）構成のサービスプロバイダー（SP）として機能します。TealiumのSSOでSAMLを使用すると、ユーザーのアカウントを信頼できるエンタープライズIdPの下で保護することができます。

### サポートされているIdP

TealiumのSSOは、以下のIdPへの接続の構成手順をサポートしています：

* Amazon AWS
* ADFS（Active Directory）
* Azure
* Jumpcloud
* OneLogin
* Okta

Tealiumは、上記に記載されていないIdPプラットフォームへのSSO実装もサポートしています。ただし、他のプラットフォームからのIdP接続を構成するためには、追加のテストと構成時間が必要になる場合があります。他のIdPプラットフォームの実装に関する質問は、Tealiumサポートにお問い合わせください。

## Tealium SSOのログインプロセス

![](https://docs.tealium.com/images/iq-tag-management/administration/security/sso-configuration1.png)

Tealium SSOのログインプロセスは以下の手順に従います：

1. 次のログインオプションのいずれかを使用して、Tealium SSOを介してTealiumアカウントにログインします：
    * Tealium経由で `https://my.tealiumiq.com/login/sso`
    * カスタムTealium URL、例えば `https://my.tealiumiq.com/login/sso/customURL`
    * あなたのIdP経由
1. `my.tealiumiq.com`経由でログインすると、Tealium SSO SPはあなたのIdP接続情報を検証し、SAMLリクエストをあなたのIdPに送信し、あなたをIdPのログインページにリダイレクトします。あなたのIdP経由でログインする場合、このステップはスキップされます。
1. あなたのIdPはSAMLレスポンスをTealium SSO SPに送信し、Tealium SSO SPはログイン情報を検証します。
1. 新しいTealiumのログインセッションが作成されます。

## SSOの構成と管理



Tealium SSOの構成と管理を行うには：  
**管理メニュー > SSO（シングルサインオン）**に移動します。

IdPへの接続を確立し、認証をオンにすると、Tealium SSOはクライアントサイドとサーバーサイドの製品全体で有効になります。

Tealium SSOを4つのステップで構成します：

[ステップ1：IdPの構成](#step-1-configure-idp)  
[ステップ2：IdPへの接続](#step-2-connect-to-idp)  
[ステップ3：SSOのテスト](#step-3-test-your-sp-initiated-sso)  
[ステップ4：SSOの有効化](#step-4-activate-your-sp-initiated-sso)

### ステップ1：IdPの構成

以下の手順を完了して、新しいSAML SSO接続を作成します：

1. **管理メニュー > SSO（シングルサインオン）**に移動します。

![](https://docs.tealium.com/images/iq-tag-management/administration/security/sso-configuration2.png)

2. **新しいSAMLシングルサインオン（SSO）接続 > IdPの構成**画面で、Tealiumのメタデータファイルをコンピュータにダウンロードし、このファイルをあなたのIdPにインポートします。
3. あなたのIdPで新しいTealiumアプリケーションを作成し、あなたのIdPのメタデータファイルをダウンロードします。各IdPは、新しいSSO接続を作成するためのメタデータファイルにアクセスしてダウンロードするための異なる構成を必要とします。  
具体的なIdPの手順については、[IdP構成手順](#idp-instructions)を参照してください。  
あなたのIdPから以下の情報を確認してください：
    * SAMLメタデータファイル
    * あなたのIdPアカウントの管理者のメールアドレス
    * （オプション）SAML 2.0署名証明書。あなたの署名証明書はメタデータファイルの一部である可能性があります。
4. IdPを構成し、新しいSSO接続に必要な情報を収集した後、Tealiumの新しいSAMLシングルサインオン（SSO）接続ウィザードで**続行**をクリックします。

### IdPの手順

以下の表は、Tealium SSOと連携するためのIdPの構成方法をリストしています：

| IdP | カスタム構成情報 |
| --- | --- |
| Amazon AWS | [Amazon AWSのドキュメンテーション](https://docs.aws.amazon.com/singlesignon/latest/userguide/other-idps.html)の指示に従って、メタデータファイルをダウンロードしてTealiumにアップロードします。 |
| ADFS | [ADFS（Active Directory）IdPとのSSO構成](https://docs.tealium.com/sso-adfs-idp/)の指示に従って、メタデータファイルをダウンロードしてTealiumにアップロードします。 |
| Azure | [Azure IdPとのSSO構成](https://docs.tealium.com/sso-azure-idp/)の手順を完了して、Azureアカウントからメタデータファイルをダウンロードします。詳細については、[Azureのドキュメンテーション](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/add-application-portal-setup-sso)を参照してください。 |
| Jumpcloud |[Jumpcloudのドキュメンテーション](https://support.jumpcloud.com/support/s/article/getting-started-applications-saml-sso2)の指示に従って、メタデータファイルをダウンロードしてTealiumにアップロードします。あなたの構成では、以下の値が構成されていることを確認してください：<ul><li>構成には、`user.email`の値を持つ**email**属性が含まれています。</li></ul> |
| OneLogin | [OneLoginのドキュメンテーション](https://onelogin.service-now.com/support?id=kb_article&sys_id=b2c91143db109700d5505eea4b9619d5)の指示に従って、メタデータファイルをダウンロードしてTealiumにアップロードします。<br> あなたの構成では、以下の値が構成されていることを確認してください：<ul><li>ユーザーには`email`と構成された属性があります。</li><li>**Audience**は、Tealiumメタデータファイルの**AssertionConsumerService**ノードの**Location**属性と同じ値に構成されています。</li><li>**Recipient**は、Tealiumメタデータファイルの**AssertionConsumerService**ノードの**Location**属性と同じ値に構成されています。</li><li>**ACS (Consumer) URL Validator**は、**Tealium**メタデータファイルの**AssertionConsumerServicenode**の**Location**属性と同じ値に構成されています。すべてのスラッシュはバックスラッシュでエスケープする必要があります。</li><ul><li>例えば、**Location**属性が`https://prod-federation.auth.us-west-1.amazoncognito.com/saml2/idpresponse`の値を持つ場合、**URL Validator**は`https:\/\/prod-federation.auth.us-west-1.amazoncognito.com\/saml2\/idpresponse`であるべきです。</li></ul><li>**ACS (Consumer) URL**は、Tealiumメタデータファイルの**AssertionConsumerService**ノードの**Location**属性と同じ値に構成されています。</li><li>**Login URL**は`https://my.tealiumiq.com/login/sso/{ACCOUNT_NAME}`に構成されています。</li><li>**SAML Initiator**は**Service Provider**に構成されています。</li></ul> |
| Okta | [Okta IdPとのSSO構成](https://docs.tealium.com/sso-okta-idp/)の手順を完了して、メタデータファイルをダウンロードしてTealiumにアップロードします。詳細については、[Oktaのドキュメンテーション](https://help.okta.com/oie/en-us/Content/Topics/Apps/Apps_App_Integration_Wizard_SAML.htm)を参照してください。 |

### Federation ID

デフォルトでは、Tealiumはユーザーのメールアドレスを使用してログイン時にユーザーを識別します。Federation IDは、代替のユーザー識別子を許可します。

* Federation IDはSAML NameIDプロパティにマッピングされます。
* Federation IDがTealiumのユーザーに割り当てられていない場合、システムはデフォルトでEmail属性にマッチングします。詳細については、[ユーザーの編集](https://docs.tealium.com/users/#edit-a-user)を参照してください。
* あなたのSAML構成では、Email属性のマッピングが依然として必要です。


<blockquote>
あなたのアカウントでFederation IDを有効にするには、Tealiumサポートにお問い合わせください。
</blockquote>


### ステップ2：IdPへの接続

以下の手順を完了して、あなたのIdPに接続します：

1. **IdPへの接続**画面で、あなたのIdPからダウンロードしたSAMLメタデータファイルをアップロードします。接続が確立されると、**Identity Provider**フィールドはあなたのIdPの名前で自動的に入力されます。

![](https://docs.tealium.com/images/iq-tag-management/administration/security/sso-configuration3.png)
2. **IdP管理者メール**フィールドに、IdPアカウントの管理者のメールアドレスを入力します。
3. （オプション）IdPが別の署名証明書を提供している場合は、そのファイルを**IdP SAML 2.0署名証明書**の下にアップロードします。
4. **接続を確立**をクリックします。

### ステップ3：SP-initiated SSOをテストする

IdPに接続した後、SSOは**テスト**認証モードに構成されます。**テスト**モードでは、アカウント内のユーザーがTealium-initiatedログインとSP-initiatedログインのどちらを選択するかを選べます。このモードを使用して、認証モードを切り替える前にSP-initiatedログインを検証します。テストが成功するためには、次のURLを使用してログインすることを確認してください：`my.tealiumiq.com/login/sso`。


<blockquote>
IdPへの接続をテストするには、**証明書詳細**の下の**テストURL**をコピーしてブラウザに貼り付けます。
</blockquote>


### ステップ4：SP-initiated SSOを有効にする

ユーザーのSP-initiatedログイン体験に満足したら、以下の手順を完了してSP-initiated SSOを有効にします。

1. **SSOを管理**画面から、**認証モード**を**オン**に切り替えます。認証モードを**オン**に切り替えると、アカウント内のすべてのユーザーがSP-initiatedログインを通じて認証を行い、すべてのユーザーのTealium提供のログイン資格情報がリセットされます。
1. 確認ダイアログが表示されます。新しいSSOログイン手順を有効にする前に、SSO認証フローをテストし、アカウント内のユーザーに新しいSSOログイン手順について通知を提供することを確認します。ステートメントを確認した後、**SSOを有効にする**をクリックします。
1. **保存**をクリックします。


<blockquote>
認証モードを**テスト**から**オン**に切り替えると、SSO認証が有効になり、Tealiumログインが無効になります。Tealiumログインを再度有効にするには、認証モードを**テスト**に戻します。
</blockquote>


Tealium SSOがオンになると、Tealiumはユーザーのパスワードを管理しなくなります。Tealium内からユーザーを追加したり、権限を管理したりすることはできますが、パスワードや認証に関連する機能（例えば、[多要素認証](https://docs.tealium.com/multi-factor-authentication-mfa/)）はTealiumインターフェースを通じては利用できなくなります。ユーザーは企業のシステムを通じて認証し、カスタムSSO URLを使用してTealiumアカウントにアクセスします。

