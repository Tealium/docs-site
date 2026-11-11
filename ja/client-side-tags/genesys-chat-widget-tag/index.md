---
title: Genesys Chat Widgetタグガイド
description: この記事では、タグ管理アカウントでGenesys Chat Widgetタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/genesys-chat-widget-tag/
---## タグに関するヒント

* マッピングを使用すると、標準構成値を動的に上書きしたり、カスタムユーザーデータを送信したり、オブジェクトや関数をマッピングしたりできます。
* 関数の内容はJavaScript拡張機能で構成できます。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **バージョン**
  * 読み込むウィジェットのバージョン。
  * 例：9.0
* **リージョン**
  * 現在地に基づいて、最も近いリージョンまたは適切なリージョンを選択します。
* **テーマ**
  * 「themes」オブジェクトから、Genesys Widgetsに適用するテーマを選択します。
  * テーマのプロパティ名を使用します。
* **言語**
  * 「i18n」言語パックから、使用する言語を選択します。
  * 言語コードは顧客が選択します。
  * このプロパティがi18n言語パック内のいずれかの言語コードと一致していれば、任意の言語コード形式を使用できます。
* **モバイルモード**
  * 値は**true**、**false**、または**auto**です。
    * **true**を指定すると、すべてのデバイスでモバイルモードが強制的に有効になります。
    * **false**を指定すると、モバイルモードが完全に無効になります。
    * 自動（**auto**）値を使用すると、Genesys Widgetsは「Mobile Mode Breakpoint」プロパティとUserAgent検出を使用して、モバイルモードとデスクトップモードを自動的に切り替えます。
* **時刻形式**
  * タイムスタンプの時刻形式を構成します。
  * 値は**12**または**24**です。
* **モバイルモードのブレークポイント**
  * Genesys Widgetsがモバイルモードに切り替わるブレークポイントの幅（ピクセル単位）。
* **カスタムスタイルシートID**
  * Genesys Widgets向けのCSSオーバーライド、カスタムテーマ、またはその他のカスタムCSSを含む`<style>`タグのHTML ID。
* **Googleフォントのダウンロード**
  * デフォルトでは、Genesys WidgetsはGoogleフォントの「Roboto」をダウンロードして使用します。
  * 値は**true**または**false**です。
  * **true**を指定すると、GoogleフォントのRobotoがダウンロードされ、使用されます。
  * このダウンロードを無効にするには、この値を**false**に構成します。
* **デプロイメントID**
  * 同じドメインで複数のウィジェットデプロイメントを実行できるように、Cookie名をカスタマイズするために使用する文字列。
* **APIキー**
  * Apigee Proxyのセキュアトークン。
* **エンドポイント**
  * チャットを開始するエンドポイントを手動で入力します。
* **データURL**
  * GMS RESTチャットサービスのURL。
  * 値は**true**または**false**です。
  * CometDが有効になっていない場合は必須です。
  * `CometD Enabled`が**true**に構成されている場合、このプロパティは無視されます。
* **カスタムヘッダーの有効化**
  * `_genesys.widgets.main.header`静的構成で定義されたカスタム認証ヘッダーの使用を有効にします。
  * すべてのWebChatServiceリクエストにカスタム認証ヘッダーをエンリッチメントします。
* **CometDの有効化**
  * CometD接続方式を有効または無効にします。
  * 値は**true**または**false**です。
  * **false**に構成するか未定義のままにした場合、WebChatServiceは指定された`dataURL`を介してRESTサービスに接続します。
* **CometD Comet URL**
  * GMS CometD接続のURL。
  * 値は**true**または**false**です。
  * `WebChatService`がこのサービスに接続するには、`CometD Enabled`を**true**に構成する必要があります。
* **CometDチャンネル**
  * チャットメッセージを受信するためのCometDチャンネル。
* **CometD API URL**
  * ファイルのアップロードやダウンロードなど、追加のCometDサービスのURL。
* **CometD WebSocketの有効化**
  * 値は**true**または**false**です。
    * **true**に構成すると、CometDはWebSocket経由での接続を試みます。
    * **false**に構成すると、CometDはロングポーリングのみを使用します。
  * WebSocket経由で接続できない場合、CometDはロングポーリングにフォールバックします。
* **非同期の有効化**
  * チャットセッションを無期限にアクティブにできる非同期チャットを有効にします。
* **Ajaxタイムアウト**
  * AJAXがタイムアウトするまで待機する時間（ミリ秒単位）。
* **ポーリング例外の上限**
  * WebChatServiceが`chatServerWentOffline`を発行するまでに許容する、連続したポーリング例外（チャットサーバーのオフライン）の回数。
* **復元タイムアウト**
  * 復元がタイムアウトするまでの時間（ミリ秒単位）。
  * セッションから一定時間離れた後にチャットセッションが復元されるのを防ぎます。
  * 例：ユーザーがチャット中に別のサイトへ移動し、セッションを終了しなかった場合。
* **絵文字**
  * 絵文字メニューを有効にします。
* **アップロードの有効化**
  * ［ファイルを送信］ボタンを表示します。
* **フォームを閉じる際の確認の有効化**
  * 登録フォームに情報が入力されている場合、WebChatを閉じる前に確認メッセージを表示します。
* **アクションメニュー**
  * チャットメッセージ入力欄の横にあるアクションメニューを有効にします。
* **最大メッセージ長**
  * チャット中にユーザーがメッセージ欄へ入力できる文字数の上限を構成します。
  * メッセージの最大文字数に達すると、ユーザーはそれ以上入力できなくなります。
* **文字数表示の有効化**：
  * ユーザーの入力中に、メッセージ入力欄へ入力できる残りの文字数を表示します。
* **自動招待の有効化**
  * 自動招待機能を有効にします。
  * ユーザーがページ上で事前構成された時間操作しなかった場合、自動的にチャットへ招待します。
* **招待までの秒数**
  * 顧客をチャットへ招待するまでのアイドル時間（秒単位）。
* **タイムアウト秒数**
  * 招待を表示してからチャット招待を閉じるまでの待機時間（秒単位）。
* **チャットボタンの有効化**
  * 画面上のチャットボタンを有効にします。
* **チャットボタン表示遅延**
  * 画面にチャットボタンを表示するまでの時間（ミリ秒単位）。
* **チャットボタンのエフェクト時間**
  * アニメーションエフェクトの長さ（ミリ秒単位）。
* **招待中にチャットボタンを非表示**
  * 自動招待機能が有効になっている場合、チャットボタンを非表示にします。
  * 招待が閉じられると、チャットボタンを再度表示します。
* **モバイルでの復元時に最小化**
  * チャット復元時のWebChatの最小化状態を有効または無効にします。
  * このオプションはモバイルモード専用です。
* **Markdownの有効化**
  * チャットメッセージのMarkdown機能を有効または無効にします。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数へ送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### メイン

|変数|説明|
|---|---|
|テーマ（main.themes）|［オブジェクト］|
|テーマ（main.theme）|［文字列］|
|言語（main.lang）|［文字列］|
|i18n（main.i18n）|［URL文字列またはJSON］|
|ヘッダー（main.header）|［オブジェクト］|
|プリロード（main.preload）|［配列］|
|モバイルモード（main.mobileMode）|［ブール値／文字列］|
|時刻形式（main.timeFormat）|［数値／文字列］|
|モバイルモードのブレークポイント（main.mobileModeBreakpoint）|［数値］|
|デバッグ（main.debug）|［ブール値］|
|カスタムスタイルシートID（main.customStylesheetID）|［文字列］|
|Googleフォントのダウンロード（main.downloadGoogleFont）|［ブール値］|
|デプロイメントID（main.deploymentID）|［文字列］|
|Cookieオプション（main.cookieOptions）|［オブジェクト］|
|onReady（mainonReady）|［関数］|
|スクリプトURL（script\_url）|［文字列］|
|CSS URL（css\_url）|［文字列］|

### Webchatサービス

|変数|説明|
|---|---|
|テーマ（main.themes）|［オブジェクト］|
|APIキー（webchat.apikey）|［文字列］|
|エンドポイント（webchat.endpoint）|［文字列］|
|データURL（webchat.dataURL）|［文字列］|
|カスタムヘッダーの有効化（webchat.enableCustomHeader）|［ブール値］|
|CometD（webchat.cometD）|［オブジェクト］|
|CometD.enabled（webchat.cometD.enabled）|［ブール値］|
|CometD.cometURL（webchat.cometD.cometURL）|［文字列］|
|CometD.channel（webchat.cometD.channel）|［文字列］|
|CometD.apiURL（webchat.cometD.apiURL）|［文字列］|
|CometD.websocketEnabled（webchat.cometD.websocketEnabled）|［ブール値］|
|CometD.logLevel（webchat.cometD.logLevel）|［文字列］|
|UserData（webchat.userData）|［オブジェクト］|
|AjaxTimeout（webchat.ajaxTimeout）|［数値］|
|XhrFields（webchat.xhrFields）|［オブジェクト］|
|PollExceptionLimit（webchat.pollExceptionLimit）|［数値］|
|RestoreTimeout（webchat.restoreTimeout）|［数値］|
|Async（webchat.async）|［オブジェクト］|
|Async.enabled（webchat.async.enabled）|［ブール値］|
|非同期の新規メッセージ復元状態（webchat.async.newMessageRestoreState）|［文字列］|
|Async.getSessionData（webchat.async.getSessionData）|［関数］|
|Async.setSessionData（webchat.async.setSessionData）|［関数］|
### WebチャットUI

|変数|説明|
|---|---|
|絵文字（webchat.emojis）|[Boolean]|
|フォーム（webchat.form）|[Object]|
|アップロードの有効化（webchat.uploadsEnabled）|[Boolean]|
|フォームを閉じる際の確認の有効化（webchat.confirmFormCloseEnabled）|[Boolean]|
|アクションメニュー（webchat.actionsMenu）|[Boolean]|
|メッセージの最大長（webchat.maxMessageLength）|[Number]|
|文字数表示の有効化（webchat.charCountEnabled）|[Boolean]|
|自動招待の有効化（webchat.autoInvite.enabled）|[Boolean]|
|自動招待までの時間（秒）（webchat.autoInvite.timeToInviteSeconds）|[Number]|
|自動招待のタイムアウト（秒）（webchat.autoInvite.inviteTimeoutSeconds）|[Number]|
|チャットボタンの有効化（webchat.chatButton.enabled）|[Boolean]|
|チャットボタンのテンプレート（webchat.chatButton.template）|[String]|
|チャットボタンのエフェクト（webchat.chatButton.effect）|[String]|
|チャットボタンを開くまでの遅延（webchat.chatButton.openDelay）|[Number]|
|チャットボタンのエフェクトの継続時間（webchat.chatButton.effectDuration）|[Number]|
|モバイルでの復元時に最小化（webchat.minimizeOnMobileRestore）|[Boolean]|
|Markdownの有効化（webchat.markdown）|[Boolean]|