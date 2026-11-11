---
title: Amazon Advertisingタグ構成ガイド
description: この記事では、タグ管理アカウントでAmazon Advertisingタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amazon-advertising-tag/
---
Amazon Advertisingシステムは、Amazonネットワーク上に広告を配信するオンライン広告サービスです。トラフィックの増加と売上の向上に使用されます。

## タグに関するヒント

* タグとコネクタの両方を使用するハイブリッド構成をお勧めします。この構成により、データの耐障害性を最大限に高め、サーバーサイドのシグナルとのイベントマッチングを改善し、リアルタイムのクライアントサイドシグナルを保持しながらデータフローの継続性を維持できます。詳細については、[Amazon Ads Conversionsコネクタ](https://docs.tealium.com/amazon-ads-conversions-connector/)を参照してください。
* マッピングを使用して、タグ構成を上書きするか、動的に構成します。
* Amazon AdsイベントIDを重複排除用のサーバーサイド属性として使用できるようにするには、**イベントIDを生成**を`true`に構成し、最新バージョンのTealium Collectタグを使用します。
* イベントIDの属性名は、`amazon_event_id_<EventName>_<TagUID>`形式です（例：`amazon_event_id_PageView_512`）。

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **リージョン**：  
Amazon Advertisingアカウントのリージョンを入力します（例：`NA`、`EU`、`FE`）。
* **タグID**：  
Amazon AdvertisingタグIDをカンマ区切りのリストとして入力します。
* **ページビューの自動トラッキング**：  
ページビューの自動トラッキングが`true`に構成され、イベントが`view`の場合、Amazonイベントは`Pageview`に構成されます。
* **購入の自動トラッキング**：  
購入の自動トラッキングが`true`に構成され、`order_id`が定義されている場合、Amazonイベントは`Purchase`に構成されます。
* **イベントIDを生成**：  
イベントIDの生成が`true`に構成されている場合、Amazon Adsの各トラッキングイベントに対して、`amazon_event_id_<EventName>_<TagUID>`形式のイベントIDが自動的に生成されます。例：`amazon_event_id_PageView_512`。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## イベントマッピング

Amazon Advertisingイベントは、イベントにマッピングする変数を選択してトリガーを入力することにより、データマッピングを通じて構成します。次のユースケースに示すように、変数が特定の値と等しい場合に、トリガーによってイベントが開始されます。

### ユースケース：カート追加イベント

カート追加イベントを構成するには、次の手順を実行します。

1. 変数ドロップダウンリストから`tealium_event`を選択し、**宛先を選択**をクリックします。
1. **カテゴリ**セクションで、**イベント**を選択します。
1. **マッピングされた変数が次と等しい場合**フィールドを`cart_add`に構成します。`tealium_event`が`cart_add`と等しい場合、カート追加がトリガーされます。
1. **イベントをトリガー**ドロップダウンリストで、`tealium_event`が`cart_add`と等しい場合にトリガーされるイベントである`AddToCart`を選択します。
 
カート追加イベントとともに追加データを送信する必要がある場合は、カスタムパラメータを使用して追加のイベントデータをマッピングします。

次の例では、カート追加イベントとともに商品IDを`productid`として渡します。

1. 変数ドロップダウンリストから`product_id`を選択し、**宛先を選択**をクリックします。
1. **カテゴリ**セクションで、**イベント固有のパラメータ**を選択します。
1. **宛先**フィールドを、カスタムパラメータの名前である`productid`に構成します。
1. **対象イベント**ドロップダウンリストで、カスタムパラメータを収集するイベント`AddToCart`を選択します。

ブラウザーが提供する開発者ツールを使用して、マッピングをテストします。

1. **ネットワーク**パネルを使用し、`Amazon`でフィルタリングして、キーワードとしてamazonを含むすべてのネットワークリクエストを表示します。
1. リクエスト名を確認し、`AddToCart`イベントが成功したことを確認します。
1. リクエストを開いて**ペイロード**を選択し、**クエリ文字列パラメータ**を表示して、構成したデータマッピング（`AddToCart`および`productid`）の値を確認します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### タグ構成

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `region`  | 文字列 | <ul><li>Amazon Advertisingアカウントのリージョン。</li></ul> |
| `ids`  | 文字列 | <ul><li>Amazon AdvertisingアカウントID。複数のアカウントIDを指定する場合は、カンマ区切りの文字列を入力します。</li></ul> |
| `auto_page_tracking`  | ブール値 | <ul><li>PageViewの自動トラッキングを有効または無効にする切り替え。</li><li>ページの読み込み時にPageViewイベントを自動的にトリガーするかどうかを切り替えます。</li><li>タグ構成での選択を上書きします。</li></ul> |
|`auto_purchase_tracking`  | ブール値 | <ul><li>Purchaseの自動トラッキングを有効または無効にする切り替え。</li><li>`order_id`が存在する場合にPurchaseイベントを自動的にトリガーするかどうかを切り替えます。</li><li>タグ構成での選択を上書きします。</li></ul>  |
| `generate_event_id`  | ブール値 | <ul><li>Amazon Adsの各トラッキングイベントに対してイベントIDを自動的に生成します。</li><li>イベントIDの属性名は、`amazon_event_id_<Event Name>_<Tag UID>`形式です。例：`amazon_event_id_PageView_512`。</li></ul> |
| `event_id`  | 文字列 | <ul><li>生成されたイベントID。</li></ul>  |
| `match_id`  | 文字列 | <ul><li>クロスチャネルのコンバージョン測定に使用する、プライバシーに配慮した広告主定義の識別子。</li><li>ロイヤルティID、CRM ID、内部ユーザーIDなど、安定した一意の識別子を使用してください。氏名、メールアドレス、電話番号などの個人識別情報（PII）は使用しないでください。</li><li>タグは値を変更せずに渡します。</li><li>`match_id`をハッシュ化する場合は、Amazon AdvertisingタグとAmazon Ads Conversionsコネクタで同じハッシュ化方式を使用してください。</li></ul> |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------| :------------|
| `order_id`（`_corder`を上書き）  | 文字列 | <ul><li>確定した注文に割り当てられる一意の識別子。</li><li>`_corder`を上書きします。</li></ul>|

### 拡張コンバージョン

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `email_raw`  | 文字列 | プレーンテキストのメールアドレスを指定します。タグは、この値の前後の空白を削除し、小文字に変換します。 |
| `phonenumber`  | 文字列 | プレーンテキストの電話番号を指定します。タグは、この値の空白と記号を削除します。 |
| `email`  | 文字列 | ユーザーのメールアドレスをSHA256でハッシュ化した値。 |
| `gdpr.enabled`  | ブール値 | アカウントでGDPR制限が有効になっているかどうか。<ul><li>`1` - GDPR制限が有効です。</li><li>`0` - GDPR制限は有効ではありません。</li></ul> |
| `gdpr.consent`  | 文字列 | 有効な[IABバージョン1または2の同意文字列](https://iabtechlab.com/standards/gdpr-transparency-and-consent-framework/)。 |

### イベント

イベントのマッピングの詳細については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-a-variable-mapping)を参照してください。

| 変数        | 説明  |
|:----------------|:-------------|
|  `AddToCart`    | AddToCart    |
|  `Application`  | Application  |
|  `Checkout`     | Checkout     |
|  `Contact`      | Contact      |
|  `Lead`         | Lead         |
|  `Purchase`     | Purchase     |
|  `PageView`     | PageView     |
|  `Search`       | Search       |
|  `SignUp`       | SignUp       |
|  `Subscription` | Subscription |
|  `Custom`       | Custom       |

### イベント固有のパラメータ

イベントのマッピングの詳細については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-a-variable-mapping)を参照してください。

特定のイベントに対してのみパラメータをマッピングするには、構成するパラメータの名前を入力し、そのパラメータに構成するイベントの名前を選択します。

イベント固有のマッピングを行うカスタムイベントを指定するには、**イベント**ドロップダウンリストから**カスタムオプション**を選択し、表示されるフィールドにカスタムイベントの名前を入力します。