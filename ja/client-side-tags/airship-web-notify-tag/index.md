---
title: Airship Web Notifyタグ構成ガイド
description: この記事では、タグ管理アカウントでAirship Web Notifyタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/airship-web-notify-tag/
---Webプッシュ通知を使用すると、ユーザーがオンライン上のどこにいても、その場に応じた関連性の高いパーソナライズされたメッセージを配信できます。AirshipのWeb Notifyは、強力なエンゲージメント戦略によって新しいWeb訪問にアプローチし、再訪問を促してコンバージョンを向上させるために必要なツールを提供します。

## タグに関するヒント

* すべてのタグ構成は、マッピングを使用して動的に構成できます。
* `secureIframeUrl`は、Airship Web Notifyをセキュアでないページに読み込む場合にのみ必要です。
* Safariをサポートするには、[Airshipダッシュボード](https://docs.urbanairship.com/tutorials/getting-started/channels/web-notify/#safari)で追加構成が必要です。
* Safariの構成後、新しいキーとトークンを含む新しいSDKバンドルをダウンロードしてください。
* 次のEコマース拡張パラメータをサポートしています。
  * 注文ID（\_corder）
  * 注文小計（\_csubtotal）
  * 商品IDのリスト（\_cprod）
  * ブランドのリスト（\_cbrand）
  * カテゴリのリスト（\_ccat）

## タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **appKey**：Airshipから提供されたappKeyです。このWebサイトが接続されているAirshipプロジェクトを識別します。
* **Token**：Airshipから提供されたトークンです。これは、Urban AirshipのプラットフォームAPIに対してJS SDKが実行するアクションを認証するためのBearerトークンです。
* **vapidPublicKey**：Airshipから提供された`vapidPublicKey`です。これは、通知の登録および送信時にブラウザとブラウザベンダーが使用する暗号鍵ペアの公開鍵です。
* **secureIframeUrl**：SDKが親ウィンドウにメッセージを送信できるように、AirshipがHTTPSではないページで使用するiframeのURLです。セキュアでないドメインでのみ使用されます。
* **Auto Prompt Enabled**：プッシュ通知への登録をユーザーに自動的に求めるには、trueを選択します。これにより、訪問にプロンプトを表示する頻度がpush-worker.jsファイルによって処理されます。falseを選択した場合は、プロンプトを手動でトリガーする必要があります。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### タグ構成

|変数| 説明|
|---| ---|
|appKey (app\_key)| [string]|
|vapidPublicKey (vapid\_public\_key)| [string]|
|Token (token)| [string]|
|secureIframeUrl (secure\_iframe\_url)| [string]|
|自動プロンプトフラグ (auto\_prompt)| ["true"/"false"]|

### Eコマース

|変数| 説明|
|---| ---|
|新規アイテムかどうか (is\_new\_item)| ["true"/"false"]|
|商品ブランドのリスト (product\_brand)（\_cbrandを上書き）| [Array]|
|商品カテゴリのリスト (product\_category)（\_ccatを上書き）| [Array]|
|商品説明のリスト (product\_description)| [Array]|
|商品IDのリスト (product\_id)（\_cprodを上書き）| [Array]|
|トランザクション／注文ID (transaction\_id)（\_corderを上書き）| [String]|
|金額／注文小計 (value)（\_csubtotalを上書き）| [String]|

### メディア

|変数| 説明|
|---| ---|
|作成者 (media\_author)| [String]|
|カテゴリ (media\_category)| [String]|
|説明 (media\_description)| [String]|
|注目コンテンツ (media\_feature)| ["true"/"false"]|
|識別子 (media\_identifier)| [String]|
|公開日 (media\_published\_date)| [String]|
|タイプ (media\_type)| [String]|

### ソーシャルメディア

|変数| 説明|
|---| ---|
|ソース (source)| [String]|
|メディア (medium)| [String]|

### アカウント

|変数| 説明|
|---| ---|
|カテゴリ (account\_category)| [String]|

### イベント

|変数| 説明|
|---| ---|
|register| register|
|BrowsedContentEvent| BrowsedContentEvent|
|ConsumedContentEvent| ConsumedContentEvent|
|SharedContentEvent| SharedContentEvent|
|StarredContentEvent| StarredContentEvent|
|AddedToCartEvent| AddedToCartEvent|
|BrowsedEvent| BrowsedEvent|
|PurchasedEvent| PurchasedEvent|
|SharedProductEvent| SharedProductEvent|
|StarredProductEvent| StarredProductEvent|
|RegisterEvent| RegisterEvent|
|Custom| Custom|