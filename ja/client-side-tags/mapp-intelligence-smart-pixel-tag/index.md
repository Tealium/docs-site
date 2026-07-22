---
title: Mapp Intelligence Smart Pixelタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでMapp Intelligence Smart Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mapp-intelligence-smart-pixel-tag/
---
Mapp Intelligenceは、ウェブサイトの使用状況と顧客理解を深めるための詳細な分析と貴重な洞察を分析者とマーケターに提供します。それは、適切なメッセージを適切なタイミングで適切なチャネルでターゲットオーディエンスに提供するための必要な情報を提供します。

## タグのヒント

* マッピングに追加された値は、`wt`オブジェクトに挿入されます（例えば、`contentId`や`internalSearch`を構成するためのマッピングを使用します）。
* `formTrackInstall()`関数は、フォームHTML IDの値を構成すると自動的にトリガーされます。
* `utag.link()`関数を呼び出してイベントをトラックします。
* 注文値を自動的に構成するには、E-Commerce Extensionが必要です。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **ライブラリバージョン**：使用するライブラリバージョンを選択します。
* **トラックID**：トラックIDを使用してリクエストをアカウントに割り当てます。トラックIDは、Mapp **システム構成**の**Mapp Q3 > 構成 > システム構成 > データ収集**の下にあります。複数のアカウントで同じ情報を記録するには、トラックIDをカンマで区切ります。
* **トラックドメイン**：アカウントマネージャーから提供されたMapp Intelligenceトラックドメインを入力します。
* **ドメイン**：Smart Pixelのドメインをリファラーとして除外するデフォルトの動作を上書きします。
* **Cookie Handling**：ブラウザまたはサーバー経由でクッキーを構成するかどうかを示します。サーバーサイドクッキーは、ウェブドメインと一致するカスタムトラックドメインを使用する場合のみ推奨されます。これにより、ファーストパーティトラッキングと最高のデータ品質が可能になります。
* **Secure Cookie**：このオプションを有効にすると、すべてのMapp Intelligenceクッキーにセキュアフラグが追加されます。これにより、セキュアクッキーはHTTPS経由でのみ送信されます。
* **Opt-Out Name**：オプトアウトクッキーの代替名を提供します。
* **Request Obfuscation**：すべてのトラッキングリクエストを難読化して、広告ブロッカーがMapp Intelligenceトラックリクエストを識別しブロックするのを難しくします。このオプションはデフォルトでは無効になっていますが、`requestObfuscation`キーを使用して有効にすることができます。
* **Force Old EverId**：古いMapp Intelligence `EverID`の使用を強制します。
* **Product Merge**：必要に応じて、同じ製品IDを持つ複数の製品のマージを無効にします。
* **サーバー間トラッキング機能のサポート**：サーバー間トラッキング機能を有効にします。
* **Use Hash for Default Page Name**：デフォルトのページ名にURLハッシュを含めます。
* **Use Params For Default Page Name**：デフォルトのページ名に特定のURLパラメータを含めます。
* **Request Queue**：すべてのトラッキングリクエストのオフラインキューを有効にします。
* **Request Limit**：大量のリクエストによるエラーのリスクを減らすために、リクエストの最大数を構成するために有効にします。
* **User Identification**：匿名トラッキングを有効にします。
* **Enable auto-tracking**：タグがトリガーされたときに`wtSmart.track()`関数を使用して自動トラッキングを有効にします。
* **Enable auto-tracking page data only**：ページデータのための`wtSmart.trackPage()`関数を使用して自動トラッキングを有効にします。
* **Enable auto-tracking event data only**：イベントデータのための`wtSmart.trackAction()`関数を使用して自動トラッキングを有効にします。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### 構成

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `trackId` | `String` | トラックID。 |
| `trackDomain` | `String` | トラックドメイン。 |
| `domain` | `Array of Strings` | ドメイン。 |
| `cookie` | `String` | クッキー構成。 |
| `secureCookie` | `Boolean` | セキュアクッキー。 |
| `optOutName` | `String` | オプトアウトクッキーの代替名。 |
| `requestObfuscation` | `Boolean` | リクエストの難読化。 |
| `forceOldEverId` | `Boolean` | 古い`EverID`の強制。 |
| `productMerge` | `String` | 製品のマージ。 |
| `sendViaServer.activated` | `Boolean` | サーバー間トラッキング。 |
| `useHashForDefaultPageName` | `Boolean` | デフォルトのページ名にハッシュを使用する。 |
| `useParamsForDefaultPageName` | `Array of Strings` | デフォルトのページ名にパラメータを使用する。 |
| `requestQueue.activated` | `Boolean` | トラッキングリクエストのオフラインキュー。 |
| `requestLimit` | `Boolean` | リクエスト制限。 |
| `userIdentification.enableAnonymousFunction` | `Boolean` | 匿名トラッキング。 |
| `autoTracking` | `Boolean` | 自動トラッキング。 |
| `autoTrackingPage` | `Boolean` | ページの自動トラッキング。 |
| `autoTrackingEvent` | `Boolean` | イベントの自動トラッキング。 |
| `keepData` | `Boolean` | 送信後、ピクセルは自動的にキャッシュからすべてのデータを削除し、それ以上アクセスできなくなります。データをアクセス可能に保つためには、これを`true`に構成します。デフォルトは`false`です。 |

### 標準

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `execCDB` | `Boolean` | Cross Device Bridgeを有効または無効にします。 |
| `useCDBCache` | `Boolean` | Cross Device Bridgeのイメージキャッシュを有効または無効にします。 |
| `sendViaServer.serverDomain` | `String` | サーバー間ライブラリがホストされているドメインを指定します。 |
| `sendViaServer.serverPath` | `String` | サーバー間ライブラリがあなたのサーバー上に保存されているパスを指定します。 |
| `sendViaServer.droppedRequests` | `Number` | ドロップされたリクエストの数。 |
| `sendViaServer.blacklist` | `String` | ピクセルによって破棄する必要がある特定のページリクエストを指定します。 |
| `requestQueue.ttl` | `Number` | リクエストがキューに残っていられる最大時間を指定します。 |
| `requestQueue.resendInterval` | `Number` | 再送信間隔。 |
| `requestQueue.size` | `Number` | キューに保存されるリクエストの最大数を定義します。 |
| `requestQueue.retries` | `Number` | 再試行の数。 |
| `requestQueue.retriesOption` | `Number` | 再試行オプション。 |
| `requestLimit.amount` | `Number` | 指定された時間内に許可されるリクエストの最大数。 |
| `requestLimit.duration` | `Number` | 最大数のリクエストを送信するための秒単位の時間間隔。 |
| `userIdentification.anonymousCookieName` | `String` | 匿名トラッキングクッキーの代替名。 |
| `userIdentification.anonymousOptIn` | `String` | デフォルトで匿名トラッキングを使用したい場合に有効にします。 |
| `userIdentification.suppressParameter` | `Array of Strings` | 抑制パラメータ。 |
| `userIdentification.temporarySessionId` | `String` | 一時的なセッションID。 |
| `userIdentification.saveTemporarySessionId` | `Boolean` | 一時的なセッションIDを保存します。 |

### ページ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `name` | `String` | デフォルトのページ命名を上書きします。 |
| `search` | `String` | 内部検索で使用される検索語。 |
| `numberSearchResults` | `Number` | 内部検索結果の数。 |
| `errorMessages` | `String` | エラーメッセージをトラックします。 |
| `paywall` | `Boolean` | 記事がペイウォールの後ろにある場合は、記事をマークします。 |
| `articleTitle` | `String` | 記事のタイトル。 |
| `contentTags` | `String` | 記事のタグ。 |
| `title` | `String` | ページのタイトル。 |
| `e.g. "overview"` | `String` | ページのタイプ。 |
| `e.g. "large"` | `String` | ページの長さ。 |
| `daysSincePublication` | `Number` | 公開からの日数。 |
| `testVariant` | `String` | テストバリアントの名前。 |
| `testExperiment` | `String` | テストの名前。 |
| `parameter` | `Object` | パラメータを使用して、分析データを自分のウェブサイト固有の情報やメトリクスでエンリッチすることができます。 |
| `Mappで"Content Groups"と呼ばれる` | `オブジェクト` | ページカテゴリー。 |
| `goal` | `オブジェクト` | ウェブサイトの目標を使用すると、すべての中心的な目標が分析とフィルタリングのためにすぐに利用可能になります。 |

### イベントパラメータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `eventName` | `文字列` | イベントの一意の識別子。 |
| `eventParameter` | `配列` | 特定の情報や/またはメトリクスで分析データをエンリッチするために使用されるパラメータ。パラメータを定義する際には構文ガイドラインに従ってください。  |
| `eventGoal` | `オブジェクト` | イベントに基づいたウェブサイトの目標を追跡するために必要です。ウェブサイトの目標は、ウェブサイトの成功を測定します。 |

### キャンペーン

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `campaignId` | `文字列` | メディアコード名とその値からなるキャンペーンID。これらは `=` で区切られます。 |
| `mediaCode` | `文字列の配列` | (`_cpromo`を上書き) メディアコードをキャンペーントラッキングのデータソースとして使用する場合、その名前を入力すると測定の精度が上がります。 |
| `oncePerSession` | `ブール値` | セッション内で各キャンペーンを一度だけ追跡します。 |
| `campaignParameter` | `オブジェクト` | キャンペーンパラメータは常に広告媒体を参照します。 |

### 顧客

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `customerId` | `文字列` | (`_ccustid`を上書き) ユーザーの一意の識別子。 |
| `emailRID` | `文字列` | ユーザーのメール受信者 `ID`。これはMapp Intelligenceとあなたのメールツールとの間のリンクとして機能します。 |
| `emailOptin` | `文字列` | ユーザーのメールオプトインステータス。 |
| `registrationEmail` | `文字列` | Mapp Engageでユーザーを識別するために使用されるメールアドレス。 |
| `registrationGroupId` | `文字列` | Mapp Engageでユーザーが新規登録する場合のグループ `ID` を提供します。 |
| `registrationMode` | `文字列` | マーケティング活動への登録に使用された登録方法を提供します。オプションには、`c` (CONFIRMED OPT IN)、`d` (DOUBLE OPT IN)、`o` (OPT IN)があります。 |
| `registrationFirstName` | `文字列` | Mapp Engageで使用するユーザーの名前。 |
| `registrationLastName` | `文字列` | Mapp Engageで使用するユーザーの姓。 |
| `undisclosed` | `文字列` | ユーザーの性別。オプションには、`u` (未公開)、`f` (女性)、`m` (男性)があります。 |
| `registrationTitle` | `文字列` | Mapp Engageで使用するユーザーのタイトル。 |
| `default` | `ブール値` | ユーザーが自分のデータの使用に同意したことを情報提供します。オプションには、`true` (ユーザー同意)、`false` (同意なし)があります。  |
| `customerCategory` | `オブジェクト` | カテゴリを使用して、顧客情報を追加のデータで豊かにします。カテゴリは `MIUserCategories` オブジェクト内で指定する必要があります。 |

### 注文

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `orderValue` | `文字列` | (`_ctotal`を上書き) 送料、税金などを含む/除く総注文価格。総注文価格を追跡する場合は、このプロパティを入力する必要があります。 |
| `order ID` | `文字列` | (`_corder`を上書き) 一意の注文番号。 |
| `orderCurrency` | `文字列` | (`_ccurrency`を上書き) 注文の通貨は `currency` プロパティで構成できます。値は `ISO` 標準に従ってMapp Intelligenceピクセルに渡す必要があります。 |
| `couponValue` | `数値` | (`_cpromo`を上書き) クーポンの値を含みます。顧客がクーポンで注文する場合にこのパラメータを使用します。 |
| `paymentMethod` | `文字列` | 注文の支払い方法を伝送します。 |
| `shippingService` | `文字列` | 注文の配送サービスを伝送します。 |
| `shippingSpeed` | `文字列` | 注文の配送速度を伝送します。 |
| `shippingCosts` | `数値` | (`_cship`を上書き) 注文の配送費を伝送します。 |
| `grossMargin` | `数値` | 注文のマージンまたはマークアップを伝送します。 |
| `orderStatus` | `文字列` | 注文の状況を伝送します。例えば、出荷済み、返品済みなど。 |
| `orderParameter` | `オブジェクト` | パラメータを使用して、自分のウェブサイト固有の情報や/またはメトリクスで分析データを豊かにします。 |

### セッション

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `visit` | `文字列` | セッションパラメータは常に完全なセッションを参照します。 |
| `visit` | `オブジェクト` | セッションパラメータは常に完全なセッションを参照します。 |

### 商品

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `productId` | `文字列の配列` | (`_cprod`を上書き) 商品の一意の識別子。 |
| `cost` | `数値の配列` | (`_cprice`を上書き) 商品のコスト。デフォルト: `0`。 |
| `quantity` | `数値の配列` | (`_cquan`を上書き) 利用可能な商品の数量。デフォルト: `0`。 |
| `soldOut` | `ブール値の配列` | 商品が売り切れているかどうかを示します。デフォルト: `false`。 |
| `productParameter` | `オブジェクトの配列` | 自分自身の特定の情報や/またはメトリクスで分析データをエンリッチするためのパラメータを使用します。 |
| `productCategory` | `オブジェクトの配列` | (`_ccat`を上書き) 商品を分類するためのカテゴリを使用します。カテゴリは `MIProductCategories` オブジェクト内で指定する必要があります。 |

