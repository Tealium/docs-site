---
title: WhatsAppビジネスコネクタ構成ガイド
description: この記事では、WhatsAppビジネスコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/whatsapp-business-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Facebook Graph API - WhatsApp Business API
* APIバージョン：v25.0
* APIエンドポイント：`https://graph.facebook.com`
* ドキュメント：[WhatsApp Business Platform Cloud API](https://developers.facebook.com/docs/whatsapp/cloud-api)

## 構成

コネクタマーケットプレイスにアクセスして新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アクセストークン**：（必須）Facebookシステムユーザーのアクセストークン。コネクタをアクセストークンを使用して認証する場合、ビジネスシステムユーザーのアクセストークンを使用することをお勧めします。ユーザーアクセストークンとは異なり、頻繁に期限切れになり、数時間ごとに再生成が必要なのに対し、ビジネスシステムユーザートークンは有効期限が長く（通常は最大60日）、より安定した信頼性の高い認証方法を提供します。ビジネスシステムユーザーアクセストークンを取得するには、Facebookビジネスマネージャーでシステムユーザーを作成し、必要なアセットと権限を割り当て、その後Facebookアプリダッシュボードでトークンを生成する必要があります。詳細な手順については、[WhatsApp: WhatsApp Business Platform用システムユーザーアクセストークンの取得](https://developers.facebook.com/docs/whatsapp/business-management-api/get-started#system-user-access-token)を参照してください。

コネクタの構成が完了したら、**完了**をクリックします。

## メッセージタイプ

WhatsApp Business APIでは、主に以下の2種類のメッセージタイプがあります：

* **テンプレートメッセージ**はWhatsAppによって事前に承認されており、アラート、更新情報、再エンゲージメントメッセージなど、ビジネスからの会話を開始するために設計されています。これらのメッセージには変数を含めることができ、ビジネスから24時間以内に連絡がなかったユーザーにメッセージを送る場合に必要です。

* **テキストベースのメッセージ**はセッションベースであり、24時間のウィンドウ内でユーザーからのメッセージに応答するためにのみ使用できます。これらはダイナミックな会話コンテンツに対してより大きな柔軟性を提供しますが、勧誘のためには使用できません。

24時間のウィンドウ外で会話を開始する場合や通知を送信する場合はテンプレートメッセージを使用し、ユーザーとのアクティブなセッション中にリアルタイムのやり取りを維持するためにテキストベースのメッセージを使用します。

テンプレートメッセージを送信する前に、テンプレートを作成する必要があります。詳細については、[WhatsApp: WhatsApp Businessアカウント用メッセージテンプレートの作成](https://www.facebook.com/business/help/2055875911147364)を参照してください。

|アクション名| AudienceStream| EventStream|
|---| ---| ---|
|テキストメッセージを送信| ✓| ✓|
|メッセージテンプレートを送信| ✓| ✓|

コネクタアクションの構成を続けるには、**続行**をクリックします。アクションの名前を入力し、アクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### テキストメッセージを送信

#### パラメータ

|パラメータ| 説明|
|---| ---|
|送信元| メッセージを送信する電話番号ID。|
|送信先| メッセージを送信するWhatsApp IDまたは電話番号。詳細については、[WhatsApp: 電話番号、フォーマット](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/phone-numbers#formatting)を参照してください。|
|メッセージ| メッセージのテキストで、URLやフォーマットを含むことができます。使用例については、[WhatsApp: テキストメッセージの送信](https://developers.facebook.com/docs/whatsapp/cloud-api/guides/send-messages#text-messages)を参照してください。|
|プレビューURL| テキストメッセージ内のURLプレビューを許可または無効にするブール値（`true`または`false`）。詳細については、[WhatsApp: テキストメッセージでのURLの送信](https://developers.facebook.com/docs/whatsapp/api/messages/text#urls)を参照してください。|

### メッセージテンプレートを送信

#### パラメータ

|パラメータ| 説明|
|---| ---|
|送信元| メッセージを送信する電話番号ID。|
|送信先| メッセージを送信するWhatsApp IDまたは電話番号。詳細については、[WhatsApp: 電話番号、フォーマット](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/phone-numbers#formatting)を参照してください。|
|メッセージテンプレート| メッセージテンプレートを提供します。使用例については、[WhatsApp: メッセージテンプレートの送信](https://developers.facebook.com/docs/whatsapp/cloud-api/guides/send-message-templates)を参照してください。&lt;br&gt; テンプレートは有効なJSONオブジェクト形式を期待します。&lt;br&gt; **メッセージテンプレート変数**セクションで指定されたテンプレート変数を使用することができます。詳細については、を参照してください。|
|メッセージテンプレート変数| **メッセージテンプレート**のデータ入力としてテンプレート変数を提供します。詳細については、を参照してください。&lt;br&gt; ドット表記（例：`items.name`）でネストされたテンプレート変数を名前付けします。&lt;br&gt; ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。