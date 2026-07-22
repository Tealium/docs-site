---
title: Genesysチャットウィジェットタグガイド
description: この記事では、Tealium iQタグ管理アカウントでGenesysチャットウィジェットタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/genesys-chat-widget-tag/
---## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きしたり、カスタムユーザーデータを送信したり、オブジェクトや関数をマップします。
* 関数の内容はJavaScript拡張で構成できます。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **バージョン**
  * ロードするウィジェットのバージョン。
  * 例：9.0
* **地域**
  * あなたが位置している場所に基づいて最も近いまたは適切な地域を選択します。
* **テーマ**
  * 'themes'オブジェクトからGenesysウィジェットに適用するテーマを選択します。
  * テーマのプロパティ名を使用します。
* **言語**
  * 'i18n'言語パックから使用する言語を選択します。
  * 言語コードは顧客によって選択されます。
  * このプロパティがあなたのi18n言語パックの言語コードのいずれかと一致する限り、任意の言語コード形式を使用できます。
* **モバイルモード**
  * 値は**true**、**false**、または**auto**です。
    * **true**の値は、すべてのデバイスでモバイルモードを強制します。
    * **false**の値は、モバイルモードを完全に無効にします。
    * 自動（**auto**）値を使用すると、Genesysウィジェットは'モバイルモードブレークポイント'プロパティとUserAgent検出を使用してモバイルモードとデスクトップモードを自動的に切り替えます。
* **時間形式**
  * タイムスタンプの時間形式を構成します。
  * 値は**12**または**24**です。
* **モバイルモードブレークポイント**
  * Genesysウィジェットがモバイルモードに切り替えるピクセル単位のブレークポイント幅。
* **カスタムスタイルシートID**
  * CSSの上書き、カスタムテーマ、またはGenesysウィジェット用のその他のカスタムCSSを含む`<style>`タグのHTML ID。
* **Googleフォントのダウンロード**
  * デフォルトでは、GenesysウィジェットはGoogleフォント'Roboto'をダウンロードして使用します。
  * 値は**true**または**false**です。
  * **true**の値はGoogleフォントRobotoをダウンロードして使用します。
  * このダウンロードを無効にするには、この値を**false**に構成します。
* **デプロイメントID**
  * 複数のウィジェットデプロイメントが同じドメインで実行できるように、クッキー名をカスタマイズするために使用される文字列。
* **APIキー**
  * Apigee Proxyセキュアトークン。
* **エンドポイント**
  * チャットを開始するエンドポイントを手動で入力します。
* **データURL**
  * GMS RESTチャットサービスのURL。
  * 値は**true**または**false**です。
  * CometDが有効になっていない場合は必要です。
  * `CometD Enabled`が**true**に構成されている場合、このプロパティは無視されます。
* **カスタムヘッダーの有効化**
  * `_genesys.widgets.main.header`静的構成で定義されたカスタム認証ヘッダーの使用を有効にします。
  * すべてのWebChatServiceリクエストにカスタム認証ヘッダーを添付します。
* **CometDの有効化**
  * CometD接続方法の有効化または無効化。
  * 値は**true**または**false**です。
  * **false**に構成されているか、未定義の場合、WebChatServiceは指定された`dataURL`を通じてRESTサービスに接続します。
* **CometD Comet URL**
  * GMS CometD接続のURL。
  * 値は**true**または**false**です。
  * `CometD Enabled`は`WebChatService`がこのサービスに接続するために**true**に構成する必要があります。
* **CometDチャンネル**
  * チャットメッセージを受信するためのCometDチャンネル。
* **CometD API URL**
  * ファイルのアップロードとダウンロードなど、追加のCometDサービスのURL。
* **CometD Websocketの有効化**
  * 値は**true**または**false**です。
    * **true**に構成されている場合、CometDはwebsocketsを通じて接続を試みます。
    * **false**に構成されている場合、CometDは長いポーリングのみを使用します。
  * CometDは、websocketsを介して接続できない場合、長いポーリングにフォールバックします。
* **非同期の有効化**
  * チャットセッションが無期限にアクティブになる非同期チャットを有効にします。
* **Ajaxタイムアウト**
  * AJAXタイムアウト前に待つミリ秒数。
* **ポーリング例外制限**
  * WebChatServiceが`chatServerWentOffline`を公開する前の連続したポーリング例外（チャットサーバーオフライン）の数。
* **復元タイムアウト**
  * 復元タイムアウト前のミリ秒数。
  * セッションから一定時間離れた後にチャットセッションの復元を防ぎます
  * 例：ユーザーがチャット中に別のサイトに移動し、セッションを終了しなかった。
* **絵文字**
  * 絵文字メニューを有効にします。
* **アップロードの有効化**
  * ファイル送信ボタンを表示します。
* **フォームクローズ確認の有効化**
  * 登録フォームに情報が入力されている場合、WebChatを閉じる前に確認メッセージを表示する機能を有効にします。
* **アクションメニュー**
  * チャットメッセージ入力の隣にアクションメニューを有効にします。
* **最大メッセージ長**
  * ユーザーがチャット中にメッセージエリアに入力できる文字数の制限を構成します。
  * 最大メッセージ長に達すると、ユーザーはこれ以上入力できません。
* **文字数カウントの有効化**：
  * ユーザーが入力中に、入力メッセージエリアに残っている文字数を表示します。
* **自動招待の有効化**
  * 自動招待機能を有効にします。
  * ユーザーがページ上で一定時間アイドル状態になった後、自動的にユーザーをチャットに招待します。
* **招待までの時間（秒）**
  * 顧客をチャットに招待するまでのアイドル時間（秒）。
* **タイムアウト秒数**
  * 招待を表示した後、チャット招待を閉じるまでの待ち時間（秒）。
* **チャットボタンの有効化**
  * 画面上のチャットボタンを有効にします。
* **チャットボタン表示遅延**
  * 画面上にチャットボタンを表示するまでのミリ秒数。
* **チャットボタンエフェクト期間**
  * アニメーション効果の長さ（ミリ秒）。
* **招待中にチャットボタンを非表示**
  * 自動招待機能が有効化されたとき、チャットボタンを非表示にします。
  * 招待が却下されたとき、再度チャットボタンを表示します。
* **モバイル復元時の最小化**
  * チャット復元時のwebchatの最小化状態の有効化/無効化。
  * このオプションはモバイルモードのみに適用されます。
* **マークダウンの有効化**
  * チャットメッセージのマークダウン機能の有効化/無効化。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からのデータをベンダータグの対応する宛先変数に送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### メイン

|変数| 説明|
|---| ---|
|テーマ (main.themes)| [オブジェクト]|
|テーマ (main.theme)| [文字列]|
|言語 (main.lang)| [文字列]|
|i18n (main.i18n)| [URL文字列またはJSON]|
|ヘッダー (main.header)| [オブジェクト]|
|プリロード (main.preload)| [配列]|
|モバイルモード (main.mobileMode)| [ブール値/文字列]|
|時間形式 (main.timeFormat)| [数値/文字列]|
|モバイルモードブレークポイント (main.mobileModeBreakpoint)| [数値]|
|デバッグ (main.debug)| [ブール値]|
|カスタムスタイルシートID (main.customStylesheetID)| [文字列]|
|Googleフォントのダウンロード (main.downloadGoogleFont)| [ブール値]|
|デプロイメントID (main.deploymentID)| [文字列]|
|クッキーオプション (main.cookieOptions)| [オブジェクト]|
|onReady (mainonReady)| [関数]|
|スクリプトURL (script\_url)| [文字列]|
|CSS URL (css\_url)| [文字列]|

### Webchatサービス

|変数| 説明|
|---| ---|
|テーマ (main.themes)| [オブジェクト]|
|APIキー (webchat.apikey)| [文字列]|
|エンドポイント (webchat.endpoint)| [文字列]|
|データURL (webchat.dataURL)| [文字列]|
|カスタムヘッダーの有効化 (webchat.enableCustomHeader)| [ブール値]|
|CometD (webchat.cometD)| [オブジェクト]|
|CometDの有効化 (webchat.cometD.enabled)| [ブール値]|
|CometD Comet URL (webchat.cometD.cometURL)| [文字列]|
|CometDチャンネル (webchat.cometD.channel)| [文字列]|
|CometD API URL (webchat.cometD.apiURL)| [文字列]|
|CometD Websocketの有効化 (webchat.cometD.websocketEnabled)| [ブール値]|
|CometDログレベル (webchat.cometD.logLevel)| [文字列]|
|ユーザーデータ (webchat.userData)| [オブジェクト]|
|Ajaxタイムアウト (webchat.ajaxTimeout)| [数値]|
|XhrFields (webchat.xhrFields)| [オブジェクト]|
|ポーリング例外制限 (webchat.pollExceptionLimit)| [数値]|
|復元タイムアウト (webchat.restoreTimeout)| [数値]|
|非同期 (webchat.async)| [オブジェクト]|
|非同期の有効化 (webchat.async.enabled)| [ブール値]|
|新しいメッセージ復元状態 (webchat.async.newMessageRestoreState)| [文字列]|
|getSessionData (webchat.async.getSessionData)| [関数]|
|setSessionData (webchat.async.setSessionData)| [関数]|

### Webchat UI

|変数| 説明|
|---| ---|
|絵文字 (webchat.emojis)| [ブール値]|
|フォーム (webchat.form)| [オブジェクト]|
|アップロードの有効化 (webchat.uploadsEnabled)| [ブール値]|
|フォームクローズ確認の有効化 (webchat.confirmFormCloseEnabled)| [ブール値]|
|アクションメニュー (webchat.actionsMenu)| [ブール値]|
|最大メッセージ長 (webchat.maxMessageLength)| [数値]|
|文字数カウントの有効化 (webchat.charCountEnabled)| [ブール値]|
|自動招待の有効化 (webchat.autoInvite.enabled)| [ブール値]|
|招待までの時間（秒） (webchat.autoInvite.timeToInviteSeconds)| [数値]|
|タイムアウト秒数 (webchat.autoInvite.inviteTimeoutSeconds)| [数値]|
|チャットボタンの有効化 (webchat.chatButton.enabled)| [ブール値]|
|チャットボタンテンプレート (webchat.chatButton.template)| [文字列]|
|チャットボタンエフェクト (webchat.chatButton.effect)| [文字列]|
|チャットボタン表示遅延 (webchat.chatButton.openDelay)| [数値]|
|チャットボタンエフェクト期間 (webchat.chatButton.effectDuration)| [数値]|
|モバイル復元時の最小化 (webchat.minimizeOnMobileRestore)| [ブール値]|
|マークダウンの有効化 (webchat.markdown)| [ブール値]|


