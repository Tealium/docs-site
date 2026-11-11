---
title: Orbeeタグ構成ガイド
description: この記事では、Orbeeタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/orbee-tag/
---
Orbeeは、Web分析およびデータソリューションをWebサイトと統合できるようにするためのタグを顧客に提供しています。Web SDKスニペットを使用すると、顧客はイベントデータとユーザーデータをOrbeeのサーバーに送信できます。

## タグに関するヒント

マッピングを使用して、次の操作を行います。
 * 構成データを動的に上書きする。
 * イベントをトリガーし、イベントパラメーターの値を構成する。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **スクリプトトークン**：クライアントのアカウントに属するスクリプトのトークンです。スクリプトトークンはSID（スクリプト識別子）と同じです。
* **ホスト**：スクリプトがホストされているドメインです。デフォルト値は`scripts.orb.ee`です。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準パラメーター

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `sid` | 文字列 | スクリプトトークン |
| `host` | 文字列 | ホスト |
| `additional_config_info.scope` | 文字列または文字列の配列 | スコープ |
| `additional_config_info.namespace` | 文字列または文字列の配列 | 名前空間 |

### イベント仕様オブジェクトのパラメーター

| 変数 | 型 | 説明 |
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
| `element.id` | 文字列 | 要素ID |
| `element.href` | 文字列 | 要素のHREF |
| `element.innerText` | 文字列 | 内部テキスト |
| `element.title` | 文字列 | 要素のタイトル |
| `element.src` | 文字列 | 要素のSRC |
| `element.alt` | 文字列 | 要素の代替テキスト |
| `element.node` | 文字列 | 要素のノード |
| `element.value` | 文字列 | 要素の値 |
| `element.type` | オブジェクトの配列 | 要素の型 |
| `elements` | オブジェクトの配列 | 要素 |
| `custom` | 文字列 | カスタム |

### Facebookプラグイン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `facebook.facebookId` | 文字列 | セグメント名 |
| `facebook.event` | 文字列 | セグメントID |
| `facebook.params` | 文字列 | Facebookセグメントの追加構成 |
| `facebook.token` | 文字列 | スクリプトトークン |

### お気に入りプラグイン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `favorites.element` | 文字列 | 登録するHTML要素 |
| `favorites.config` | 文字列 | お気に入りノードのオプションパラメーター |

### Google広告プラグイン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `googleAds.adwordsID` | 文字列 | Google広告のセグメント名 |
| `googleAds.event` | 文字列 | Google広告のセグメントID |
| `googleAds.params` | 文字列 | Google広告セグメントの追加構成 |

### Google Analyticsプラグイン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `googleAnalytics.adwordsID` | 文字列 | Googleセグメント名 |
| `googleAnalytics.event` | 文字列 | GoogleセグメントID |
| `googleAnalytics.params` | 文字列 | スクリプトトークン |

### レイアウトマネージャープラグイン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `layoutManager.config` | 文字列 | ORB要素コンテナーのレイアウト構成 |
| `layoutManager.config.id` | 文字列 | 構成ID |
| `layoutManager.config.location` | 文字列 | 構成場所 |
| `layoutManager.config.position` | 文字列 | 構成位置 |
| `layoutManager.config.attributes` | オブジェクト | 構成属性 |

### 通知プラグイン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `notifications.message` | 文字列 | メッセージ |
| `layoutManager.config` | オブジェクト | カスタムオブジェクト |
| `notifications.notificationId` | 文字列 | 通知ID |

### ポップアッププラグイン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `popupConfig.plugin_id` | 文字列 | プラグインID |
| `popupConfig.context_id` | 文字列 | コンテキストID |
| `popupConfig.css_url` | 文字列 | CSS URL |
| `popupConfig.display_type` | 文字列 | 表示形式 |
| `popupConfig.popupTimer` | 文字列 | ポップアップタイマー |
| `popupConfig.visitThreshold` | 文字列 | 訪問しきい値 |
| `popupConfig.scrollPersentThreshold` | 文字列 | スクロール率のしきい値 |
| `popupConfig.scrollTrigger` | 文字列 | スクロールトリガー |
| `popupConfig.disableConvertedUsers` | 文字列 | コンバージョン済みユーザーを無効化 |
| `popupConfig.disaleNewVisit` | 文字列 | 新規訪問を無効化 |
| `popupConfig.maxContentDisplayCount` | 文字列 | コンテンツの最大表示回数 |
| `popupConfig.cookieExpirationDays` | 文字列 | Cookieの有効期限（日数） |

### Snapchatプラグイン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `snapchat.pixelID` | 文字列 | SnapchatピクセルID |
| `snapchat.event` | 文字列 | イベント名 |
| `snapchat.params` | オブジェクト | 追加構成 |
| `snapchat.token` | 文字列 | トークン |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `dropSegment` | Facebookプラグイン：セグメントをドロップ |
| `registerFavoriteNode` | お気に入りプラグイン：お気に入りノードを登録 |
| `dropSegment` | Google Analyticsプラグイン：Google Analyticsセグメントをドロップ |
| `inject` | レイアウトマネージャープラグイン：挿入 |
| `runModules` | メタデータプラグイン：モジュールを実行 |
| `renderNotifications` | 通知プラグイン：通知をレンダリング |
| `push` | 通知プラグイン：プッシュ |
| `pop` | 通知プラグイン：ポップ |
| `closeNotification` | 通知プラグイン：通知を閉じる |
| `hideNotifications` | 通知プラグイン：通知を非表示にする |
| `showNotifications` | 通知プラグイン：通知を表示する |
| `loadPopup` | ポップアッププラグイン：ポップアップを読み込む |
| `dropSegment` | Snapchatプラグイン：セグメントをドロップ |
| `Custom` | カスタム |
### イベント固有のパラメーター

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

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
| `element.id`| 要素ID |
| `element.href`| 要素のHREF |
| `element.innerText`| 内部テキスト |
| `element.title`| 要素のタイトル |
| `element.src`| 要素のSRC |
| `element.alt`| 要素の代替テキスト |
| `element.node`| 要素ノード |
| `element.value`| 要素の値 |
| `element.type`| 要素のタイプ |
| `elements`| 要素 |
| `custom`| カスタム要素 |
| `facebook.facebookId`| Facebookプラグイン：Facebook ID |
| `facebook.event`| Facebookプラグイン：FacebookイベントID |
| `facebook.params`| Facebookプラグイン：Facebookセグメントの追加構成 |
| `facebook.token`| Facebookプラグイン：Facebookスクリプトのトークン |
| `favorites.element`| お気に入りプラグイン：登録するHTML要素 |
| `favorites.config`| お気に入りプラグイン：お気に入りノードのオプションパラメーター |
| `googleAds.adwordsID`| Google Adsプラグイン：Google Adsセグメント名 |
| `googleAds.event`| Google Adsプラグイン：Google AdsセグメントID |
| `googleAds.params`| Google Adsプラグイン：Google Adsセグメントの追加構成 |
| `googleAnalytics.adwordsID`| Google Analyticsプラグイン：Google Analyticsセグメント名 |
| `googleAnalytics.event`| Google Analyticsプラグイン：Google AnalyticsセグメントID |
| `googleAnalytics.params`| Google Analyticsプラグイン：Google Analyticsスクリプトのトークン |
| `layoutManager.config`| Layout Managerプラグイン：ORB要素コンテナーのLayout Manager構成 |
| `layoutManager.config.id`| Layout Managerプラグイン：Layout Manager構成ID |
| `layoutManager.config.location`| Layout Managerプラグイン：Layout Manager構成の場所 |
| `layoutManager.config.position`| Layout Managerプラグイン：Layout Manager構成の位置 |
| `layoutManager.config.attributes`| Layout Managerプラグイン：Layout Manager構成の属性 |
| `notifications.message` | 通知プラグイン：メッセージ |
| `notifications.config`| 通知プラグイン：構成 |
| `notifications.notificationId`| 通知プラグインID |
| `popupConfig.plugin_id` | ポップアッププラグイン：ID |
| `popupConfig.context_id`| ポップアッププラグイン：コンテキストID |
| `popupConfig.css_url` | ポップアッププラグイン：CSS URL |
| `popupConfig.display_type`| ポップアッププラグイン：表示タイプ |
| `popupConfig.popupTimer`| ポップアッププラグイン：タイマー |
| `popupConfig.visitThreshold`| ポップアッププラグイン：訪問回数のしきい値 |
| `popupConfig.scrollPersentThreshold`| ポップアッププラグイン：スクロール率のしきい値 |
| `popupConfig.scrollTrigger` | ポップアッププラグイン：スクロールトリガー |
| `popupConfig.disableConvertedUsers`| ポップアッププラグイン：コンバージョン済みユーザーを無効化 |
| `popupConfig.disaleNewVisit`| ポップアッププラグイン：新規訪問を無効化 |
| `popupConfig.maxContentDisplayCount`| ポップアッププラグイン：コンテンツの最大表示回数 |
| `popupConfig.cookieExpirationDays`| ポップアッププラグイン：Cookieの有効期限（日数） |
| `snapchat.pixelID`| SnapchatピクセルID |
| `snapchat.event`| Snapchatプラグイン：Snapchatイベント名 |
| `snapchat.config`| Snapchatプラグイン：Snapchatの追加構成 |
| `snapchat.token`| Snapchatプラグイン：Snapchatトークン |
| `Custom_Parameter`| カスタムパラメーター |
| `facebookDropSegment`| Facebookプラグイン：Facebookセグメントを削除 |
| `registerFavoriteNode`| お気に入りプラグイン：お気に入りノードを登録 |
| `googleAdsDropSegment`| Google Adsプラグイン：Google Adsセグメントを削除 |
| `googleAnalyticsDropSegment`| Google Analyticsプラグイン：Google Analyticsセグメントを削除 |
| `inject`| Layout Managerプラグインに挿入 |
| `runModules`| MetaDataプラグインでモジュールを実行 |
| `renderNotifications`| 通知プラグインをレンダリング |
| `push`| 通知プラグインのプッシュ |
| `pop` | 通知プラグインのポップ |
| `closeNotification` | 通知プラグイン：通知を閉じる |
| `hideNotifications`| 通知プラグイン：通知を非表示にする |
| `showNotifications`| 通知プラグイン：通知を表示する |
| `loadPopup` | ポップアッププラグインを読み込む |
| `snapchatDropSegment`| Snapchatプラグイン：Snapchatセグメントを削除 |
| `Custom_Event`| カスタムイベント |