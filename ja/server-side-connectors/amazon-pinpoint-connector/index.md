---
title: Amazon Pinpoint コネクタ構成ガイド
description: この記事では、Amazon Pinpoint コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/amazon-pinpoint-connector/
---
## API 情報

このコネクタは以下のベンダー API を使用します：

* API 名: Amazon Pinpoint API
* API バージョン: v1
* API エンドポイント: `https://pinpoint.us-east-1.amazonaws.com`
* ドキュメント: [Amazon Pinpoint ドキュメント](https://docs.aws.amazon.com/pinpoint/latest/apireference/welcome.html)

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|メッセージ送信| ✓| ✓|
|プッシュ通知送信| ✓| ✓|
|テンプレート送信| ✓| ✓|
|イベント登録| ✓| ✓|
|エンドポイント更新| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスにアクセスして新しいコネクタを追加します。コネクタの追加方法については、[コネクタ概要]() の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アクセスキー**
  * 必須：IAM ユーザーのアクセスキーを提供してください
  * 関連する IAM ポリシー（IAM ユーザーまたは仮定されたロール用）は `mobiletargeting:*`, `ses:*`, `sms-voice:*` の権限を付与する必要があります。
  * 詳細については、[Amazon Pinpoint](https://docs.aws.amazon.com/pinpoint/latest/developerguide/security_iam_service-with-iam.html) を参照してください。

* **シークレットキー**
  * 必須
  * IAM ユーザーのシークレットキーを提供してください

* **リージョン**
  * 必須
  * リージョンを選択してください。

* **ロールの仮定: ARN**
  * オプション
  * 仮定するロールの Amazon リソース名 (ARN) を提供してください。
  * 例: `arn:aws:iam::222222222222:role/myrole`
  * 詳細については、[IAM ロールへの切り替え](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html) を参照してください。

* **ロールの仮定: セッション名**
  * オプション
  * 仮定されたロールセッションの識別子を提供してください。

* **ロールの仮定: 外部 ID**
  * オプション
  * 外部識別子を提供してください。
  * 詳細については、[外部 ID の使用方法](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html) を参照してください。

## アクション構成 - パラメータとオプション

**次へ** をクリックするか、**アクション** タブに進みます。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - メッセージ送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリケーション ID|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;アプリケーションの一意の識別子。&lt;/li&gt;&lt;li&gt;この識別子は Amazon Pinpoint コンソールでプロジェクト ID として表示されます。&lt;/li&gt;&lt;/ul&gt; |
|メッセージタイプ|  &lt;ul&gt;&lt;li&gt;メッセージタイプ&lt;/li&gt;&lt;li&gt;オプションは **Email**, **SMS**, または **Voice** です。  &lt;ul&gt;&lt;li&gt;アドレス (テンプレート)、エンドポイント (テンプレート)、または宛先が必要で、それぞれ1つのみ許可されます。&lt;/li&gt;&lt;li&gt;宛先、本文、およびタイトルのフィールドは、アドレス (テンプレート) を構築するために使用されます。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;SMS  &lt;ul&gt;&lt;li&gt;SMS メッセージタイプの本文は必須です。&lt;/li&gt;&lt;li&gt;メッセージタイプの有効な値は `TRANSACTIONAL` または `PROMOTIONAL` です。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|テンプレート変数|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;テンプレートにデータ入力としてテンプレート変数を提供してください。&lt;/li&gt;&lt;li&gt;詳細については  を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名前付けしてください。&lt;/li&gt;&lt;li&gt;例: `items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。&lt;/li&gt;&lt;li&gt;詳細については  を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは、サポートされるフィールドに名前で二重中括弧で注入されます。&lt;/li&gt;&lt;li&gt;例: `{{SomeTemplateName}}`。&lt;/li&gt;&lt;/ul&gt; |
|文字セット|  &lt;ul&gt;&lt;li&gt;メッセージ内容の文字セットマッピング。&lt;/li&gt;&lt;/ul&gt; |
|HTML パート|  &lt;ul&gt;&lt;li&gt;テキストパートまたはHTMLパートのいずれか一方のみが許可されます。&lt;/li&gt;&lt;/ul&gt; |
|件名|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;メールの件名。&lt;/li&gt;&lt;/ul&gt; |
|テキストパート|  &lt;ul&gt;&lt;li&gt;テキストまたはHTML。&lt;/li&gt;&lt;li&gt;すべてのテキストまたはすべてのHTMLを使用します。&lt;/li&gt;&lt;/ul&gt; |
|生のメール|  &lt;ul&gt;&lt;li&gt;タイプ=Emailが選択された場合のみ使用されます。&lt;/li&gt;&lt;li&gt;生のMIMEメッセージとして表されるメールメッセージ。&lt;/li&gt;&lt;li&gt;メッセージ全体をbase64でエンコードする必要があります。&lt;/li&gt;&lt;/ul&gt; |

### アクション - プッシュ通知送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリケーション ID|  &lt;ul&gt;&lt;li&gt;アプリケーションの一意の識別子。&lt;/li&gt;&lt;li&gt;この識別子は Amazon Pinpoint コンソールでプロジェクト ID として表示されます。&lt;/li&gt;&lt;/ul&gt; |
|プッシュ通知タイプ|  &lt;ul&gt;&lt;li&gt;プッシュ通知タイプ。&lt;/li&gt;&lt;li&gt;カスタムを入力するか、**ADM**, **AMPS**, **BAIDU**, または **GCM** を選択します。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート変数|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;テンプレートにデータ入力としてテンプレート変数を提供してください。&lt;/li&gt;&lt;li&gt;詳細については  を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名前付けしてください。&lt;/li&gt;&lt;li&gt;例: `items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。&lt;/li&gt;&lt;li&gt;詳細については  を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは、サポートされるフィールドに名前で二重中括弧で注入されます。&lt;/li&gt;&lt;li&gt;例: `{{SomeTemplateName}}`。&lt;/li&gt;&lt;/ul&gt; |

### アクション - テンプレート送信


#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリケーションID|  &lt;ul&gt;&lt;li&gt;アプリケーションの一意の識別子。&lt;/li&gt;&lt;li&gt;この識別子はAmazon PinpointコンソールでプロジェクトIDとして表示されます。&lt;/li&gt;&lt;/ul&gt; |
|テンプレートタイプ|  &lt;ul&gt;&lt;li&gt;テンプレートタイプ&lt;/li&gt;&lt;li&gt;オプションは **Email**、**Push**、**SMS**、**Voice**、または **Custom**。&lt;/li&gt;&lt;/ul&gt; |
|アドレス（テンプレート）|  &lt;ul&gt;&lt;li&gt;アドレス（テンプレート）、エンドポイント（テンプレート）またはデスティネーションが必要です。&lt;/li&gt;&lt;li&gt;アドレス（テンプレート）、エンドポイント（テンプレート）またはデスティネーションのいずれか一つのみが許可されます。&lt;/li&gt;&lt;li&gt;デスティネーション、ボディ、タイトルのフィールドを使用してアドレス（テンプレート）を構築します。&lt;/li&gt;&lt;/ul&gt; |
|コンテキスト（テンプレート）|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;カスタム属性をアドレスの属性にマッピングするオブジェクトで、メッセージに添付されます。&lt;/li&gt;&lt;li&gt;属性は大文字と小文字を区別します。&lt;/li&gt;&lt;li&gt;プッシュ通知の場合、このペイロードは `data.pinpoint` オブジェクトに追加されます。&lt;/li&gt;&lt;li&gt;メールまたはテキストメッセージの場合、このペイロードはメール/SMS配信受領イベント属性に追加されます。&lt;/li&gt;&lt;/ul&gt; |
|デスティネーション|  &lt;ul&gt;&lt;li&gt;アドレス（テンプレート）、エンドポイント（テンプレート）またはデスティネーションが必要です。&lt;/li&gt;&lt;li&gt;アドレス（テンプレート）、エンドポイント（テンプレート）またはデスティネーションのいずれか一つのみが許可されます。&lt;/li&gt;&lt;li&gt;デスティネーション、ボディ、タイトルのフィールドを使用してアドレス（テンプレート）を構築します。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイント（テンプレート）|  &lt;ul&gt;&lt;li&gt;アドレス（テンプレート）、エンドポイント（テンプレート）またはデスティネーションが必要です。&lt;/li&gt;&lt;li&gt;アドレス（テンプレート）、エンドポイント（テンプレート）またはデスティネーションのいずれか一つのみが許可されます。&lt;/li&gt;&lt;li&gt;デスティネーション、ボディ、タイトルのフィールドを使用してアドレス（テンプレート）を構築します。&lt;/li&gt;&lt;/ul&gt; |
|名前|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;メッセージに使用するメッセージテンプレートの名前。&lt;/li&gt;&lt;li&gt;指定された場合、この値は既存のメッセージテンプレートの名前と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|トレースID|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;メッセージのトレース用の一意の識別子。&lt;/li&gt;&lt;li&gt;この識別子はメッセージイベントで表示されます。&lt;/li&gt;&lt;/ul&gt; |
|バージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;メッセージに使用するメッセージテンプレートのバージョンの一意の識別子。&lt;/li&gt;&lt;li&gt;指定された場合、この値は既存のテンプレートバージョンの識別子と一致する必要があります。&lt;/li&gt;&lt;li&gt;テンプレートのバージョンとバージョン識別子のリストを取得するには、[Template Versions](https://docs.aws.amazon.com/pinpoint/latest/apireference/templates-template-name-template-type-versions.html)リソースを使用します。&lt;/li&gt;&lt;li&gt;このプロパティの値を指定しない場合、Amazon Pinpointはテンプレートのアクティブバージョンを使用します。&lt;/li&gt;&lt;li&gt;アクティブバージョンは通常、最も最近レビューされ承認された使用バージョンであり、必ずしも最新バージョンではありません。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート変数|  &lt;ul&gt;&lt;li&gt;オプショナル&lt;/li&gt;&lt;li&gt;テンプレートにデータ入力としてテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名前付けします。&lt;/li&gt;&lt;li&gt;例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます&lt;/li&gt;&lt;/ul&gt; |
|テンプレート|  &lt;ul&gt;&lt;li&gt;オプショナル&lt;/li&gt;&lt;li&gt;URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。&lt;/li&gt;&lt;li&gt;例：`{{SomeTemplateName}}`&lt;/li&gt;&lt;/ul&gt; |

### アクション - イベントを追加する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリケーションID|  &lt;ul&gt;&lt;li&gt;アプリケーションの一意の識別子。&lt;/li&gt;&lt;li&gt;この識別子はAmazon PinpointコンソールでプロジェクトIDとして表示されます。&lt;/li&gt;&lt;/ul&gt; |
|アプリパッケージ名|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベントを記録するアプリのパッケージ名。&lt;/li&gt;&lt;/ul&gt; |
|アプリタイトル|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベントを記録するアプリのタイトル。&lt;/li&gt;&lt;/ul&gt; |
|アプリバージョンコード|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベントを記録するアプリのバージョン番号。&lt;/li&gt;&lt;/ul&gt; |
|クライアントSDKバージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;クライアントデバイスで実行されているSDKのバージョン。&lt;/li&gt;&lt;/ul&gt; |
|イベントタイプ|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベントの名前。&lt;/li&gt;&lt;/ul&gt; |
|SDK名|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベントを記録するために使用されるSDKの名前。&lt;/li&gt;&lt;/ul&gt; |
|タイムスタンプ|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベントが発生した日時。ISO 8601形式。&lt;/li&gt;&lt;/ul&gt; |
|イベント属性|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;イベントに関連付けられた1つ以上のカスタム属性。&lt;/li&gt;&lt;/ul&gt; |
|イベントメトリクス|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;イベントに関連付けられた1つ以上のカスタムメトリクス。&lt;/li&gt;&lt;/ul&gt; |
|期間|  &lt;ul&gt;&lt;li&gt;整数&lt;/li&gt;&lt;li&gt;セッションの期間（ミリ秒単位）。&lt;/li&gt;&lt;/ul&gt; |
|ID|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;セッションの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|開始タイムスタンプ|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;セッションが開始された日時。&lt;/li&gt;&lt;/ul&gt; |
|停止タイムスタンプ|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;セッションが終了した日時。&lt;/li&gt;&lt;/ul&gt; |
|アドレス|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;受信者の一意の識別子。デバイストークン、メールアドレス、または携帯電話番号など。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィックアプリバージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントに関連付けられたアプリのバージョン。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィックロケール|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントのロケール。&lt;/li&gt;&lt;li&gt;ISO 639-1 alpha-2コードに続いてアンダースコア(\_)、ISO 3166-1 alpha-2値の形式。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィックメーカー|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスの製造元。&lt;/li&gt;&lt;li&gt;例: **Apple**、**Samsung**&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィックモデル|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスのモデル名または番号。&lt;/li&gt;&lt;li&gt;例: **iPhone**、**SM-G900F**&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィックモデルバージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスのモデルバージョン。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィックプラットフォーム|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスのプラットフォーム。&lt;/li&gt;&lt;li&gt;例: **ios**&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィックプラットフォームバージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスのプラットフォームバージョン。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィックタイムゾーン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントのタイムゾーン。&lt;/li&gt;&lt;li&gt;`tz`データベース名値として指定される。例: **America/Los_Angeles**。&lt;/li&gt;&lt;/ul&gt; |
|有効日|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントが最後に更新された日時。ISO 8601 UTC形式。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントID|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントステータス|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントへのメッセージ送信またはプッシュ通知の送信を指定します。&lt;/li&gt;&lt;li&gt;有効な値は:  &lt;ul&gt;&lt;li&gt;**ACTIVE**: エンドポイントにメッセージが送信されます。&lt;/li&gt;&lt;li&gt;**INACTIVE**: エンドポイントにメッセージが送信されません。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;エンドポイントを作成または更新するとき、Amazon Pinpointは自動的にこの値を**ACTIVE**に構成します。&lt;/li&gt;&lt;li&gt;`address`プロパティで指定されたアドレスと同じアドレスを持つ別のエンドポイントを更新する場合、Amazon Pinpointは自動的にこの値を**INACTIVE**に構成します。&lt;/li&gt;&lt;/ul&gt; |
|ロケーションシティ|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントが位置している都市の名前。&lt;/li&gt;&lt;/ul&gt; |
|ロケーションカントリー|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントが位置している国または地域の2文字コード。ISO 3166-1 alpha-2形式。&lt;/li&gt;&lt;li&gt;例: **en_US** はアメリカ合衆国&lt;/li&gt;&lt;/ul&gt; |
|ロケーション緯度|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;li&gt;エンドポイントの位置の緯度座標。小数点以下1桁に丸められます。&lt;/li&gt;&lt;/ul&gt; |
|ロケーション経度|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;li&gt;エンドポイントの位置の経度座標。小数点以下1桁に丸められます。&lt;/li&gt;&lt;/ul&gt; |
|ロケーション郵便番号|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントが位置している地域の郵便番号または郵便番号。&lt;/li&gt;&lt;/ul&gt; |
|ロケーションリージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントが位置している地域の名前。&lt;/li&gt;&lt;li&gt;アメリカ合衆国内の場合、値は州の名前です。&lt;/li&gt;&lt;/ul&gt; |
|リクエストID|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントを作成または更新するリクエストの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|ユーザーID|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイント属性|  &lt;ul&gt;&lt;li&gt;エンドポイントを説明する1つ以上のカスタム属性。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントメトリクス|  &lt;ul&gt;&lt;li&gt;アプリがAmazon Pinpointに報告するエンドポイントの1つ以上のカスタムメトリクス。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントユーザー属性|  &lt;ul&gt;&lt;li&gt;名前と値の配列を関連付けることでユーザーを説明する1つ以上のカスタム属性。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントチャネルタイプ|  &lt;ul&gt;&lt;li&gt;エンドポイントにメッセージやプッシュ通知を送信する際に使用されるチャネル。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントオプトアウト|  &lt;ul&gt;&lt;li&gt;エンドポイントに関連付けられたユーザーがあなたからのメッセージやプッシュ通知の受信を拒否しているかどうかを指定します。&lt;/li&gt;&lt;/ul&gt; |

### アクション - エンドポイントの更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリケーションID|  &lt;ul&gt;&lt;li&gt;アプリケーションの一意の識別子。&lt;/li&gt;&lt;li&gt;この識別子はAmazon PinpointコンソールでプロジェクトIDとして表示されます。&lt;/li&gt;&lt;/ul&gt; |
|アドレス|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;デバイストークン、メールアドレス、または携帯電話番号など、受信者の一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィック アプリバージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントに関連付けられたアプリのバージョン。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィック ロケール|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントのロケール。&lt;/li&gt;&lt;li&gt;形式はISO 639-1アルファ2コード、アンダースコア(\_)、ISO 3166-1アルファ2値の順です。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィック メーカー|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスの製造者。&lt;/li&gt;&lt;li&gt;例: **Apple**、**Samsung**&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィック モデル|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスのモデル名または番号。&lt;/li&gt;&lt;li&gt;例: **iPhone**、**SM-G900F**&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィック モデルバージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスのモデルバージョン。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィック プラットフォーム|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスのプラットフォーム。&lt;/li&gt;&lt;li&gt;例: **ios**&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィック プラットフォームバージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントデバイスのプラットフォームバージョン。&lt;/li&gt;&lt;/ul&gt; |
|デモグラフィック タイムゾーン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントのタイムゾーン。&lt;/li&gt;&lt;li&gt;`tz`データベース名値として指定されます。例: **America/Los_Angeles**。&lt;/li&gt;&lt;/ul&gt; |
|有効日|  &lt;ul&gt;&lt;li&gt;ISO 8601 UTC形式の有効日。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントステータス|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントへのメッセージ送信またはプッシュ通知の送信を指定します。&lt;/li&gt;&lt;li&gt;有効な値:  &lt;ul&gt;&lt;li&gt;**ACTIVE**: エンドポイントへメッセージが送信されます。&lt;/li&gt;&lt;li&gt;**INACTIVE**: エンドポイントへメッセージが送信されません。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;エンドポイントを作成または更新するとき、Amazon Pinpointは自動的にこの値を**ACTIVE**に構成します。&lt;/li&gt;&lt;li&gt;`address`プロパティで指定されたアドレスと同じ別のエンドポイントを更新する場合、Amazon Pinpointは自動的にこの値を**INACTIVE**に構成します。&lt;/li&gt;&lt;/ul&gt; |
|ID|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;セッションの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|ロケーション シティ|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントが位置する都市の名前。&lt;/li&gt;&lt;/ul&gt; |
|ロケーション カントリー|  &lt;ul&gt;&lt;li&gt;ロケーション国&lt;/li&gt;&lt;li&gt;国はISO 369-1アルファ2コード、アンダースコア(\_)、ISO 3166-1アルファ2値の順で表されます。&lt;/li&gt;&lt;li&gt;例: **en_US** はアメリカ合衆国&lt;/li&gt;&lt;/ul&gt; |
|ロケーション 緯度|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;li&gt;エンドポイントの位置の緯度座標。小数点以下1桁に丸められます。&lt;/li&gt;&lt;/ul&gt; |
|ロケーション 経度|  &lt;ul&gt;&lt;li&gt;数値&lt;/li&gt;&lt;li&gt;エンドポイントの位置の経度座標。小数点以下1桁に丸められます。&lt;/li&gt;&lt;/ul&gt; |
|ロケーション 郵便番号|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントが位置する地域の郵便番号または郵便番号。&lt;/li&gt;&lt;/ul&gt; |
|ロケーション リージョン|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;エンドポイントが位置する地域の名前。&lt;/li&gt;&lt;li&gt;アメリカ合衆国内の場所の場合、値は州の名前です。&lt;/li&gt;&lt;/ul&gt; |
|リクエストID|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;リクエストまたはレスポンスの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|ユーザーID|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイント属性|  &lt;ul&gt;&lt;li&gt;エンドポイントを説明する1つ以上のカスタム属性。名前と値の配列を関連付けます。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントメトリクス|  &lt;ul&gt;&lt;li&gt;アプリがAmazon Pinpointに報告するエンドポイントの1つ以上のカスタムメトリック。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントユーザー属性|  &lt;ul&gt;&lt;li&gt;ユーザーを説明する1つ以上のカスタム属性。名前と値の配列を関連付けます。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントチャネルタイプ|  &lt;ul&gt;&lt;li&gt;エンドポイントへのメッセージ送信またはプッシュ通知の送信に使用されるチャネル。&lt;/li&gt;&lt;/ul&gt; |
|エンドポイントオプトアウト|  &lt;ul&gt;&lt;li&gt;エンドポイントに関連付けられたユーザーがメッセージやプッシュ通知の受信を拒否しているかどうかを指定します。&lt;/li&gt;&lt;li&gt;有効な値は **ALL** または **NONE** です。&lt;/li&gt;&lt;/ul&gt; |
