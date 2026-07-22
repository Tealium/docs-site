---
title: Facebook オフラインコンバージョンコネクタ構成ガイド
description: この記事では、Facebook オフラインコンバージョンコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/facebook-offline-conversions-connector/
---

<blockquote>
新しい統合には、Facebook オフラインコンバージョンコネクタの代わりに [Facebook Conversions connector](https://docs.tealium.com/facebook-conversions-connector/) を推奨します。Facebook Conversions コネクタを通じてオフラインおよびストアイベントを処理するには、`action_source` パラメータを `physical_store` に構成します。詳細については、[Facebook Conversions connector](https://docs.tealium.com/facebook-conversions-connector/) を参照してください。
</blockquote>


## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Facebook Graph API - Marketing API
* APIバージョン：v16.0
* APIエンドポイント：`https://graph.facebook.com`

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|コンバージョンの送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[Connector Overview](https://docs.tealium.com/about-connectors/) 記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アクセストークン**
  * 必須。
  * 広告アカウントとオフラインイベントセットにアクセスできるFacebookシステムユーザーのアクセストークン。

* **ビジネスマネージャーID**
  * 必須。
  * この値は **Facebook Business Manager > Business Settings > Business Info > Business Manager Info** ページで見つけることができます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - コンバージョンの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|オフラインイベントセット|  <ul><li>必須。</li><li>コンバージョンを送信するオフラインイベントセットを選択します。</li><li>**作成**タブで新しいオフラインイベントセットを作成するか、[Facebook Event Manager](https://business.facebook.com/offline_events)を通じて作成できます。</li><li>[Facebook オフラインコンバージョン](https://www.facebook.com/business/help/339320669734609)のドキュメンテーションの詳細を参照してください。</li></ul> |
|クライアントIPアドレス|  <ul><li>データ処理オプションがLDUにマッピングされ、ジオロケーションが要求される場合は必須。</li></ul> |
|コンテンツID|  <ul><li>オフラインイベントセットの各トランザクションまたは注文の一意の識別子またはレシート。</li><li>例：`ATN10001`</li></ul> |
|コンテンツタイプ|  <ul><li>ダイナミック広告に必須。</li><li>有効なダイナミック広告のコンテンツタイプ。</li><li>例：`product`</li></ul> |
|通貨|  <ul><li>"Purchase"イベントに必須。</li><li>3文字のISO通貨コード</li></ul> |
|データ処理オプション|  <ul><li>必須</li><li>Facebookがイベントを限定データ使用制限で処理するようにLDUに値をマップします。</li><li>それ以外の場合は、イベントが限定データ使用制限で処理されないように`None`をマップします。</li><li>詳細については、[Facebook Data Processing Options](https://developers.facebook.com/docs/marketing-apis/data-processing-options)を参照してください。</li></ul> |
|データ処理オプション国|  <ul><li>データ処理オプションがLDUにマッピングされている場合は必須。</li><li>ユーザーイベントに関連する国コードをマップします。</li><li>受け入れられるコード値：  <ul><li>`1`はアメリカ合衆国</li><li>`0`はFacebookによる国のジオロケーションを要求する</li></ul> </li><li>ジオロケーションには、"クライアントIPアドレス"属性のマッピングも必要です。</li></ul> |
|データ処理オプション州|  <ul><li>データ処理オプションがLDUにマッピングされている場合は必須。</li><li>ユーザーイベントに関連する州コードをマップします。</li><li>受け入れられるコード値：  <ul><li>`1000`はカリフォルニア</li><li>`0`はFacebookによる州のジオロケーションを要求する。</li></ul> </li><li>ジオロケーションには、"クライアントIPアドレス"属性のマッピングも必要です。</li></ul> |
|イベント名|  <ul><li>必須。</li><li>文字列。</li><li>[標準的なFacebook Pixelイベント](https://developers.facebook.com/docs/marketing-api/offline-conversions#data-parameters)のうちの1つ。</li></ul> |
|イベント時間|  <ul><li>必須</li><li>Unixタイムスタンプ、秒単位。</li></ul> |
|アイテム番号|  <ul><li>同じ注文またはトランザクションのイベントを区別するための一意の識別子、例えば`1`または`a`。</li></ul> |
|ネームスペースID|  <ul><li>サードパーティのユーザーIDまたはリードIDを解決するための数値スコープ。</li><li>マッチキーを参照してください。</li></ul> |
|注文ID|  <ul><li>オフラインイベントセットの各トランザクションまたは注文の一意の識別子またはレシート。</li><li>例：`ATN10001`</li></ul> |
|アップロードタグ|  <ul><li>必須。</li><li>イベントアップロードを追跡するための文字列。</li><li>例：`monthly`または`in-store uploads`</li></ul> |
|値|  <ul><li>"Purchase"イベントに必須。</li><li>コンバージョンイベントの金額。</li></ul> |
|市区町村|  <ul><li>小文字。</li><li>句読点やスペースは含まない。</li></ul> |
|国|  <ul><li>ISO 3166-1 alpha-2形式の2文字の国コード。</li></ul> |
|生年月日の日|  <ul><li>`01`から`31`までの`DD`。</li></ul> |
|メールアドレス|  <ul><li>ユーザーをそのメールアドレスに基づいて識別します。</li><li>アドレスは小文字に変換されます。</li></ul> |
|名の頭文字|  <ul><li>小文字。</li><li>句読点や特殊文字は含まない。</li><li>UTF-8形式。</li></ul> |
|名|  <ul><li>小文字。</li><li>句読点や特殊文字は含まない。</li><li>UTF-8形式。</li></ul> |
|性別|  <ul><li>値は：  <ul><li>`m`は男性</li><li>`f`は女性</li></ul> </li><li>大文字の値は小文字に変換されます。</li></ul> |
|姓|  <ul><li>小文字。</li><li>句読点や特殊文字は含まない。</li><li>UTF-8形式。</li></ul> |
|リード広告からのリードID|  <ul><li>リードIDの値。</li></ul> |
|モバイル広告ID|  <ul><li>Apple Advertising IDまたはAndroid Advertising IDのいずれかの値を指定して、モバイルユーザーをターゲットにします。</li></ul> |
|生年月日の月|  <ul><li>`01`から`12`までの`MM`。</li></ul> |
|電話番号|  <ul><li>ユーザーをその電話番号に基づいて識別します。</li><li>国コード、地域コード、番号を含む数字のみを含めます。例えば、`16505551212`。</li></ul> |
|サードパーティユーザーID|  <ul><li>外部システムのID</li></ul> |
|US州|  <ul><li>2文字のANSI省略コード、小文字。</li></ul> |
|生年|  <ul><li>`1900`から現在の年までの`YYYY`。</li></ul> |
|郵便番号|  <ul><li>郵便番号。</li><li>正確な形式は国によります。</li></ul> |
|このボックスをチェックすると、ターゲットユーザー識別データはすでにハッシュ化されている|  <ul><li>ターゲットユーザー識別データがすでにハッシュ化されている場合はチェックします。</li></ul> |
|カスタムデータプロパティ|  <ul><li>オプション</li><li>Facebookによって指定されていないカスタムプロパティ</li></ul> |
|テンプレート変数|  <ul><li>オプション。</li><li>カスタムデータプロパティセクションでサポートされています。</li><li>テンプレートのデータ入力としてテンプレート変数を提供します。</li><li>詳細については、[Template Variables Guide](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記法を使用してネストしたテンプレート変数を名付けます。例えば、items.name。</li><li>ネストしたテンプレート変数は通常、データレイヤーリスト属性から作成されます。</li></ul> |
|テンプレート|  <ul><li>オプション</li><li>カスタムデータプロパティセクションで参照される有効なJSONテンプレートを提供します</li><li>テンプレートは、`{{SomeTemplateName}}`のように、二重中括弧で囲まれた名前でサポートされるフィールドに注入されます。</li><li>詳細については、[Templates Guide](https://docs.tealium.com/about-connector-templates/)を参照してください。</li></ul> |