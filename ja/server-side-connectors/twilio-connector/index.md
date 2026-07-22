---
title: Twilioコネクタ構成ガイド
description: この記事では、Twilioコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/twilio-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|SMSまたはMMSを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタの概要](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アカウントSID（ユーザー名）**
  * REST APIへのHTTPリクエストはHTTP Basic認証で保護されています。
  * HTTP Basic認証のユーザー名とパスワードとして、TwilioアカウントのSIDと認証トークンを使用します。
  * 詳細については、[SMS API: Messaging](https://www.twilio.com/docs/api/messaging)を参照してください。

* **認証トークン（パスワード）**
  * REST APIへのHTTPリクエストはHTTP Basic認証で保護されています。
  * HTTP Basic認証のユーザー名とパスワードとして、TwilioアカウントのSIDと認証トークンを使用します。
  * 詳細については、[SMS API: Messaging](https://www.twilio.com/docs/api/messaging)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタのアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - SMSまたはMMSを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アカウントSID|  <ul><li>コンソールでアカウントSIDを見つけることができます。</li><li>このエンドポイントについての詳細は、[Sending Messages](https://www.twilio.com/docs/api/messaging/send-messages#http-post-to-messages)を参照してください。</li></ul> |
|To|  <ul><li>宛先の電話番号。</li><li>プラス記号(`+`)と国コードを含む(E.164形式)。</li><li>例：`+16175551212`</li></ul> |
|From|  <ul><li>Twilioの電話番号（E.164形式）または、送信したいメッセージのタイプに対応した英数字の送信者ID。</li><li>Twilioから購入した電話番号またはショートコードがここで機能します。</li><li>自分の携帯電話番号からメッセージを「偽装」することはできません。
<blockquote>
メッセージの**From**電話番号または送信者IDを決定するために、以下のパラメータの少なくとも1つをPOSTする必要があります：`From`、`Messaging Service SID`
</blockquote>
 </li></ul> |
|Messaging Service SID|  <ul><li>このメッセージに関連付けたいMessaging Serviceの34文字の一意のID。</li><li>このパラメータを構成すると、構成したMessaging Service SettingsとCopilot Featuresが使用されます。</li><li>このパラメータのみが構成されている場合、Twilioは有効なCopilot機能を使用して配信用の**From**電話番号を選択します。
<blockquote>
メッセージの**From**電話番号または送信者IDを決定するために、以下のパラメータの少なくとも1つをPOSTする必要があります：`From`、`Messaging Service SID`
</blockquote>
 </li></ul> |
|Body|  <ul><li>送信したいメッセージのテキスト。最大1600文字まで。
<blockquote>
メッセージの内容のために、以下のパラメータの少なくとも1つをPOSTする必要があります：`Body`、`MediaUrl`
</blockquote>
 </li></ul> |
|Media URL|  <ul><li>メッセージと一緒に送信したいメディアのURL。</li><li>GIF、PNG、JPEGのコンテンツは現在サポートされており、受信者のデバイスで正しくフォーマットされます。</li><li>他のファイルタイプもAPIによって受け入れられます。</li><li>メディアのサイズ制限は5メガバイト（MB）です。</li><li>メッセージ本文に複数の画像を送信するには、POSTリクエストに複数の`MediaUrls`値を提供します。</li><li>メッセージごとに最大10の`MediaUrls`を含めることができます 
<blockquote>
メッセージの内容のために、以下のパラメータの少なくとも1つをPOSTする必要があります：`Body`、`MediaUrl`
</blockquote>
 </li></ul> |
|Status Callback|  <ul><li>メッセージのステータスが以下のいずれかに変更するたびにTwilioがPOSTするURL：  <ul><li>`queued`</li><li>`failed`</li><li>`sent`</li><li>`delivered`</li><li>`undelivered`</li></ul> </li><li>Twilioは`MessageSid`と他の標準的なリクエストパラメータ、および`MessageStatus`と`ErrorCode`をPOSTします。</li><li>このパラメータが`MessagingServiceSid`と一緒に渡されると、TwilioはMessaging ServiceのStatus Callback URLを上書きします。</li><li>URLには有効なホスト名が含まれている必要があります。</li><li>ホスト名にアンダースコア文字(`_`)は許可されていません。</li></ul> |
|Application SID|  <ul><li>Twilioは`MessageSid`および`MessageStatus=sent`または`MessageStatus=failed`をこのアプリケーションの`MessageStatusCallback`プロパティのURLにPOSTします。</li><li>上記の`StatusCallback`パラメータも渡される場合、アプリケーションの`MessageStatusCallback`パラメータが優先されます。</li></ul> |
|Max Price|  <ul><li>メッセージが配信されるための最大合計価格（米ドルで`0.0001`まで）。</li><li>すべてのメッセージは配信待ちの状態でキューに入れられます。</li><li>後で`Sent`または`Failed`のステータス変更とともにStatus Callback URLにPOSTリクエストが行われます。</li><li>メッセージの価格がこの値を超えると、メッセージは失敗し、送信されません。</li><li>`MaxPrice`が構成されていない場合、メッセージのすべての価格が受け入れられます。</li></ul> |
|Provide Feedback|  <ul><li>トラッキング可能なユーザーアクションを持つメッセージを送信していて、Message Feedback APIを使用してメッセージの配信を確認するつもりであれば、この値を`true`に構成します。</li><li>このパラメータはデフォルトで`false`に構成されています</li></ul> |
|Validity Period|  <ul><li>メッセージがTwilioのキューに残ることができる秒数。</li><li>この時間制限を超えると、メッセージは失敗し、後でStatus Callback URLにPOSTリクエストが行われます。</li><li>有効な値は`1`から`14400`秒（デフォルト）です。</li><li>Twilioは、キャリアがメッセージを受け入れた後にメッセージがキューに入れられないことを保証できません。</li><li>5秒未満の有効期間を構成することはお勧めしません</li></ul> |
