---
title: Facebookオーディエンス顧客提供資格情報コネクタ構成ガイド
description: この記事では、お客様のCustomer Data HubアカウントでFacebookオーディエンス顧客提供資格情報コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/facebook-audiences-customer-provided-credentials-connector/
---
この記事では、Facebookオーディエンス顧客提供資格情報コネクタの構成方法について説明します。

## 前提条件

Facebookアプリの作成についての詳細は、[Facebook: アプリ開発](https://developers.facebook.com/docs/apps/)を参照してください。

コネクタを構成する前に、以下の手順を完了してください：

1. [Facebookカスタムオーディエンス利用規約](https://www.facebook.com/ads/manage/customaudiences/tos.php)に同意する。
1. Facebookアカウントに次のリダイレクトURIを追加する：`https://my.tealiumiq.com/oauth/facebook/callback.html`。Facebookアプリダッシュボードから**Facebookログイン &gt; 構成**に移動し、**有効なOAuthリダイレクトURIのFacebookアプリ**の下にURIを入力します。
1. Facebookアプリで`ads_management`権限をリクエストする。`ads_management`権限により、アプリは所有する広告アカウント、または広告アカウント所有者からアクセス権を付与された広告アカウントを読み取りおよび管理できます。詳細については、[Facebook: 権限リファレンス](https://developers.facebook.com/docs/facebook-login/permissions/#reference-ads_management)を参照してください。

より多くのアプリリソース、例えばより良いレート制限を要求するには、広告管理**標準アクセス**を要求してください。詳細については、[Facebook: アクセスと認証](https://developers.facebook.com/docs/marketing-api/access/)を参照してください。

## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Facebook Graph API - Marketing API
* APIバージョン：v25.0
* APIエンドポイント：`https://graph.facebook.com`

## バッチ制限

このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントがベンダーに順不同で到達する可能性があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチ処理アクション]()を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：10000
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：1 MB

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]()を参照してください。

コネクタを追加した後、次の構成を構成します：

* **アプリID**：(必須) 接続したいFacebookアプリID。
* **アプリシークレット**：(必須) 接続したいFacebookアプリのアプリシークレット。
* **広告アカウントID**：(必須) 管理したいFacebook広告アカウントID。Facebook広告アカウントIDについての詳細は、[Facebook: Facebook広告アカウントID番号の検索](https://www.facebook.com/help/1492627900875762)を参照してください。

この接続は通常60日以内に期限切れになり、すべてのFacebook広告アクションに予測不可能な結果をもたらします。

いつでも**接続の確立/接続済み**をクリックして接続を再確立します。

**接続の確立**ボタンをクリックする前に、使用している広告アカウントIDにリンクされているアカウントでFacebookにサインインしていることを確認してください。そうでない場合、生成されるトークンに問題が発生する可能性があります。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| カスタムオーディエンスにユーザーを追加 | ✓ | ✗ |
| カスタムオーディエンスからユーザーを削除 | ✓ | ✗ |
| すべてのカスタムオーディエンスからユーザーをオプトアウト | ✓ | ✗ |

アクションの名前を入力し、アクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### カスタムオーディエンスにユーザーを追加

サポートされている識別子のタイプは4つあります：メール、電話番号、ユーザーまたはアプリID、およびセカンダリID。複数のセカンダリ識別子がサポートされています。**FacebookユーザーID**を指定する場合、**FacebookアプリID**も提供する必要があります。メールまたは電話番号は1つのみサポートされています。複数の識別子が指定されている場合、上記の順序で選択されます。たとえば、メールと電話番号の両方が指定されている場合、メールが選択されますが、値がない場合は電話番号が選択されます。

#### パラメータ

| パラメータ | 説明|
| --- | --- |
|カスタムオーディエンスにユーザーを追加|  &lt;ul&gt;&lt;li&gt;(必須) 対象のカスタムオーディエンスを選択します。&lt;/li&gt;&lt;li&gt;顧客ファイルから作成されたオーディエンスは表示されません。&lt;/li&gt;&lt;li&gt;このコネクタを使用し、Facebookでカスタムオーディエンスを構築する前に、[Facebookカスタムオーディエンス利用規約](https://www.facebook.com/ads/manage/customaudiences/tos.php)に同意する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|メールアドレス|  &lt;ul&gt;&lt;li&gt;メールアドレスに基づいてユーザーを特定します。&lt;/li&gt;&lt;/ul&gt; |
|電話番号|  &lt;ul&gt;&lt;li&gt;電話番号に基づいてユーザーを特定します。&lt;/li&gt;&lt;li&gt;国コード、エリアコード、番号のみの数字を含めます。例：`16505551212`。&lt;/li&gt;&lt;/ul&gt; |
|FacebookユーザーID|  &lt;ul&gt;&lt;li&gt;Facebook IDに基づいてユーザーを特定します。&lt;/li&gt;&lt;li&gt;この識別タイプを使用する場合は、「FacebookアプリID」を提供する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|FacebookアプリID|  &lt;ul&gt;&lt;li&gt;「FacebookユーザーID」がユーザー識別子として使用される場合に必要です。&lt;/li&gt;&lt;li&gt;「FacebookユーザーID」を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|モバイル広告ID|  &lt;ul&gt;&lt;li&gt;アプリユーザーID、Appleの広告識別子（IDFA）、またはAndroidの広告IDに基づいてユーザーをターゲットにします。&lt;/li&gt;&lt;/ul&gt; |
|郵便番号|  &lt;ul&gt;&lt;li&gt;郵便番号。&lt;/li&gt;&lt;li&gt;国によって形式が異なります。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;ユーザーの市区町村。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点やスペースは含まれません。&lt;/li&gt;&lt;/ul&gt; |
|国|  &lt;ul&gt;&lt;li&gt;ユーザーの国。&lt;/li&gt;&lt;li&gt;2文字の国コード。&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2形式。&lt;/li&gt;&lt;/ul&gt; |
|米国の州|  &lt;ul&gt;&lt;li&gt;アメリカ合衆国のユーザー州。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;2文字のANSI省略コード。&lt;/li&gt;&lt;/ul&gt; |
|名|  &lt;ul&gt;&lt;li&gt;ユーザーの名前。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まれません。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;ユーザーの姓。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まれません。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|イニシャル|  &lt;ul&gt;&lt;li&gt;ユーザーの名のイニシャル。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まれません。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|生年|  &lt;ul&gt;&lt;li&gt;ユーザーの生年。&lt;/li&gt;&lt;li&gt;`YYYY`形式。&lt;/li&gt;&lt;li&gt;`1900`年から現在の年までの値。&lt;/li&gt;&lt;/ul&gt; |
|生日|  &lt;ul&gt;&lt;li&gt;ユーザーの生日。&lt;/li&gt;&lt;li&gt;`DD`形式。&lt;/li&gt;&lt;li&gt;`01`から`31`までの値。&lt;/li&gt;&lt;/ul&gt; |
|誕生月|  &lt;ul&gt;&lt;li&gt;ユーザーの誕生月。&lt;/li&gt;&lt;li&gt;`MM`形式。&lt;/li&gt;&lt;li&gt;`01`から`12`までの値。&lt;/li&gt;&lt;/ul&gt; |
|性別|  &lt;ul&gt;&lt;li&gt;ユーザーの性別。&lt;/li&gt;&lt;li&gt;`M`は男性、`F`は女性&lt;/li&gt;&lt;/ul&gt; |
|ルックアライク値|  &lt;ul&gt;&lt;li&gt;CRMデータからシードカスタムオーディエンスを作成する際に各ユーザーに構成される任意の数値。&lt;/li&gt;&lt;li&gt;Facebookはこれを使用して、オーディエンス内のどのユーザーがあなたにとって最も価値があるかを定量的に判断します。&lt;/li&gt;&lt;/ul&gt; |
|カスタムオーディエンスオーバーライド| (オプション) 必須セクションの値をオーバーライドするカスタムオーディエンスIDを提供します。このフィールドを使用すると、AudienceStream変数を使用してオーディエンスIDを入力できます。 |
|ユーザー識別子が既にハッシュ化されている| このボックスをチェックすると、ターゲットユーザー識別子が既にハッシュ化されていることを示します。 FacebookはSHA256ハッシュ方式のみを受け入れます。  |

### カスタムオーディエンスからユーザーを削除

サポートされている識別子のタイプは4つあります：メール、電話番号、ユーザーまたはアプリID、およびセカンダリID。複数のセカンダリ識別子がサポートされています。**FacebookユーザーID**を指定する場合、**FacebookアプリID**も提供する必要があります。メールまたは電話番号は1つのみサポートされています。複数の識別子が指定されている場合、上記の順序で選択されます。たとえば、メールと電話番号の両方が指定されている場合、メールが選択されますが、値がない場合は電話番号が選択されます。
#### パラメータ

| パラメータ | 説明 |
| --- | --- |
|削除対象のカスタムオーディエンス|  &lt;ul&gt;&lt;li&gt;（必須）ターゲットのカスタムオーディエンスを選択してください。&lt;/li&gt;&lt;li&gt;このコネクタを使用してFacebookでカスタムオーディエンスを構築する前に、[Facebookカスタムオーディエンス利用規約](https://www.facebook.com/ads/manage/customaudiences/tos.php)に同意する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|メールアドレス|  &lt;ul&gt;&lt;li&gt;メールアドレスに基づいてユーザーを特定します。&lt;/li&gt;&lt;/ul&gt; |
|電話番号|  &lt;ul&gt;&lt;li&gt;電話番号に基づいてユーザーを特定します。&lt;/li&gt;&lt;li&gt;国コード、地域コード、番号のみを含めてください。例：`16505551212`。&lt;/li&gt;&lt;/ul&gt; |
|FacebookユーザーID|  &lt;ul&gt;&lt;li&gt;Facebook IDに基づいてユーザーを特定します。&lt;/li&gt;&lt;li&gt;この識別タイプを使用する場合は、「FacebookアプリID」を提供する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|FacebookアプリID|  &lt;ul&gt;&lt;li&gt;「FacebookユーザーID」がユーザー識別子として使用される場合に必要です。&lt;/li&gt;&lt;li&gt;「FacebookユーザーID」を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|モバイル広告ID|  &lt;ul&gt;&lt;li&gt;アプリユーザーID、Appleの広告識別子（IDFA）、またはAndroidの広告IDに基づいてユーザーをターゲットにします。&lt;/li&gt;&lt;/ul&gt; |
|郵便番号|  &lt;ul&gt;&lt;li&gt;郵便番号。&lt;/li&gt;&lt;li&gt;国によって形式が異なります。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;ユーザーの市区町村。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点やスペースは含まない。&lt;/li&gt;&lt;/ul&gt; |
|国|  &lt;ul&gt;&lt;li&gt;ユーザーの国。&lt;/li&gt;&lt;li&gt;2文字の国コード。&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2形式。&lt;/li&gt;&lt;/ul&gt; |
|米国の州|  &lt;ul&gt;&lt;li&gt;アメリカ合衆国の州。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;2文字のANSI略語コード。&lt;/li&gt;&lt;/ul&gt; |
|名|  &lt;ul&gt;&lt;li&gt;ユーザーの名。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;ユーザーの姓。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|イニシャル|  &lt;ul&gt;&lt;li&gt;ユーザーの名のイニシャル。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|生年|  &lt;ul&gt;&lt;li&gt;ユーザーの生年。&lt;/li&gt;&lt;li&gt;`YYYY`形式。&lt;/li&gt;&lt;li&gt;`1900`年から現在の年までの値。&lt;/li&gt;&lt;/ul&gt; |
|生日|  &lt;ul&gt;&lt;li&gt;ユーザーの生日。&lt;/li&gt;&lt;li&gt;`DD`形式。&lt;/li&gt;&lt;li&gt;`01`から`31`までの値。&lt;/li&gt;&lt;/ul&gt; |
|生月|  &lt;ul&gt;&lt;li&gt;ユーザーの生月。&lt;/li&gt;&lt;li&gt;`MM`形式。&lt;/li&gt;&lt;li&gt;`01`から`12`までの値。&lt;/li&gt;&lt;/ul&gt; |
|性別|  &lt;ul&gt;&lt;li&gt;ユーザーの性別。&lt;/li&gt;&lt;li&gt;`M`は男性、`F`は女性&lt;/li&gt;&lt;/ul&gt; |
|ルックアライク値|  &lt;ul&gt;&lt;li&gt;CRMデータからシードカスタムオーディエンスを作成する際に各ユーザーに構成される任意の数値。&lt;/li&gt;&lt;li&gt;Facebookはこの値を使用して、オーディエンス内のどのユーザーがあなたにとって最も価値があるかを定量的に判断します。&lt;/li&gt;&lt;/ul&gt; |
|カスタムオーディエンスの上書き| （オプション）必須セクションの値を上書きするカスタムオーディエンスIDを提供します。このフィールドを使用すると、AudienceStreamの変数を使用してオーディエンスIDを入力できます。 |
|ユーザー識別子が既にハッシュ化されている| このボックスをチェックすると、ターゲットユーザー識別子が既にハッシュ化されていることを示します。FacebookはSHA256ハッシュ方式のみを受け付けます。 |

### すべてのカスタムオーディエンスからユーザーをオプトアウト

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
|メールアドレス|  &lt;ul&gt;&lt;li&gt;メールアドレスに基づいてユーザーを特定します。&lt;/li&gt;&lt;/ul&gt; |
|電話番号|  &lt;ul&gt;&lt;li&gt;電話番号に基づいてユーザーを特定します。&lt;/li&gt;&lt;li&gt;国コード、地域コード、番号のみを含めてください。例：`16505551212`。&lt;/li&gt;&lt;/ul&gt; |
|FacebookユーザーID|  &lt;ul&gt;&lt;li&gt;Facebook IDに基づいてユーザーを特定します。&lt;/li&gt;&lt;li&gt;この識別タイプを使用する場合は、「FacebookアプリID」を提供する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|FacebookアプリID|  &lt;ul&gt;&lt;li&gt;「FacebookユーザーID」がユーザー識別子として使用される場合に必要です。&lt;/li&gt;&lt;li&gt;「FacebookユーザーID」を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|モバイル広告ID|  &lt;ul&gt;&lt;li&gt;アプリユーザーID、Appleの広告識別子（IDFA）、またはAndroidの広告IDに基づいてユーザーをターゲットにします。&lt;/li&gt;&lt;/ul&gt; |
|郵便番号|  &lt;ul&gt;&lt;li&gt;郵便番号。&lt;/li&gt;&lt;li&gt;国によって形式が異なります。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;ユーザーの市区町村。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点やスペースは含まない。&lt;/li&gt;&lt;/ul&gt; |
|国|  &lt;ul&gt;&lt;li&gt;ユーザーの国。&lt;/li&gt;&lt;li&gt;2文字の国コード。&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2形式。&lt;/li&gt;&lt;/ul&gt; |
|米国の州|  &lt;ul&gt;&lt;li&gt;アメリカ合衆国の州。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;2文字のANSI略語コード。&lt;/li&gt;&lt;/ul&gt; |
|名|  &lt;ul&gt;&lt;li&gt;ユーザーの名。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;ユーザーの姓。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|イニシャル|  &lt;ul&gt;&lt;li&gt;ユーザーの名のイニシャル。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|生年|  &lt;ul&gt;&lt;li&gt;ユーザーの生年。&lt;/li&gt;&lt;li&gt;`YYYY`形式。&lt;/li&gt;&lt;li&gt;`1900`年から現在の年までの値。&lt;/li&gt;&lt;/ul&gt; |
|生日|  &lt;ul&gt;&lt;li&gt;ユーザーの生日。&lt;/li&gt;&lt;li&gt;`DD`形式。&lt;/li&gt;&lt;li&gt;`01`から`31`までの値。&lt;/li&gt;&lt;/ul&gt; |
|生月|  &lt;ul&gt;&lt;li&gt;ユーザーの生月。&lt;/li&gt;&lt;li&gt;`MM`形式。&lt;/li&gt;&lt;li&gt;`01`から`12`までの値。&lt;/li&gt;&lt;/ul&gt; |
|性別|  &lt;ul&gt;&lt;li&gt;ユーザーの性別。&lt;/li&gt;&lt;li&gt;`M`は男性、`F`は女性&lt;/li&gt;&lt;/ul&gt; |
|ルックアライク値|  &lt;ul&gt;&lt;li&gt;CRMデータからシードカスタムオーディエンスを作成する際に各ユーザーに構成される任意の数値。&lt;/li&gt;&lt;li&gt;Facebookはこの値を使用して、オーディエンス内のどのユーザーがあなたにとって最も価値があるかを定量的に判断します。&lt;/li&gt;&lt;/ul&gt; |
|ユーザー識別子が既にハッシュ化されている| このボックスをチェックすると、ターゲットユーザー識別子が既にハッシュ化されていることを示します。FacebookはSHA256ハッシュ方式のみを受け付けます。 |

## Facebookオーディエンス顧客提供資格情報コネクタの使用

### 訪問ID属性の作成

Facebookオーディエンス顧客提供資格情報コネクタは、少なくとも1つの訪問ID属性が必要であり、Facebookオーディエンスに渡すことができます。

訪問ID属性を構成するためのリソースを以下に使用してください：

* [訪問ID属性の構成]()
* [FacebookマーケティングAPI](https://developers.facebook.com/docs/marketing-api/audiences-api)

### オーディエンスの定義

アカウントには複数の訪問ID属性が定義されている場合があります。この場合、訪問IDが割り当てられている訪問のみが含まれるオーディエンスを確実にするために、ブールデータ型で「Known Visitor」という名前の訪問スコープ属性を作成することが重要です。この属性を使用することで、Facebookに渡すことができる訪問IDが割り当てられている訪問のみがオーディエンスに含まれることが保証されます。未知の訪問をターゲットにすることはできません。

このコネクタには、メール、電話、アプリ、またはユーザーIDなどの必須IDパラメータもあります。これらのIDの少なくとも1つが必要です。これらのIDをオーディエンスフィルターに含めることで、コネクタエラーを避けるのに役立ちます。

以下の例を使用して、「Known Visitor」ブールデータ型が`true`に構成されている訪問の[オーディエンスフィルターを作成]()します。バッジとブール属性を事前に追加するか、フィルターを作成する際に追加します。

![](/images/server-side-connectors/edit-audience-shoe-fan.png)

### TealiumをFacebookオーディエンスアカウントに接続

コネクタをFacebookオーディエンスアカウントに構成するには、アカウントIDが必要です。

FacebookオーディエンスアカウントIDを取得するための手順は以下の通りです：

1. Facebookオーディエンスアカウントにログインします。
1. [広告マネージャー](https://www.facebook.com/ads/manage)で広告アカウント、キャンペーン、広告セット、または広告をクリックします。
1. ブラウザのURLから`account_id`パラメータ値をコピーしてから、AudienceStreamのコネクタに戻ります。
![](/images/server-side-connectors/facebook-account-id.png)

1. **構成**ウィンドウで、タイトルと関連するメモ、および上記からコピーした広告アカウントIDを追加します。
1. **接続の確立**をクリックして、接続を確認します。
### カスタムオーディエンスの作成

Facebook Audiencesアカウントに接続したので、カスタムオーディエンスを作成する時が来ました。コネクタを使用してカスタムオーディエンスを作成する前に、Facebookサイトで最初のカスタムオーディエンスを作成し、利用規約に同意する必要があります。

カスタムオーディエンスを作成するには、次の手順を使用します：

1. コネクタ構成で、**作成**タブをクリックします。
1. 次のフィールドを構成します：
   * **オーディエンス名**（必須）：カスタムオーディエンスの名前。CRMからのオーディエンスまたはセグメント名を使用します（例：`Qualified Leads - US - Q3 2026` または `High Value Customers - EMEA`）。Metaはこの名前を使用してオーディエンスセグメントを識別します。
   * **オーディエンスメタデータ（JSON）**（オプション）：Meta APIの`description`パラメータにマッピングされたオーディエンス基準を記述するJSONオブジェクト。集計またはカテゴリ属性のキーバリューペアを使用します。PIIは含めないでください。例：`{&#34;lifecycle_stage&#34;:&#34;churned&#34;,&#34;region&#34;:&#34;EMEA&#34;,&#34;tier&#34;:&#34;high_value&#34;}`。Metaはこのメタデータをオーディエンスラベルと最適化機能で使用します。ラベルの割り当てはMeta Ads Managerで行われます。値はMetaがメタデータを解析するために有効なJSONでなければなりません。
1. **作成**をクリックします。  
`customer_file_source`パラメータは以下の値をサポートします：
    * `USER_PROVIDED_ONLY`
    * `PARTNER_PROVIDED_ONLY`
    * `BOTH_USER_AND_PARTNER_PROVIDED`

Facebook Audiencesサイトでは、顧客リスト、ウェブサイトのトラフィック、またはアプリのアクティビティに基づいてオーディエンスを作成するオプションがあります。この例では、顧客リストに基づいてオーディエンスを作成します。

カスタムオーディエンスを使用するには、最低20エントリを含む必要があります。オーディエンスが正常に作成された場合、ボタンの横に小さなチェックアイコンが表示されます。

### コネクタのアクションを指定する

次に、コネクタに実行させたいアクションを指定する必要があります。

コネクタのアクションを指定するには、次の手順を使用します：

1. **アクション**タブをクリックします。
1. **カスタムオーディエンスにユーザーを追加**を選択します。  
![](/images/server-side-connectors/facebook-ads-connector-action-add-user-to-custom-audience.jpg)
1. **&#43; アクションを作成**をクリックします。

### コネクタアクションの構成

コネクタのアクションを構成するには、次の手順を使用します：

1. **オーディエンス**メニューから、以前に作成した**Shoe-Fans**オーディエンスを選択します。  
**カスタムオーディエンスにユーザーを追加する**メニューには、Facebook Audiencesアカウントに存在するオーディエンスが表示されます。
1. **カスタムオーディエンスにユーザーを追加する**ドロップダウンリストから、訪問を追加したいオーディエンスを選択します。
1. **ターゲットユーザー識別子**ドロップダウンリストで、訪問のメール属性をFacebook Audiencesアカウントの対応する訪問識別子にマッピングします。
1. **WHEN**は**Joined Audience**に構成したままにします。
1. **保存**をクリックします。

### テスト

最も効果的なテスト方法は、イベントが適切に処理されていることを確認し、Facebookダッシュボードでカスタムオーディエンスが作成され、入力されていることを確認するために[Trace]()を実行することです。

## FAQ

### なぜAudienceStreamのドロップダウンリストにオーディエンスが表示されないのですか？

Facebookに2,000を超えるオーディエンスがある場合、それらはAudienceStreamコネクタのドロップダウンリストで選択可能ではありません。

Facebookで全てのオーディエンスを表示し、特定のオーディエンスの識別子を選択するには、次の手順を使用します：

1. Facebook Audiencesアカウントにアクセス権を持つユーザーとしてFacebookにログインします。
1. &lt;https://www.facebook.com/adsmanager/audiences&gt;にアクセスします。
1. 探しているオーディエンスを見つけて、オーディエンスIDをコピーします。  
    オーディエンスIDが表示されない場合は、テーブルの列ビューを変更してそれを含めることができます。  

    ![](/images/server-side-connectors/facebook-ads-find-audience-id.png)
1. AudienceStreamに戻り、AudienceStreamコネクタのカスタム値としてオーディエンスIDを入力します。