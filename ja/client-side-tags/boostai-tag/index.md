---
title: Boost.aiタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでboost.aiタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/boostai-tag/
---
Boost.aiは、市場をリードする機械学習を使用して、会話型AIチャットボットの構築、実装、運用を支援し、対話を簡素化します。

## タグのヒント

* マッピングを使用してタグの構成を上書きまたは動的に構成します。

## タグ構成

新しいタグを追加するために、タグマーケットプレイスに移動します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **サーバー名**: サーバーURLは次のようになります：`https://[your-server-name].boost.ai`。
* **ターゲットエレメント**: チャットパネルがウェブサイトに挿入されるHTMLエレメント名を入力します。
  * ターゲットエレメントがクラスの場合、ピリオド(`.`)を先行させます。例えば、クラスが`chat-container`の場合、`.chat-container`を入力します。
  * ターゲットエレメントがIDの場合、ハッシュ(`#`)を先行させます。例えば、IDが`chat-container`の場合、`#chat-container`を入力します。
* **自動チャットオープニング**: ロード時にチャットを自動的に開きます。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリーは以下の通りです：

### スタンダード

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `serverName`  | 文字列 | サーバー名（タグ構成を上書き） | 
| `targetElement`  |文字列| ターゲットエレメント（タグ構成を上書き） |
|  `autoChatOpening`  | 文字列 | 自動チャットオープニング（タグ構成を上書き） |
|  `filter_values`  | 文字列 | フィルター値 |
|  `once`  | ブール | 一度 |
|  `contextIntentId`  | 数値 |  コンテキストインテントID |
|  `authType`  | 文字列 | 認証タイプ  |
|  `authContent`  | 文字列 | 認証コンテンツ |
|  `actionId`  | 数値 | アクションID  |
|  `customPayload`  | 文字列 | カスタムペイロード  |
|  `newTitle`  | 文字列 | 新しいタイトル  |
|  `newConversationId`  | ブール | 新しい会話ID |

### オプション

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `contextTopicIntentId` |  数値  | コンテキストトピックインテントID |
| `conversationId`  | 文字列 | 会話ID |
| `startLanguage` | 文字列  | 開始言語 |
| `openTextLinksInNewTab` | ブール | 新しいタブでテキストリンクを開く |
| `showLinkClickAsChatBubble` | ブール | チャットバブルとしてリンククリックを表示 |
| `messageFeedbackOnFirstAction`  | ブール | 最初のアクションに対するメッセージフィードバック |
| `startTriggerActionId`  | 文字列  | スタートトリガーアクションID |
| `authStartTriggerActionId`  | 文字列 |  認証スタートトリガーアクションID  |
| `skill`  | 文字列 |  スキル |
| `startNewConversationOnResumeFailure`  | ブール | レジューム失敗時に新しい会話を開始  |
| `fileUploadServiceEndpointUrl`  | 文字列 | ファイルアップロードサービスエンドポイントURL |
| `requestFeedback`  | ブール | フィードバックの要求  |
| `pageUrl`  | 文字列 | ページURL  |
| `triggerActionOnResume`  | ブール | レジューム時のトリガーアクション  |
| `enableProactivityForSmallDevices`  | ブール | 小型デバイスのためのプロアクティブ性を有効にする  |
| `removeRememberedConversationOnChatPanelClose`  | ブール | チャットパネルを閉じるときに記憶された会話を削除  |
| `alwaysFullscreen`  | ブール | 常にフルスクリーン |

### Emit Parameters

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `emitEvent` | オブジェクト  | イベントを発行  |
| `emitOnResume`  | ブール  | レジューム時に発行 |
| `detail`  | オブジェクト  | 詳細  |
| `type`  | 文字列  | タイプ  |

### イベント

イベントのマッピングについては、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

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

### イベント固有のパラメータ

イベントのマッピングについては、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

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

