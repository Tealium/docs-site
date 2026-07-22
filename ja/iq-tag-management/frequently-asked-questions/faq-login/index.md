---
title: Tealiumプラットフォームにログインする方法は？
description: この記事では、Tealiumプラットフォームにログインする方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/frequently-asked-questions/faq-login/
---
Tealiumのメインログインページは[https://my.tealiumiq.com](https://my.tealiumiq.com)にあります。

## メールアドレスとパスワード

メールアドレスとパスワードでアカウントにログインするには：

1. **メール**フィールドにメールアドレスを入力します。
1. **パスワード**フィールドにパスワードを入力します。
    + パスワードを忘れた場合は、**パスワードを忘れた方はこちら**をクリックします。詳細は[パスワードのリセット方法は？](https://docs.tealium.com/ja/iq-tag-management/frequently-asked-questions/how-do-i-reset-my-password/)を参照してください。
1. **ログイン**をクリックします。

### マルチファクタ認証

マルチファクタ認証（MFA）は、ログインにスマートフォンやブラウザアプリなどの2つ目の認証方法を必要とするセキュリティ方法です。アカウント管理者は、アカウントにログインするためにMFAの使用を要求する場合があります。

MFAが有効なアカウントにログインする方法については、[マルチファクタ認証](https://docs.tealium.com/multi-factor-authentication-mfa/)を参照してください。

## シングルサインオン

シングルサインオン（SSO）は、一つのアイデンティティ管理ソリューションを使用して複数のアプリケーションにアクセスする安全な方法です。主要なアカウントのSSOプロバイダにログインすると、Tealiumプラットフォーム上のすべてのアカウントにアクセスできます。

[組織のSSO用のアイデンティティ管理ソリューション](https://docs.tealium.com/set-up-single-sign-on/)は、サードパーティのプロバイダを使用するか、自己ホスト型の認証システムを使用することができます。

TealiumのSSOユーザーの大部分は、まず組織のアイデンティティ管理ソリューションにログインしますが、以下のようにSSOを使用して直接Tealiumのプラットフォームにログインすることも可能です：

1. 次のログインページのいずれかに移動します：
    * メインのTealiumログインページ[https://my.tealiumiq.com](https://my.tealiumiq.com)で**SSOログイン**をクリックします。
    * SSOログインページ[https://my.tealiumiq.com/login/sso/?ssoMethod=accountNameSSO](https://my.tealiumiq.com/login/sso/?ssoMethod=accountNameSSO)。
1. 主要なアカウント名を覚えている場合は、**アカウント名**フィールドに主要なアカウント名を入力し、**次へ**をクリックします。
    - 現在SSOサービスで認証されていない場合、そのログイン画面にリダイレクトされます。
1. 主要なアカウント名を覚えていない場合：
     1. **アカウント名を忘れた方はこちら**をクリックします。
     1. **メール**フィールドにメールアドレスを入力します。
     1. **送信**をクリックします。
     1. システムは主要なアカウント名を含むメールを送信します。
