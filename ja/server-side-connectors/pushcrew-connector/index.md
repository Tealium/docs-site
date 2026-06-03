---
title: PushCrewコネクタ構成ガイド
description: PushCrewは、マーケターが自分のウェブサイト内から購読者にプッシュ通知を送るためのプラットフォームを提供します。
url: https://docs.tealium.com/ja/server-side-connectors/pushcrew-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|購読者をセグメントに追加| ✓| ✓|
|購読者をセグメントから削除| ✓| ✓|
|購読者に通知を送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIトークン**
  * 各APIリクエストは、リクエストヘッダーの認証トークンによって認証されます。
  * 認証トークンを取得するには、[info@pushcrew.com](mailto:info@pushcrew.com)にメールを送信します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 購読者をセグメントに追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|セグメントID|  &lt;ul&gt;&lt;li&gt;購読者を追加するセグメントのID。&lt;/li&gt;&lt;li&gt;詳細については、[購読者をセグメントに追加](https://api.pushcrew.com/docs/add-subscribers-to-a-segment)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|購読者ID|  &lt;ul&gt;&lt;li&gt;セグメントに追加する購読者のID。&lt;/li&gt;&lt;li&gt;購読者IDは、PushCrewのクッキーから構成するか、PushCrewのJavaScript APIを使用して構成できます。&lt;/li&gt;&lt;li&gt;詳細については、[現在のユーザーの購読者IDを取得](https://api.pushcrew.com/docs/get-subscriberid-of-current-user)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 購読者をセグメントから削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|セグメントID|  &lt;ul&gt;&lt;li&gt;購読者を削除するセグメントのID。&lt;/li&gt;&lt;li&gt;詳細については、[購読者をセグメントから削除](https://api.pushcrew.com/docs/remove-subscribers-from-a-segment)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|購読者ID|  &lt;ul&gt;&lt;li&gt;セグメントから削除する購読者のID。&lt;/li&gt;&lt;li&gt;購読者IDは、PushCrewのクッキーから構成するか、PushCrewのJavaScript APIを使用して構成できます。&lt;/li&gt;&lt;li&gt;詳細については、[現在のユーザーの購読者IDを取得](https://api.pushcrew.com/docs/get-subscriberid-of-current-user)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 購読者に通知を送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|タイトル|  &lt;ul&gt;&lt;li&gt;プッシュ通知のタイトル。&lt;/li&gt;&lt;li&gt;最大35文字。&lt;/li&gt;&lt;li&gt;詳細については、[個々の購読者に送信](https://api.pushcrew.com/docs/send-to-an-individual-subscriber)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|メッセージ|  &lt;ul&gt;&lt;li&gt;プッシュ通知に表示するメッセージ。&lt;/li&gt;&lt;li&gt;最大80文字。&lt;/li&gt;&lt;/ul&gt; |
|URL| プッシュ通知をクリックしたときに開くURL。|
|購読者ID| 購読者の購読者ID。|
|画像URL|  &lt;ul&gt;&lt;li&gt;通知に表示するアイコンのURL。&lt;/li&gt;&lt;li&gt;URLはHTTPを使用し、192x192のPNGファイルを指す必要があります。これが提供されていない場合、デフォルトの会社ロゴが通知に表示されます。&lt;/li&gt;&lt;/ul&gt; |
|ヒーロー画像URL|  &lt;ul&gt;&lt;li&gt;通知に表示するヒーロー画像のURL。&lt;/li&gt;&lt;li&gt;URLはHTTPSを使用し、画像ファイルを指す必要があります。&lt;/li&gt;&lt;li&gt;この機能はビジネスアカウントとエンタープライズアカウントでのみ使用できます。&lt;/li&gt;&lt;/ul&gt; 注：Chromeの購読者のみ対応。Mozilla Firefoxはまだサポートしていません。|
|ボタン1のラベル|  &lt;ul&gt;&lt;li&gt;これは、通知に表示される最初のコールトゥアクションボタンのラベルです。&lt;/li&gt;&lt;li&gt;このパラメータの最大長は12文字です。&lt;/li&gt;&lt;li&gt;この機能はビジネスアカウントとエンタープライズアカウントでのみ使用できます。&lt;/li&gt;&lt;/ul&gt; 注：Chromeの購読者のみ対応。Mozilla Firefoxはまだサポートしていません。|
|ボタン1のURL|  &lt;ul&gt;&lt;li&gt;これは、通知に表示される最初のコールトゥアクションボタンをクリックしたときに開くURLです。&lt;/li&gt;&lt;li&gt;この機能はビジネスアカウントとエンタープライズアカウントでのみ使用できます。&lt;/li&gt;&lt;/ul&gt; 注：Chromeの購読者のみ対応。Mozilla Firefoxはまだサポートしていません。 |
|ボタン2のラベル|  &lt;ul&gt;&lt;li&gt;これは、通知に表示される2つ目のコールトゥアクションボタンのラベルです。&lt;/li&gt;&lt;li&gt;このパラメータの最大長は12文字です。&lt;/li&gt;&lt;li&gt;この機能はビジネスアカウントとエンタープライズアカウントでのみ使用できます。&lt;/li&gt;&lt;/ul&gt; 注：Chromeの購読者のみ対応。Mozilla Firefoxはまだサポートしていません。 |
|ボタン2のURL|  &lt;ul&gt;&lt;li&gt;これは、通知に表示される2つ目のコールトゥアクションボタンをクリックしたときに開くURLです。&lt;/li&gt;&lt;li&gt;この機能はビジネスアカウントとエンタープライズアカウントでのみ使用できます。&lt;/li&gt;&lt;/ul&gt; 注：Chromeの購読者のみ対応。Mozilla Firefoxはまだサポートしていません。 |
|生存時間|  &lt;ul&gt;&lt;li&gt;整数属性タイプでなければなりません。&lt;/li&gt;&lt;li&gt;このパラメータは、購読者がオフラインの場合に通知を試行する時間を制御するために使用されます。&lt;/li&gt;&lt;li&gt;通知を送信しないようにするために経過した秒数を渡します。&lt;/li&gt;&lt;li&gt;デフォルト値（`2419200`）は4週間を表します。&lt;/li&gt;&lt;/ul&gt; |
|通知の自動非表示|  &lt;ul&gt;&lt;li&gt;整数属性タイプでなければなりません。  &lt;ul&gt;&lt;li&gt;数字の`1`は、通知がクリックされたり閉じられたりするまで画面に表示され続けることを示します。&lt;/li&gt;&lt;li&gt;ゼロ`0`は、通知が20秒間クリックされたり閉じられたりしない場合に自動的に非表示になることを示します。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
