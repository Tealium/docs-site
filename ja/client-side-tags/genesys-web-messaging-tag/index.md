---
title: Genesys Web Messagingタグ構成ガイド
description: この記事では、Genesys Web Messagingタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/genesys-web-messaging-tag/
---
Genesys Web Messagingは、顧客がWebサイト上でボットまたはエージェントと会話できるようにする機能です。非同期の会話、受信および送信画像の添付、Genesys Cloudのすべてのメッセージングチャネルで統一されたエージェントおよびスーパーバイザーエクスペリエンスなど、Webチャットに比べてさまざまな利点があります。

## タグに関するヒント

* マッピングを使用して、標準構成値を動的に上書きします。

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **デプロイメントID**：  
ユーザーから提供されたGenesys識別子。
* **環境**：  
タグがデプロイされる環境。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `deploymentId` | 文字列 | デプロイメントID。 |
| `environment` | 文字列 | 環境。 |
| `debug` | ブール値 | デバッグ。 |
| `base_url` | 文字列 | ベースURL。 |

### 認証

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `authCode` | 文字列 | 認証コード。 |
| `redirectUri` | 文字列 | 構成されたリダイレクトURI。 |
| `nonce` | 文字列 | ランダムな文字列（UUIDを推奨）。 |
| `maxAge` | 文字列 | 経過時間（秒単位）。 |
| `codeVerifier` | 文字列 | PKCEフロー用のコードベリファイア。 |
| `iss` | 文字列 | 発行者。 |

### データベースパラメーター

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `customAttributes` | オブジェクト | カスタム属性。 |
| `name` | 文字列 | 取得するオブジェクトプロパティの名前。 |

### Cobrowseサービスパラメーター

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `joinCode` | 文字列 | 参加コード。 |
| `sessionId` | 文字列 | セッションID。 |

### エンゲージメントパラメーター

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `engageContent` | オブジェクト | エンゲージコンテンツ。 |
| `engageContent.offerText` | 文字列 | エンゲージコンテンツのオファーテキスト。 |

### ジャーニーパラメーター

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `pageTitle` | 文字列 | ページタイトル。 |
| `pageLocation` | 文字列 | ページの場所。 |
| `customAttributes` | オブジェクト | カスタム属性。 |
| `traitsMapper` | オブジェクトの配列 | 特性マッパー。 |
| `eventName` | 文字列 | HTML要素がクリックされたときに送信するイベントの名前。 |
| `selector` | 文字列 | 追跡するCSSセレクター。 |
| `formName` | 文字列 | フォーム名。 |
| `captureFormDataOnAbandon` | ブール値 | フォームが放棄されたときにフォームデータを取得するかどうかを示します。 |
| `captureFormDataOnSubmit` | ブール値 | フォームが送信されたときにフォームデータを取得するかどうかを示します。|
| `clickEvents.selector` | 配列 | クリックイベントのセレクター。 |
| `clickEvents.eventName` | 配列 | クリックイベントのイベント名。 |
| `clickEvents.customAttributes` | 配列 | クリックイベントのカスタム属性。 |
| `idleEvents.idleAfterSeconds` | 配列 | イベントを記録するまでに待機するユーザーの非アクティブ時間（秒）。 |
| `idleEvents.eventName` | 配列 | アイドルイベントのイベント名。 |
| `idleEvents.customAttributes` | 配列 | アイドルイベントのカスタム属性。 |
| `inViewportEvents.selector` | 文字列 | ビューポート内イベントのセレクター。 |
| `inViewportEvents.eventName` | 文字列 | ビューポート内イベントのイベント名。 |
| `inViewportEvents.customAttributes` | オブジェクト | ビューポート内イベントのカスタム属性。 |
| `scrollDepthEvents.percentage` | 数値 | スクロール深度イベントの割合。 |
| `scrollDepthEvents.eventName` | 文字列 | スクロール深度イベントのイベント名。 |
| `scrollDepthEvents.customAttributes` | オブジェクト | スクロール深度イベントのカスタム属性。 |
| `actionId` | 文字列 | アクションID。 |
| `actionState` | 文字列 | アクションの状態。 |
| `errorCode` | 文字列 | エラーコード。 |
| `errorReason` | 文字列 | エラーの理由。 |

### MessagingServiceパラメーター

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `message` | 文字列 | 送信するテキストメッセージ。 |

### Toasterパラメーター

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `title` | 文字列 | トーストメッセージのタイトル。 |
| `body` | 文字列 | トーストメッセージの本文テキスト。 |
| `buttons.type` | 文字列 | トーストメッセージ内のボタンの種類。指定可能な値は、ボタンが1つの場合は`unary`、ボタンが2つの場合は`two`です。 |
| `buttons.primary` | 文字列 | トーストメッセージ内のプライマリボタンのテキスト。デフォルト値は`Accept`です。 |
| `buttons.secondary` | 文字列 | トーストメッセージ内のセカンダリボタンのテキスト。デフォルト値は`Accept`です。 |

### イベント固有のパラメーター

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `authCode` | 認証コード。 |
| `redirectUri` | 構成されたリダイレクトURI。 |
| `nonce` | ランダムな文字列（UUIDを推奨）。 |
| `maxAge` | 経過時間（秒単位）。 |
| `codeVerifier` | PKCEフロー用のコードベリファイア。 |
| `iss` | 発行者。 |
| `customAttributes` | カスタム属性。 |
| `name` | 取得するオブジェクトプロパティの名前。 |
| `joinCode` | 参加コード。 |
| `sessionId` | セッションID。 |
| `engageContent` | エンゲージコンテンツ。 |
| `engageContent.offerText` | エンゲージコンテンツのオファーテキスト。 |
| `pageTitle` | ページタイトル。 |
| `pageLocation` | ページの場所。 |
| `customAttributes` | カスタム属性。 |
| `traitsMapper` | 特性マッパー。 |
| `eventName` | HTML要素がクリックされたときに送信するイベントの名前。 |
| `selector` | 追跡するCSSセレクター。 |
| `formName` | フォーム名。 |
| `captureFormDataOnAbandon` | フォームが放棄されたときにフォームデータを取得するかどうかを示します。 |
| `captureFormDataOnSubmit` | フォームが送信されたときにフォームデータを取得するかどうかを示します。 |
| `clickEvents.selector` | クリックイベントのセレクター。 |
| `clickEvents.eventName` | クリックイベントのイベント名。 |
| `clickEvents.customAttributes` | クリックイベントのカスタム属性。 |
| `idleEvents.idleAfterSeconds` | イベントを記録するまでに待機するユーザーの非アクティブ時間（秒）。 |
| `idleEvents.eventName` | アイドルイベントのイベント名。 |
| `idleEvents.customAttributes` | アイドルイベントのカスタム属性。 |
| `inViewportEvents.selector` | ビューポート内イベントのセレクター。 |
| `inViewportEvents.eventName` | ビューポート内イベントのイベント名。 |
| `inViewportEvents.customAttributes` | ビューポート内イベントのカスタム属性。 |
| `scrollDepthEvents.percentage` | スクロール深度イベントの割合。 |
| `scrollDepthEvents.eventName` | スクロール深度イベントのイベント名。 |
| `scrollDepthEvents.customAttributes` | スクロール深度イベントのカスタム属性。 |
| `actionId` | アクションID。 |
| `actionState` | アクションの状態。 |
| `errorCode` | エラーコード。 |
| `errorReason` | エラーの理由。 |
| `message` | メッセージ。 |
| `title` | 文字列 | トーストメッセージのタイトル。 |
| `body` | 文字列 | トーストメッセージの本文テキスト。 |
| `buttons.type` | 文字列 | トーストメッセージ内のボタンの種類。指定可能な値は、ボタンが1つの場合は`unary`、ボタンが2つの場合は`two`です。 |
| `buttons.primary` | 文字列 | トーストメッセージ内のプライマリボタンのテキスト。デフォルト値は`Accept`です。 |
| `buttons.secondary` | 文字列 | トーストメッセージ内のセカンダリボタンのテキスト。デフォルト値は`Accept`です。 |