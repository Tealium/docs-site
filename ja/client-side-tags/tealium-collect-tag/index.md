---
title: Tealium Collect タグ構成ガイド
description: Tealium Collect タグは、Tealium EventStream および AudienceStream の主要なデータ収集タグです。この記事では、iQ タグ管理プロファイルに Tealium Collect タグを追加および構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tealium-collect-tag/
---
## 要件

* このタグをアカウントで有効にするには、アカウントマネージャーに連絡してください。

## 動作方法

Tealium Collect タグは、ページからの事前定義されたデータと動的データの両方をキャプチャします。このタグにはマッピングが必要なく、`utag.data`に構成されているすべてのデータやトラッキングコールに渡されたデータを自動的に送信します。

収集される変数の完全なリストについては、[eventstore-data-guide](https://docs.tealium.com/eventstore-data-guide/) を参照してください。このデータが EventDB でどのように表示されるかについては、[eventdb-data-guide](https://docs.tealium.com/eventdb-data-guide/) を参照してください。

Tealium Collect タグからの受信データを確認するには、[Live Events](https://docs.tealium.com/about-live-events/)を参照してください。

Tealium Collect タグは以下の機能と共に使用します：

* **EventStream でピクセルリクエストを削減**  
  このタグを EventStream およびイベントフィードと共に使用し、クライアントサイドタグをサーバーサイドコネクター、例えば [Webhook connector](https://docs.tealium.com/about-webhook-connectors/) へ移行します。
* **AudienceStream**  
  このタグを AudienceStream と共に使用して、訪問を識別し、アクションを起こします。
* **DataAccess**  
  このタグからのイベントデータは DataAccess でも利用可能で、お好みのビジネスインテリジェンス（BI）ツールを使用して分析できます。
* **データレイヤーをエンリッチする**  
  AudienceStream からの訪問属性をデータレイヤーに追加するデータエンリッチメント構成を使用します。  
  詳細については、[configure-data-layer-enrichment-iq](https://docs.tealium.com/configure-data-layer-enrichment-iq/) を参照してください。

## タグのヒント

* このタグは、初期ページロード時または `utag.view()` や `utag.link()` に渡された任意のデータオブジェクトに対して `utag.data` 内のすべてのデータを自動的に送信します。
* ネットワークリクエストを検査するためにプロキシツールを使用する場合は、GETではなく `POST` メソッドを探します。
* **Tealium Profile** フィールドに値を指定するのは、**Tealium Collect Endpoint** フィールドが空白で、サーバーサイドデータ収集プロファイルが現在のプロファイルと異なる場合のみです。

## ベストプラクティス

実装において以下のベストプラクティスを適用してください：

* サードパーティのクライアントサイドタグを優先するために、Tealium Collect タグをタグリストの最後に配置し、他のタグが先に実行されるようにします。
* プロファイルに Tealium Collect タグのインスタンスを複数追加しないでください。
* uTag Loader テンプレートの最新バージョンを使用してください。詳細については、[version-4-50](https://docs.tealium.com/version-4-50/) を参照してください。

## タグ構成

まず、タグマーケットプレースにアクセスして Tealium Collect タグを追加します。詳細については、[Manage tags](https://docs.tealium.com/manage-tags/#add-a-tag)を参照してください。

タグを追加した後、次の構成を構成します：

* **タイトル**
  * このタグのタイトルを入力します。
  * デフォルト：`Tealium Collect`。
* **Tealium Collect エンドポイント**（オプション）
  * カスタムデータ収集エンドポイントでの使用のみです。
  * このフィールドに入力されたカスタムURLは、指定されていない限り自動的にHTTPSになります。
  * デフォルト：構成されていません。
* **データレイヤーエンリッチメント頻度**  
  * AudienceStream データレイヤーエンリッチメントを有効にします。
  * AudienceStream データでデータレイヤーをエンリッチする頻度を選択します。  
    * **なし**：（デフォルト）エンリッチメントは行われません。
    * **まれ**：（推奨）セッションごとに一度エンリッチメントが行われます。
    * **頻繁**：各ページロードごとにエンリッチメントが行われます。
* **Tealium Collect プロファイル**（オプション）  
  * 既存のデータ収集エンドポイント、例えばサイトからデータを受け取る AudienceStream プロファイルを上書きするために使用します。
  * **Tealium Collect エンドポイント** フィールドが空白で、AudienceStream のデータ収集プロファイルが現在のプロファイルと異なる場合にのみ、このフィールドに値を指定します。
  * デフォルト：構成されていません。
* **Tealium データソースキー**  
  * （オプション）Customer Data Hub を通じて追跡しているデータソースの一意の識別子です。
  * デフォルト：構成されていません。
* **Tealium 収集地域**
  * データ収集サーバーの地理的位置です。
  * デフォルト：グローバル（推奨）。
  * どれを選択すべきかわからない場合は、アカウントマネージャーに連絡してください。
* **サンプルサイズ**（オプション）  
  * デフォルト：100%（推奨）。
  * 高トラフィックサイトの試用中に訪問の小さな割合にデータ収集を制限するためにこのオプションを使用します。
* **SendBeacon の使用**
  * `navigator.sendBeacon()` を使用してトラッキングコールを送信するには `true` に構成します。
  * 従来のブラウザメソッド `XMLHttpRequest` を使用してトラッキングコールを送信するには `false` に構成します。
  * SendBeacon は少量のデータに適しており、ほとんどのブラウザでデータサイズの制限は64Kbです。詳細については、[Navigator:sendBeacon() method](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)を参照してください。
  * デフォルト：`true`。
* **HTTP API エンドポイントの使用**
  * Tealium Collect エンドポイントの代わりに [HTTP API endpoint](https://docs.tealium.com/platforms/http-api/endpoint-spec/) を使用するには true に構成します。
  * デフォルト：`false`。
* **Visitor Service Override**
  * データレイヤーエンリッチメントのために Tealium AudienceStream から訪問プロファイルデータを取得するドメインを指定します。
  * デフォルト値を上書きするカスタムドメインを入力します。
  * この値は通常、`visitor-service.yourdomain.com` のようなファーストパーティドメインに構成されます。
* **Tealium Cookie ドメイン**（オプション）
  * Tealium 匿名 ID（TAPID cookie）を構成するドメインです。
  * デフォルト値を上書きするカスタムドメインを入力します。
  * このオプションは、[first-party domains feature](https://docs.tealium.com/about-first-party-domains/)が有効になっており、Tealium Collect タグがそのファーストパーティドメインにある場合にのみ適用されます。
* **Tealium Cookie 有効期限**（オプション）
  * TAPID cookie の有効期限（秒単位）です。
* Tealium Collect エンドポイントに送信するデータを次の構成を使用してフィルタリングします：
  * **UDO 変数の送信**：デフォルトは `true` です。
  * **Cookie 値の送信**：デフォルトは `true` です。
  * **Meta 値の送信**：デフォルトは `true` です。
  * **QP 値の送信**：デフォルトは `true` です。
  * **セッション保存変数の送信**：デフォルトは `false` です。
  * **ローカル保存変数の送信**：デフォルトは `false` です。

## 高度な構成

データレイヤーエンリッチメントのために Tealium 訪問サービスエンドポイントのファーストパーティ CNAME を使用する場合、Tealium Collect タグにスコープされた JavaScript Code 拡張機能を使用して URL を次のコードで上書きします：

```js
u.visitor_service_override = "https://visitor-service.example.co.uk";
```

## ロードルール

**すべてのページとイベント**のロードルールを使用することがベストプラクティスです。このタグをすべてのページでロードすることで、すべてのイベントがサーバーサイドで追跡され、イベントデータとオーディエンスデータの完全な活用が可能になります。このタグにカスタムロードルールを使用すると、サーバーサイドで活用できるデータが制限されるため、推奨されません。

### トレースとの連携

より制限的なロードルールを使用していて、トレースツールでセッションを終了できないことに気付いた場合、特別なイベントをトリガーするためにカスタムロードルールが必要です。

次のロードルールを作成し、Tealium Collect タグに割り当てます。

```
ut.event equals (ignore case) kill_visitor_session
```

![](https://docs.tealium.com/images/client-side-tags/tealium-collect-load-rule-for-trace.png)


## モバイルでの実装

[Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/install/)または[Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/install/)を使用するデプロイメントでは、以下の点に注意してください：

* デフォルトの[モバイル公開構成](https://docs.tealium.com/create-mobile-profile/#configure-mobile-settings)では、ネイティブモバイルTealium Collectサービスがデフォルトで有効になっています。
モバイル用の[native Collectモジュール](https://docs.tealium.com/platforms/getting-started-mobile/server-side/#native-module)について詳しく学びましょう。
* モバイル用の[Tag ManagementモジュールとTealium Collectタグ](https://docs.tealium.com/platforms/getting-started-mobile/server-side/#javascript-tag)を使用する場合は、[モバイル公開構成](https://docs.tealium.com/create-mobile-profile/#configure-mobile-settings)の**Tealium Collect**オプションがオフになっていることを確認してください。これにより、重複したトラッキングを避けることができます。

## クッキー

Tealium Collectタグは以下のクッキーを作成します：

* `utag_main_v_id`: データプライバシーおよび同意ルールに準拠するための一意で部分的にランダムな識別子。[`always_set_v_id` utag構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)が`true`に構成されている場合、`utag.js`バージョン4.50以降でこのクッキーが作成されます。それ以外の場合は、以下の条件でクッキーが作成されます：
    * `suppress_v_id` Collect構成が`false`に構成されているか、構成されていない。
    * クッキーの値がまだ構成されていない。
    このクッキーについての詳細は、[`utag.js`リリースノートバージョン4.50](https://docs.tealium.com/platforms/javascript/version-4-50/)を参照してください。
* `utag_main_dc_group`: **サンプルサイズ**構成で使用するランダムな数値。
* `utag_main_dc_region`: 訪問セッションが保存されるAudienceStream地域。このクッキーは、[データレイヤーのエンリッチメント](https://docs.tealium.com/data-layer-enrichment/)のエンドポイントを決定するために使用されます。

### レガシークッキー

互換性のため、Tealium Collectタグは以下のレガシークッキーを作成します：

* `utag_main_dc_visit`: Tealium Collectタグが発火したセッションの数。
* `utag_main_dc_event`: Tealium Collectタグが発火したイベントの数。

これらのクッキーについての詳細は、[データレイヤー：クッキー](https://docs.tealium.com/platforms/javascript/data-layer/#cookies)を参照してください。