---
title: マルチファクター認証 (MFA)
description: マルチファクター認証は、ログインにスマートフォンやブラウザアプリなどの2つ目の認証方法を必要とするセキュリティ方法です。
url: https://docs.tealium.com/ja/administration/security-access/mfa/
---
## 必要条件

* **スマートフォン**  
iOS、Android、Windowsが対応しています。
* **認証アプリ**  
MFAは、[Google Authenticator](https://googleauthenticator.net/)や[Windows Authenticator](https://www.microsoft.com/en-us/store/apps/authenticator/9wzdncrfj3rj)などのサードパーティアプリケーションと連携して、パスワード以上の保護を提供します。これらのアプリケーションは、あなたのアカウント専用の一回限りの6桁のセキュリティトークンをスマートフォン上で生成します。スマートフォンプラットフォームと互換性のある認証アプリケーションをインストールしてください。
* **バーコードリーダーアプリ**  
Androidデバイスをお持ちの場合は、認証アプリケーションをアカウントと同期させる際に必要となるQRコードを読み取るための組み込みアプリがあることを確認してください。これはiPhoneには適用されません。
* **ブラウザのサポート**  
MFAはiPhone、Android、Windowsのスマートフォンのみでサポートされています。あなたのスマートフォンがこれらのいずれでもない場合は、[Authenticator Chrome Extension](https://chrome.google.com/webstore/detail/authenticator/bhghoamapcdpbohphigoooaddinpkbai)を使用してChromeブラウザからトークンを受け取ることができます。

## 仕組み

MFAは、主アカウントや割り当てられた他のアカウントで有効にされている場合、ログインプロセス中に必要となります。MFAは認証アプリケーションと連携して、ログインリクエストを2ステップで確認します。

MFAが有効なアカウントにサインインする際には、以下の情報を提供するよう求められます：

* **ログイン認証情報**  
あなたのアカウントのユーザー名とパスワード
* **セキュリティコード**  
スマートフォン上の認証アプリによって生成される6桁のトークン

## アカウントのMFAを有効または無効にする

MFAの有効化または無効化には、[アカウントの管理]()の権限が必要です。この構成を切り替える権限はアカウント管理者のみが持っています。

### MFAの有効化

アカウントのMFAを有効にするには、以下の手順を使用します：

1. [https://my.tealiumiq.com/](https://my.tealiumiq.com/)に移動します。
1. 管理メニューで、**パスワードポリシーの管理**をクリックします。
1. **このアカウントのMFAを有効にする**をクリックします。  
    ![](/images/iq-tag-management/tiq-manage-password-policy-dialog.jpg)
1. 確認画面から、**マルチファクター認証を有効にする**をクリックします。  
ステータスが**有効**に変わります。  
    ![](/images/iq-tag-management/tiq-confirm-enable-mfa.jpg)
1. **パスワード構成を更新してログアウト**をクリックして確認します。  
ログアウトした後、自動的に再ログインされます。
1. アカウントにログインし、[認証アプリとの同期構成の手順](#認証アプリの構成)に従います。

### MFAの無効化

アカウントのMFAを無効にするには、以下の手順を使用します：

1. [https://my.tealiumiq.com/](https://my.tealiumiq.com/)に移動します。
1. 管理メニューで、**パスワードポリシーの管理**をクリックします。
1. **このアカウントのMFAを無効にする**をクリックします。
1. 確認画面から、**マルチファクター認証を無効にする**をクリックします。  
ステータスが**無効**に変わります。
1. **パスワード構成を更新**をクリックして変更を確認します。

## 認証アプリケーションのインストール

Tealium MFAは、[Google](https://googleauthenticator.net/)と[Windows](https://www.microsoft.com/en-us/store/apps/authenticator/9wzdncrfj3rj)の認証アプリケーションからのトークンのみを受け入れます。以下のリンクをクリックして、デバイスに認証アプリケーションをインストールする方法の詳細情報をご覧ください：

* Android/iOS用の[Google Authenticatorのインストール](https://support.google.com/accounts/answer/1066447?hl=en)
* [Microsoft Corporation: Authenticator](https://www.microsoft.com/en-us/store/apps/authenticator/9wzdncrfj3rj)

### 認証アプリの構成

アプリがトークンを生成するためには、MFAが有効なアカウントとリンクしている必要があります。通常、これは一度だけ行う必要があります（トークンがリセットされた場合や新しいデバイスを使用する場合を除く）。

認証アプリを構成するには、以下の手順を使用します：

1. MFAが有効なアカウントに移動し、正しいユーザー名とパスワードでログインします。  
**構成**画面が表示されます。
1. スマートフォンのプラットフォームを選択し、**次へ**をクリックします。バーコードが表示されます。
    MFAはBlackberryデバイスをサポートしていません。主アカウント保有者またはTealiumアカウントマネージャーに連絡してサポートを受けてください。 
1. スマートフォン上の一般的なバーコードリーダーアプリを使用してバーコードをスキャンします。  
この手順はスマートフォンのプラットフォームにより異なります。  
    * Android: **アカウントを構成 &gt; アカウントのバーコードをスキャン**をタップします。
    * iPhone: プラスアイコン（**&#43;**）をタップし、バーコードをスキャンします。
1. アプリが最初のトークンを生成します。
1. **コード**の隣のテキストボックスにトークンを入力し、**確認して保存**をクリックします。

完了すると成功メッセージが表示されます。

![](/images/iq-tag-management/scan-barcode-sample-do-not-use.jpg)

## MFAが有効なアカウントへのサインイン

サインインする前に、認証アプリはすでにインストールされ、アカウントと同期されている必要があります。以下の手順を使用して、MFAが有効なアカウントにサインインします：

1. [Tealium Tag Management](https://my.tealiumiq.com/)に移動します。  
1. ユーザー名とパスワードを入力します。
1. 認証アプリを開いてトークンを受け取ります。
1. トークンを**MFAトークン**フィールドにコピー＆ペーストまたは入力します。  
トークンが間違っているか期限切れの場合、認証は失敗し、アクセスが拒否されます。
    * （オプション）Tealiumに8時間トークンを記憶させたい場合は、**これは公共のコンピュータではありません**のチェックボックスをチェックします。ブラウザの履歴をクリアしない限り、トークンは8時間保存されます。8時間経過後、トークンを再入力する必要があります。
1. トークンが正しく、それでもサインインできない場合は、トラブルシューティングのヒントを読むか、アカウント管理者に連絡してください。

## MFAトークンのリセット

新しいデバイスや新しい認証アプリに切り替えた場合、既存のトークンをリセットする必要があります。これにより、新しいデバイス上の認証アプリが新鮮なトークンを生成することができます。トークンのリセットは、MFA構成自体を無効にするわけではありません。

### （管理者）ユーザーのMFAをリセット

1. 管理メニューで、**ユーザーの管理**をクリックします。
1. **ユーザーマネージャー**ウィンドウで、トークンをリセットするユーザーを選択するためのチェックボックスをクリックします。
1. **ユーザー構成の編集/表示**をクリックします。
1. 左パネルで、**MFA構成**をクリックし、次に**MFAコードのリセット**をクリックします。  
    ![](/images/iq-tag-management/no-title-253i1283b0c0ea68a93e.png)
1. ウィンドウを閉じます。

次に、ユーザーに通知して、アプリを再同期させるようにログインするよう指示します。

### 自分のMFAをリセット

1. 管理メニューで、**ユーザー構成の編集/表示**をクリックします。
1. 左パネルで、**MFA構成**をクリックし、次に**MFAコードのリセット**をクリックします。
1. ウィンドウを閉じます。
1. 管理メニューで、**ログアウト**をクリックします。

次に、再ログインして新しいMFAトークンを構成します。

## スマートフォンなしでMFAを取得する

このセクションでは、スマートフォンを使用せずにTealiumにログインする際のマルチファクター認証（MFA）の使用方法について説明します。

### Authenticator Chrome Extensionのインストール

以下の手順を使用して、Authenticator Chrome extensionをインストールおよび構成します：

1. [Chrome Web Store](https://chrome.google.com/webstore/category/extensions)に移動し、[Authenticator Chrome Extension](https://chrome.google.com/webstore/detail/authenticator/bhghoamapcdpbohphigoooaddinpkbai)を追加します。  
    ![](/images/iq-tag-management/add-authenticator-chrome-extension.jpg)
1. 完了したら、次のセクションに進みます。

### Tealiumにログインし、Authenticatorを構成する
以下の手順を使用してTealium iQにログインし、認証器を構成します：

1. [Tealium iQタグ管理](https://my.tealiumiq.com/)にログインします。  
**MFA構成**画面が表示されます。  
    ![](/images/iq-tag-management/google-authenticator-setup-android.jpg)

1. **Android**を選択し、**次へ**をクリックします。  
    Androidは、Authenticator Chrome拡張機能と互換性のあるオプションです。
1. **QRコード**画面が表示されます。  
    ![](/images/iq-tag-management/google-authenticator-setup-scan-qr-code.jpg)
1. AuthenticatorアイコンをクリックしてAuthenticator拡張機能を起動し、新しいQRコードを追加するために鉛筆をクリックします。  
    ![](/images/iq-tag-management/launch-authenticator.jpg)
1. **&#43;**ボタンをクリックして新しいコードをスキャンします。  
    ![](/images/iq-tag-management/launch-authenticator-and-add-new.jpg)
1. **QRコードをスキャン**をクリックします。
1. ログイン画面に戻り、マウスを使用してページ内のQRコード上に四角を描きます。
1. 完了したら、Authenticatorに戻ります。  
Tealiumの新しいエントリが表示されます。
1. ログイン画面から、メールアドレスとパスワードを入力し、**続行**をクリックします。  
MFAコード画面が表示されます。
1. Authenticatorからの6桁のコードをMFAコードフィールドに入力し、**ログイン**をクリックします。  
    ![](/images/iq-tag-management/enter-mfa-code-to-log-in.jpg)
    以上で完了です！これでスマートフォンを使わずにMFAを使用してTealiumにログインする準備ができました。
1. 次回Tealiumのログイン画面でMFAコードを求められた場合は、新しく生成されたコードを取得するためにAuthenticatorに戻ります。

## AuthenticatorにアクセスせずにMFAコードを取得する

認証器にアクセスできない場合は、以下の手順を使用して一時的なMFAコードをメールで受け取ります：

1. [Tealium iQタグ管理](https://my.tealiumiq.com/)にログインします。
1. ログイン画面から、メールアドレスとパスワードを入力し、**続行**をクリックします。  
MFAコード画面が表示されます。
1. 一時的なものを受け取るために**ここをクリック**します。  
一時的なMFAがメールに送信されたというメッセージが表示されます。  
    ![](/images/iq-tag-management/enter-mfa-code-to-log-in.jpg)
1. メールに移動し、サポートからの新しいメール**Tealium Temporary MFA Code**を開きます。  
    ![](/images/iq-tag-management/temporary-mfa-code-email.jpg)
1. リカバリーコードを取得し、ログインページに戻ります。
1. コードを入力し、**ログイン**をクリックします。  
ログインしたら、アカウントに移動し、**Edit/View User Settings &gt; MFA Settings**をクリックしてMFAパスワードをリセットすることをお勧めします。