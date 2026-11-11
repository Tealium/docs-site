---
title: データレイヤーエンリッチメントについて
description: データレイヤーエンリッチメントは、顧客データプラットフォーム（CDP）の属性をタグ管理のデータレイヤーにインポートし、公開 API を通じて訪問プロファイルデータへのアクセスを提供します。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/about/
---
データレイヤーエンリッチメントには、次の 2 つのコンポーネントがあります。

* タグ管理の構成では、顧客データプラットフォーム（CDP）の[属性]()をデータレイヤーにインポートして Web サイト上で構成します。これらの属性をロードルール、拡張機能、タグで使用することで、訪問にパーソナライズされたエクスペリエンスを提供できます。
* サーバー側コンポーネントは、Data Layer Enrichment API と Profile Definition API を通じて訪問プロファイルデータへのアクセスを提供します。

## 要件

データレイヤーエンリッチメントには、次のものが必要です。

* 訪問および訪問属性が定義された有効な **CDP** プロファイル。
* 有効な **Tealium Collect タグ**。
* `utag.js` バージョン 4.27 以降。`utag.js` テンプレートの更新について詳しくは、ナレッジベースの記事「[utag.js を最新バージョンに更新するためのベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)」を参照してください。

## 仕組み

### タグ管理のデータレイヤーエンリッチメントプロファイル

タグ管理の構成により、iQ プロファイルが対応する CDP プロファイルにリンクされます。タグ管理でデータレイヤーエンリッチメントプロファイルを構成すると、データレイヤー画面の変数リストに AudienceStream Attribute という新しい種類のデータレイヤー変数が表示されます。CDP プロファイルの訪問および訪問属性がインポートされ、ほかのデータレイヤー変数と同様に使用できるようになります。

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-audiencestreamattributes.png)

これらの属性は、[Tealium Collect タグ](https://docs.tealium.com/tealium-collect-tag/)を使用して、リアルタイムの顧客データとしてユニバーサルデータオブジェクト（UDO）に構成されます。

訪問がサイトに初めてアクセスすると、Tealium Collect タグが CDP にリクエストを送信し、最新の訪問プロファイル属性を取得します。取得したデータは、今後使用するためにブラウザーのローカル保存に保存されます。

2 回目のトラッキングコールでは、CDP 属性が UDO に格納され、それらを使用するように構成されたロードルール、拡張機能、またはタグに適用されます。


<blockquote>
タグは非同期で読み込まれるため、直近に取得された属性セットは、現在のページのイベントではなく、後続のトラッキングコールで使用できます。
</blockquote>


#### 同一オリジンポリシー

訪問データは、セキュリティ上の理由から[同一オリジンポリシー](https://en.wikipedia.org/wiki/Same-origin_policy)に従う `localStorage` を使用してブラウザーに保存される点に注意してください。つまり、データレイヤーエンリッチメントのデータは、異なる `http` プロトコル間やサブドメイン間では維持されません。

たとえば、`www.tealium.com` のページから `secure.tealium.com` のページに移動すると、`localStorage` に保存されたデータレイヤーエンリッチメントのデータは、新しいサブドメインには引き継がれません。そのため、ユーザーがサブドメインまたはプロトコルを変更した場合は、`localStorage` にデータを再構成するために新しいデータレイヤーエンリッチメントコールを実行する必要があり、そのデータは後続のトラッキングコールまで利用できない場合があります。

### サーバー側データレイヤーエンリッチメント

サーバー側コンポーネントは、次の 2 つの公開エンドポイントを通じて訪問プロファイルデータを公開します。

* Data Layer Enrichment API：フィルタリングせずに訪問プロファイル全体を返します。
* Profile Definition API：バッジとオーディエンスの定義を返します。

サーバー側コンポーネントが無効になっている場合、どちらの API も `404` レスポンスを返し、これらのエンドポイントから訪問データを利用することはできません。

また、ドメイン許可リストを作成して、TAPID Cookie を使用して訪問プロファイルにアクセスできるドメインを制限することもできます。詳しくは、[ドメイン許可リスト](https://docs.tealium.com/enable-data-layer-enrichment/#domain-allow-list)を参照してください。

## 次のステップ

* [サーバー側データレイヤーエンリッチメントを有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)
* [タグ管理でデータレイヤーエンリッチメントを構成する](https://docs.tealium.com/configure-data-layer-enrichment-iq/)