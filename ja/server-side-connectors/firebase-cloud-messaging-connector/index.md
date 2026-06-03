---
title: Firebase Cloud Messaging（FCM）コネクタ構成ガイド
description: この記事では、Firebase Cloud Messagingコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/firebase-cloud-messaging-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google Firebase API
* APIバージョン：v1
* APIエンドポイント：`https://fcm.googleapis.com/`
* ドキュメント：[Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/concept-options)

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| Androidデバイスへのメッセージ送信 | ✓ | ✓ |
| iOSデバイスへのメッセージ送信 | ✓ | ✓ |
| Webアプリへのメッセージ送信 | ✓ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **FirebaseプロジェクトID**  
**必須。** プロジェクトIDを入力します。FirebaseプロジェクトのIDはFirebaseコンソールを使用して見つけることができます。[プロジェクト構成](https://console.firebase.google.com/project/_/settings/general/)を開きます。プロジェクトIDは上部のペインに表示されます。
* **クライアントID**  
**必須。** Firebase Cloud Messaging APIにアクセスできるWebアプリケーションのクライアントIDを入力します。[Google APIコンソールの認証情報ページ](https://console.developers.google.com/apis/credentials)で承認されたリダイレクトURI：`https://my.tealiumiq.com/oauth/google/callback.html`をホワイトリストに登録する必要があります。[認証情報の作成](https://developers.google.com/identity/protocols/OAuth2InstalledApp#creatingcred)を参照してください。
* **クライアントシークレット**  
**必須。** Webアプリケーションクライアントシークレットを入力します。

## アクション

アクション名を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### Androidデバイスへのメッセージ送信


#### パラメータ

 メッセージの対象を指定するには、以下のパラメータのうち**いずれか一つ**を構成してください: `Token`, `Topic`, `Condition`。

| **パラメータ** | **説明** |
| --- | --- |
| Token | メッセージを送信する登録トークン。 |
| Topic | メッセージを送信する購読済みトピック名。例: `weather`。注: `/topics/` プレフィックスは含めないでください。 |
| Condition | トピックの購読条件を指定してメッセージを送信します。例: `foo in topics &amp;&amp; bar in topics`。 |
| Analytics Label | メッセージの分析データに関連付けられたラベル。 |
| Collapse Key | メッセージのグループを識別するキーで、配信が再開されたときに最後のメッセージのみが送信されるようにすることができます。同時に許可される異なるコラプスキーは最大4つです。 |
| Priority | メッセージの優先度。値は `NORMAL` または `HIGH` があります。詳細については、[メッセージの優先度の構成](https://firebase.google.com/docs/cloud-messaging/concept-options#setting-the-priority-of-a-message)を参照してください。 |
| Time to Live | 秒単位の期間で、最大9桁の小数点以下の桁数を持ち、`s` で終わります。例: `3.5s`。このフィールドは、デバイスがオフラインの場合にメッセージがFCM保存に保持される時間（秒）を表します。サポートされる最大の生存時間は4週間で、構成されていない場合のデフォルト値は4週間です。メッセージをすぐに送信したい場合は `0` に構成します。 |
| Restricted Package Name | アプリケーションのパッケージ名で、メッセージを受信するためには登録トークンと一致している必要があります。 |
| Direct Boot Ok | `true` に構成すると、デバイスがダイレクトブートモードの間にアプリへのメッセージが配信されます。詳細については、[ダイレクトブートモードのサポート](https://developer.android.com/training/articles/direct-boot)を参照してください。|
| Title | 通知のタイトル。 |
| Body | 通知の本文テキスト。 |
| Icon | 通知のアイコン。通知アイコンを `myicon` に構成すると、ドローアブルリソース `myicon` が使用されます。指定されていない場合、FCMはアプリマニフェストで指定されたランチャーアイコンを表示します。 |
| Color | 通知アイコンの色を `#rrggbb` 形式で表します。 |
| Sound | デバイスが通知を受信したときに再生するサウンド。`default` またはアプリにバンドルされているサウンドリソースのファイル名をサポートします。サウンドファイルは `/res/raw/` に存在する必要があります。 |
| Tag | 通知ドロワー内の既存の通知を置き換えるために使用される識別子。指定されていない場合、各リクエストは新しい通知を作成します。指定されており、同じタグの通知が既に表示されている場合、新しい通知は通知ドロワー内の既存の通知を置き換えます。 |
| Click Action | 通知をクリックしたユーザーに関連付けられたアクション。指定されている場合、ユーザーが通知をクリックすると一致するインテントフィルターを持つアクティビティが起動されます。 |
| Body Localization Key | アプリリソース内の本文文字列のキーで、ユーザーの現在のロケールに本文テキストをローカライズするために使用されます。詳細については、[文字列リソース](https://developer.android.com/guide/topics/resources/string-resource.html)を参照してください。 |
| Body Localization Args | **Body Localization Key**でローカライズされた本文テキストにおいて、フォーマット指定子の代わりに使用される文字列値です。詳細については、[フォーマットとスタイリング](https://developer.android.com/guide/topics/resources/string-resource.html#FormattingAndStyling)を参照してください。 |
| Title Localization Key | アプリのリソース内のタイトル文字列のキーで、ユーザーの現在のロケールにタイトルテキストをローカライズするために使用されます。詳細については、[文字列リソース](https://developer.android.com/guide/topics/resources/string-resource.html)を参照してください。 |
| Title Localization Args | **Title Localization Key**でローカライズされたタイトルテキストにおいて、フォーマット指定子の代わりに使用される文字列値です。詳細については、[フォーマットとスタイリング](https://developer.android.com/guide/topics/resources/string-resource.html#FormattingAndStyling)を参照してください。 |
| Channel ID | [通知のチャンネルID](https://developer.android.com/develop/ui/views/notifications#ManageChannels)（Android Oで新設）。アプリはこのチャンネルIDでチャンネルを作成する必要があります。指定されていない場合、または提供されたチャンネルIDがアプリによってまだ作成されていない場合、FCMは代わりにアプリで指定されたチャンネルIDを使用します。 |
| Ticker | このパラメータは、アクセシビリティサービスに送信される通知ティッカーテキストを構成します。APIレベル21（Lollipop）より前では、通知が最初に到着したときにステータスバーに表示されるテキストを構成します。 |
| Sticky | `false`に構成されている場合、または指定されていない場合、ユーザーがパネルでクリックすると通知は自動的に消去されます。`true`に構成すると、ユーザーがクリックしても通知は持続します。 |
| Event Time | 通知のイベントが発生した時間。パネル内の通知はこの時間によってソートされます。RFC3339 UTC形式のタイムスタンプで、ナノ秒解像度と最大9桁の小数点以下の桁数を持ちます。例: `2014-10-02T15:01:23Z` および `2014-10-02T15:01:23.045123456Z`。 |
| Local Only | `true`に構成すると、通知が現在のデバイスにのみ関連していることを示します。 |
| Notification Priority | この通知の相対的な優先度を構成します。優先度は通知の重要性の指標です。値は `PRIORITY_UNSPECIFIED`, `PRIORITY_MIN`, `PRIORITY_LOW`, `PRIORITY_DEFAULT`, `PRIORITY_HIGH`, `PRIORITY_MAX` のいずれかです。 |
| Default Sound | `true`に構成すると、通知にAndroidフレームワークのデフォルトのサウンドを使用します。 |
| Default Vibrate Timings | `true`に構成すると、通知にAndroidフレームワークのデフォルトの振動パターンを使用します。 |
| Default Light Settings | `true`に構成すると、通知にAndroidフレームワークのデフォルトのLEDライト構成を使用します。 |
| Vibrate Timings | 使用する振動パターンを構成します。秒単位の期間で、最大9桁の小数点以下の桁数を持ち、`s`で終わります。例: `3.5s`。[Firebaseリソース: メッセージ](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification)を参照してください。 |
| Visibility | 通知の[可視性](https://developer.android.com/reference/android/app/Notification#visibility)を構成します。値は `VISIBILITY_UNSPECIFIED`, `PRIVATE`, `PUBLIC`, `SECRET` のいずれかです。 |
| Notification Count | この通知内のアイテム数を構成します。 |
| Light On Duration | **Light Off Duration**とともに、LEDフラッシュの点滅レートを定義します。秒単位の期間で、最大9桁の小数点以下の桁数を持ち、`s`で終わります。例: `3.5s`。 |
| Light Off Duration | **Light On Duration**とともに、LEDフラッシュの点滅レートを定義します。秒単位の期間で、最大9桁の小数点以下の桁数を持ち、`s`で終わります。例: `3.5s`。 |
| Color Red | 全体のライトカラーの中で赤の量を表す `0` から `1` の間の値です。この値を Color Green および Color Blue で構成した値と組み合わせて、全体の色を決定します。例えば、Color Red = `1`, Color Blue = `.5`, Color Green = `0` はフューシャまたは濃いピンクを作り出します。 |
| Color Green | 全体のライトカラーの中で緑の量を表す `0` から `1` の間の値です。この値を Color Red および Color Blue で構成した値と組み合わせて、全体の色を決定します。 |
| Color Blue | 全体のライトカラーの中で青の量を表す `0` から `1` の間の値です。この値を Color Green および Color Red で構成した値と組み合わせて、全体の色を決定します。 |
| Color Alpha | この色がピクセルに適用されるべき割合を表す分数です。つまり、最終的なピクセルの色は次の方程式によって定義されます: **ピクセルの色 = alpha \* (この色) &#43; (1.0 - alpha) \* (背景色)**。 |
| Image | 通知に表示される画像のURL。 |
| Data | `&#34;key&#34; : &#34;value&#34;` ペア形式のユーザー指定データ。 |
| テンプレート変数 | **テンプレート**用のテンプレート変数をデータ入力として提供します。詳細と使用例については、を参照してください。&lt;ul&gt;&lt;li&gt;ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`。&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
| テンプレート | **メッセージオプション**および**通知オプション**セクションで参照されるテンプレートを提供します。詳細については、を参照してください。テンプレートは、サポートされるフィールドに名前で二重中括弧で挿入されます。例：`{{template_name}}` |

* [リソース: メッセージ](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#resource:-message)、[AndroidConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidconfig)のドキュメントを参照して使用例を確認してください。

* ネストされたオブジェクトをサポートするには、**テンプレート**セクションでテンプレートを定義します。テンプレートは、一致する二重中括弧でその名前を参照する**カスタムテキスト**オプションを使用してマッピングする必要があります：`{{template_name}}`。

### iOSデバイスへのメッセージ送信

#### パラメータ

 メッセージのターゲットを指定するには、次のパラメータの**いずれか一つ**を構成します：`Token`、`Topic`、または`Condition`。 

| **パラメータ** | **説明** |
| --- | --- |
| Token | メッセージを送信する登録トークン。 |
| Topic | メッセージを送信する購読済みトピック名。例：`weather`。注：`/topics/`プレフィックスは含めないでください。 |
| Condition | トピックの購読条件を送信する。例：`foo in topics &amp;&amp; bar in topics`。 |
| Analytics Label | メッセージの分析データに関連付けられたラベル。 |
| Image | 通知に表示される画像のURL。 |
| Title | 通知のタイトル。Apple Watchはこの文字列を短い見た目の通知インターフェースで表示します。 |
| Subtitle | 通知の目的を説明する追加情報。 |
| Body | アラートメッセージの内容。 |
| Launch Image | 表示する起動画像ファイルの名前。 |
| Title Localization Key | ローカライズされたタイトル文字列のキー。**Title**キーの代わりにこのキーを指定して、アプリの`Localizable.strings`ファイルからタイトルを取得します。値は文字列ファイルのキー名を含む必要があります。 |
| Title Localization Args | タイトル文字列の変数に対する置換値を含む文字列の配列。**Title Localization Key**で指定された文字列の`%@`文字は、この配列の値によって置換されます。配列の最初の項目は文字列の最初の`%@`文字を置換し、次の項目は次の`%@`文字を置換します。 |
| Subtitle Localization Key | ローカライズされたサブタイトル文字列のキー。**Subtitle**キーの代わりにこのキーを使用して、アプリの`Localizable.strings`ファイルからサブタイトルを取得します。値は文字列ファイルのキー名を含む必要があります。 |
| Subtitle Localization Args | サブタイトル文字列の変数に対する置換値を含む文字列の配列。**Subtitle Localization Key**で指定された文字列の`%@`文字は、この配列の値によって置換されます。 |
| Body Localization Key | ローカライズされたメッセージ文字列のキー。**Body**キーの代わりにこのキーを使用して、アプリの`Localizable.strings`ファイルからメッセージテキストを取得します。値は文字列ファイルのキー名を含む必要があります。 |
| Body Localization Args | メッセージテキストの変数に対する置換値を含む文字列の配列。**Body Localization Key**で指定された文字列の`%@`文字は、この配列の値によって置換されます。 |
| Badge | アプリのアイコンに表示するバッジの数。このパラメータを`0`に構成すると、現在のバッジがある場合はそれを削除します。 |
| Sound Critical | クリティカルアラートフラグ。このパラメータを`1`に構成すると、クリティカルアラートが有効になります。 |
| Sound File Name | アプリのメインバンドルまたはアプリのコンテナディレクトリのLibrary/Soundsフォルダにあるサウンドファイルの名前。この値を`default`に構成すると、システムサウンドが再生されます。 |
| Sound Volume | クリティカルアラートのサウンドの音量。このパラメータを`0`（無音）から`1`（最大音量）の間の値に構成します。 |
| Thread ID | 関連する通知をグループ化するためのアプリ固有の識別子。 |
| Category | 通知のタイプ。 |
| Content Available | バックグラウンド通知フラグ。サイレントバックグラウンド更新を実行するには、値`1`を指定し、ペイロードに**Alert**、**Badge**、または**Sound**キーを含めないでください。 |
| Mutable Content | 通知サービスアプリ拡張フラグ。値が1の場合、システムは配信前に通知を通知サービスアプリ拡張に渡します。 |
| Target Content ID | 最前面に持ち出されるウィンドウの識別子。 |
| Interruption Level | 通知の重要度と配信タイミング。 |
| Relevance Score | システムがアプリの通知を並べ替えるために使用する関連性スコア。`0`から`1`の間の数値。 |
| Filter Criteria | 現在の**Focus**で通知が表示されるかどうかをシステムが評価するための文字列。 |
| Stale Date | **Live Activity**が古くなったり、時代遅れになったりする日付を表すUNIXタイムスタンプ。 |
| Content State | **Live Activity**の更新されたコンテンツまたは最終コンテンツを含むJSONオブジェクト。このパラメータの内容は、カスタム[ActivityAttributes](https://developer.apple.com/documentation/activitykit/activityattributes)実装で説明するデータと一致する必要があります。このオプションはテンプレートをサポートしています。 |
| Timestamp | リモート通知が**Live Activity**を更新または終了するために送信される時刻を指定するUNIXタイムスタンプ。 |
| Events | リモートプッシュ通知で進行中の**Live Activity**を更新または終了するかどうかを指定します。値は`update`または`end`になります。 |
| Data | `&#34;key&#34; : &#34;value&#34;`ペア形式のユーザー指定データ。 |
| Headers | Apple Push Notification Serviceで定義されたHTTPリクエストヘッダー。**apns-expiration**や**apns-priority**などのサポートされているヘッダーについては、[APNsリクエストヘッダー](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/sending_notification_requests_to_apns)を参照してください。[Firebaseリソース: メッセージ](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification)の詳細を参照してください。|
| テンプレート変数 | **テンプレート**用のテンプレート変数をデータ入力として提供します。詳細と使用例については、を参照してください。&lt;ul&gt;&lt;li&gt;ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`。&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
| テンプレート | **メッセージオプション**および**通知オプション**セクションで参照されるテンプレートを提供します。詳細については、を参照してください。テンプレートは、サポートされるフィールドに名前で二重中括弧で挿入されます。例：`{{template_name}}` |

* [AndroidConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidconfig)のドキュメントを参照して使用例を確認してください。

* ネストされたオブジェクトをサポートするには、**テンプレート**セクションでテンプレートを定義します。テンプレートは、一致する二重中括弧でその名前を参照する**カスタムテキスト**オプションを使用してマッピングする必要があります：`{{template_name}}`。

### Webアプリへのメッセージ送信

#### パラメータ

 メッセージの対象を指定するには、以下のパラメータのうち**いずれか一つ**を構成してください: `Token`, `Topic`, `Condition`。

| **パラメータ** | **説明** |
| --- | --- |
| Token | メッセージを送信する登録トークン。 |
| Topic | メッセージを送信する購読済みトピック名。例: `weather`。注: `/topics/` プレフィックスは含めないでください。 |
| Condition | トピックの購読条件を指定してメッセージを送信します。例: `foo in topics &amp;&amp; bar in topics`。 |
| Analytics Label | メッセージの分析データに関連付けられたラベル。 |
| Link | ユーザーが通知をクリックしたときに開くセキュアリンク。値は `https://` で始まる必要があります。 |
| Action | 通知に表示されるユーザーアクションを識別する文字列。 |
| Action Title | ユーザーに表示されるアクションテキストを含む文字列。 |
| Action Icon | アクションと共に表示されるアイコンのURLを含む文字列。 |
| Badge | 通知自体を表示するスペースが不足している場合に通知を表すために使用される画像のURL。 |
| Title | 通知のタイトル。 |
| Body | 通知の本文文字列。 |
| Data | 通知のデータの構造化クローンを返します。このオプションはテンプレートをサポートしています。 |
| Direction | 通知のテキスト方向。 |
| Icon | 通知のアイコンとして使用される画像のURL。 |
| Image | 通知の一部として表示される画像のURL。 |
| Language | 通知の言語コード。 |
| Renotify | 古い通知を新しい通知が置き換えた後にユーザーに通知するかどうかを指定します。 |
| Require Interaction | 通知が自動的に閉じるのではなく、ユーザーがクリックまたは閉じるまでアクティブのままであることを示すブール値。 |
| Silent | 通知が無音であるかどうかを指定します。このパラメータが `true` に構成されている場合、デバイスの構成に関わらず、音や振動は発生しません。 |
| Tag | 通知のID。 |
| Timestamp | 通知が作成される時間、または適用される時間（過去、現在、または未来）を指定します。 |
| Vibrate | 振動ハードウェアを持つデバイスが発する振動パターンを指定します。秒単位で最大9桁の小数点以下の桁数を持つ期間。例: `3.5s`。[Firebase Resource: Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification)を参照してください。 |
| Data | `&#34;key&#34; : &#34;value&#34;` 形式のユーザー指定データ。 |
| Headers | Webpushプロトコルで定義されたHTTPヘッダー。サポートされるヘッダーについては、[Webpush protocol](https://www.rfc-editor.org/rfc/rfc8030#section-5)を参照してください。例: `&#34;TTL&#34;: &#34;15&#34;`。詳細については、[Firebase Resource: Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification)を参照してください。 |
| Template Variables | **テンプレート**にデータ入力としてテンプレート変数を提供します。詳細と使用例については、を参照してください。&lt;ul&gt;&lt;li&gt;ドット表記を使用してネストされたテンプレート変数に名前を付けます。例: `items.name`。&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
| Templates | **メッセージオプション**および**通知オプション**セクションで参照されるテンプレートを提供します。詳細については、を参照してください。テンプレートは、対応するフィールドに名前で二重中括弧を使用して注入されます。例: `{{template_name}}` |

* 使用例については、[AndroidConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidconfig)のドキュメントを参照してください。

* ネストされたオブジェクトをサポートするには、**テンプレート**セクションでテンプレートを定義し、**カスタムテキスト**オプションを使用して名前でマッピングします: `{{template_name}}`。&lt;/li&gt;&lt;/ul&gt;
