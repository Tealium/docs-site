---
title: Orbeeタグの設定ガイド
description: この記事では、Orbeeタグのセットアップ方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/orbee-tag/
---
Orbeeは、顧客がウェブ解析とデータソリューションをウェブサイトと統合するためのタグを提供しています。ウェブSDKスニペットを使用すると、顧客はイベントデータとユーザーデータをOrbeeのサーバーに送信できます。

## タグのヒント

マッピングを使用して、次のことができます：
 * 動的に構成データを上書きする。
 * イベントをトリガーし、イベントパラメータの値を構成する。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します：

* **スクリプトトークン**：クライアントのアカウントに属するスクリプトのトークン。スクリプトトークンはSID（スクリプト識別子）と同じです。
* **ホスト**：スクリプトがホストされているドメイン。デフォルト値は `scripts.orb.ee` です。

## ロードルール

タグをすべてのページにロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングとは、データレイヤー変数からベンダータグの対応する変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準パラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `sid` | 文字列 | スクリプトトークン |
| `host` | 文字列 | ホスト |
| `additional_config_info.scope` | 文字列または文字列の配列 | スコープ |
| `additional_config_info.namespace` | 文字列または文字列の配列 | 名前空間 |

### イベント仕様オブジェクトパラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `action` | 文字列 | アクション |
| `object` | 文字列 | オブジェクト |
| `token` | 文字列 | トークン |
| `namespaces` | 文字列または文字列の配列 | 名前空間 |
| `vendor` | 文字列 | ベンダー |
| `product` | 文字列 | 製品 |
| `label` | 文字列 | ラベル |
| `score` | 数値 | スコア |
| `instanceID` | 文字列 | インスタンスID |
| `element` | オブジェクト | 要素 |
| `element.classes` | テキストの配列 | 要素のクラス |
| `element.id` | 文字列 | 要素のID |
| `element.href` | 文字列 | 要素のHREF |
| `element.innerText` | 文字列 | 内部テキスト |
| `element.title` | 文字列 | 要素のタイトル |
| `element.src` | 文字列 | 要素のSRC |
| `element.alt` | 文字列 | 要素の代替テキスト |
| `element.node` | 文字列 | 要素のノード |
| `element.value` | 文字列 | 要素の値 |
| `element.type` | オブジェクトの配列 | 要素のタイプ |
| `elements` | オブジェクトの配列 | 要素 |
| `custom` | 文字列 | カスタム |

### Facebookプラグイン

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `facebook.facebookId` | 文字列 | セグメント名 |
| `facebook.event` | 文字列 | セグメントID |
| `facebook.params` | 文字列 | Facebookセグメントの追加構成 |
| `facebook.token` | 文字列 | スクリプトトークン |

### Favoritesプラグイン

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `favorites.element` | 文字列 | 登録するHTML要素 |
| `favorites.config` | 文字列 | Favoriteノードのオプションパラメータ |

### Google Adsプラグイン

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `googleAds.adwordsID` | 文字列 | Google Adsセグメント名 |
| `googleAds.event` | 文字列 | Google AdsセグメントID |
| `googleAds.params` | 文字列 | Google Adsセグメントの追加構成 |

### Google Analyticsプラグイン

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `googleAnalytics.adwordsID` | 文字列 | Googleセグメント名 |
| `googleAnalytics.event` | 文字列 | GoogleセグメントID |
| `googleAnalytics.params` | 文字列 | Google Analyticsスクリプトトークン |

### Layout Managerプラグイン

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `layoutManager.config` | 文字列 | ORB要素コンテナのレイアウト構成 |
| `layoutManager.config.id` | 文字列 | 構成ID |
| `layoutManager.config.location` | 文字列 | 構成の場所 |
| `layoutManager.config.position` | 文字列 | 構成の位置 |
| `layoutManager.config.attributes` | オブジェクト | 構成の属性 |

### Notificationsプラグイン

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `notifications.message` | 文字列 | メッセージ |
| `layoutManager.config` | オブジェクト | カスタムオブジェクト |
| `notifications.notificationId` | 文字列 | 通知ID |

### Popupプラグイン

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `popupConfig.plugin_id` | 文字列 | プラグインID |
| `popupConfig.context_id` | 文字列 | コンテキストID |
| `popupConfig.css_url` | 文字列 | CSSのURL |
| `popupConfig.display_type` | 文字列 | 表示タイプ |
| `popupConfig.popupTimer` | 文字列 | ポップアップタイマー |
| `popupConfig.visitThreshold` | 文字列 | 訪問閾値 |
| `popupConfig.scrollPersentThreshold` | 文字列 | スクロールパーセントの閾値 |
| `popupConfig.scrollTrigger` | 文字列 | スクロールトリガー |
| `popupConfig.disableConvertedUsers` | 文字列 | 変換済みユーザーの無効化 |
| `popupConfig.disaleNewVisit` | 文字列 | 新しい訪問の無効化 |
| `popupConfig.maxContentDisplayCount` | 文字列 | 最大コンテンツ表示回数 |
| `popupConfig.cookieExpirationDays` | 文字列 | クッキーの有効期限（日数） |

### Snapchatプラグイン

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `snapchat.pixelID` | 文字列 | SnapchatピクセルID |
| `snapchat.event` | 文字列 | イベント名 |
| `snapchat.params` | オブジェクト | 追加構成 |
| `snapchat.token` | 文字列 | トークン |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `dropSegment` | Facebookプラグイン：セグメントの削除 |
| `registerFavoriteNode` | Favoritesプラグイン：Favoriteノードの登録 |
| `dropSegment` | Google Analyticsプラグイン：Google Analyticsセグメントの削除 |
| `inject` | Layout Managerプラグイン：インジェクト |
| `runModules` | Metadataプラグイン：モジュールの実行 |
| `renderNotifications` | Notificationsプラグイン：通知のレンダリング |
| `push` | Notificationsプラグイン：プッシュ |
| `pop` | Notificationsプラグイン：ポップ |
| `closeNotification` | Notificationsプラグイン：通知の閉じる |
| `hideNotifications` | Notificationsプラグイン：通知の非表示 |
| `showNotifications` | Notificationsプラグイン：通知の表示 |
| `loadPopup` | Popupプラグイン：ポップアップのロード |
| `dropSegment` | SnapChatプラグイン：セグメントの削除 |
| `Custom` | カスタム |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `additional_config_info.scope`| スコープ |
| `additional_config_info.namespace`| 名前空間 |
| `action`| アクション |
| `object`| オブジェクト |
| `token`| トークン |
| `namespaces`| 名前空間 |
| `vendor`| ベンダー |
| `product`| 製品 |
| `label`| ラベル |
| `score`| スコア |
| `instanceID`| インスタンスID |
| `element`| 要素オブジェクト |
| `element.classes`| 要素のクラス |
| `element.id`| 要素のID |
| `element.href`| 要素のHREF |
| `element.innerText`| 内部テキスト |
| `element.title`| 要素のタイトル |
| `element.src`| 要素のSRC |
| `element.alt`| 要素の代替テキスト |
| `element.node`| 要素のノード |
| `element.value`| 要素の値 |
| `element.type`| 要素のタイプ |
| `elements`| 要素 |
| `custom`| カスタム要素 |
| `facebook.facebookId`| Facebookプラグイン：Facebook ID |
| `facebook.event`| Facebookプラグイン：FacebookイベントID |
| `facebook.params`| Facebookプラグイン：Facebookセグメントの追加構成 |
| `facebook.token`| Facebookプラグイン：Facebookスクリプトトークン |
| `favorites.element`| Favoritesプラグイン：登録するHTML要素 |
| `favorites.config`| Favoritesプラグイン：Favoriteノードのオプションパラメータ |
| `googleAds.adwordsID`| Google Adsプラグイン：Google Adsセグメント名 |
| `googleAds.event`| Google Adsプラグイン：Google AdsセグメントID |
| `googleAds.params`| Google Adsプラグイン：Google Adsセグメントの追加構成 |
| `googleAnalytics.adwordsID`| Google Analyticsプラグイン：Google Analyticsセグメント名 |
| `googleAnalytics.event`| Google Analyticsプラグイン：Google AnalyticsセグメントID |
| `googleAnalytics.params`| Google Analyticsプラグイン：Google Analyticsスクリプトトークン |
| `layoutManager.config`| Layout Managerプラグイン：ORB要素コンテナのレイアウト構成 |
| `layoutManager.config.id`| Layout Managerプラグイン：Layout Managerの構成ID |
| `layoutManager.config.location`| Layout Managerプラグイン：Layout Managerの構成場所 |
| `layoutManager.config.position`| Layout Managerプラグイン：Layout Managerの構成位置 |
| `layoutManager.config.attributes`| Layout Managerプラグイン：Layout Managerの構成属性 |
| `notifications.message` | Notificationsプラグイン：メッセージ |
| `notifications.config`| Notificationsプラグイン：構成 |
| `notifications.notificationId`| Notificationsプラグイン：通知ID |
| `popupConfig.plugin_id` | Popupプラグイン：ID |
| `popupConfig.context_id`| Popupプラグイン：コンテキストID |
| `popupConfig.css_url` | Popupプラグイン：CSSのURL |
| `popupConfig.display_type`| Popupプラグイン：表示タイプ |
| `popupConfig.popupTimer`| Popupプラグイン：タイマー |
| `popupConfig.visitThreshold`| Popupプラグイン：訪問閾値 |
| `popupConfig.scrollPersentThreshold`| Popupプラグイン：スクロールパーセントの閾値 |
| `popupConfig.scrollTrigger` | Popupプラグイン：スクロールトリガー |
| `popupConfig.disableConvertedUsers`| Popupプラグイン：変換済みユーザーの無効化 |
| `popupConfig.disaleNewVisit`| Popupプラグイン：新しい訪問の無効化 |
| `popupConfig.maxContentDisplayCount`| Popupプラグイン：最大コンテンツ表示回数 |
| `popupConfig.cookieExpirationDays`| Popupプラグイン：クッキーの有効期限（日数） |
| `snapchat.pixelID`| Snapchatプラグイン：SnapchatピクセルID |
| `snapchat.event`| Snapchatプラグイン：Snapchatイベント名 |
| `snapchat.config`| Snapchatプラグイン：Snapchatの追加構成 |
| `snapchat.token`| Snapchatプラグイン：Snapchatトークン |
| `Custom_Parameter`| カスタムパラメータ |
| `facebookDropSegment`| Facebookプラグイン：Facebookセグメントの削除 |
| `registerFavoriteNode`| Favoriteプラグイン：Favoriteノードの登録 |
| `googleAdsDropSegment`| Google Adsプラグイン：Google Adsセグメントの削除 |
| `googleAnalyticsDropSegment`| Google Analyticsプラグイン：Google Analyticsセグメントの削除 |
| `inject`| Layout Managerプラグイン：インジェクト |
| `runModules`| Metadataプラグイン：モジュールの実行 |
| `renderNotifications`| Notificationsプラグイン：通知のレンダリング |
| `push`| Notificationsプラグイン：プッシュ |
| `pop` | Notificationsプラグイン：ポップ |
| `closeNotification` | Notificationsプラグイン：通知の閉じる |
| `hideNotifications`| Notificationsプラグイン：通知の非表示 |
| `showNotifications`| Notificationsプラグイン：通知の表示 |
| `loadPopup` | Popupプラグイン：ポップアップのロード |
| `snapchatDropSegment`| Snapchatプラグイン：Snapchatセグメントの削除 |
| `Custom_Event`| カスタムイベント |

