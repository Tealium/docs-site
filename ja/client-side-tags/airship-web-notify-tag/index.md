---
title: Airship Web Notifyタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAirship Web Notifyタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/airship-web-notify-tag/
---Webプッシュ通知を使用すると、ユーザーがオンラインである場所で関連性のある、パーソナライズされた、その瞬間のメッセージを配信することができます。AirshipのWeb Notifyは、新しいWeb訪問に強力なエンゲージメント戦略でアプローチし、再訪問を促し、コンバージョンを促進するための必要なツールを提供します。

## タグのヒント

* タグの構成はすべてマッピングを介して動的に構成できます。
* `secureIframeUrl`は、Airship Web Notifyが非セキュアページでロードされる場合にのみ必要です。
* Safariのサポートは、[あなたのAirshipダッシュボード](https://docs.urbanairship.com/tutorials/getting-started/channels/web-notify/#safari)内で追加の構成が必要です。
* Safariの構成後は、新しいキーとトークンが含まれた新しいSDKバンドルをダウンロードすることを確認してください。
* 以下のE-Commerce拡張パラメータをサポートしています：
  * 注文ID (\_corder)
  * 注文小計 (\_csubtotal)
  * 製品IDのリスト (\_cprod)
  * ブランドのリスト (\_cbrand)
  * カテゴリのリスト (\_ccat)

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグ概要]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **appKey**: Airshipが提供するappKey。これにより、このウェブサイトがどのAirshipプロジェクトに接続されているかが識別されます。
* **Token**: Airshipが提供するトークン。これは、JS SDKがUrban AirshipのプラットフォームAPIに対して行うアクションを認証するベアラートークンです。
* **vapidPublicKey**: Airshipが提供する`vapidPublicKey`。これは、ブラウザとブラウザベンダが通知の登録と送信時に使用する暗号化キーペアの公開側です。
* **secureIframeUrl**: Airshipが非HTTPSページで使用するiframeのURLで、SDKが親ウィンドウにメッセージを投稿できるようにします。これは非セキュアドメインでのみ使用されます。
* **Auto Prompt Enabled**: trueを選択すると、ユーザーに自動的にプッシュ通知の登録を促すプロンプトが表示され、push-worker.jsファイルが訪問に対するプロンプトの頻度を処理します。falseを選択した場合、プロンプトを手動でトリガーする必要があります。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### タグ構成

|変数| 説明|
|---| ---|
|appKey (app\_key)| [文字列]|
|vapidPublicKey (vapid\_public\_key)| [文字列]|
|Token (token)| [文字列]|
|secureIframeUrl (secure\_iframe\_url)| [文字列]|
|Auto Prompt Flag (auto\_prompt)| [&#34;true&#34;/&#34;false&#34;]|

### E-Commerce

|変数| 説明|
|---| ---|
|Is New Item (is\_new\_item)| [&#34;true&#34;/&#34;false&#34;]|
|List of Product Brands (product\_brand) (Overrides \_cbrand)| [配列]|
|List of Product Categories (product\_category) (Overrides \_ccat)| [配列]|
|List of Product Descriptions (product\_description)| [配列]|
|List of Product IDs (product\_id) (Overrides \_cprod)| [配列]|
|Transaction/Order ID (transaction\_id) (Overrides \_corder)| [文字列]|
|Value/Order Subtotal (value) (Overrides \_csubtotal)| [文字列]|

### メディア

|変数| 説明|
|---| ---|
|Author (media\_author)| [文字列]|
|Category (media\_category)| [文字列]|
|Description (media\_description)| [文字列]|
|Feature (media\_feature)| [&#34;true&#34;/&#34;false&#34;]|
|Identifier (media\_identifier)| [文字列]|
|Published Date (media\_published\_date)| [文字列]|
|Type (media\_type)| [文字列]|

### ソーシャルメディア

|変数| 説明|
|---| ---|
|Source (source)| [文字列]|
|Medium (medium)| [文字列]|

### アカウント

|変数| 説明|
|---| ---|
|Category (account\_category)| [文字列]|

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


