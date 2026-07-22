---
title: Genesys Webメッセージングタグ構成ガイド
description: この記事では、Genesys Webメッセージングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/genesys-web-messaging-tag/
---
Genesys Webメッセージングは、お客様がウェブサイト上でボットやエージェントと会話できる機能を提供します。非同期会話、受信および送信の画像添付、すべてのGenesys Cloudメッセージングチャネルにわたる統一されたエージェントおよびスーパーバイザーの経験など、ウェブチャットに比べていくつかの利点があります。

## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **Deployment ID**：  
ユーザーによって提供されるGenesys識別子。
* **Environment**：  
タグがデプロイされる環境。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `deploymentId` | 文字列 | デプロイメントID。 |
| `environment` | 文字列 | 環境。 |
| `debug` | ブール値   | デバッグ。 |
| `base_url` | 文字列 | ベースURL。 |

### 認証

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `authCode` | 文字列 | 認証コード。 |
| `redirectUri` | 文字列 | 構成されたリダイレクションURI。 |
| `nonce` | 文字列 | ランダム文字列、できればUUID。 |
| `maxAge` | 文字列 | 経過時間（秒）。 |
| `codeVerifier` | 文字列 | PKCEフローのコード検証器。 |
| `iss` | 文字列 | 発行者。 |

### データベースパラメータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `customAttributes` | オブジェクト  | カスタム属性。 |
| `name` | 文字列 | 取得したいオブジェクトプロパティの名前。 |

### コブラウズサービスパラメータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `joinCode` | 文字列 | 参加コード。 |
| `sessionId` | 文字列 | セッションID。 |

### エンゲージメントパラメータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `engageContent` | オブジェクト  | エンゲージコンテンツ。 |
| `engageContent.offerText` | 文字列 | エンゲージコンテンツのオファーテキスト。 |

### ジャーニーパラメータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `pageTitle` | 文字列 | ページタイトル。 |
| `pageLocation` | 文字列 | ページの場所。 |
| `customAttributes` | オブジェクト  | カスタム属性。 |
| `traitsMapper` | オブジェクトの配列 | トレイトマッパー。 |
| `eventName` | 文字列 | HTML要素がクリックされたときに投稿するイベントの名前。 |
| `selector` | 文字列 | トラックするCSSセレクタ。 |
| `formName` | 文字列 | フォーム名。 |
| `captureFormDataOnAbandon` | ブール値   | フォームが放棄されたときにフォームデータをキャプチャするかどうかを示します。 |
| `captureFormDataOnSubmit` | ブール値   | フォームが提出されたときにフォームデータをキャプチャするかどうかを示します。|
| `clickEvents.selector` | 配列    | クリックイベントセレクタ。 |
| `clickEvents.eventName` | 配列    | クリックイベントのイベント名。 |
| `clickEvents.customAttributes` | 配列    | クリックイベントのカスタム属性。 |
| `idleEvents.idleAfterSeconds` | 配列    | ユーザーの非活動状態を待つ秒数。 |
| `idleEvents.eventName` | 配列    | アイドルイベントのイベント名。 |
| `idleEvents.customAttributes` | 配列    | アイドルイベントのカスタム属性。 |
| `inViewportEvents.selector` | 文字列 | ビューポートイベントセレクタ。 |
| `inViewportEvents.eventName` | 文字列 | ビューポートイベントのイベント名。 |
| `inViewportEvents.customAttributes` | オブジェクト  | ビューポートイベントのカスタム属性。 |
| `scrollDepthEvents.percentage` | 数値 | スクロール深度イベントのパーセンテージ。 |
| `scrollDepthEvents.eventName` | 文字列 | スクロール深度イベントのイベント名。 |
| `scrollDepthEvents.customAttributes` | オブジェクト  | スクロール深度イベントのカスタム属性。 |
| `actionId` | 文字列 | アクションID。 |
| `actionState` | 文字列 | アクション状態。 |
| `errorCode` | 文字列 | エラーコード。 |
| `errorReason` | 文字列 | エラー理由。 |

### メッセージングサービスパラメータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `message` | 文字列 | 送信するテキストメッセージ。 |

### トースターパラメータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `title` | 文字列 | トーストメッセージのタイトル。 |
| `body` | 文字列 | トーストメッセージの本文。 |
| `buttons.type` | 文字列 | トーストメッセージ内のボタンのタイプ。`unary`は1つのボタン、`two`は2つのボタンの値が受け入れられます。 |
| `buttons.primary` | 文字列 | トーストメッセージのプライマリボタンのテキスト。デフォルト値は`Accept`です。 |
| `buttons.secondary` | 文字列 | トーストメッセージのセカンダリボタンのテキスト。デフォルト値は`Accept`です。 |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `authCode` | 認証コード。 |
| `redirectUri` | 構成されたリダイレクションURI。 |
| `nonce` | ランダム文字列、できればUUID。 |
| `maxAge` | 経過時間（秒）。 |
| `codeVerifier` | PKCEフローのコード検証器。 |
| `iss` | 発行者。 |
| `customAttributes` | カスタム属性。 |
| `name` | 取得したいオブジェクトプロパティの名前。 |
| `joinCode` | 参加コード。 |
| `sessionId` | セッションID。 |
| `engageContent` | エンゲージコンテンツ。 |
| `engageContent.offerText` | エンゲージコンテンツのオファーテキスト。 |
| `pageTitle` | ページタイトル。 |
| `pageLocation` | ページの場所。 |
| `customAttributes` | カスタム属性。 |
| `traitsMapper` | トレイトマッパー。 |
| `eventName` | HTML要素がクリックされたときに投稿するイベントの名前。 |
| `selector` | トラックするCSSセレクタ。 |
| `formName` | フォーム名。 |
| `captureFormDataOnAbandon` | フォームが放棄されたときにフォームデータをキャプチャするかどうかを示します。 |
| `captureFormDataOnSubmit` | フォームが提出されたときにフォームデータをキャプチャするかどうかを示します。 |
| `clickEvents.selector` | クリックイベントセレクタ。 |
| `clickEvents.eventName` | クリックイベントのイベント名。 |
| `clickEvents.customAttributes` | クリックイベントのカスタム属性。 |
| `idleEvents.idleAfterSeconds` | ユーザーの非活動状態を待つ秒数。 |
| `idleEvents.eventName` | アイドルイベントのイベント名。 |
| `idleEvents.customAttributes` | アイドルイベントのカスタム属性。 |
| `inViewportEvents.selector` | ビューポートイベントセレクタ。 |
| `inViewportEvents.eventName` | ビューポートイベントのイベント名。 |
| `inViewportEvents.customAttributes` | ビューポートイベントのカスタム属性。 |
| `scrollDepthEvents.percentage` | スクロール深度イベントのパーセンテージ。 |
| `scrollDepthEvents.eventName` | スクロール深度イベントのイベント名。 |
| `scrollDepthEvents.customAttributes` | スクロール深度イベントのカスタム属性。 |
| `actionId` | アクションID。 |
| `actionState` | アクション状態。 |
| `errorCode` | エラーコード。 |
| `errorReason` | エラー理由。 |
| `message` | メッセージ。 |
| `title` | トーストメッセージのタイトル。 |
| `body` | トーストメッセージの本文。 |
| `buttons.type` | トーストメッセージ内のボタンのタイプ。`unary`は1つのボタン、`two`は2つのボタンの値が受け入れられます。 |
| `buttons.primary` | トーストメッセージのプライマリボタンのテキスト。デフォルト値は`Accept`です。 |
| `buttons.secondary` | トーストメッセージのセカンダリボタンのテキスト。デフォルト値は`Accept`です。 |
