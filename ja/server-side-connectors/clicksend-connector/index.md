---
title: ClickSendコネクタ構成ガイド
description: この記事では、ClickSendコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/clicksend-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|新しい連絡先を作成| ✓| ✓|
|特定の連絡先を更新| ✓| ✓|
|特定の連絡先を削除| ✓| ✓|
|SMSを送信| ✓| ✓|
|トランザクションメールを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を構成します。

* **ユーザー名**  
ユーザー名はアカウントのユーザー名、パスワードはアカウントのパスワードです。これらは、ダッシュボードへのログインに使用するものと同じ認証情報です。詳細については、[ClickSendの認証ドキュメント](https://clicksend.docs.apiary.io/#introduction/authentication)を参照してください。
* **パスワード**  
ユーザー名はアカウントのユーザー名、パスワードはアカウントのパスワードです。これらは、ダッシュボードへのログインに使用するものと同じ認証情報です。詳細については、[ClickSendの認証ドキュメント](https://clicksend.docs.apiary.io/#introduction/authentication)を参照してください。

コネクタの構成が完了したら、**完了**をクリックします。

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### アクション — 新しい連絡先を作成

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID| 連絡先が関連付けられている連絡先リストのID。このエンドポイントの詳細については、[ClickSendの新しい連絡先の作成に関するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を参照してください。|
|電話番号| E.164形式の連絡先電話番号。`phone_number`、`fax_number`、`address_line_1`、`email`の各フィールドはすべて任意です。ただし、そのうち少なくとも1つを指定する必要があります。指定しない場合、API呼び出しは失敗します。詳細については、[ClickSendの新しい連絡先の作成に関するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を参照してください。|
|名| 連絡先の名。|
|姓| 連絡先の姓。|
|FAX番号| 連絡先のFAX番号。`phone_number`、`fax_number`、`address_line_1`、`email`の各フィールドはすべて任意です。ただし、そのうち少なくとも1つを指定する必要があります。指定しない場合、API呼び出しは失敗します。詳細については、[ClickSendの新しい連絡先の作成に関するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を参照してください。|
|組織名| 組織名。|
|メールアドレス| 連絡先のメールアドレス。`phone_number`、`fax_number`、`address_line_1`、`email`の各フィールドはすべて任意です。ただし、そのうち少なくとも1つを指定する必要があります。指定しない場合、API呼び出しは失敗します。詳細については、[ClickSendの新しい連絡先の作成に関するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を参照してください。|
|住所1| 連絡先の住所1。`phone_number`、`fax_number`、`address_line_1`、`email`の各フィールドはすべて任意です。ただし、そのうち少なくとも1つを指定する必要があります。指定しない場合、API呼び出しは失敗します。詳細については、[ClickSendの新しい連絡先の作成に関するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を参照してください。|
|住所2| 連絡先の住所2。|
|市区町村| 連絡先の市区町村。|
|都道府県／州| 連絡先の都道府県または州。|
|郵便番号| 連絡先の郵便番号。|
|国| ISO 3166で定義された、連絡先の2文字の国コード。|
|カスタム属性| 含める任意のカスタム属性。|

### アクション — 特定の連絡先を更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID| アクセスする連絡先リストのID。このエンドポイントの詳細については、[ClickSendの連絡先の更新に関するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact/update-a-specific-contact)を参照してください。|
|連絡先ID| アクセスする連絡先のID。|
|電話番号| E.164形式の連絡先電話番号。|
|名| 連絡先の名。|
|姓| 連絡先の姓。|
|FAX番号| 連絡先のFAX番号。|
|組織名| 組織名。|
|メールアドレス| 連絡先のメールアドレス。|
|住所1| 連絡先の住所1。|
|住所2| 連絡先の住所2。|
|市区町村| 連絡先の市区町村。|
|都道府県／州| 連絡先の都道府県または州。|
|郵便番号| 連絡先の郵便番号。|
|国| ISO 3166形式で定義された、連絡先の2文字の国コード。|
|カスタム属性| 含める任意のカスタム属性。|

### アクション — 特定の連絡先を削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID| アクセスする連絡先リストのID。このエンドポイントの詳細については、[ClickSendの連絡先の削除に関するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact/delete-a-specific-contact)を参照してください。|
|連絡先ID| アクセスする連絡先のID。|

### アクション — SMSを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|宛先| E.164形式またはローカル形式の受信者番号。詳細については、[ClickSendのSMS送信に関するドキュメント](https://clicksend.docs.apiary.io/#reference/sms/send-an-sms)を参照してください。|
|本文| メッセージ。|
|ソース| 送信方法。例：`wordpress`、`php`、`c#`。|
|送信元| 送信者ID。詳細については、[SendGridの送信者IDまたは送信者番号に関するドキュメント](https://help.clicksend.com/SMS/what-is-a-sender-id-or-sender-number)を参照してください。|
|スケジュール| Unixタイムスタンプ形式の送信予定時刻。即時配信する場合は空白のままにします。|
|カスタム文字列| 参照情報。すべての返信および配信レポートとともに返されます。|
|国| 受信者の国。|
|返信先メールアドレス| 返信の転送先メールアドレス。省略した場合、返信は送信SMSを送ったユーザーにメールで転送されます。|

### アクション — トランザクションメールを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メールアドレス| 受信者のメールアドレス。|
|名前（宛先）| 受信者の名前。|
|メールアドレスID| 送信者のメールアドレスID。|
|名前（送信元）| 送信者の名前。|
|件名| メールの件名。|
|本文| メールの内容。|