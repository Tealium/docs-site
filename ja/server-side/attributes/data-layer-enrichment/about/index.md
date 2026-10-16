---
title: データレイヤーエンリッチメントについて
description: データレイヤーエンリッチメントは、AudienceStreamの属性をTealium iQデータレイヤーにインポートし、公開APIを通じて訪問プロファイルデータにアクセスすることを可能にします。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/about/
---
データレイヤーエンリッチメントには二つのコンポーネントがあります：

* Tealium iQの構成は、AudienceStreamの[属性]()をデータレイヤーにインポートし、ウェブサイト上でそれらを利用可能にし、ロードルール、エクステンション、タグを使用して訪問にパーソナライズされた体験を提供します。
* サーバーサイドコンポーネントは、データレイヤーエンリッチメントAPIおよびプロファイル定義APIを通じて訪問プロファイルデータへのアクセスを提供します。

## 要件

データレイヤーエンリッチメントには以下が必要です：

* アクティブな**AudienceStream**プロファイルで、訪問と訪問の属性が定義されていること。
* アクティブな**Tealium Collectタグ**。
* `utag.js` バージョン4.27以降。`utag.js`テンプレートの更新についての詳細は、当社のナレッジベース記事[utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)をご覧ください。

## 動作方法

### Tealium iQでのデータレイヤーエンリッチメントプロファイル

Tealium iQの構成は、iQプロファイルを対応するAudienceStreamプロファイルにリンクします。Tealium iQでデータレイヤーエンリッチメントプロファイルを構成すると、新しいタイプのデータレイヤー変数であるAudienceStream属性がデータレイヤースクリーンの変数リストに表示されます。AudienceStreamプロファイルからの訪問と訪問の属性がインポートされ、他のデータレイヤー変数と同様に使用できるようになります。

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-audiencestreamattributes.png)

これらの属性は、[Tealium Collect Tag](https://docs.tealium.com/tealium-collect-tag/)を使用してリアルタイムの顧客データでユニバーサルデータオブジェクト（UDO）に入力されます。

訪問がサイトに初めて訪れた際、Tealium CollectタグはAudienceStreamに最新の訪問プロファイル属性を取得するための呼び出しを送信します。データは将来の使用のためにブラウザのローカル保存に配置されます。

二回目のトラッキングコールでは、AudienceStreamの属性がUDOにあり、それらを構成したロードルール、エクステンション、またはタグに影響を与えます。


<blockquote>
タグは非同期にロードされるため、最新に取得された属性セットは、現在のページのイベントではなく、後続のトラッキングコールで使用可能です。
</blockquote>


#### 同一生成元ポリシー

訪問データはセキュリティ目的で[同一生成元ポリシー](https://en.wikipedia.org/wiki/Same-origin_policy)に従って`localStorage`を使用してブラウザに保存されることが重要です。これは、データレイヤーエンリッチメントが`http`プロトコルやサブドメイン間で持続しないことを意味します。

例えば、`www.tealium.com`のページから`secure.tealium.com`のページに移動する場合、`localStorage`に保存されたデータレイヤーエンリッチメントデータは新しいサブドメインに持続しません。そのため、ユーザーがサブドメインやプロトコルを変更すると、`localStorage`を再度入力するために新しいデータレイヤーエンリッチメントコールが必要になり、データは後続のトラッキングコールまで利用可能ではない場合があります。

### サーバーサイドのデータレイヤーエンリッチメント

サーバーサイドコンポーネントは、二つの公開エンドポイントを通じて訪問プロファイルデータを公開します：

* データレイヤーエンリッチメントAPIは、フィルタリングなしで完全な訪問プロファイルを返します。
* プロファイル定義APIは、バッジとオーディエンスの定義を返します。

サーバーサイドコンポーネントが無効の場合、両方のAPIは`404`レスポンスを返し、それらのエンドポイントを通じて訪問データは利用できません。

また、TAPIDクッキーを使用して訪問プロファイルにアクセスできるドメインを制限するためにドメイン許可リストを作成することもできます。詳細については、[ドメイン許可リスト](https://docs.tealium.com/enable-data-layer-enrichment/#domain-allow-list)を参照してください。

## 次のステップ

* [サーバーサイドデータレイヤーエンリッチメントを有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)
* [Tealium iQでデータレイヤーエンリッチメントを構成する](https://docs.tealium.com/configure-data-layer-enrichment-iq/)