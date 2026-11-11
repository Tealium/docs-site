---
title: 多要素認証（MFA）
description: 多要素認証は、スマートフォンやブラウザーアプリなど、ログイン時に2つ目の認証方法を要求するセキュリティ手法です。
url: https://docs.tealium.com/ja/administration/security-access/multi-factor-authentication-mfa/
---
## 要件

* **スマートフォン**  
iOS、Android、Windowsがサポートされています。
* **認証アプリ**  
MFAは、[Google Authenticator](https://googleauthenticator.net/)や[Windows Authenticator](https://www.microsoft.com/en-us/store/apps/authenticator/9wzdncrfj3rj)などのサードパーティー製アプリケーションと連携し、パスワードに加えて保護レイヤーを追加します。これらのアプリケーションは、アカウント専用の使い捨て6桁セキュリティトークンをスマートフォン上で生成します。使用しているスマートフォンプラットフォームと互換性のある認証アプリケーションをインストールしてください。
* **バーコードリーダーアプリ**  
Androidデバイスを使用している場合は、認証アプリケーションをアカウントと同期するときに必要となるため、QRコードを読み取るためのアプリが搭載されていることを確認してください。iPhoneには該当しません。
* **ブラウザーのサポート**  
MFAは、iPhone、Android、Windowsのスマートフォンでのみサポートされています。スマートフォンがこれらのいずれにも該当しない場合は、[Authenticator Chrome拡張機能](https://chrome.google.com/webstore/detail/authenticator/bhghoamapcdpbohphigoooaddinpkbai)を使用してChromeブラウザーからトークンを受信できます。

## 仕組み

プライマリアカウント、または割り当てられているその他のアカウントでMFAが有効になっている場合、ログイン処理中にMFAが必要になります。MFAは認証アプリケーションと連携し、2つの手順でログイン要求を検証します。

MFAが有効なアカウントにサインインするときは、次の情報の入力を求められます。

* **ログイン認証情報**  
アカウントのユーザー名とパスワード
* **セキュリティコード**  
スマートフォンの認証アプリによって生成される6桁のトークン

## アカウントのMFAを有効化または無効化する

MFAを有効化または無効化するには、[アカウントの管理]()権限が必要です。この構成を切り替える権限があるのは、アカウント管理者のみです。

### MFAを有効化する

アカウントのMFAを有効化するには、次の手順を実行します。

1. [https://my.tealiumiq.com/](https://my.tealiumiq.com/)に移動します。
1. 管理メニューで、**Manage Password Policy**をクリックします。
1. **Enable MFA for this Account**をクリックします。  
    ![](https://docs.tealium.com/images/tag-management/tiq-manage-password-policy-dialog.jpg)
1. 確認画面で、**Enable Multi-Factor Authentication**をクリックします。  
ステータスが**Enabled**に変わります。  
    ![](https://docs.tealium.com/images/tag-management/tiq-confirm-enable-mfa.jpg)
1. **Update Password Settings and Logout**をクリックして確定します。  
ログアウトすると、自動的に再度ログインします。
1. アカウントにログインし、[認証アプリケーションと同期する手順](#setting-up-your-authenticator-application)に従います。

### MFAを無効化する

アカウントのMFAを無効化するには、次の手順を実行します。

1. [https://my.tealiumiq.com/](https://my.tealiumiq.com/)に移動します。
1. 管理メニューで、**Manage Password Policy**をクリックします。
1. **Disable MFA for this Account**をクリックします。
1. 確認画面で、**Disable Multi-Factor Authentication**をクリックします。  
ステータスが**Not Enabled**に変わります。
1. **Update Password Settings**をクリックして変更を確定します。

## 認証アプリケーションをインストールする

Tealium MFAでは、[Google](https://googleauthenticator.net/)および[Windows](https://www.microsoft.com/en-us/store/apps/authenticator/9wzdncrfj3rj)のAuthenticatorアプリケーションからのトークンのみを使用できます。デバイスに認証アプリケーションをインストールする方法の詳細については、次のいずれかのリンクをクリックしてください。

* Android/iOS向けの[Google Authenticatorをインストールする](https://support.google.com/accounts/answer/1066447?hl=en)
* [Microsoft Corporation：Authenticator](https://www.microsoft.com/en-us/store/apps/authenticator/9wzdncrfj3rj)

### 認証アプリケーションを構成する

アプリでトークンの生成を開始するには、MFAが有効なアカウントにアプリをリンクする必要があります。通常、この操作が必要なのは1回だけです（トークンをリセットした場合や、新しいデバイスを使用する場合を除きます）。

認証アプリケーションを構成するには、次の手順を実行します。

1. MFAが有効なアカウントに移動し、正しいユーザー名とパスワードでログインします。  
**Setup**画面が表示されます。
1. スマートフォンプラットフォームを選択し、**Next**をクリックします。バーコードが表示されます。
1. スマートフォンの汎用バーコードリーダーアプリを使用して、バーコードをスキャンします。  
この手順は、使用するスマートフォンプラットフォームによって異なります。  
    * Android：**Set an Account > Scan account barcode**をタップします。
    * iPhone：プラスアイコン（**+**）をタップし、バーコードをスキャンします。
1. アプリによって最初のトークンが生成されます。
1. **Code**の横にあるテキストボックスにトークンを入力し、**Verify and Save**をクリックします。

完了すると、成功メッセージが表示されます。

![](https://docs.tealium.com/images/tag-management/scan-barcode-sample-do-not-use.jpg)

## MFAが有効なアカウントにサインインする

サインインする前に、認証アプリがインストール済みで、アカウントと同期されている必要があります。MFAが有効なアカウントにサインインするには、次の手順を実行します。

1. [タグ管理](https://my.tealiumiq.com/)に移動します。  
1. ユーザー名とパスワードを入力します。
1. 認証アプリを開いてトークンを取得します。
1. トークンをコピーして貼り付けるか、**MFA TOKEN**フィールドに入力します。  
トークンが正しくないか、有効期限が切れている場合は認証に失敗し、アクセスが拒否されます。
    * （任意）Tealiumにトークンを8時間記憶させる場合は、**This is not a public computer**チェックボックスをオンにします。ブラウザーの履歴を消去しない限り、トークンは8時間保持されます。8時間が経過した後は、トークンを再入力する必要があります。
1. トークンが正しいにもかかわらずサインインできない場合は、トラブルシューティングのヒントを参照するか、アカウント管理者にお問い合わせください。

## MFAトークンをリセットする

最近新しいデバイスまたは新しい認証アプリに切り替えた場合は、既存のトークンをリセットする必要があります。これにより、新しいデバイス上の認証アプリで新しいトークンを生成できるようになります。トークンをリセットしても、MFA構成自体は無効になりません。

### （管理者）ユーザーのMFAをリセットする

1. 管理メニューで、**Manage Users**をクリックします。
1. **User Manager**ウィンドウで、トークンをリセットするユーザーのチェックボックスをクリックして選択します。
1. **Edit/View User Settings**をクリックします。
1. 左側のパネルで、**MFA Settings**をクリックし、**Reset MFA Code**をクリックします。  
    ![](https://docs.tealium.com/images/tag-management/no-title-253i1283b0c0ea68a93e.png)
1. ウィンドウを閉じます。

次に、アカウントへログインしてアプリを再同期するようユーザーに通知します。

### 自分のMFAをリセットする

1. 管理メニューで、**Edit/View User Settings**をクリックします。
1. 左側のパネルで、**MFA Settings**をクリックし、**Reset MFA Code**をクリックします。
1. ウィンドウを閉じます。
1. 管理メニューで、**Logout**をクリックします。

次に、再度ログインして新しいMFAトークンを構成します。

## スマートフォンを使用せずにMFAを利用する

このセクションでは、Tealiumへのログイン時にスマートフォンを使用せずに多要素認証（MFA）を利用する方法について説明します。

### Authenticator Chrome拡張機能をインストールする

Authenticator Chrome拡張機能をインストールして構成するには、次の手順を実行します。

1. [Chromeウェブストア](https://chrome.google.com/webstore/category/extensions)に移動し、[Authenticator Chrome拡張機能](https://chrome.google.com/webstore/detail/authenticator/bhghoamapcdpbohphigoooaddinpkbai)を追加します。  
    ![](https://docs.tealium.com/images/tag-management/add-authenticator-chrome-extension.jpg)
1. 完了したら、次のセクションに進みます。
### Tealium にログインして Authenticator を構成する

以下の手順に従って Tag Management にログインし、Authenticator を構成します。

1. [Tag Management](https://my.tealiumiq.com/) にログインします。  
**MFA のセットアップ**画面が表示されます。  
    ![](https://docs.tealium.com/images/tag-management/google-authenticator-setup-android.jpg)

1. **Android** を選択し、**次へ**をクリックします。  
    
<blockquote>
Android is the option that is compatible with the Authenticator Chrome extension.
</blockquote>

1. **QR コード**画面が表示されます。  
    ![](https://docs.tealium.com/images/tag-management/google-authenticator-setup-scan-qr-code.jpg)
1. Authenticator アイコンをクリックして Authenticator 拡張機能を起動し、鉛筆アイコンをクリックして新しい QR コードを追加します。  
    ![](https://docs.tealium.com/images/tag-management/launch-authenticator.jpg)
1. **+** ボタンをクリックして、新しいコードをスキャンします。  
    ![](https://docs.tealium.com/images/tag-management/launch-authenticator-and-add-new.jpg)
1. **QR コードをスキャン**をクリックします。
1. ログイン画面に戻り、マウスを使用してページ上の QR コードを囲むように四角形をドラッグして描きます。
1. 完了したら、Authenticator に戻ります。  
Tealium の新しいエントリが表示されます。
1. ログイン画面でメールアドレスとパスワードを入力し、**続行**をクリックします。  
MFA コード画面が表示されます。
1. Authenticator に表示された 6 桁のコードを MFA コードフィールドに入力し、**ログイン**をクリックします。  
    ![](https://docs.tealium.com/images/tag-management/enter-mfa-code-to-log-in.jpg)
    以上で完了です。スマートフォンを使用せずに、MFA を使って Tealium にログインできるようになりました。
1. 次回、Tealium のログイン画面で MFA コードの入力を求められたら、Authenticator に戻って新しく生成されたコードを取得します。

## Authenticator にアクセスせずに MFA コードを取得する

Authenticator にアクセスできない場合は、以下の手順に従って一時的な MFA コードをメールで受信します。

1. [Tag Management](https://my.tealiumiq.com/) にログインします。
1. ログイン画面でメールアドレスとパスワードを入力し、**続行**をクリックします。  
MFA コード画面が表示されます。
1. 一時的なコードを受信するには、**ここをクリック**をクリックします。  
一時的な MFA コードがメールで送信されたことを示すメッセージが表示されます。  
    ![](https://docs.tealium.com/images/tag-management/enter-mfa-code-to-log-in.jpg)
1. メールを確認し、サポートから届いた **Tealium 一時 MFA コード**という件名の新しいメールを開きます。  
    ![](https://docs.tealium.com/images/tag-management/temporary-mfa-code-email.jpg)
1. リカバリコードを取得し、ログインページに戻ります。
1. コードを入力し、**ログイン**をクリックします。  
ログイン後、アカウントに移動して **ユーザー構成の編集／表示 > MFA 構成**をクリックし、MFA パスワードをリセットすることをお勧めします。