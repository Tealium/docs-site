---
title: Facebook オフラインコンバージョンコネクタ構成ガイド
description: この記事では、Facebook オフラインコンバージョンコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/facebook-offline-conversions-connector/
---
 新しい統合には、Facebook オフラインコンバージョンコネクタの代わりに [Facebook Conversions connector]() を推奨します。Facebook Conversions コネクタを通じてオフラインおよびストアイベントを処理するには、`action_source` パラメータを `physical_store` に構成します。詳細については、[Facebook Conversions connector]() を参照してください。 

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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[Connector Overview]() 記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アクセストークン**
  * 必須。
  * 広告アカウントとオフラインイベントセットにアクセスできるFacebookシステムユーザーのアクセストークン。

* **ビジネスマネージャーID**
  * 必須。
  * この値は **Facebook Business Manager &gt; Business Settings &gt; Business Info &gt; Business Manager Info** ページで見つけることができます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - コンバージョンの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|オフラインイベントセット|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;コンバージョンを送信するオフラインイベントセットを選択します。&lt;/li&gt;&lt;li&gt;**作成**タブで新しいオフラインイベントセットを作成するか、[Facebook Event Manager](https://business.facebook.com/offline_events)を通じて作成できます。&lt;/li&gt;&lt;li&gt;[Facebook オフラインコンバージョン](https://www.facebook.com/business/help/339320669734609)のドキュメンテーションの詳細を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|クライアントIPアドレス|  &lt;ul&gt;&lt;li&gt;データ処理オプションがLDUにマッピングされ、ジオロケーションが要求される場合は必須。&lt;/li&gt;&lt;/ul&gt; |
|コンテンツID|  &lt;ul&gt;&lt;li&gt;オフラインイベントセットの各トランザクションまたは注文の一意の識別子またはレシート。&lt;/li&gt;&lt;li&gt;例：`ATN10001`&lt;/li&gt;&lt;/ul&gt; |
|コンテンツタイプ|  &lt;ul&gt;&lt;li&gt;ダイナミック広告に必須。&lt;/li&gt;&lt;li&gt;有効なダイナミック広告のコンテンツタイプ。&lt;/li&gt;&lt;li&gt;例：`product`&lt;/li&gt;&lt;/ul&gt; |
|通貨|  &lt;ul&gt;&lt;li&gt;&#34;Purchase&#34;イベントに必須。&lt;/li&gt;&lt;li&gt;3文字のISO通貨コード&lt;/li&gt;&lt;/ul&gt; |
|データ処理オプション|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;Facebookがイベントを限定データ使用制限で処理するようにLDUに値をマップします。&lt;/li&gt;&lt;li&gt;それ以外の場合は、イベントが限定データ使用制限で処理されないように`None`をマップします。&lt;/li&gt;&lt;li&gt;詳細については、[Facebook Data Processing Options](https://developers.facebook.com/docs/marketing-apis/data-processing-options)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|データ処理オプション国|  &lt;ul&gt;&lt;li&gt;データ処理オプションがLDUにマッピングされている場合は必須。&lt;/li&gt;&lt;li&gt;ユーザーイベントに関連する国コードをマップします。&lt;/li&gt;&lt;li&gt;受け入れられるコード値：  &lt;ul&gt;&lt;li&gt;`1`はアメリカ合衆国&lt;/li&gt;&lt;li&gt;`0`はFacebookによる国のジオロケーションを要求する&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;ジオロケーションには、&#34;クライアントIPアドレス&#34;属性のマッピングも必要です。&lt;/li&gt;&lt;/ul&gt; |
|データ処理オプション州|  &lt;ul&gt;&lt;li&gt;データ処理オプションがLDUにマッピングされている場合は必須。&lt;/li&gt;&lt;li&gt;ユーザーイベントに関連する州コードをマップします。&lt;/li&gt;&lt;li&gt;受け入れられるコード値：  &lt;ul&gt;&lt;li&gt;`1000`はカリフォルニア&lt;/li&gt;&lt;li&gt;`0`はFacebookによる州のジオロケーションを要求する。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;ジオロケーションには、&#34;クライアントIPアドレス&#34;属性のマッピングも必要です。&lt;/li&gt;&lt;/ul&gt; |
|イベント名|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;文字列。&lt;/li&gt;&lt;li&gt;[標準的なFacebook Pixelイベント](https://developers.facebook.com/docs/marketing-api/offline-conversions#data-parameters)のうちの1つ。&lt;/li&gt;&lt;/ul&gt; |
|イベント時間|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;Unixタイムスタンプ、秒単位。&lt;/li&gt;&lt;/ul&gt; |
|アイテム番号|  &lt;ul&gt;&lt;li&gt;同じ注文またはトランザクションのイベントを区別するための一意の識別子、例えば`1`または`a`。&lt;/li&gt;&lt;/ul&gt; |
|ネームスペースID|  &lt;ul&gt;&lt;li&gt;サードパーティのユーザーIDまたはリードIDを解決するための数値スコープ。&lt;/li&gt;&lt;li&gt;マッチキーを参照してください。&lt;/li&gt;&lt;/ul&gt; |
|注文ID|  &lt;ul&gt;&lt;li&gt;オフラインイベントセットの各トランザクションまたは注文の一意の識別子またはレシート。&lt;/li&gt;&lt;li&gt;例：`ATN10001`&lt;/li&gt;&lt;/ul&gt; |
|アップロードタグ|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;イベントアップロードを追跡するための文字列。&lt;/li&gt;&lt;li&gt;例：`monthly`または`in-store uploads`&lt;/li&gt;&lt;/ul&gt; |
|値|  &lt;ul&gt;&lt;li&gt;&#34;Purchase&#34;イベントに必須。&lt;/li&gt;&lt;li&gt;コンバージョンイベントの金額。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点やスペースは含まない。&lt;/li&gt;&lt;/ul&gt; |
|国|  &lt;ul&gt;&lt;li&gt;ISO 3166-1 alpha-2形式の2文字の国コード。&lt;/li&gt;&lt;/ul&gt; |
|生年月日の日|  &lt;ul&gt;&lt;li&gt;`01`から`31`までの`DD`。&lt;/li&gt;&lt;/ul&gt; |
|メールアドレス|  &lt;ul&gt;&lt;li&gt;ユーザーをそのメールアドレスに基づいて識別します。&lt;/li&gt;&lt;li&gt;アドレスは小文字に変換されます。&lt;/li&gt;&lt;/ul&gt; |
|名の頭文字|  &lt;ul&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|名|  &lt;ul&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|性別|  &lt;ul&gt;&lt;li&gt;値は：  &lt;ul&gt;&lt;li&gt;`m`は男性&lt;/li&gt;&lt;li&gt;`f`は女性&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;大文字の値は小文字に変換されます。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|リード広告からのリードID|  &lt;ul&gt;&lt;li&gt;リードIDの値。&lt;/li&gt;&lt;/ul&gt; |
|モバイル広告ID|  &lt;ul&gt;&lt;li&gt;Apple Advertising IDまたはAndroid Advertising IDのいずれかの値を指定して、モバイルユーザーをターゲットにします。&lt;/li&gt;&lt;/ul&gt; |
|生年月日の月|  &lt;ul&gt;&lt;li&gt;`01`から`12`までの`MM`。&lt;/li&gt;&lt;/ul&gt; |
|電話番号|  &lt;ul&gt;&lt;li&gt;ユーザーをその電話番号に基づいて識別します。&lt;/li&gt;&lt;li&gt;国コード、地域コード、番号を含む数字のみを含めます。例えば、`16505551212`。&lt;/li&gt;&lt;/ul&gt; |
|サードパーティユーザーID|  &lt;ul&gt;&lt;li&gt;外部システムのID&lt;/li&gt;&lt;/ul&gt; |
|US州|  &lt;ul&gt;&lt;li&gt;2文字のANSI省略コード、小文字。&lt;/li&gt;&lt;/ul&gt; |
|生年|  &lt;ul&gt;&lt;li&gt;`1900`から現在の年までの`YYYY`。&lt;/li&gt;&lt;/ul&gt; |
|郵便番号|  &lt;ul&gt;&lt;li&gt;郵便番号。&lt;/li&gt;&lt;li&gt;正確な形式は国によります。&lt;/li&gt;&lt;/ul&gt; |
|このボックスをチェックすると、ターゲットユーザー識別データはすでにハッシュ化されている|  &lt;ul&gt;&lt;li&gt;ターゲットユーザー識別データがすでにハッシュ化されている場合はチェックします。&lt;/li&gt;&lt;/ul&gt; |
|カスタムデータプロパティ|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;Facebookによって指定されていないカスタムプロパティ&lt;/li&gt;&lt;/ul&gt; |
|テンプレート変数|  &lt;ul&gt;&lt;li&gt;オプション。&lt;/li&gt;&lt;li&gt;カスタムデータプロパティセクションでサポートされています。&lt;/li&gt;&lt;li&gt;テンプレートのデータ入力としてテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、[Template Variables Guide]()を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記法を使用してネストしたテンプレート変数を名付けます。例えば、items.name。&lt;/li&gt;&lt;li&gt;ネストしたテンプレート変数は通常、データレイヤーリスト属性から作成されます。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;カスタムデータプロパティセクションで参照される有効なJSONテンプレートを提供します&lt;/li&gt;&lt;li&gt;テンプレートは、`{{SomeTemplateName}}`のように、二重中括弧で囲まれた名前でサポートされるフィールドに注入されます。&lt;/li&gt;&lt;li&gt;詳細については、[Templates Guide]()を参照してください。&lt;/li&gt;&lt;/ul&gt; |