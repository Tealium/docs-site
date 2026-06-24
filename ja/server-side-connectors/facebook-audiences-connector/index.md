---
title: Facebookオーディエンスコネクタ構成ガイド
description: この記事では、お客様のCustomer Data HubアカウントでFacebookオーディエンスコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/facebook-audiences-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Facebook Graph API - Marketing API
* APIバージョン：v25.0
* APIエンドポイント：`https://graph.facebook.com`
* ドキュメント：[Facebook Marketing API](https://developers.facebook.com/docs/marketing-api/)

## バッチ制限

このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントがベンダーに順不同で到達する可能性があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチ処理アクション]()を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：10000
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：1 MB

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[コネクタ概要]()の記事を読んで一般的な指示を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **認証タイプ**：Facebookに接続するために使用する認証タイプを選択します。このオプションはレガシーコネクタインターフェースでは利用できません。
    * **SUAT（システムユーザー認証トークン）**：（推奨）より安定した持続的な認証方法としてこのオプションを選択します。詳細については、[Facebook: システムユーザーアクセストークンの取得](https://developers.facebook.com/docs/news-indexing/guides/access-tokens/)を参照してください。
    * **OAuth2**：この接続は通常60日以内に期限切れになり、すべてのFacebook広告アクションに予測不可能な結果をもたらす可能性があります。問題を避けるために、期限切れになる前に接続を再認証する必要があります。このオプションを選択した場合、**接続を確立**ボタンをクリックしてFacebookで認証を行います。  
    **接続を確立**ボタンをクリックする前に、使用している広告アカウントIDにリンクされているアカウントでFacebookにサインインしていることを確認してください。そうでない場合、生成されるトークンに問題が生じる可能性があります。
* **広告アカウントID**：（必須）管理したいFacebookオーディエンスアカウントIDです。詳細については、[Facebook: Facebook広告アカウントID番号の検索](https://www.facebook.com/business/help/1492627900875762)を参照してください。

このコネクタを使用してFacebookでカスタムオーディエンスを構築する前に、[Facebookカスタムオーディエンス規約](https://www.facebook.com/ads/manage/customaudiences/tos.php)に同意する必要があります。

### カスタムオーディエンスの作成

Facebookサイトで最初のカスタムオーディエンスを作成し、条件に同意する必要があります。その後、コネクタを通じてカスタムオーディエンスを作成できます。

カスタムオーディエンスを使用するには、最低20エントリを含む必要があります。オーディエンスが正常に作成された場合、ボタンの横に小さなチェックアイコンが表示されます。

**カスタムオーディエンスの作成**をクリックし、次の構成を構成します：

* **新しいカスタムオーディエンス名**：（必須）カスタムオーディエンスの名前。
* **新しいカスタムオーディエンスの説明**：カスタムオーディエンスの説明。
* **顧客ファイルソース**：
  * `USER_PROVIDED_ONLY`：顧客から直接収集した広告主の情報を使用します。
  * `PARTNER_PROVIDED_ONLY`：代理店やデータプロバイダーなどのパートナーから直接提供された広告主の情報を使用します。
  * `BOTH_USER_AND_PARTNER_PROVIDED`：顧客から直接収集した広告主の情報と、代理店などのパートナーから提供された情報を使用します。
* **オーディエンスタイプ**：
  * `VALUE_BASED_AUDIENCE`：最も価値の高い顧客と同様の行動を共有する顧客を特定します。
  * `CUSTOMER_FILE_AUDIENCE`：（デフォルト）顧客ファイルの情報、例えばメールアドレス、電話番号、または他の識別子に基づいて顧客を特定します。

Facebookオーディエンスサイトでは、顧客リスト、ウェブサイトのトラフィック、またはアプリのアクティビティに基づいてオーディエンスを作成するオプションがあります。この例では、顧客リストに基づいてオーディエンスを作成します。

詳細については、[Meta Business Help Center: 顧客リストカスタムオーディエンスの作成](https://www.facebook.com/business/help/170456843145568?id=2469097953376494)を参照してください。

## アクション

| アクション名 | AudienceStream | EventStream |
|---| ---| ---|
|カスタムオーディエンスへのユーザー追加| ✓| ✗|
|カスタムオーディエンスからのユーザー削除| ✓| ✗|
|すべてのカスタムオーディエンスからのユーザーのオプトアウト| ✓| ✗|

アクションの名前を入力し、アクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### カスタムオーディエンスへのユーザー追加

#### パラメータ

|パラメータ| 説明|
|---| ---|
|ユーザーを追加するカスタムオーディエンス|  &lt;ul&gt;&lt;li&gt;(必須) 対象のカスタムオーディエンスを選択します。&lt;/li&gt;&lt;li&gt;顧客ファイルから作成されたオーディエンスは表示されません。&lt;/li&gt;&lt;li&gt;このコネクタを使用してFacebookでカスタムオーディエンスを構築する前に、[Facebookカスタムオーディエンス規約](https://www.facebook.com/ads/manage/customaudiences/tos.php)に同意する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|メールアドレス|  &lt;ul&gt;&lt;li&gt;メールアドレスに基づいてユーザーを特定します。&lt;/li&gt;&lt;/ul&gt; |
|電話番号|  &lt;ul&gt;&lt;li&gt;電話番号に基づいてユーザーを特定します。国コード、エリアコード、番号のみの数字を含めます。例：`16505551212`。&lt;/li&gt;&lt;/ul&gt; |
|FacebookユーザーID|  &lt;ul&gt;&lt;li&gt;Facebook IDに基づいてユーザーを特定します。&lt;/li&gt;&lt;li&gt;この識別タイプを使用する場合は、「FacebookアプリID」を提供する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|FacebookアプリID|  &lt;ul&gt;&lt;li&gt;「FacebookユーザーID」がユーザー識別子として使用される場合は必須です。&lt;/li&gt;&lt;li&gt;「FacebookユーザーID」を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|モバイル広告ID|  &lt;ul&gt;&lt;li&gt;アプリユーザーID、AppleのAdvertising Identifier（IDFA）、またはAndroidの広告IDに基づいてユーザーをターゲットにします。&lt;/li&gt;&lt;/ul&gt; |
|外部ID|  &lt;ul&gt;&lt;li&gt;ハッシュ化しないでください。&lt;/li&gt;&lt;li&gt;広告主のロイヤルティ会員ID、ユーザーID、外部クッキーIDなど、広告主の任意の一意のIDです。&lt;/li&gt;&lt;/ul&gt; |
|郵便番号|  &lt;ul&gt;&lt;li&gt;郵便番号。&lt;/li&gt;&lt;li&gt;国によって形式が異なります。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;ユーザーの市区町村。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点やスペースは含まない。&lt;/li&gt;&lt;/ul&gt; |
|国|  &lt;ul&gt;&lt;li&gt;ユーザーの国。&lt;/li&gt;&lt;li&gt;2文字の国コード。&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2形式。&lt;/li&gt;&lt;/ul&gt; |
|米国の州|  &lt;ul&gt;&lt;li&gt;アメリカ合衆国の州。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;2文字のANSI省略コード。&lt;/li&gt;&lt;/ul&gt; |
|名|  &lt;ul&gt;&lt;li&gt;ユーザーの名前。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;ユーザーの姓。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|生年|  &lt;ul&gt;&lt;li&gt;ユーザーの生年。&lt;/li&gt;&lt;li&gt;&lt;code&gt;YYYY&lt;/code&gt;形式。&lt;/li&gt;&lt;li&gt;&lt;code&gt;1900&lt;/code&gt;年から現在の年までの値。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|生日|  &lt;ul&gt;&lt;li&gt;ユーザーの生日。&lt;/li&gt;&lt;li&gt;`DD`形式。&lt;/li&gt;&lt;li&gt;`01`から`31`までの値。&lt;/li&gt;&lt;/ul&gt; |
|生月|  &lt;ul&gt;&lt;li&gt;ユーザーの生月。&lt;/li&gt;&lt;li&gt;`MM`形式。&lt;/li&gt;&lt;li&gt;`01`から`12`までの値。&lt;/li&gt;&lt;/ul&gt; |
|カスタムオーディエンスオーバーライド|  &lt;ul&gt;&lt;li&gt;（オプション）**カスタムオーディエンスID**を提供して、必須セクションの値を上書きします。このフィールドを使用して、AudienceStream変数でオーディエンスIDを入力できます。&lt;/li&gt;&lt;/ul&gt; |
|ユーザー識別子が既にハッシュ化されている|  &lt;ul&gt;&lt;li&gt;ターゲットユーザー識別子が既にハッシュ化されている場合は、このオプションを選択します。FacebookではSHA256でハッシュ化された値のみがサポートされています。&lt;/li&gt;&lt;/ul&gt;

### カスタムオーディエンスからのユーザー削除


#### パラメータ

|パラメータ| 説明|
|---| ---|
|削除対象のカスタムオーディエンス|  &lt;ul&gt;&lt;li&gt;（必須）ターゲットのカスタムオーディエンスを選択してください。&lt;/li&gt;&lt;li&gt;このコネクタを使用してFacebookでカスタムオーディエンスを構築する前に、[Facebookカスタムオーディエンス利用規約](https://www.facebook.com/ads/manage/customaudiences/tos.php)に同意する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|メールアドレス|  &lt;ul&gt;&lt;li&gt;メールアドレスに基づいてユーザーを特定します。&lt;/li&gt;&lt;/ul&gt; |
|電話番号|  &lt;ul&gt;&lt;li&gt;電話番号に基づいてユーザーを特定します。国コード、市外局番、番号のみを含めてください。例：`16505551212`。&lt;/li&gt;&lt;/ul&gt; |
|FacebookユーザーID|  &lt;ul&gt;&lt;li&gt;Facebook IDに基づいてユーザーを特定します。&lt;/li&gt;&lt;li&gt;この識別タイプを使用する場合は、FacebookユーザーID（UID）に対応する「FacebookアプリID」を提供する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|FacebookアプリID|  &lt;ul&gt;&lt;li&gt;「FacebookユーザーID」がユーザー識別子として使用される場合に必要です。&lt;/li&gt;&lt;li&gt;「FacebookユーザーID」を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|モバイル広告ID|  &lt;ul&gt;&lt;li&gt;アプリユーザーID、Appleの広告識別子（IDFA）、またはAndroidの広告IDに基づいてユーザーをターゲットにします。&lt;/li&gt;&lt;/ul&gt; |
|外部ID|  &lt;ul&gt;&lt;li&gt;ハッシュ化しないでください。&lt;/li&gt;&lt;li&gt;広告主からの任意の一意のID、例えばロイヤルティ会員ID、ユーザーID、外部クッキーIDなど。&lt;/li&gt;&lt;/ul&gt; |
|郵便番号|  &lt;ul&gt;&lt;li&gt;郵便番号。&lt;/li&gt;&lt;li&gt;国によって形式が異なります。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;ユーザーの市区町村。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点やスペースは含まない。&lt;/li&gt;&lt;/ul&gt; |
|国|  &lt;ul&gt;&lt;li&gt;ユーザーの国。&lt;/li&gt;&lt;li&gt;2文字の国コード。&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2形式。&lt;/li&gt;&lt;/ul&gt; |
|米国の州|  &lt;ul&gt;&lt;li&gt;アメリカ合衆国の州。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;2文字のANSI省略形コード。&lt;/li&gt;&lt;/ul&gt; |
|名|  &lt;ul&gt;&lt;li&gt;ユーザーの名前。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;ユーザーの姓。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|イニシャル|  &lt;ul&gt;&lt;li&gt;ユーザーのイニシャル。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|生年|  &lt;ul&gt;&lt;li&gt;ユーザーの生年。&lt;/li&gt;&lt;li&gt;`YYYY`形式。&lt;/li&gt;&lt;li&gt;`1900`年から現在の年までの値。&lt;/li&gt;&lt;/ul&gt; |
|生日|  &lt;ul&gt;&lt;li&gt;ユーザーの生日。&lt;/li&gt;&lt;li&gt;`DD`形式。&lt;/li&gt;&lt;li&gt;`01`から`31`までの値。&lt;/li&gt;&lt;/ul&gt; |
|生月|  &lt;ul&gt;&lt;li&gt;ユーザーの生月。&lt;/li&gt;&lt;li&gt;`MM`形式。&lt;/li&gt;&lt;li&gt;`01`から`12`までの値。&lt;/li&gt;&lt;/ul&gt; |
|性別|  &lt;ul&gt;&lt;li&gt;ユーザーの性別。&lt;/li&gt;&lt;li&gt;`M`は男性、`F`は女性&lt;/li&gt;&lt;/ul&gt; |
|ルックアライク値|  &lt;ul&gt;&lt;li&gt;CRMデータからシードカスタムオーディエンスを作成する際に各ユーザーに構成される任意の数値。&lt;/li&gt;&lt;li&gt;Facebookはこの値を使用して、オーディエンス内のどのユーザーがあなたにとって最も価値があるかを定量的に判断します。&lt;/li&gt;&lt;/ul&gt; |
|カスタムオーディエンスの上書き|  &lt;ul&gt;&lt;li&gt;（オプション）**カスタムオーディエンスID**を提供して、必須セクションの値を上書きします。このフィールドを使用すると、AudienceStreamの変数を使用してオーディエンスIDを入力できます。&lt;/li&gt;&lt;/ul&gt; |
|ユーザー識別子が既にハッシュ化されている|  &lt;ul&gt;&lt;li&gt;ターゲットのユーザー識別子が既にハッシュ化されている場合は、このオプションを選択します。FacebookではSHA256でハッシュ化された値のみがサポートされています。&lt;/li&gt;&lt;/ul&gt; |

### すべてのカスタムオーディエンスからユーザーをオプトアウト

#### パラメータ

|パラメータ| 説明|
|---| ---|
|メールアドレス|  &lt;ul&gt;&lt;li&gt;メールアドレスに基づいてユーザーを特定します。&lt;/li&gt;&lt;/ul&gt; |
|電話番号|  &lt;ul&gt;&lt;li&gt;電話番号に基づいてユーザーを特定します。国コード、市外局番、番号のみを含めてください。例：`16505551212`。&lt;/li&gt;&lt;/ul&gt; |
|FacebookユーザーID|  &lt;ul&gt;&lt;li&gt;Facebook IDに基づいてユーザーを特定します。&lt;/li&gt;&lt;li&gt;この識別タイプを使用する場合は、FacebookユーザーID（UID）に対応する「FacebookアプリID」を提供する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|FacebookアプリID|  &lt;ul&gt;&lt;li&gt;「FacebookユーザーID」がユーザー識別子として使用される場合に必要です。&lt;/li&gt;&lt;li&gt;「FacebookユーザーID」を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|モバイル広告ID|  &lt;ul&gt;&lt;li&gt;アプリユーザーID、Appleの広告識別子（IDFA）、またはAndroidの広告IDに基づいてユーザーをターゲットにします。&lt;/li&gt;&lt;/ul&gt; |
|外部ID|  &lt;ul&gt;&lt;li&gt;ハッシュ化しないでください。&lt;/li&gt;&lt;li&gt;広告主からの任意の一意のID、例えばロイヤルティ会員ID、ユーザーID、外部クッキーIDなど。&lt;/li&gt;&lt;/ul&gt; |
|郵便番号|  &lt;ul&gt;&lt;li&gt;郵便番号。&lt;/li&gt;&lt;li&gt;国によって形式が異なります。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;ユーザーの市区町村。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点やスペースは含まない。&lt;/li&gt;&lt;/ul&gt; |
|国|  &lt;ul&gt;&lt;li&gt;ユーザーの国。&lt;/li&gt;&lt;li&gt;2文字の国コード。&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2形式。&lt;/li&gt;&lt;/ul&gt; |
|米国の州|  &lt;ul&gt;&lt;li&gt;アメリカ合衆国の州。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;2文字のANSI省略形コード。&lt;/li&gt;&lt;/ul&gt; |
|生年|  &lt;ul&gt;&lt;li&gt;ユーザーの生年。&lt;/li&gt;&lt;li&gt;`YYYY`形式。&lt;/li&gt;&lt;li&gt;`1900`年から現在の年までの値。&lt;/li&gt;&lt;/ul&gt; |
|生日|  &lt;ul&gt;&lt;li&gt;ユーザーの生日。&lt;/li&gt;&lt;li&gt;`DD`形式。&lt;/li&gt;&lt;li&gt;`01`から`31`までの値。&lt;/li&gt;&lt;/ul&gt; |
|生月|  &lt;ul&gt;&lt;li&gt;ユーザーの生月。&lt;/li&gt;&lt;li&gt;`MM`形式。&lt;/li&gt;&lt;li&gt;`01`から`12`までの値。&lt;/li&gt;&lt;/ul&gt; |
|ユーザー識別子が既にハッシュ化されている|  &lt;ul&gt;&lt;li&gt;ターゲットのユーザー識別子が既にハッシュ化されている場合は、このオプションを選択します。FacebookではSHA256でハッシュ化された値のみがサポートされています。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;ユーザーの姓。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|イニシャル|  &lt;ul&gt;&lt;li&gt;ユーザーのイニシャル。&lt;/li&gt;&lt;li&gt;小文字。&lt;/li&gt;&lt;li&gt;句読点や特殊文字は含まない。&lt;/li&gt;&lt;li&gt;UTF-8形式。&lt;/li&gt;&lt;/ul&gt; |
|性別|  &lt;ul&gt;&lt;li&gt;ユーザーの性別。&lt;/li&gt;&lt;li&gt;`M`は男性、`F`は女性&lt;/li&gt;&lt;/ul&gt; |
|ルックアライク値|  &lt;ul&gt;&lt;li&gt;CRMデータからシードカスタムオーディエンスを作成する際に各ユーザーに構成される任意の数値。&lt;/li&gt;&lt;li&gt;Facebookはこの値を使用して、オーディエンス内のどのユーザーがあなたにとって最も価値があるかを定量的に判断します。&lt;/li&gt;&lt;/ul&gt; |

## Facebookオーディエンスコネクタの使用

### 訪問IDの作成

Facebookオーディエンスコネクタは、少なくとも1つの訪問ID属性を必要とし、Facebookオーディエンスに渡すことができます。

訪問ID属性を構成するためのリソースを以下に示します：

* [訪問ID属性の構成]()
* [FacebookマーケティングAPI](https://developers.facebook.com/docs/marketing-api/audiences-api)

### オーディエンスの定義

アカウントには複数の訪問ID属性が定義されている場合があります。この場合、訪問IDが割り当てられている訪問のみが含まれるオーディエンスを確実にするために、[「既知の訪問」バッジ]()を作成することが重要です。この属性を使用することで、Facebookに渡すことができる訪問IDが割り当てられている訪問のみが含まれるオーディエンスを確保できます。未知の訪問をターゲットにすることはできません。

「既知の訪問」バッジを他の条件と組み合わせて、コネクタ用のオーディエンスを作成します。

このコネクタには、メール、電話、アプリ、またはユーザーIDなどの必須IDパラメータがあります。これらのIDのいずれかが必要です。これらのIDをオーディエンスフィルターに含めることで、コネクタエラーを避けるのに役立ちます。

### テスト

最も効果的なテスト方法は、[トレース]()を実行してイベントが適切に処理されていることを確認し、Facebookダッシュボードを確認してカスタムオーディエンスが作成され、人が追加されていることを確認することです。

## FAQ

### なぜAudienceStreamのドロップダウンリストに私のオーディエンスが表示されないのですか？

Facebookに2,000を超えるオーディエンスがある場合、それらはすべてAudienceStreamコネクタのドロップダウンリストで選択可能ではありません。

Facebookですべてのオーディエンスを表示し、特定のオーディエンスの識別子を選択するための次の手順を使用してください：

1. Facebookオーディエンスアカウントにアクセス権を持つユーザーとしてFacebookにログインします。
1. &lt;https://www.facebook.com/adsmanager/audiences&gt;にアクセスします。
1. 探しているオーディエンスを見つけて、オーディエンスIDをコピーします。
    オーディエンスIDが表示されない場合は、テーブル列ビューを変更してそれを含めることができます。

    ![](/images/server-side-connectors/facebook-ads-find-audience-id.png)
1. AudienceStreamに戻り、AudienceStreamコネクタのカスタム値としてオーディエンスIDを入力します。