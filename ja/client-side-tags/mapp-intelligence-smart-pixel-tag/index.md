---
title: Mapp Intelligence Smart Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでMapp Intelligence Smart Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mapp-intelligence-smart-pixel-tag/
---
Mapp Intelligenceは、アナリストやマーケターに、Webサイトの利用状況に関する詳細な分析と有益なインサイトを提供し、顧客への理解を深めます。適切なタイミングとチャネルで、対象オーディエンスに適切なメッセージを届けるために必要な情報を提供します。

## タグに関するヒント

* マッピングに追加した値は、`wt`オブジェクトに挿入されます（たとえば、`contentId`や`internalSearch`を構成するにはマッピングを使用します）。
* フォームのHTML IDに値を構成すると、`formTrackInstall()`関数が自動的にトリガーされます。
* `utag.link()`関数を呼び出してイベントをトラッキングします。
* 注文の値を自動的に構成するには、E-Commerce Extensionが必要です。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の構成を行います。

* **ライブラリバージョン**：使用するライブラリのバージョンを選択します。
* **トラックID**：トラックIDを使用して、リクエストをアカウントに割り当てます。トラックIDは、Mappの**システム構成**にある**Mapp Q3 > Configuration > System Configuration > Data Collection**で確認できます。複数のアカウントで同じ情報を記録するには、トラックIDをカンマで区切ります。
* **トラックドメイン**：アカウントマネージャーから提供されたMapp Intelligenceのトラックドメインを入力します。
* **ドメイン**：Smart Pixelのドメインをリファラーから除外するデフォルトの動作を上書きします。
* **Cookieの処理**：Cookieをブラウザーとサーバーのどちらで構成するかを指定します。サーバー側Cookieは、Webドメインと一致するカスタムトラックドメインを使用する場合にのみ推奨されます。これにより、ファーストパーティートラッキングと最高品質のデータが実現します。
* **セキュアCookie**：このオプションを有効にすると、すべてのMapp Intelligence CookieにSecure属性が追加されます。これにより、セキュアCookieはHTTPS経由でのみ送信されます。
* **オプトアウト名**：オプトアウトCookieの代替名を指定します。
* **リクエストの難読化**：すべてのトラッキングリクエストを難読化し、広告ブロッカーがMapp Intelligenceのトラッキングリクエストを識別してブロックすることを困難にします。このオプションはデフォルトでは無効ですが、`requestObfuscation`キーを使用して有効にできます。
* **旧EverIdの強制使用**：旧Mapp Intelligence `EverID`を強制的に使用します。
* **商品の統合**：必要に応じて、同じ商品IDを持つ複数の商品の統合を無効にします。
* **サーバー間トラッキング機能のサポート**：サーバー間トラッキング機能を有効にします。
* **デフォルトページ名にハッシュを使用**：デフォルトのページ名にURLハッシュを含めます。
* **デフォルトページ名にパラメータを使用**：デフォルトのページ名に特定のURLパラメータを含めます。
* **リクエストキュー**：すべてのトラッキングリクエストに対してオフラインキューを有効にします。
* **リクエスト制限**：リクエスト数の上限を構成して、大量のリクエストによってエラーが発生するリスクを軽減します。
* **ユーザー識別**：匿名トラッキングを有効にします。
* **自動トラッキングを有効化**：タグがトリガーされたときに、`wtSmart.track()`関数による自動トラッキングを有効にします。
* **ページデータのみの自動トラッキングを有効化**：ページデータに対して、`wtSmart.trackPage()`関数による自動トラッキングを有効にします。
* **イベントデータのみの自動トラッキングを有効化**：イベントデータに対して、`wtSmart.trackAction()`関数による自動トラッキングを有効にします。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 構成

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `trackId` | `String` | トラックID。 |
| `trackDomain` | `String` | トラックドメイン。 |
| `domain` | `Array of Strings` | ドメイン。 |
| `cookie` | `String` | Cookie構成。 |
| `secureCookie` | `Boolean` | セキュアCookie。 |
| `optOutName` | `String` | オプトアウトCookieの代替名。 |
| `requestObfuscation` | `Boolean` | リクエストの難読化。 |
| `forceOldEverId` | `Boolean` | 旧`EverID`を強制的に使用します。 |
| `productMerge` | `String` | 商品の統合。 |
| `sendViaServer.activated` | `Boolean` | サーバー間トラッキング。 |
| `useHashForDefaultPageName` | `Boolean` | デフォルトのページ名にハッシュを使用します。 |
| `useParamsForDefaultPageName` | `Array of Strings` | デフォルトのページ名にパラメータを使用します。 |
| `requestQueue.activated` | `Boolean` | トラッキングリクエストのオフラインキュー。 |
| `requestLimit` | `Boolean` | リクエスト制限。 |
| `userIdentification.enableAnonymousFunction` | `Boolean` | 匿名トラッキング。 |
| `autoTracking` | `Boolean` | 自動トラッキング。 |
| `autoTrackingPage` | `Boolean` | ページの自動トラッキング。 |
| `autoTrackingEvent` | `Boolean` | イベントの自動トラッキング。 |
| `keepData` | `Boolean` | 送信後、ピクセルはキャッシュからすべてのデータを自動的に削除し、以後アクセスできなくなります。データに引き続きアクセスできるようにするには、これを`true`に構成します。デフォルト：`false`。 |

### 標準

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `execCDB` | `Boolean` | Cross Device Bridgeを有効または無効にします。 |
| `useCDBCache` | `Boolean` | Cross Device Bridgeの画像キャッシュを有効または無効にします。 |
| `sendViaServer.serverDomain` | `String` | サーバー間ライブラリがホストされているドメインを指定します。 |
| `sendViaServer.serverPath` | `String` | サーバー上でサーバー間ライブラリが保存されているパスを指定します。 |
| `sendViaServer.droppedRequests` | `Number` | 破棄されたリクエストの数。 |
| `sendViaServer.blacklist` | `String` | ピクセルによって破棄する必要がある特定のページリクエストを指定します。 |
| `requestQueue.ttl` | `Number` | リクエストが削除されるまでキューに保持できる最長時間を指定します。 |
| `requestQueue.resendInterval` | `Number` | 再送間隔。 |
| `requestQueue.size` | `Number` | キューに保存するリクエストの最大数を定義します。 |
| `requestQueue.retries` | `Number` | 再試行回数。 |
| `requestQueue.retriesOption` | `Number` | 再試行オプション。 |
| `requestLimit.amount` | `Number` | 指定された期間内に許可されるリクエストの最大数。 |
| `requestLimit.duration` | `Number` | 最大数のリクエストを送信する時間間隔（秒）。 |
| `userIdentification.anonymousCookieName` | `String` | 匿名トラッキングCookieの代替名。 |
| `userIdentification.anonymousOptIn` | `String` | 匿名トラッキングをデフォルトで使用する場合は有効にします。 |
| `userIdentification.suppressParameter` | `Array of Strings` | 抑制するパラメータ。 |
| `userIdentification.temporarySessionId` | `String` | 一時セッションID。 |
| `userIdentification.saveTemporarySessionId` | `Boolean` | 一時セッションIDを保存します。 |
### ページ

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `name` | `String` | デフォルトのページ名を上書きします。 |
| `search` | `String` | 内部検索で使用される検索語句です。 |
| `numberSearchResults` | `Number` | 内部検索結果の件数です。 |
| `errorMessages` | `String` | エラーメッセージを追跡します。 |
| `paywall` | `Boolean` | 記事がペイウォールの内側にある場合、その記事をマークします。 |
| `articleTitle` | `String` | 記事のタイトルです。 |
| `contentTags` | `String` | 記事のタグです。 |
| `title` | `String` | ページのタイトルです。 |
| `e.g. "overview"` | `String` | ページの種類です。 |
| `e.g. "large"` | `String` | ページの長さです。 |
| `daysSincePublication` | `Number` | 公開からの経過日数です。 |
| `testVariant` | `String` | テストバリアントの名前です。 |
| `testExperiment` | `String` | テストの名前です。 |
| `parameter` | `Object` | パラメーターを使用して、Webサイト固有の情報や指標を分析データに追加できます。 |
| `called "Content Groups" in Mapp` | `Object` | ページのカテゴリーです。 |
| `goal` | `Object` | Webサイト目標を使用すると、すべての主要な目標を分析やフィルタリングですぐに利用できます。 |

### イベントパラメーター

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `eventName` | `String` | イベントを一意に識別する識別子です。 |
| `eventParameter` | `Array` | 特定の情報や指標を分析データに追加するために使用するパラメーターです。パラメーターを定義する際は、構文ガイドラインに従ってください。 |
| `eventGoal` | `Object` | イベントに基づいてWebサイト目標を追跡するために必要です。Webサイト目標は、Webサイトの成果を測定します。 |

### キャンペーン

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `campaignId` | `String` | メディアコード名とその値を `=` で区切って構成されるキャンペーンIDです。 |
| `mediaCode` | `Array of Strings` | （`_cpromo` を上書きします）キャンペーントラッキングのデータソースとしてメディアコードを使用する場合、その名前を入力することで測定精度を高められます。 |
| `oncePerSession` | `Boolean` | 各キャンペーンを1回のセッションにつき一度だけ追跡します。 |
| `campaignParameter` | `Object` | キャンペーンパラメーターは、常に広告媒体を参照します。 |

### 顧客

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `customerId` | `String` | （`_ccustid` を上書きします）ユーザーの一意の識別子です。 |
| `emailRID` | `String` | ユーザーのメール受信者 `ID` です。Mapp Intelligenceとメールツールを連携するために使用されます。 |
| `emailOptin` | `String` | ユーザーのメールオプトインステータスです。 |
| `registrationEmail` | `String` | Mapp Engageでユーザーを識別するために使用するメールアドレスです。 |
| `registrationGroupId` | `String` | Mapp Engageでユーザーを新規登録する場合は、グループ `ID` を指定します。 |
| `registrationMode` | `String` | マーケティング活動への登録に使用した登録方法を指定します。オプションには、`c`（確認済みオプトイン）、`d`（ダブルオプトイン）、`o`（オプトイン）があります。 |
| `registrationFirstName` | `String` | Mapp Engageで使用するユーザーの名です。 |
| `registrationLastName` | `String` | Mapp Engageで使用するユーザーの姓です。 |
| `undisclosed` | `String` | ユーザーの性別です。オプションには、`u`（非開示）、`f`（女性）、`m`（男性）があります。 |
| `registrationTitle` | `String` | Mapp Engageで使用するユーザーの敬称です。 |
| `default` | `Boolean` | ユーザーが自身のデータの使用に同意したかどうかを示す情報を指定します。オプションには、`true`（ユーザーが同意）、`false`（同意なし）があります。 |
| `customerCategory` | `Object` | カテゴリーを使用して、顧客情報に追加データをエンリッチメントします。カテゴリーは `MIUserCategories` オブジェクト内で指定する必要があります。 |

### 注文

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `orderValue` | `String` | （`_ctotal` を上書きします）送料、税金などを含む、または含まない注文総額です。注文総額を追跡する場合は、このプロパティを入力する必要があります。 |
| `order ID` | `String` | （`_corder` を上書きします）一意の注文番号です。 |
| `orderCurrency` | `String` | （`_ccurrency` を上書きします）注文の通貨は、プロパティ `currency` で構成できます。値は `ISO` 規格に従ってMapp Intelligenceピクセルに渡す必要があります。 |
| `couponValue` | `Number` | （`_cpromo` を上書きします）クーポンの金額を格納します。顧客がクーポンを使用して注文する場合に、このパラメーターを使用します。 |
| `paymentMethod` | `String` | 注文の支払い方法を送信します。 |
| `shippingService` | `String` | 注文の配送サービスを送信します。 |
| `shippingSpeed` | `String` | 注文の配送速度を送信します。 |
| `shippingCosts` | `Number` | （`_cship` を上書きします）注文の送料を送信します。 |
| `grossMargin` | `Number` | 注文のマージンまたは値入額を送信します。 |
| `orderStatus` | `String` | 注文のステータスを送信します。たとえば、発送済み、返品済みなどです。 |
| `orderParameter` | `Object` | パラメーターを使用して、Webサイト固有の情報や指標を分析データに追加します。 |

### セッション

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `visit` | `String` | セッションパラメーターは、常にセッション全体を参照します。 |
| `visit` | `Object` | セッションパラメーターは、常にセッション全体を参照します。 |

### 商品

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `productId` | `Array of Strings` | （`_cprod` を上書きします）商品の一意の識別子です。 |
| `cost` | `Array of Numbers` | （`_cprice` を上書きします）商品の価格です。デフォルト：`0`。 |
| `quantity` | `Array of Numbers` | （`_cquan` を上書きします）利用可能な商品の数量です。デフォルト：`0`。 |
| `soldOut` | `Array of Booleans` | 商品が売り切れているかどうかを示します。デフォルト：`false`。 |
| `productParameter` | `Array of Objects` | パラメーターを使用して、独自の情報や指標を分析データに追加します。 |
| `productCategory` | `Array of Objects` | （`_ccat` を上書きします）カテゴリーを使用して商品を分類します。カテゴリーは `MIProductCategories` オブジェクト内で指定する必要があります。 |