---
title: ClickSendコネクタ構成ガイド
description: この記事では、ClickSendコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/clicksend-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|新しい連絡先を作成| ✓| ✓|
|特定の連絡先を更新| ✓| ✓|
|特定の連絡先を削除| ✓| ✓|
|SMSを送信| ✓| ✓|
|トランザクションメールを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **ユーザー名**  
ユーザー名はあなたのアカウントのユーザー名で、パスワードはあなたのアカウントのパスワードです。これらはダッシュボードにログインするときに使用するのと同じ認証情報です。詳細については、[ClickSend認証ドキュメント](https://clicksend.docs.apiary.io/#introduction/authentication)を参照してください。
* **パスワード**  
ユーザー名はあなたのアカウントのユーザー名で、パスワードはあなたのアカウントのパスワードです。これらはダッシュボードにログインするときに使用するのと同じ認証情報です。詳細については、[ClickSend認証ドキュメント](https://clicksend.docs.apiary.io/#introduction/authentication)を参照してください。

コネクタの構成が完了したら、**完了**をクリックします。

## アクション構成 — パラメータとオプション

**続行**をクリックしてコネクタアクションを構成します。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション — 新しい連絡先を作成

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID| 連絡先が関連付けられている連絡先リストIDです。このエンドポイントの詳細については、[ClickSendの新しい連絡先を作成するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を読んでください。|
|電話番号| E.164形式の連絡先電話番号です。`phone_number`、`fax_number`、`address_line_1`、および`email`のフィールドはすべてオプションですが、少なくとも1つは指定されていなければAPIコールは失敗します。詳細については、[ClickSendの新しい連絡先を作成するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を読んでください。|
|名| 連絡先の名前です。|
|姓| 連絡先の姓です。|
|ファックス番号| 連絡先のファックス番号です。`phone_number`、`fax_number`、`address_line_1`、および`email`のフィールドはすべてオプションですが、少なくとも1つは指定されていなければAPIコールは失敗します。詳細については、[ClickSendの新しい連絡先を作成するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を読んでください。|
|組織名| あなたの組織名です。|
|メール| 連絡先のメールです。`phone_number`、`fax_number`、`address_line_1`、および`email`のフィールドはすべてオプションですが、少なくとも1つは指定されていなければAPIコールは失敗します。詳細については、[ClickSendの新しい連絡先を作成するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を読んでください。|
|住所1行目| 連絡先の住所1行目です。`phone_number`、`fax_number`、`address_line_1`、および`email`のフィールドはすべてオプションですが、少なくとも1つは指定されていなければAPIコールは失敗します。詳細については、[ClickSendの新しい連絡先を作成するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact-collection/create-a-new-contact)を読んでください。|
|住所2行目| 連絡先の住所2行目です。|
|住所の市| 連絡先の市です。|
|住所の州| 連絡先の州です。|
|住所の郵便番号| 連絡先の郵便番号です。|
|住所の国| ISO 3166で定義された2文字の国コードです。|
|カスタム属性| 含めたい任意のカスタム属性です。|

### アクション — 特定の連絡先を更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID| アクセスしたい連絡先リストIDです。このエンドポイントの詳細については、[ClickSendの連絡先を更新するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact/update-a-specific-contact)を読んでください。|
|連絡先ID| アクセスしたい連絡先IDです。|
|電話番号| E.164形式の連絡先電話番号です。|
|名| 連絡先の名前です。|
|姓| 連絡先の姓です。|
|ファックス番号| 連絡先のファックス番号です。|
|組織名| あなたの組織名です。|
|メール| 連絡先のメールです。|
|住所1行目| 連絡先の住所1行目です。|
|住所2行目| 連絡先の住所2行目です。|
|住所の市| 連絡先の市です。|
|住所の州| 連絡先の州です。|
|住所の郵便番号| 連絡先の郵便番号です。|
|住所の国| ISO 3166形式で定義された2文字の国コードです。|
|カスタム属性| 含めたい任意のカスタム属性です。|

### アクション — 特定の連絡先を削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID| アクセスしたいあなたの連絡先リストIDです。このエンドポイントの詳細については、[ClickSendの連絡先を削除するドキュメント](https://clicksend.docs.apiary.io/#reference/contacts/contact/delete-a-specific-contact)を読んでください。|
|連絡先ID| アクセスしたいあなたの連絡先IDです。|

### アクション — SMSを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|宛先| E.164形式またはローカル形式の受信者番号です。詳細については、[ClickSendのSMSを送信するドキュメント](https://clicksend.docs.apiary.io/#reference/sms/send-an-sms)を読んでください。|
|本文| あなたのメッセージです。|
|送信元| 送信方法です。例えば、`wordpress`、`php`、`c#`です。|
|送信者ID| あなたの送信者IDです。詳細については、[SendGridの送信者IDまたは番号のドキュメント](https://help.clicksend.com/SMS/what-is-a-sender-id-or-sender-number)を読んでください。|
|スケジュール| Unixタイムスタンプとしてのスケジュールされた時間です。即時配信の場合は空白のままにしてください。|
|カスタム文字列| あなたの参照です。すべての返信と配信レポートと共に返されます。|
|国| 受信者の国です。|
|返信用メール| 返信がメールで送られるべきメールアドレスです。省略された場合、返信はSMSを送ったユーザーにメールで返されます。|

### アクション — トランザクションメールを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メール| 受信者のメールアドレスです。|
|名前 (宛先)| 受信者の名前です。|
|メールアドレスID| 送信者のメールアドレスIDです。|
|名前 (送信者)| 送信者の名前です。|
|件名| メールの件名です。|
|本文| メールの内容です。|
