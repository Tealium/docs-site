---
title: Boost.ai タグ構成ガイド
description: この記事では、タグ管理アカウントで boost.ai タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/boostai-tag/
---
Boost.ai を使用すると、市場をリードする機械学習を活用して会話型 AI チャットボットを構築、実装、運用し、ユーザーとのやり取りを簡素化できます。

## タグに関するヒント

* マッピングを使用して、タグ構成を上書きするか、動的に構成します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の項目を構成します。

* **サーバー名**：サーバー URL は `https://[your-server-name].boost.ai` のような形式にする必要があります。
* **ターゲット要素**：Web サイト上でチャットパネルを挿入する HTML 要素名を入力します。
  * ターゲット要素がクラスの場合は、先頭にピリオド（`.`）を付けます。たとえば、クラスが `chat-container` の場合は `.chat-container` と入力します。
  * ターゲット要素が ID の場合は、先頭にハッシュ記号（`#`）を付けます。たとえば、ID が `chat-container` の場合は `#chat-container` と入力します。
* **チャットを自動的に開く**：読み込み時にチャットを自動的に開きます。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `serverName` | 文字列 | サーバー名（タグ構成を上書き） |
| `targetElement` | 文字列 | ターゲット要素（タグ構成を上書き） |
| `autoChatOpening` | 文字列 | チャットの自動オープン（タグ構成を上書き） |
| `filter_values` | 文字列 | フィルター値 |
| `once` | ブール値 | 1 回のみ |
| `contextIntentId` | 数値 | コンテキストインテント ID |
| `authType` | 文字列 | 認証タイプ |
| `authContent` | 文字列 | 認証コンテンツ |
| `actionId` | 数値 | アクション ID |
| `customPayload` | 文字列 | カスタムペイロード |
| `newTitle` | 文字列 | 新しいタイトル |
| `newConversationId` | ブール値 | 新しい会話 ID |

### オプション

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `contextTopicIntentId` | 数値 | コンテキストトピックインテント ID |
| `conversationId` | 文字列 | 会話 ID |
| `startLanguage` | 文字列 | 開始言語 |
| `openTextLinksInNewTab` | ブール値 | テキストリンクを新しいタブで開く |
| `showLinkClickAsChatBubble` | ブール値 | リンクのクリックをチャットバブルとして表示する |
| `messageFeedbackOnFirstAction` | ブール値 | 最初のアクション時にメッセージフィードバックを表示する |
| `startTriggerActionId` | 文字列 | 開始トリガーアクション ID |
| `authStartTriggerActionId` | 文字列 | 認証開始トリガーアクション ID |
| `skill` | 文字列 | スキル |
| `startNewConversationOnResumeFailure` | ブール値 | 再開に失敗した場合に新しい会話を開始する |
| `fileUploadServiceEndpointUrl` | 文字列 | ファイルアップロードサービスのエンドポイント URL |
| `requestFeedback` | ブール値 | フィードバックを要求する |
| `pageUrl` | 文字列 | ページ URL |
| `triggerActionOnResume` | ブール値 | 再開時にアクションをトリガーする |
| `enableProactivityForSmallDevices` | ブール値 | 小型デバイスでプロアクティブ機能を有効にする |
| `removeRememberedConversationOnChatPanelClose` | ブール値 | チャットパネルを閉じたときに記憶された会話を削除する |
| `alwaysFullscreen` | ブール値 | 常に全画面表示にする |

### Emit パラメーター

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `emitEvent` | オブジェクト | Emit イベント |
| `emitOnResume` | ブール値 | 再開時に Emit する |
| `detail` | オブジェクト | 詳細 |
| `type` | 文字列 | タイプ |

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `chatPanelOpened` | chatPanelOpened |
| `chatPanelClosed` | chatPanelClosed |
| `chatPanelMinimized` | chatPanelMinimized |
| `conversationIdChanged` | conversationIdChanged |
| `messageSent` | messageSent |
| `menuOpened` | menuOpened |
| `menuClosed` | menuClosed |
| `conversationDownloaded` | conversationDownloaded |
| `conversationDeleted` | conversationDeleted |
| `actionLinkClicked` | actionLinkClicked |
| `externalLinkClicked` | externalLinkClicked |
| `conversationReferenceChanged` | conversationReferenceChanged |
| `filterValuesChanged` | filterValuesChanged |
| `authStatusChanged` | authStatusChanged |
| `vanLinkClicked` | vanLinkClicked |
| `conversationTransferredToHuman` | conversationTransferredToHuman |
| `conversationTransferredToVirtualAgent` | conversationTransferredToVirtualAgent |
| `custom` | custom |
| `getVisibility` | getVisibility |
| `loginEvent` | loginEvent |
| `logoutEvent` | logoutEvent |
| `minimize` | minimize |
| `removeEventListener` | removeEventListener |
| `reportAbTestSuccess` | reportAbTestSuccess |
| `setContextIntentId` | setContextIntentId |
| `setConversationId` | setConversationId |
| `setCustomPayload` | setCustomPayload |
| `setFilterValues` | setFilterValues |
| `setSkill` | setSkill |
| `setTitle` | setTitle |
| `show` | show |
| `triggerAction` | triggerAction |

### イベント固有のパラメーター

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `chatPanelOpened` | chatPanelOpened |
| `chatPanelClosed` | chatPanelClosed |
| `chatPanelMinimized` | chatPanelMinimized |
| `conversationIdChanged` | conversationIdChanged |
| `messageSent` | messageSent |
| `menuOpened` | menuOpened |
| `menuClosed` | menuClosed |
| `conversationDownloaded` | conversationDownloaded |
| `conversationDeleted` | conversationDeleted |
| `actionLinkClicked` | actionLinkClicked |
| `externalLinkClicked` | externalLinkClicked |
| `conversationReferenceChanged` | conversationReferenceChanged |
| `filterValuesChanged` | filterValuesChanged |
| `authStatusChanged` | authStatusChanged |
| `vanLinkClicked` | vanLinkClicked |
| `conversationTransferredToHuman` | conversationTransferredToHuman |
| `conversationTransferredToVirtualAgent` | conversationTransferredToVirtualAgent |
| `custom` | custom |
| `getVisibility` | getVisibility |
| `loginEvent` | loginEvent |
| `logoutEvent` | logoutEvent |
| `minimize` | minimize |
| `removeEventListener` | removeEventListener |
| `reportAbTestSuccess` | reportAbTestSuccess |
| `setContextIntentId` | setContextIntentId |
| `setConversationId` | setConversationId |
| `setCustomPayload` | setCustomPayload |
| `setFilterValues` | setFilterValues |
| `setSkill` | setSkill |
| `setTitle` | setTitle |
| `show` | show |
| `triggerAction` | triggerAction |