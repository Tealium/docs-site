---
title: Facebookメッセンジャーコネクタ構成ガイド
description: この記事では、Facebookメッセンジャーコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/facebook-messenger-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Facebook Graph API - Messenger Platform
* APIバージョン：v25.0
* APIエンドポイント：`https://graph.facebook.com`
* ドキュメント：[Facebookページのページアクセストークン](https://developers.facebook.com/docs/facebook-login/access-tokens#pagetokens)

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **ページアクセストークン**  
  * このトークンは、Messenger APIの呼び出しに使用されます。
  * 詳細については、[Facebook: ページアクセストークン](https://developers.facebook.com/docs/facebook-login/access-tokens#pagetokens)を参照してください。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| テキストのみのメッセージを送信 | ✓ | ✗ |
| メディアメッセージを送信 | ✓ | ✗ |
| 送信者アクションを送信 | ✓ | ✗ |
| テンプレートメッセージを送信（高度） | ✓ | ✗ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### テキストのみのメッセージを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メッセージングタイプ | (必須) 送信されるメッセージのメッセージングタイプを指定し、特定のメッセージングタイプに対するポリシーの遵守をより明確にし、人々の好みを尊重することを保証します。詳細については、[Facebook: メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`)を参照してください。 |
|受信者識別子| (必須) メッセージを送信する受信者を識別します。ID、電話番号、またはユーザー参照を構成する必要があります。電話番号を使用して受信者を識別する場合、あなたのボットは[顧客マッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)の承認を受け、国コード、エリアコード、番号（例：`16505551212`）のみを含む必要があります。電話番号を使用する場合、名と姓の構成も可能です。 |
| メッセージテキスト | (必須) ユーザーに送信するメッセージの内容。このフィールドは2000文字に制限されています。このフィールドはTealiumのテンプレートエンジンもサポートしています。詳細については、を参照してください。 |
| メッセージテキストテンプレート変数 | メッセージデータのテンプレート変数を提供します。詳細については、を参照してください。 |
| クイック返信| クイック返信は、タイトルとオプションの画像を含む最大11個のボタンのセットを会話中に提示する方法を提供し、コンポーザーの上に目立って表示されます。また、クイック返信を使用してユーザーの位置情報、メールアドレス、電話番号を要求することもできます。サポートされているのは配列属性のみであり、ここで指定される配列は同じサイズでなければなりません。詳細については、[Facebook: クイック返信ドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies)を参照してください。 |
| メタデータ | [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/reference/webhook-events/)を通じて`message_echoes`フィールドで配信されるカスタム文字列。1,000文字制限。メタデータは自動的にテンプレート機能とテンプレート変数をサポートします。詳細については、を参照してください。 |
| メタデータテンプレート変数 | メタデータのテンプレート変数を提供します。詳細については、を参照してください。 |
| 通知タイプ | プッシュ通知のタイプ。&lt;ul&gt;&lt;li&gt;**通常:** 音/振動（構成されていない場合に使用されます）。&lt;/li&gt;&lt;li&gt;**サイレントプッシュ:** 画面上の通知のみ。&lt;/li&gt;&lt;li&gt;**ノープッシュ:** 通知なし&lt;/li&gt;&lt;/ul&gt;。 |
| メッセージタグ | **メッセージングタイプ**が`Message Tag`に構成されている場合に使用します。すべてのメッセージタグの完全なリストについては、[Facebook: メッセージタグドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)を参照してください。 |

### メディアメッセージを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メッセージングタイプ | (必須) 送信されるメッセージのメッセージングタイプを指定し、特定のメッセージングタイプに対するポリシーの遵守をより明確にし、ユーザーの好みを尊重することを保証します。詳細については、[Facebook: メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`)を参照してください。 |
|受信者識別子| (必須) メッセージを送信する受信者を識別します。ID、電話番号、またはユーザー参照を構成する必要があります。電話番号を使用して受信者を識別する場合、あなたのボットは[顧客マッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)の承認を受け、国コード、エリアコード、番号（例：`16505551212`）のみを含む必要があります。電話番号を使用する場合、名と姓の構成も可能です。 |
| メディアタイプ | (必須) 受信者に送信するメディアのタイプ。サポートされている値は`Image`、`Audio`、`Video`、または`File`です。 |
| メディアURL | (必須) 送信されるメディアのウェブ`URL`アドレス。 |
| 再利用可能か | このオプションを選択して、他の受信者に送信できる再利用可能なコンテンツとしてコンテンツをマークします。 |
| クイック返信| クイック返信は、タイトルとオプションの画像を含む最大11個のボタンのセットを会話中に提示する方法を提供し、コンポーザーの上に目立って表示されます。また、クイック返信を使用してユーザーの位置情報、メールアドレス、電話番号を要求することもできます。サポートされているのは配列属性のみであり、ここで指定される配列は同じサイズでなければなりません。詳細については、[Facebook: クイック返信ドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies)を参照してください。 |
| メタデータ | [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/reference/webhook-events/)を通じて`message_echoes`フィールドで配信されるカスタム文字列。1,000文字制限。メタデータは自動的にテンプレート機能とテンプレート変数をサポートします。詳細については、を参照してください。 |
| メタデータテンプレート変数 | メタデータのテンプレート変数を提供します。詳細については、を参照してください。 |
| 通知タイプ | プッシュ通知のタイプ。&lt;ul&gt;&lt;li&gt;**通常:** 音/振動（構成されていない場合に使用されます）。&lt;/li&gt;&lt;li&gt;**サイレントプッシュ:** 画面上の通知のみ。&lt;/li&gt;&lt;li&gt;**ノープッシュ:** 通知なし&lt;/li&gt;&lt;/ul&gt;。 |
| メッセージタグ | **メッセージングタイプ**が`Message Tag`に構成されている場合に使用します。すべてのメッセージタグの完全なリストについては、[Facebook: メッセージタグドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)を参照してください。 |

### 送信者アクションを送信


#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メッセージングタイプ | (必須) 送信されるメッセージのメッセージングタイプを指定し、特定のメッセージングタイプに対するポリシーの遵守とユーザーの構成を尊重するためのより明確な方法です。詳細については、[Facebook: メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`)を参照してください。 |
| 受信者識別子 | (必須) メッセージを送信する受信者を識別します。ID、電話番号、またはユーザー参照が構成されている必要があります。受信者を識別するために電話番号を使用する場合、あなたのボットは[カスタマーマッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)の承認を受け、国コード、地域コード、番号（例：`16505551212`）のみを含む必要があります。電話番号を使用する場合、名と姓の構成も可能です。 |
| 送信者アクション | (必須) 受信者に表示する送信者アクション。サポートされる値は `typing_on`、`typing_off`、または `mark_seen` です。 |
| メッセージタグ | **メッセージングタイプ**が `メッセージタグ`に構成されている場合に使用します。すべてのメッセージタグの完全なリストについては、[Facebook: メッセージタグのドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)を参照してください。 |

### テンプレートメッセージの送信（高度）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| メッセージングタイプ | (必須) 送信されるメッセージのメッセージングタイプを指定し、特定のメッセージングタイプに対するポリシーの遵守とユーザーの構成を尊重するためのより明確な方法です。詳細については、[Facebook: メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`)を参照してください。 |
| 受信者識別子 | (必須) メッセージを送信する受信者を識別します。ID、電話番号、またはユーザー参照が構成されている必要があります。受信者を識別するために電話番号を使用する場合、あなたのボットは[カスタマーマッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)の承認を受け、国コード、地域コード、番号（例：`16505551212`）のみを含む必要があります。電話番号を使用する場合、名と姓の構成も可能です。 |
| テンプレートペイロード | (必須) 送信されるテンプレートペイロード。ペイロードはテンプレート機能とテンプレート変数をサポートしています。JSON形式でフォーマットされるべきです：`{ &#34;template_type&#34;: &#34;&lt;TEMPLATE_TYPE&gt;&#34;, ... }`。具体的なペイロード内容については、[メッセージテンプレートのドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/templates)を参照してください。 |
| テンプレート変数 | テンプレートエンジンを使用する場合、テンプレート変数が使用されます。これらのフィールドは属性をテンプレートペイロードで使用される変数名にマッピングします。詳細については、を参照してください。 |
| クイック返信 | クイック返信は、会話中に最大11個のボタンをタイトルとオプションの画像を含めて提示する方法を提供し、コンポーザーの上に目立って表示されます。また、クイック返信を使用してユーザーの位置情報、メールアドレス、電話番号を要求することもできます。サポートされるのは配列属性のみで、ここで指定される配列は同じサイズでなければなりません。詳細については、[Facebook: クイック返信のドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies)を参照してください。 |
| メタデータ | [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/reference/webhook-events/)を通じて `message_echoes` フィールドで配信されるカスタム文字列。1,000文字制限。メタデータは自動的にテンプレート機能とテンプレート変数をサポートします。詳細については、[Trimou テンプレートエンジン]()を参照してください。 |
| メタデータテンプレート変数 | テンプレートエンジンを使用する場合、テンプレート変数が使用されます。これらのフィールドは属性をメタデータで使用される変数名にマッピングします。詳細については、を参照してください。 |
| 通知タイプ | プッシュ通知のタイプ。&lt;ul&gt;&lt;li&gt;**通常:** 音/振動（構成されていない場合に使用されます）。&lt;/li&gt;&lt;li&gt;**サイレントプッシュ:** 画面上の通知のみ。&lt;/li&gt;&lt;li&gt;**ノープッシュ:** 通知なし&lt;/li&gt;&lt;/ul&gt;。 |
| メッセージタグ | **メッセージングタイプ**が `メッセージタグ`に構成されている場合に使用します。すべてのメッセージタグの完全なリストについては、[Facebook: メッセージタグのドキュメント](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)を参照してください。 |

## ベンダー文書

* [ページアクセストークン](https://developers.facebook.com/docs/facebook-login/access-tokens#pagetokens)
* [メッセージングタイプ](https://developers.facebook.com/docs/messenger-platform/send-messages/#messaging_types)
* [カスタマーマッチング](https://developers.facebook.com/docs/messenger-platform/customer-matching)
* [クイック返信](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies)
* [メッセージタグ](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)
* [メッセージテンプレート](https://developers.facebook.com/docs/messenger-platform/send-messages/templates)

##### API

* [Facebook 送信 HTTP API](https://developers.facebook.com/docs/messenger-platform/reference/send-api)