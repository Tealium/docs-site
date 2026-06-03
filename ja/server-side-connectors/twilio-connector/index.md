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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタの概要]()を参照してください。

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
|アカウントSID|  &lt;ul&gt;&lt;li&gt;コンソールでアカウントSIDを見つけることができます。&lt;/li&gt;&lt;li&gt;このエンドポイントについての詳細は、[Sending Messages](https://www.twilio.com/docs/api/messaging/send-messages#http-post-to-messages)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|To|  &lt;ul&gt;&lt;li&gt;宛先の電話番号。&lt;/li&gt;&lt;li&gt;プラス記号(`&#43;`)と国コードを含む(E.164形式)。&lt;/li&gt;&lt;li&gt;例：`&#43;16175551212`&lt;/li&gt;&lt;/ul&gt; |
|From|  &lt;ul&gt;&lt;li&gt;Twilioの電話番号（E.164形式）または、送信したいメッセージのタイプに対応した英数字の送信者ID。&lt;/li&gt;&lt;li&gt;Twilioから購入した電話番号またはショートコードがここで機能します。&lt;/li&gt;&lt;li&gt;自分の携帯電話番号からメッセージを「偽装」することはできません。メッセージの**From**電話番号または送信者IDを決定するために、以下のパラメータの少なくとも1つをPOSTする必要があります：`From`、`Messaging Service SID` &lt;/li&gt;&lt;/ul&gt; |
|Messaging Service SID|  &lt;ul&gt;&lt;li&gt;このメッセージに関連付けたいMessaging Serviceの34文字の一意のID。&lt;/li&gt;&lt;li&gt;このパラメータを構成すると、構成したMessaging Service SettingsとCopilot Featuresが使用されます。&lt;/li&gt;&lt;li&gt;このパラメータのみが構成されている場合、Twilioは有効なCopilot機能を使用して配信用の**From**電話番号を選択します。メッセージの**From**電話番号または送信者IDを決定するために、以下のパラメータの少なくとも1つをPOSTする必要があります：`From`、`Messaging Service SID` &lt;/li&gt;&lt;/ul&gt; |
|Body|  &lt;ul&gt;&lt;li&gt;送信したいメッセージのテキスト。最大1600文字まで。メッセージの内容のために、以下のパラメータの少なくとも1つをPOSTする必要があります：`Body`、`MediaUrl` &lt;/li&gt;&lt;/ul&gt; |
|Media URL|  &lt;ul&gt;&lt;li&gt;メッセージと一緒に送信したいメディアのURL。&lt;/li&gt;&lt;li&gt;GIF、PNG、JPEGのコンテンツは現在サポートされており、受信者のデバイスで正しくフォーマットされます。&lt;/li&gt;&lt;li&gt;他のファイルタイプもAPIによって受け入れられます。&lt;/li&gt;&lt;li&gt;メディアのサイズ制限は5メガバイト（MB）です。&lt;/li&gt;&lt;li&gt;メッセージ本文に複数の画像を送信するには、POSTリクエストに複数の`MediaUrls`値を提供します。&lt;/li&gt;&lt;li&gt;メッセージごとに最大10の`MediaUrls`を含めることができます メッセージの内容のために、以下のパラメータの少なくとも1つをPOSTする必要があります：`Body`、`MediaUrl` &lt;/li&gt;&lt;/ul&gt; |
|Status Callback|  &lt;ul&gt;&lt;li&gt;メッセージのステータスが以下のいずれかに変更するたびにTwilioがPOSTするURL：  &lt;ul&gt;&lt;li&gt;`queued`&lt;/li&gt;&lt;li&gt;`failed`&lt;/li&gt;&lt;li&gt;`sent`&lt;/li&gt;&lt;li&gt;`delivered`&lt;/li&gt;&lt;li&gt;`undelivered`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Twilioは`MessageSid`と他の標準的なリクエストパラメータ、および`MessageStatus`と`ErrorCode`をPOSTします。&lt;/li&gt;&lt;li&gt;このパラメータが`MessagingServiceSid`と一緒に渡されると、TwilioはMessaging ServiceのStatus Callback URLを上書きします。&lt;/li&gt;&lt;li&gt;URLには有効なホスト名が含まれている必要があります。&lt;/li&gt;&lt;li&gt;ホスト名にアンダースコア文字(`_`)は許可されていません。&lt;/li&gt;&lt;/ul&gt; |
|Application SID|  &lt;ul&gt;&lt;li&gt;Twilioは`MessageSid`および`MessageStatus=sent`または`MessageStatus=failed`をこのアプリケーションの`MessageStatusCallback`プロパティのURLにPOSTします。&lt;/li&gt;&lt;li&gt;上記の`StatusCallback`パラメータも渡される場合、アプリケーションの`MessageStatusCallback`パラメータが優先されます。&lt;/li&gt;&lt;/ul&gt; |
|Max Price|  &lt;ul&gt;&lt;li&gt;メッセージが配信されるための最大合計価格（米ドルで`0.0001`まで）。&lt;/li&gt;&lt;li&gt;すべてのメッセージは配信待ちの状態でキューに入れられます。&lt;/li&gt;&lt;li&gt;後で`Sent`または`Failed`のステータス変更とともにStatus Callback URLにPOSTリクエストが行われます。&lt;/li&gt;&lt;li&gt;メッセージの価格がこの値を超えると、メッセージは失敗し、送信されません。&lt;/li&gt;&lt;li&gt;`MaxPrice`が構成されていない場合、メッセージのすべての価格が受け入れられます。&lt;/li&gt;&lt;/ul&gt; |
|Provide Feedback|  &lt;ul&gt;&lt;li&gt;トラッキング可能なユーザーアクションを持つメッセージを送信していて、Message Feedback APIを使用してメッセージの配信を確認するつもりであれば、この値を`true`に構成します。&lt;/li&gt;&lt;li&gt;このパラメータはデフォルトで`false`に構成されています&lt;/li&gt;&lt;/ul&gt; |
|Validity Period|  &lt;ul&gt;&lt;li&gt;メッセージがTwilioのキューに残ることができる秒数。&lt;/li&gt;&lt;li&gt;この時間制限を超えると、メッセージは失敗し、後でStatus Callback URLにPOSTリクエストが行われます。&lt;/li&gt;&lt;li&gt;有効な値は`1`から`14400`秒（デフォルト）です。&lt;/li&gt;&lt;li&gt;Twilioは、キャリアがメッセージを受け入れた後にメッセージがキューに入れられないことを保証できません。&lt;/li&gt;&lt;li&gt;5秒未満の有効期間を構成することはお勧めしません&lt;/li&gt;&lt;/ul&gt; |
