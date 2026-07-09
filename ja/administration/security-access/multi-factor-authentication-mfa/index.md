---
title: 多要素認証（MFA）
description: 多要素認証は、スマートフォンやブラウザアプリなど、ログイン時に第二の認証方法を要求するセキュリティ手法です。
url: https://docs.tealium.com/ja/administration/security-access/multi-factor-authentication-mfa/
---
## 要件

* **スマートフォン**  
iOS、Android、Windowsがサポートされています。
* **認証アプリ**  
MFAは、[Google Authenticator](https://googleauthenticator.net/)や[Windows Authenticator](https://www.microsoft.com/en-us/store/apps/authenticator/9wzdncrfj3rj)などのサードパーティアプリと連携して、パスワードを超えた保護層を追加します。これらのアプリケーションは、あなたのアカウント専用の一回限りの6桁のセキュリティトークンをスマートフォンで生成します。スマートフォンプラットフォームに対応した認証アプリケーションをインストールしてください。
* **バーコードリーダーアプリ**  
Androidデバイスをお持ちの場合は、アカウントと認証アプリケーションを同期する際に必要となるQRコードを読み取るための内蔵アプリがあることを確認してください。これはiPhoneには適用されません。
* **ブラウザサポート**  
MFAはiPhone、Android、Windowsスマートフォンでのみサポートされています。お使いのスマートフォンがこれらのいずれでもない場合は、[Authenticator Chrome Extension](https://chrome.google.com/webstore/detail/authenticator/bhghoamapcdpbohphigoooaddinpkbai)を使用してChromeブラウザからトークンを受け取ることができます。

## 動作原理

MFAは、主アカウントおよび/またはあなたが割り当てられている他のアカウントで有効にされている場合、ログインプロセス中に必要とされます。MFAは認証アプリケーションと連携して、ログインリクエストを2段階で確認します。

MFAが有効なアカウントにサインインする際、以下の情報の提供が求められます：

* **ログイン資格情報**  
アカウントのユーザー名とパスワード
* **セキュリティコード**  
スマートフォンの認証アプリによって生成される6桁のトークン

## アカウントのMFAの有効化または無効化

MFAの有効化または無効化には[Manage Accounts]()の権限が必要です。アカウント管理者のみがこの構成を切り替える権限を持っています。

### MFAの有効化

アカウントのMFAを有効にするには、以下の手順に従ってください：

1. [https://my.tealiumiq.com/](https://my.tealiumiq.com/)にアクセスします。
1. 管理メニューで**パスワードポリシーの管理**をクリックします。
1. **このアカウントのMFAを有効にする**をクリックします。  
    ![](/images/iq-tag-management/tiq-manage-password-policy-dialog.jpg)
1. 確認画面で**多要素認証を有効にする**をクリックします。  
状態が**有効**に変わります。  
    ![](/images/iq-tag-management/tiq-confirm-enable-mfa.jpg)
1. **パスワード構成を更新してログアウト**をクリックして確認します。  
ログアウト後、自動的に再ログインされます。
1. アカウントにログインし、認証アプリとの同期[手順に従ってください](#setting-up-your-authenticator-application)。

### MFAの無効化

アカウントのMFAを無効にするには、以下の手順に従ってください：

1. [https://my.tealiumiq.com/](https://my.tealiumiq.com/)にアクセスします。
1. 管理メニューで**パスワードポリシーの管理**をクリックします。
1. **このアカウントのMFAを無効にする**をクリックします。
1. 確認画面で**多要素認証を無効にする**をクリックします。  
状態が**無効**に変わります。
1. 変更を確認するために**パスワード構成を更新**をクリックします。

## 認証アプリケーションのインストール

Tealium MFAは、[Google](https://googleauthenticator.net/)および[Windows](https://www.microsoft.com/en-us/store/apps/authenticator/9wzdncrfj3rj)の認証アプリケーションからのトークンのみを受け入れます。デバイスに認証アプリケーションをインストールする方法については、以下のリンクをクリックして詳細情報をご覧ください：

* [Google Authenticatorのインストール](https://support.google.com/accounts/answer/1066447?hl=en) for Android/iOS
* [Microsoft Corporation: Authenticator](https://www.microsoft.com/en-us/store/apps/authenticator/9wzdncrfj3rj)

### 認証アプリケーションの構成

アプリがトークンを生成するようにするには、アカウントにリンクする必要があります。通常、これは一度だけ行う必要があります（トークンがリセットされた場合や新しいデバイスに変更した場合を除く）。

認証アプリケーションを構成するには、以下の手順に従ってください：

1. MFAが有効なアカウントにアクセスし、正しいユーザー名とパスワードでログインします。  
**構成**画面が表示されます。
1. スマートフォンのプラットフォームを選択し、次に**次へ**をクリックします。バーコードが表示されます。
1. スマートフォンの一般的なバーコードリーダーアプリを使用してバーコードをスキャンします。  
この手順は、使用しているスマートフォンのプラットフォームによって異なります。  
    * Android: **アカウントの構成 &gt; アカウントバーコードのスキャン**をタップします。
    * iPhone: プラスアイコン（**&#43;**）をタップしてバーコードをスキャンします。
1. アプリが最初のトークンを生成します。
1. **コード**の隣のテキストボックスにトークンを入力し、**検証して保存**をクリックします。

完了すると成功メッセージが表示されます。

![](/images/iq-tag-management/scan-barcode-sample-do-not-use.jpg)

## MFAが有効なアカウントへのサインイン

サインインする前に、認証アプリがすでにインストールされ、アカウントと同期されている必要があります。MFAが有効なアカウントにサインインするには、以下の手順に従ってください：

1. [Tealium iQ Tag Management](https://my.tealiumiq.com/)にアクセスします。  
1. ユーザー名とパスワードを入力します。
1. 認証アプリを開いてトークンを受け取ります。
1. **MFA TOKEN**フィールドにトークンを貼り付けるか入力します。  
トークンが間違っているか期限切れの場合、認証は失敗し、アクセスが拒否されます。
    * （オプション）。Tealiumにトークンを8時間覚えてもらいたい場合は、**これは公共のコンピュータではありません**のチェックボックスをオンにします。ブラウザの履歴をクリアしない限り、トークンは8時間保存されます。8時間後には、トークンを再入力する必要があります。
1. トークンが正しくてもサインインできない場合は、トラブルシューティングのヒントを読むか、アカウント管理者に連絡してください。

## MFAトークンのリセット

新しいデバイスに切り替えたり、新しい認証アプリに変更した場合、既存のトークンをリセットする必要があります。これにより、新しいデバイスの認証アプリが新しいトークンを生成できるようになります。トークンのリセットはMFA構成自体を無効にするものではありません。

### （管理者）ユーザーのMFAをリセットする

1. 管理メニューで**ユーザー管理**をクリックします。
1. **ユーザーマネージャー**ウィンドウで、トークンをリセットするユーザーを選択するためのチェックボックスをクリックします。
1. **ユーザー構成の編集/表示**をクリックします。
1. 左パネルで**MFA構成**をクリックし、次に**MFAコードのリセット**をクリックします。  
    ![](/images/iq-tag-management/no-title-253i1283b0c0ea68a93e.png)
1. ウィンドウを閉じます。

次に、ユーザーにアプリを再同期するためにアカウントにログインするよう通知します。

### 自分のMFAをリセットする

1. 管理メニューで**ユーザー構成の編集/表示**をクリックします。
1. 左パネルで**MFA構成**をクリックし、次に**MFAコードのリセット**をクリックします。
1. ウィンドウを閉じます。
1. 管理メニューで**ログアウト**をクリックします。

次に、ログインし直して新しいMFAトークンを構成します。

## スマートフォンなしでMFAを取得する

このセクションでは、スマートフォンを使用せずにTealiumにログインする際に多要素認証（MFA）を使用する方法について説明します。

### Authenticator Chrome Extensionのインストール

Authenticator Chrome拡張機能をインストールして構成するには、以下の手順に従ってください：

1. [Chrome Web Store](https://chrome.google.com/webstore/category/extensions)にアクセスし、[Authenticator Chrome Extension](https://chrome.google.com/webstore/detail/authenticator/bhghoamapcdpbohphigoooaddinpkbai)を追加します。  
    ![](/images/iq-tag-management/add-authenticator-chrome-extension.jpg)
1. 完了したら、次のセクションに進みます。
### Tealiumにログインして認証器を構成する

Tealium iQにログインし、認証器を構成するには、以下の手順に従ってください：

1. [Tealium iQタグ管理](https://my.tealiumiq.com/)にログインします。  
**MFA構成**画面が表示されます。  
    ![](/images/iq-tag-management/google-authenticator-setup-android.jpg)

1. **Android**を選択し、次に**次へ**をクリックします。  
    AndroidはAuthenticator Chrome拡張機能と互換性のあるオプションです。
1. **QRコード**画面が表示されます。  
    ![](/images/iq-tag-management/google-authenticator-setup-scan-qr-code.jpg)
1. 認証器アイコンをクリックして認証器拡張機能を起動し、新しいQRコードを追加するために鉛筆をクリックします。  
    ![](/images/iq-tag-management/launch-authenticator.jpg)
1. 新しいコードをスキャンするために**&#43;**ボタンをクリックします。  
    ![](/images/iq-tag-management/launch-authenticator-and-add-new.jpg)
1. **QRコードをスキャン**をクリックします。
1. ログイン画面に戻り、マウスを使用してページ内のQRコードの上に四角を描画します。
1. 完了したら、認証器に戻ります。  
Tealiumの新しいエントリが表示されます。
1. ログイン画面からメールアドレスとパスワードを入力し、**続行**をクリックします。  
MFAコード画面が表示されます。
1. 認証器からの6桁のコードをMFAコードフィールドに入力し、**ログイン**をクリックします。  
    ![](/images/iq-tag-management/enter-mfa-code-to-log-in.jpg)
    これで完了です！これでスマートフォンなしでMFAを使用してTealiumにログインする準備が整いました。
1. 次回Tealiumのログイン画面でMFAコードの入力を求められた場合は、新しく生成されたコードを取得するために認証器に戻ります。

## 認証器にアクセスせずにMFAコードを取得する

認証器にアクセスできない場合は、以下の手順に従ってメールで一時的なMFAコードを受け取ってください：

1. [Tealium iQタグ管理](https://my.tealiumiq.com/)にログインします。
1. ログイン画面からメールアドレスとパスワードを入力し、**続行**をクリックします。  
MFAコード画面が表示されます。
1. 一時的なものを受け取るために**ここをクリック**します。  
一時的なMFAがメールに送信されたことを示すメッセージが表示されます。  
    ![](/images/iq-tag-management/enter-mfa-code-to-log-in.jpg)
1. メールにアクセスし、**Tealium Temporary MFA Code**というタイトルの新しいメールを開きます。  
    ![](/images/iq-tag-management/temporary-mfa-code-email.jpg)
1. 回復コードを取得し、ログインページに戻ります。
1. コードを入力し、**ログイン**をクリックします。  
ログインしたら、アカウントにアクセスし、**ユーザー構成の編集/表示 &gt; MFA構成**をクリックしてMFAパスワードをリセットすることをお勧めします。