---
title: Facebook Messengerコネクタ構成ガイド
description: この記事では、Facebook Messengerコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/facebook-messenger-connector/
---
## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：Facebook Graph API - Messenger Platform
* APIバージョン：v25.0
* APIエンドポイント：`https://graph.facebook.com`
* ドキュメント：[Facebookページのページアクセストークン](https://developers.facebook.com/docs/facebook-login/access-tokens#pagetokens)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の項目を構成します。

* **ページアクセストークン**  
  * このトークンは、Messenger APIの呼び出しに使用します。
  * 詳細については、[Facebook：ページアクセストークン](https://developers.facebook.com/docs/facebook-login/access-tokens#pagetokens)を参照してください。

コネクタを構成したら、**完了**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| テキストのみのメッセージを送信 | ✓ | ✗ |
| メディアメッセージを送信 | ✓ | ✗ |
| 送信者アクションを送信 | ✓ | ✗ |
| テンプレートメッセージを送信（詳細構成） | ✓ | ✗ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### テキストのみのメッセージを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メッセージングタイプ | （必須）送信するメッセージのメッセージングタイプを指定します。これは、ボットが特定のメッセージングタイプに関するポリシーを遵守し、利用者の構成を尊重していることを、より明示的に保証するための方法です。詳細については、[Facebook：メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`)を参照してください。 |
| 受信者識別子 | （必須）メッセージの送信先となる受信者を識別します。ID、電話番号、またはユーザー参照のいずれかを構成する必要があります。電話番号を使用して受信者を識別する場合、ボットが[カスタマーマッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)の承認を受けている必要があります。また、国番号、市外局番、電話番号を数字のみで指定してください（例：`16505551212`）。電話番号を使用する場合は、名と姓も構成できます。 |
| メッセージテキスト | （必須）ユーザーに送信するメッセージの内容です。このフィールドは2,000文字までに制限されています。また、このフィールドではTealiumテンプレートエンジンもサポートされています。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。 |
| メッセージテキストのテンプレート変数 | メッセージデータのテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| クイック返信 | クイック返信を使用すると、タイトルと任意の画像を含む最大11個のボタンを会話内に表示できます。これらのボタンは、入力欄の上部に目立つように表示されます。また、クイック返信を使用して、ユーザーの位置情報、メールアドレス、電話番号を要求することもできます。配列属性のみがサポートされ、ここで指定する配列はすべて同じサイズである必要があります。詳細については、[Facebook：クイック返信のドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies)を参照してください。 |
| メタデータ | [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/reference/webhook-events/)を介して`message_echoes`フィールドに配信されるカスタム文字列です。上限は1,000文字です。メタデータでは、テンプレート機能とテンプレート変数が自動的にサポートされます。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。 |
| メタデータのテンプレート変数 | メタデータのテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| 通知タイプ | プッシュ通知のタイプです。<ul><li>**通常：** 音／バイブレーション（構成されていない場合に使用されます）。</li><li>**サイレントプッシュ：** 画面上の通知のみ。</li><li>**プッシュなし：** 通知なし</li></ul> |
| メッセージタグ | **メッセージングタイプ**が`Message Tag`に構成されている場合に使用します。すべてのメッセージタグの一覧については、[Facebook：メッセージタグのドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)を参照してください。 |

### メディアメッセージを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メッセージングタイプ | （必須）送信するメッセージのメッセージングタイプを指定します。これは、ボットが特定のメッセージングタイプに関するポリシーを遵守し、ユーザーの構成を尊重していることを、より明示的に保証するための方法です。詳細については、[Facebook：メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`)を参照してください。 |
| 受信者識別子 | （必須）メッセージの送信先となる受信者を識別します。ID、電話番号、またはユーザー参照のいずれかを構成する必要があります。電話番号を使用して受信者を識別する場合、ボットが[カスタマーマッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)の承認を受けている必要があります。また、国番号、市外局番、電話番号を数字のみで指定してください（例：`16505551212`）。電話番号を使用する場合は、名と姓も構成できます。 |
| メディアタイプ | （必須）受信者に送信するメディアのタイプです。サポートされている値は、`Image`、`Audio`、`Video`、または`File`です。 |
| メディアURL | （必須）送信するメディアのWeb `URL`アドレスです。 |
| 再利用可能 | コンテンツを他の受信者にも送信できる再利用可能なコンテンツとしてマークするには、このオプションを選択します。 |
| クイック返信 | クイック返信を使用すると、タイトルと任意の画像を含む最大11個のボタンを会話内に表示できます。これらのボタンは、入力欄の上部に目立つように表示されます。また、クイック返信を使用して、ユーザーの位置情報、メールアドレス、電話番号を要求することもできます。配列属性のみがサポートされ、ここで指定する配列はすべて同じサイズである必要があります。詳細については、[Facebook：クイック返信のドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies)を参照してください。 |
| メタデータ | [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/reference/webhook-events/)を介して`message_echoes`フィールドに配信されるカスタム文字列です。上限は1,000文字です。メタデータでは、テンプレート機能とテンプレート変数が自動的にサポートされます。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。 |
| メタデータのテンプレート変数 | メタデータのテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| 通知タイプ | プッシュ通知のタイプです。<ul><li>**通常：** 音／バイブレーション（構成されていない場合に使用されます）。</li><li>**サイレントプッシュ：** 画面上の通知のみ。</li><li>**プッシュなし：** 通知なし</li></ul> |
| メッセージタグ | **メッセージングタイプ**が`Message Tag`に構成されている場合に使用します。すべてのメッセージタグの一覧については、[Facebook：メッセージタグのドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)を参照してください。 |

### 送信者アクションを送信
#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| メッセージングタイプ | （必須）送信するメッセージのメッセージングタイプを指定します。これは、ボットが特定のメッセージングタイプに関するポリシーを遵守し、ユーザー構成を尊重するための、より明示的な方法です。詳細については、[Facebook：メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`)を参照してください。 |
|受信者識別子| （必須）メッセージの送信先となる受信者を識別します。ID、電話番号、またはユーザー参照を構成する必要があります。電話番号を使用して受信者を識別する場合、ボットが[カスタマーマッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)の承認を受けている必要があります。また、国番号、市外局番、電話番号を含む数字のみを指定してください（例：`16505551212`）。電話番号を使用する場合、名と姓を構成することもできます。 |
| 送信者アクション | （必須）受信者に表示する送信者アクションです。サポートされる値は、`typing_on`、`typing_off`、または`mark_seen`です。 |
| メッセージタグ | **メッセージングタイプ**が`Message Tag`に構成されている場合に使用します。すべてのメッセージタグの一覧については、[Facebook：メッセージタグのドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)を参照してください。 |

### テンプレートメッセージの送信（高度）

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| メッセージングタイプ | （必須）送信するメッセージのメッセージングタイプを指定します。これは、ボットが特定のメッセージングタイプに関するポリシーを遵守し、ユーザー構成を尊重するための、より明示的な方法です。詳細については、[Facebook：メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`)を参照してください。 |
|受信者識別子| （必須）メッセージの送信先となる受信者を識別します。ID、電話番号、またはユーザー参照を構成する必要があります。電話番号を使用して受信者を識別する場合、ボットが[カスタマーマッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)の承認を受けている必要があります。また、国番号、市外局番、電話番号を含む数字のみを指定してください（例：`16505551212`）。電話番号を使用する場合、名と姓を構成することもできます。 |
| テンプレートペイロード | （必須）送信するテンプレートペイロードです。ペイロードは、テンプレート機能とテンプレート変数をサポートします。JSON形式で指定する必要があります：`{ "template_type": "<TEMPLATE_TYPE>", ... }`。具体的なペイロードの内容については、[メッセージテンプレートのドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/templates)を参照してください。 |
| テンプレート変数 | テンプレートエンジンを使用する場合、テンプレート変数が使用されます。これらのフィールドは、属性をテンプレートペイロードで使用される変数名にマッピングします。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| クイック返信| クイック返信を使用すると、タイトルと任意の画像を含む最大11個のボタンを会話内に表示できます。これらのボタンは、入力欄の上に目立つように表示されます。また、クイック返信を使用して、ユーザーの位置情報、メールアドレス、電話番号を要求することもできます。配列属性のみがサポートされ、ここで指定する配列はすべて同じサイズである必要があります。詳細については、[Facebook：クイック返信のドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies)を参照してください。 |
| メタデータ | [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/reference/webhook-events/)を介して`message_echoes`フィールドで配信されるカスタム文字列です。上限は1,000文字です。メタデータは、テンプレート機能とテンプレート変数を自動的にサポートします。詳細については、[Trimouテンプレートエンジン](https://docs.tealium.com/about-connector-templates/)を参照してください。 |
| メタデータテンプレート変数 | テンプレートエンジンを使用する場合、テンプレート変数が使用されます。これらのフィールドは、属性をメタデータで使用される変数名にマッピングします。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| 通知タイプ | プッシュ通知のタイプです。<ul><li>**通常：** 音／バイブレーション（未構成の場合に使用されます）。</li><li>**サイレントプッシュ：** 画面上の通知のみ。</li><li>**プッシュなし：** 通知なし</li></ul>。 |
| メッセージタグ | **メッセージングタイプ**が`Message Tag`に構成されている場合に使用します。すべてのメッセージタグの一覧については、[Facebook：メッセージタグのドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)を参照してください。 |

## ベンダーのドキュメント

* [ページアクセストークン](https://developers.facebook.com/docs/facebook-login/access-tokens#pagetokens)
* [メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages/#messaging_types)
* [カスタマーマッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)
* [クイック返信](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies)
* [メッセージタグ](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)
* [メッセージテンプレート](https://developers.facebook.com/docs/messenger-platform/send-messages/templates)

##### API

* [Facebook Send HTTP API](https://developers.facebook.com/docs/messenger-platform/reference/send-api)