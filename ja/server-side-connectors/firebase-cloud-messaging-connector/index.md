---
title: Firebase Cloud Messaging（FCM）コネクタ構成ガイド
description: この記事では、Firebase Cloud Messagingコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/firebase-cloud-messaging-connector/
---
## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：Google Firebase API
* APIバージョン：v1
* APIエンドポイント：`https://fcm.googleapis.com/`
* ドキュメント：[Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging)

## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| Androidデバイスにメッセージを送信 | ✓ | ✓ |
| iOSデバイスにメッセージを送信 | ✓ | ✓ |
| Webアプリにメッセージを送信 | ✓ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の項目を構成します。

* **FirebaseプロジェクトID**  
（必須）プロジェクトIDを入力します。FirebaseコンソールでFirebaseプロジェクトのIDを確認できます。[プロジェクト構成](https://console.firebase.google.com/project/_/settings/general/)を開きます。プロジェクトIDは上部のペインに表示されます。
* **クライアントID**  
（必須）Firebase Cloud Messaging APIへのアクセス権を持つWebアプリケーションのクライアントIDを入力します。[Google APIコンソールの認証情報ページ](https://console.developers.google.com/apis/credentials)で、承認済みのリダイレクトURIとして`https://my.tealiumiq.com/oauth/google/callback.html`を許可リストに追加する必要があります。[認証情報の作成](https://developers.google.com/identity/protocols/OAuth2InstalledApp#creatingcred)を参照してください。
* **クライアントシークレット**  
（必須）Webアプリケーションのクライアントシークレットを入力します。

## アクション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### Androidデバイスにメッセージを送信
#### パラメーター


<blockquote>
メッセージの送信先を指定するには、次のパラメーターのうち **1 つだけ** を構成してください：`Token`、`Topic`、または `Condition`。
</blockquote>


| **パラメーター** | **説明** |
| --- | --- |
| Token | メッセージの送信先となる登録トークン。 |
| Topic | メッセージの送信先となる、購読済みトピックの名前。例：`weather`。注：`/topics/` プレフィックスは含めないでください。 |
| Condition | メッセージの送信先となる、購読済みトピックの条件。例：`foo in topics && bar in topics`。 |
| Analytics Label | メッセージの分析データに関連付けられるラベル。 |
| Collapse Key | 配信を再開できるようになったときに最後のメッセージだけが送信されるよう、まとめることができるメッセージグループの識別子。同時に使用できる異なる Collapse Key は最大 4 つです。 |
| Priority | メッセージの優先度。値には `NORMAL` または `HIGH` を指定できます。詳細については、[メッセージの優先度の構成](https://firebase.google.com/docs/cloud-messaging/concept-options#setting-the-priority-of-a-message)を参照してください。 |
| Time to Live | 秒単位の期間。小数部は最大 9 桁で、末尾に `s` を付けます。例：`3.5s`。このフィールドは、デバイスがオフラインの場合にメッセージを FCM 保存に保持する時間（秒）を表します。サポートされる最大有効期間は 4 週間で、未構成の場合のデフォルト値も 4 週間です。メッセージを直ちに送信する場合は `0` に構成します。 |
| Restricted Package Name | アプリケーションのパッケージ名。メッセージを受信するには、登録トークンと一致している必要があります。 |
| Direct Boot Ok | `true` に構成すると、デバイスがダイレクトブートモードの間もメッセージがアプリに配信されます。詳細については、[ダイレクトブートモードのサポート](https://developer.android.com/training/articles/direct-boot)を参照してください。|
| Title | 通知のタイトル。 |
| Body | 通知の本文テキスト。 |
| Icon | 通知のアイコン。Drawable リソース `myicon` を通知アイコンとして構成するには、`myicon` を指定します。指定しない場合、FCM はアプリのマニフェストで指定されたランチャーアイコンを表示します。 |
| Color | `#rrggbb` 形式で表される通知アイコンの色。 |
| Sound | デバイスが通知を受信したときに再生するサウンド。`default`、またはアプリにバンドルされているサウンドリソースのファイル名を指定できます。サウンドファイルは `/res/raw/` に配置する必要があります。 |
| Tag | 通知ドロワー内の既存の通知を置き換えるために使用する識別子。指定しない場合、リクエストごとに新しい通知が作成されます。指定した場合、同じタグを持つ通知がすでに表示されていれば、新しい通知が通知ドロワー内の既存の通知を置き換えます。 |
| Click Action | ユーザーが通知をクリックしたときに実行されるアクション。指定した場合、ユーザーが通知をクリックすると、一致するインテントフィルターを持つアクティビティが起動します。 |
| Body Localization Key | アプリのリソース内にある本文文字列のキー。本文テキストをユーザーの現在のロケールに合わせてローカライズするために使用されます。詳細については、[文字列リソース](https://developer.android.com/guide/topics/resources/string-resource.html)を参照してください。 |
| Body Localization Args | **Body Localization Key** 内の書式指定子の代わりに使用する文字列値。本文テキストをユーザーの現在のロケールに合わせてローカライズするために使用されます。詳細については、[書式構成とスタイル構成](https://developer.android.com/guide/topics/resources/string-resource.html#FormattingAndStyling)を参照してください。 |
| Title Localization Key | アプリのリソース内にあるタイトル文字列のキー。タイトルテキストをユーザーの現在のロケールに合わせてローカライズするために使用されます。詳細については、[文字列リソース](https://developer.android.com/guide/topics/resources/string-resource.html)を参照してください。 |
| Title Localization Args | **Title Localization Key** 内の書式指定子の代わりに使用する文字列値。タイトルテキストをユーザーの現在のロケールに合わせてローカライズするために使用されます。詳細については、[書式構成とスタイル構成](https://developer.android.com/guide/topics/resources/string-resource.html#FormattingAndStyling)を参照してください。 |
| Channel ID | [通知のチャンネル ID](https://developer.android.com/develop/ui/views/notifications#ManageChannels)（Android O で新たに導入）。このチャンネル ID を持つ通知を受信する前に、アプリで同じチャンネル ID のチャンネルを作成する必要があります。指定しない場合、または指定したチャンネル ID がアプリでまだ作成されていない場合、FCM は代わりにアプリで指定されたチャンネル ID を使用します。 |
| Ticker | 通知のティッカーテキストを構成します。このテキストはアクセシビリティサービスに送信されます。API レベル 21（Lollipop）より前では、通知が最初に届いたときにステータスバーに表示されるテキストを構成します。 |
| Sticky | `false` に構成するか指定しない場合、ユーザーがパネル内の通知をクリックすると、その通知は自動的に閉じられます。`true` に構成すると、ユーザーがクリックした後も通知は表示されたままになります。 |
| Event Time | 通知に関するイベントが発生した時刻。パネル内の通知はこの時刻に基づいて並べ替えられます。RFC3339 UTC 形式のタイムスタンプを使用し、ナノ秒の精度で小数部を最大 9 桁まで指定できます。例：`2014-10-02T15:01:23Z` および `2014-10-02T15:01:23.045123456Z`。 |
| Local Only | `true` に構成すると、その通知が現在のデバイスにのみ関連することを示します。 |
| Notification Priority | この通知の相対的な優先度を構成します。優先度は、通知の重要性を示します。値には `PRIORITY_UNSPECIFIED`、`PRIORITY_MIN`、`PRIORITY_LOW`、`PRIORITY_DEFAULT`、`PRIORITY_HIGH`、または `PRIORITY_MAX` を指定できます。 |
| Default Sound | `true` に構成すると、通知に Android フレームワークのデフォルトサウンドを使用します。 |
| Default Vibrate Timings | `true` に構成すると、通知に Android フレームワークのデフォルトのバイブレーションパターンを使用します。 |
| Default Light Settings | `true` に構成すると、通知に Android フレームワークのデフォルトの LED ライト構成を使用します。 |
| Vibrate Timings | 使用するバイブレーションパターンを構成します。秒単位の期間を、小数部最大 9 桁、末尾に `s` を付けて指定します。例：`3.5s`。詳細については、[Firebase リソース：Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification)を参照してください。 |
| Visibility | 通知の[公開範囲](https://developer.android.com/reference/android/app/Notification#visibility)を構成します。値には `VISIBILITY_UNSPECIFIED`、`PRIVATE`、`PUBLIC`、または `SECRET` を指定できます。 |
| Notification Count | この通知内の項目数を構成します。 |
| Light On Duration | **Light Off Duration** とともに、LED 点滅の速度を定義します。秒単位の期間を、小数部最大 9 桁、末尾に `s` を付けて指定します。例：`3.5s`。 |
| Light Off Duration | **Light On Duration** とともに、LED 点滅の速度を定義します。秒単位の期間を、小数部最大 9 桁、末尾に `s` を付けて指定します。例：`3.5s`。 |
| Color Red | ライト全体の色に含まれる赤の量を表す、`0` から `1` までの値。この値を Color Green および Color Blue に構成した値と組み合わせて、全体の色を決定します。たとえば、Color Red = `1`、Color Blue = `.5`、Color Green = `0` とすると、フクシアまたは濃いピンクになります。 |
| Color Green | ライト全体の色に含まれる緑の量を表す、`0` から `1` までの値。この値を Color Red および Color Blue に構成した値と組み合わせて、全体の色を決定します。 |
| Color Blue | ライト全体の色に含まれる青の量を表す、`0` から `1` までの値。この値を Color Green および Color Red に構成した値と組み合わせて、全体の色を決定します。 |
| Color Alpha | この色をピクセルに適用する割合。つまり、最終的なピクセルの色は、次の式で定義されます：**ピクセルの色 = アルファ \*（この色）+（1.0 - アルファ）\*（背景色）**。 |
| Image | 通知に表示する画像の URL。 |
| Data | ユーザーが指定する `"key" : "value"` ペア
形式のデータ。 |
| テンプレート変数 | **Templates** へのデータ入力としてテンプレート変数を指定します。詳細と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<ul><li>ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`。</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から構築されます。</li></ul> |
| テンプレート | **Message Options** セクションと **Notification Options** セクションで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。例：`{{template_name}}` |

* 使用例については、[Resource: Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#resource:-message)および[AndroidConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidconfig)のドキュメントを参照してください。

* ネストされたオブジェクトをサポートするには、**Templates** セクションを使用してテンプレートを定義します。テンプレート名を対応する二重波括弧で参照し、**Custom Text** オプションを使用してテンプレートをマッピングする必要があります：`{{template_name}}`。

### iOS デバイスへのメッセージ送信

#### パラメーター


<blockquote>
To specify a target for the message, set **only** the one of the following parameters: `Token`, `Topic`, or `Condition`.
</blockquote>


| **パラメーター** | **説明** |
| --- | --- |
| Token | メッセージの送信先となる登録トークン。 |
| Topic | メッセージの送信先となる、購読済みトピックの名前。例：`weather`。注：`/topics/` プレフィックスを含めないでください。 |
| Condition | メッセージの送信先となる、購読済みトピックの条件。例：`foo in topics && bar in topics`。 |
| Analytics Label | メッセージの分析データに関連付けられるラベル。 |
| Image | 通知に表示する画像の URL。 |
| Title | 通知のタイトル。Apple Watch では、この文字列がショートルック通知インターフェイスに表示されます。 |
| Subtitle | 通知の目的を説明する追加情報。 |
| Body | アラートメッセージの内容。 |
| Launch Image | 表示する起動画像ファイルの名前。 |
| Title Localization Key | ローカライズされたタイトル文字列のキー。アプリの `Localizable.strings` ファイルからタイトルを取得するには、**Title** キーの代わりにこのキーを指定します。値には、strings ファイル内のキー名を指定する必要があります。 |
| Title Localization Args | タイトル文字列内の変数の置換値を含む文字列の配列。**Title Localization Key** で指定された文字列内の各 `%@` 文字は、この配列の値に置き換えられます。配列の最初の項目が文字列内の最初の `%@` 文字を置き換え、2 番目の項目が 2 番目の `%@` 文字を置き換えます。以降も同様です。 |
| Subtitle Localization Key | ローカライズされたサブタイトル文字列のキー。アプリの `Localizable.strings` ファイルからサブタイトルを取得するには、**Subtitle** キーの代わりにこのキーを使用します。値には、strings ファイル内のキー名を指定する必要があります。 |
| Subtitle Localization Args | タイトル文字列内の変数の置換値を含む文字列の配列。**Subtitle Localization Key** で指定された文字列内の各 `%@` 文字は、この配列の値に置き換えられます。 |
| Body Localization Key | ローカライズされたメッセージ文字列のキー。アプリの `Localizable.strings` ファイルからメッセージテキストを取得するには、**Body** キーの代わりにこのキーを使用します。値には、strings ファイル内のキー名を指定する必要があります。 |
| Body Localization Args | メッセージテキスト内の変数の置換値を含む文字列の配列。**Body Localization Key** で指定された文字列内の各 `%@` 文字は、この配列の値に置き換えられます。 |
| Badge | アプリのアイコン上のバッジに表示する数値。現在のバッジがある場合、それを削除するには、このパラメーターを `0` に構成します。 |
| Sound Critical | 重大なアラートのフラグ。重大なアラートを有効にするには、このパラメーターを `1` に構成します。 |
| Sound File Name | アプリのメインバンドル、またはアプリのコンテナディレクトリ内の Library/Sounds フォルダーにあるサウンドファイルの名前。システムサウンドを再生するには、この値を文字列 `default` に構成します。 |
| Sound Volume | 重大なアラート音の音量。このパラメーターには、`0`（無音）から `1`（最大音量）までの値を構成します。 |
| Thread ID | 関連する通知をグループ化するための、アプリ固有の識別子。 |
| Category | 通知の種類。 |
| Content Available | バックグラウンド通知のフラグ。サイレントバックグラウンド更新を実行するには、値 `1` を指定し、ペイロードに **Alert**、**Badge**、**Sound** キーを含めないでください。 |
| Mutable Content | 通知サービスアプリ拡張機能のフラグ。値が 1 の場合、システムは配信前に通知を通知サービスアプリ拡張機能へ渡します。 |
| Target Content ID | 前面に表示するウィンドウの識別子。 |
| Interruption Level | 通知の重要度と配信タイミング。 |
| Relevance Score | 関連度スコア。アプリからの通知を並べ替えるためにシステムが使用する、`0` から `1` までの数値です。 |
| Filter Criteria | 現在の **Focus** で通知を表示するかどうかを判断するために、システムが評価する文字列。 |
| Stale Date | **Live Activity** が古くなった、または期限切れになったと見なされる日時を表す UNIX タイムスタンプ。 |
| Content State | **Live Activity** の更新済みまたは最終コンテンツを含む JSON オブジェクト。このパラメーターの内容は、カスタム [ActivityAttributes](https://developer.apple.com/documentation/activitykit/activityattributes) 実装で記述したデータと一致する必要があります。このオプションはテンプレート化をサポートします。 |
| Timestamp | **Live Activity** を更新または終了するためにリモート通知が送信される時刻を指定する UNIX タイムスタンプ。 |
| Events | リモートプッシュ通知によって進行中の **Live Activity** を更新するか終了するかを指定します。値には `update` または `end` を指定できます。 |
| Data | ユーザーが指定する、`"key" : "value"` ペア形式のデータ。 |
| Headers | Apple Push Notification Service で定義された HTTP リクエストヘッダー。**apns-expiration** や **apns-priority** など、サポートされるヘッダーについては、[APNs request headers](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/sending_notification_requests_to_apns)を参照してください。詳細については、[Firebase Resource: Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification)を参照してください。|
| Template Variables | **Templates** へのデータ入力としてテンプレート変数を指定します。詳細と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<ul><li>ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`。</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から構築されます。</li></ul> |
| Templates | **Message Options** セクションと **Notification Options** セクションで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。例：`{{template_name}}` |

* 使用例については、[AndroidConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidconfig)のドキュメントを参照してください。

* ネストされたオブジェクトをサポートするには、**Templates** セクションを使用してテンプレートを定義します。テンプレート名を対応する二重波括弧で参照し、**Custom Text** オプションを使用してテンプレートをマッピングする必要があります：`{{template_name}}`

### Web アプリへのメッセージ送信
#### パラメーター


<blockquote>
メッセージの送信先を指定するには、次のパラメーターのうち、**いずれか1つのみ**を構成します：`Token`、`Topic`、または `Condition`。
</blockquote>


| **パラメーター** | **説明** |
| --- | --- |
| Token | メッセージの送信先となる登録トークン。 |
| Topic | メッセージの送信先となる、購読済みのトピック名。例：`weather`。注：`/topics/` プレフィックスは含めないでください。 |
| Condition | メッセージの送信先となる、購読済みトピックの条件。例：`foo in topics && bar in topics`。 |
| Analytics Label | メッセージの分析データに関連付けられるラベル。 |
| Link | ユーザーが通知をクリックしたときに開くセキュアリンク。値は `https://` で始まる必要があります。 |
| Action | 通知に表示するユーザーアクションを識別する文字列。 |
| Action Title | ユーザーに表示するアクションテキストを含む文字列。 |
| Action Icon | アクションとともに表示するアイコンのURLを含む文字列。 |
| Badge | 通知自体を表示するための十分なスペースがない場合に、通知を表すために使用される画像のURL。 |
| Title | 通知のタイトル。 |
| Body | 通知の本文文字列。 |
| Data | 通知データの構造化クローンを返します。このオプションはテンプレートをサポートします。 |
| Direction | 通知のテキスト方向。 |
| Icon | 通知のアイコンとして使用する画像のURL。 |
| Image | 通知の一部として表示する画像のURL。 |
| Language | 通知の言語コード。 |
| Renotify | 新しい通知が古い通知を置き換えた後に、ユーザーへ再通知するかどうかを指定します。 |
| Require Interaction | 通知を自動的に閉じるのではなく、ユーザーがクリックまたは閉じるまでアクティブな状態にするかどうかを示すブール値。 |
| Silent | 通知をサイレントにするかどうかを指定します。このパラメーターを `true` に構成すると、デバイスの構成に関係なく、音や振動は発生しません。 |
| Tag | 通知のID。 |
| Timestamp | 通知が作成された時刻、または通知が適用される時刻（過去、現在、未来）を指定します。 |
| Vibrate | 振動機能を備えたデバイスで発生させる振動パターンを指定します。秒単位の期間で、小数点以下最大9桁まで指定でき、末尾に `s` を付けます。例：`3.5s`。[Firebaseリソース：Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification)を参照してください。 |
| Data | ユーザー指定のデータ。形式は `"key" : "value"` のペアです。 |
| Headers | Web Pushプロトコルで定義されたHTTPヘッダー。サポートされているヘッダーについては、[Web Pushプロトコル](https://www.rfc-editor.org/rfc/rfc8030#section-5)を参照してください。例：`"TTL": "15"`。詳細については、[Firebaseリソース：Message](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#Notification)を参照してください。 |
| Template Variables | **Templates** のデータ入力としてテンプレート変数を指定します。詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<ul><li>ネストされたテンプレート変数には、ドット表記で名前を付けます。例：`items.name`。</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</li></ul> |
| Templates | **Message Options** セクションおよび **Notification Options** セクションで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。例：`{{template_name}}` |

* 使用例については、[AndroidConfig](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#androidconfig)のドキュメントを参照してください。

* ネストされたオブジェクトをサポートするには、**Templates** セクションを使用してテンプレートを定義します。テンプレートは、名前を対応する二重波括弧で参照し、**Custom Text** オプションを使用してマッピングする必要があります：`{{template_name}}`。</li></ul>