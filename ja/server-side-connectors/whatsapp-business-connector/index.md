---
title: WhatsApp Businessコネクター構成ガイド
description: この記事では、WhatsApp Businessコネクターの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/whatsapp-business-connector/
---
## API情報

このコネクターは、以下のベンダーAPIを使用します。

* API名：Facebook Graph API - WhatsApp Business API
* APIバージョン：v25.0
* APIエンドポイント：`https://graph.facebook.com`
* ドキュメント：[WhatsApp Business Platform Cloud API](https://developers.facebook.com/docs/whatsapp/cloud-api)

## 構成

コネクターマーケットプレイスに移動し、新しいコネクターを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクターを追加した後、以下の構成を行います。

* **アクセストークン**：（必須）Facebookシステムユーザーのアクセストークン。
<blockquote>
アクセストークンを使用してコネクターを認証する場合は、Businessシステムユーザーのアクセストークンを使用することをお勧めします。頻繁に期限切れとなり、数時間ごとに再生成する必要があるユーザーアクセストークンとは異なり、Businessシステムユーザートークンは有効期間が長く（通常は最大60日間）、より安定した信頼性の高い認証方法を提供します。Businessシステムユーザーのアクセストークンを取得するには、Facebook Business Managerでシステムユーザーを作成し、必要なアセットと権限を割り当てたうえで、Facebookアプリダッシュボードからトークンを生成する必要があります。詳細な手順については、[WhatsApp：WhatsApp Business Platform用のシステムユーザーアクセストークンの取得](https://developers.facebook.com/docs/whatsapp/business-management-api/get-started#system-user-access-token)を参照してください。
</blockquote>


コネクターの構成が完了したら、**完了**をクリックします。

## メッセージタイプ

WhatsApp Business APIには、主に次の2種類のメッセージタイプがあります。

* **テンプレートメッセージ**はWhatsAppによって事前承認されており、アラート、更新情報、再エンゲージメントメッセージの送信など、企業側から開始する会話向けに設計されています。これらのメッセージには変数を含めることができ、過去24時間以内に企業へ連絡していないユーザーにメッセージを送信する場合に必要です。

* **テキストベースメッセージ**はセッションベースであり、ユーザーが開始したメッセージに対して24時間以内に返信する場合にのみ使用できます。動的な会話形式のコンテンツを柔軟に作成できますが、依頼されていないアウトリーチには使用できません。

会話を開始する場合や24時間の時間枠外で通知を送信する場合はテンプレートメッセージを使用し、ユーザーとのアクティブなセッション中にリアルタイムのやり取りを維持する場合はテキストベースメッセージを使用します。

テンプレートメッセージを送信する前に、テンプレートを作成する必要があります。詳細については、[WhatsApp：WhatsApp Businessアカウント用メッセージテンプレートの作成](https://www.facebook.com/business/help/2055875911147364)を参照してください。

|アクション名|訪問プロファイル|イベントデータ|
|---|---|---|
|テキストメッセージを送信|✓|✓|
|メッセージテンプレートを送信|✓|✓|

**続行**をクリックして、コネクターアクションを構成します。アクションの名前を入力し、アクションタイプを選択します。

以下のセクションでは、各アクションのパラメーターとオプションを構成する方法について説明します。

### テキストメッセージを送信

#### パラメーター

|パラメーター|説明|
|---|---|
|送信元|メッセージの送信元として使用する電話番号ID。|
|送信先|メッセージの送信先となるWhatsApp IDまたは電話番号。詳細については、[WhatsApp：電話番号の書式構成](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/phone-numbers#formatting)を参照してください。|
|メッセージ|メッセージのテキスト。URLや書式を含めることができます。使用例については、[WhatsApp：テキストメッセージの送信](https://developers.facebook.com/docs/whatsapp/cloud-api/guides/send-messages#text-messages)を参照してください。|
|URLをプレビュー|テキストメッセージ内のURLプレビューを有効または無効にするブール値（`true`または`false`）。詳細については、[WhatsApp：テキストメッセージでのURLの送信](https://developers.facebook.com/docs/whatsapp/api/messages/text#urls)を参照してください。|

### メッセージテンプレートを送信

#### パラメーター

|パラメーター|説明|
|---|---|
|送信元|メッセージの送信元として使用する電話番号ID。|
|送信先|メッセージの送信先となるWhatsApp IDまたは電話番号。詳細については、[WhatsApp：電話番号の書式構成](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/phone-numbers#formatting)を参照してください。|
|メッセージテンプレート|メッセージテンプレートを指定します。使用例については、[WhatsApp：メッセージテンプレートの送信](https://developers.facebook.com/docs/whatsapp/cloud-api/guides/send-message-templates)を参照してください。<br>テンプレートには、有効なJSONオブジェクト形式が必要です。<br>**メッセージテンプレート変数**セクションで指定したテンプレート変数を使用できます。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。|
|メッセージテンプレート変数|**メッセージテンプレート**のデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ネストされたテンプレート変数には、ドット記法を使用して名前を付けます（例：`items.name`）。<br>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます。|