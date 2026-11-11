---
title: Tealium Collectタグ構成ガイド
description: Tealium Collectタグは、イベントストリーミングおよび顧客データプラットフォーム（CDP）向けの主要なデータ収集タグです。この記事では、タグ管理プロファイルにTealium Collectタグを追加して構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tealium-collect-tag/
---
## 要件

* このタグをアカウントで有効にするには、アカウントマネージャーにお問い合わせください。

## 仕組み

Tealium Collectタグは、ページから事前定義されたデータと動的データを組み合わせて取得します。このタグにはマッピングは必要ありません。`utag.data`に構成されているすべてのデータ、またはトラッキング呼び出しに渡されたすべてのデータが自動的に送信されます。

収集される変数の完全なリストについては、[eventstore-data-guide](https://docs.tealium.com/eventstore-data-guide/)を参照してください。このデータがEventDBにどのように表示されるかについては、[eventdb-data-guide](https://docs.tealium.com/eventdb-data-guide/)を参照してください。

Tealium Collectタグから受信するデータを確認するには、[ライブイベント](https://docs.tealium.com/about-live-events/)を参照してください。

Tealium Collectタグは、次の機能とともに使用します。

* **イベントストリーミングによるピクセルリクエストの削減**  
このタグをイベントストリーミングおよびイベントフィードとともに使用して、クライアントサイドタグを[Webhookコネクタ](https://docs.tealium.com/about-webhook-connectors/)などのサーバーサイドコネクタに移行します。
* **CDP**  
このタグをCDPとともに使用して、訪問を識別し、訪問に対してアクションを実行します。
* **DataAccess**  
このタグから取得したイベントデータをDataAccessでも利用できるようにし、任意のビジネスインテリジェンス（BI）ツールを使用して分析できます。
* **データレイヤーのエンリッチメント**  
データエンリッチメント構成を使用して、CDPの訪問および訪問属性をデータレイヤーに追加します。  
詳細については、[configure-data-layer-enrichment-iq](https://docs.tealium.com/configure-data-layer-enrichment-iq/)を参照してください。

## タグに関するヒント

* このタグは、最初のページ読み込み時に`utag.data`内のすべてのデータを自動的に送信します。また、`utag.view()`または`utag.link()`に渡されたすべてのデータオブジェクトも自動的に送信します。
* プロキシツールを使用してネットワークリクエストを調査する場合は、GETではなく`POST`メソッドを探してください。
* **Tealium Collect Endpoint**フィールドが空で、サーバーサイドのデータ収集プロファイルが現在のプロファイルと異なる場合にのみ、**Tealium Profile**フィールドに値を指定してください。

## ベストプラクティス

実装には、次のベストプラクティスを適用してください。

* サードパーティのクライアントサイドタグを優先するには、それらが先に実行されるように、タグリストの最後にTealium Collectタグを配置します。
* プロファイルにTealium Collectタグのインスタンスを複数追加しないでください。
* 最新バージョンのuTag Loaderテンプレートを使用してください。詳細については、[version-4-50](https://docs.tealium.com/version-4-50/)を参照してください。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の構成を行います。

* **タイトル**
  * このタグのタイトルを入力します。
  * デフォルト：`Tealium Collect`
* **Tealium Collectエンドポイント**（オプション）
  * カスタムデータ収集エンドポイントでのみ使用します。
  * このフィールドに入力したカスタムURLは、別途指定しない限り、自動的にHTTPSを使用します。
  * デフォルト：未構成
* **データレイヤーエンリッチメントの頻度**  
  * CDPデータレイヤーのエンリッチメントを有効にします。
  * CDPデータでデータレイヤーをエンリッチする頻度を選択します。  
    * **なし**：（デフォルト）エンリッチメントは実行されません。
    * **低頻度**：（推奨）セッションごとに1回エンリッチメントが実行されます。
    * **高頻度**：ページが読み込まれるたびにエンリッチメントが実行されます。
* **Tealium Collectプロファイル**（オプション）  
  * サイトからデータを受信するCDPプロファイルなど、既存のデータ収集エンドポイントを上書きするために使用します。
  * **Tealium Collect Endpoint**フィールドが空で、CDPのデータ収集プロファイルが現在のプロファイルと異なる場合にのみ、このフィールドに値を指定してください。
  * デフォルト：未構成
* **Tealiumデータソースキー**  
  * （オプション）Customer Data Hubを通じてトラッキングするデータソースの一意の識別子です。
  * デフォルト：未構成
* **Tealium収集リージョン**
  * データ収集サーバーの地理的な場所です。
  * デフォルト：グローバル（推奨）
  * どれを選択すべきかわからない場合は、アカウントマネージャーにお問い合わせください。
* **サンプルサイズ**（オプション）  
  * デフォルト：100%（推奨）
  * トラフィック量の多いサイトでのトライアル中にこのオプションを使用すると、データ収集を訪問の一部に限定できます。
* **SendBeaconを使用**
  * `navigator.sendBeacon()`を使用してトラッキング呼び出しを送信するには、`true`に構成します。
  * 従来のブラウザーメソッドである`XMLHttpRequest`を使用してトラッキング呼び出しを送信するには、`false`に構成します。
  * SendBeaconは少量のデータを対象としており、ほとんどのブラウザーでデータサイズが64Kbに制限されています。詳細については、[Navigator: sendBeacon()メソッド](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)を参照してください。
  * デフォルト：`true`
* **HTTP APIエンドポイントを使用**
  * Tealium Collectエンドポイントの代わりに[HTTP APIエンドポイント](https://docs.tealium.com/platforms/http-api/endpoint-spec/)を使用するには、trueに構成します。
  * デフォルト：`false`
* **訪問サービスの上書き**
  * データレイヤーのエンリッチメント用に、Tealium CDPから訪問プロファイルデータを取得する際に使用するドメインを指定します。
  * デフォルト値を上書きするには、カスタムドメインを入力します。
  * 通常、この値には`visitor-service.yourdomain.com`などのファーストパーティドメインを構成します。
* **Tealium Cookieドメイン**（オプション）
  * Tealium匿名ID（TAPID Cookie）の構成に使用するドメインです。
  * デフォルト値を上書きするには、カスタムドメインを入力します。
  * 通常、この値には`.yourdomain.com`などのファーストパーティドメインを構成します。
  * このオプションは、[ファーストパーティドメイン機能](https://docs.tealium.com/about-first-party-domains/)が有効で、Tealium Collectタグがそのファーストパーティドメイン上にある場合にのみ適用されます。
* **Tealium Cookieの有効期限**（オプション）
  * TAPID Cookieの有効期限（秒単位）です。
* 次の構成を使用して、Tealium Collectエンドポイントに送信されるデータをフィルタリングします。
  * **UDO変数を送信**：デフォルトは`true`です。
  * **Cookie値を送信**：デフォルトは`true`です。
  * **メタ値を送信**：デフォルトは`true`です。
  * **QP値を送信**：デフォルトは`true`です。
  * **セッション保存変数を送信**：デフォルトは`false`です。
  * **LocalStorage変数を送信**：デフォルトは`false`です。

## 詳細構成

データレイヤーのエンリッチメントに使用するTealium訪問サービスエンドポイントのファーストパーティCNAMEについては、Tealium Collectタグをスコープに構成したJavaScriptコード拡張機能を使用し、次のコードでURLを上書きします。

```js
u.visitor_service_override = "https://visitor-service.example.co.uk";
```

## 読み込みルール

ベストプラクティスは、**すべてのページとイベント**読み込みルールを使用することです。このタグをすべてのページで読み込むことで、すべてのイベントがサーバーサイドでトラッキングされ、イベントデータとオーディエンスデータの両方を完全にアクティベーションできます。このタグにカスタム読み込みルールを使用すると、サーバーサイドでアクティベーションできるデータが制限されるため、推奨されません。

### トレースの操作

より制限の厳しい読み込みルールを使用していて、トレースツールでセッションを終了できない場合は、トレースによってトリガーされる特別なイベントを許可するためのカスタム読み込みルールが必要です。

次の読み込みルールを作成し、Tealium Collectタグに割り当てます。

```
ut.event equals (ignore case) kill_visitor_session
```

![](https://docs.tealium.com/images/client-side-tags/tealium-collect-load-rule-for-trace.png)

## モバイルでの実装

[Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/install/)または[Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/install/)を使用するデプロイでは、次の点に注意してください。

* デフォルトの[モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/#configure-mobile-settings)では、ネイティブモバイルTealium Collectサービスがデフォルトで有効になっています。  
[モバイル向けネイティブCollectモジュール](https://docs.tealium.com/platforms/getting-started-mobile/server-side/#native-module)の詳細をご覧ください。
* [モバイル向けタグ管理モジュールでTealium Collectタグ](https://docs.tealium.com/platforms/getting-started-mobile/server-side/#javascript-tag)を使用する場合は、トラッキングの重複を避けるため、[モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/#configure-mobile-settings)の**Tealium Collect**オプションがオフになっていることを確認してください。
## Cookie

Tealium Collectタグは、以下のCookieを作成します。

* `utag_main_v_id`：データプライバシーおよび同意に関するルールへの準拠を確保するための、一部がランダムな一意の識別子です。[`always_set_v_id` utag構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)が`true`に構成されている場合、Collectタグは`utag.js`バージョン4.50以降でこのCookieを作成します。それ以外の場合、Collectタグは以下の条件でCookieを作成します。
    * Collectの`suppress_v_id`構成が`false`に構成されているか、構成されていない。
    * Cookieの値がまだ構成されていない。  
    このCookieの詳細については、[`utag.js`リリースノート（バージョン4.50）](https://docs.tealium.com/platforms/javascript/version-4-50/)を参照してください。
* `utag_main_dc_group`：**サンプルサイズ**構成で使用するランダムな数値です。
* `utag_main_dc_region`：訪問セッションが保存されるCDPリージョンです。このCookieは、[データレイヤーエンリッチメント](https://docs.tealium.com/data-layer-enrichment/)のエンドポイントを決定するために使用されます。

### レガシーCookie

互換性を維持するため、Tealium Collectタグは以下のレガシーCookieを作成します。

* `utag_main_dc_visit`：Tealium Collectタグが発火したセッションの数です。
* `utag_main_dc_event`：Tealium Collectタグが発火したイベントの数です。

これらのCookieの詳細については、[データレイヤー：Cookie](https://docs.tealium.com/platforms/javascript/data-layer/#cookies)を参照してください。