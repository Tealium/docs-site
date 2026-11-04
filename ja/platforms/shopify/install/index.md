---
title: ShopifyにTealiumアプリをインストールする
description: この記事では、Tealium Shopifyアプリのインストールについて説明します。
url: https://docs.tealium.com/ja/platforms/shopify/install/
---
Tealium Shopifyアプリをインストールして構成する前に、Tealiumで以下を構成します。

* Tealium HTTP APIデータソース
* イベント仕様
* データレイヤーの`restock`変数

これらの構成作業については、[Tealiumの構成]()を参照してください。

## インストール

以下のセクションでは、ShopifyへのTealiumアプリのインストール、Shopifyテーマの有効化、Checkout Pixelの構成方法について説明します。

### Tealiumアプリをインストールする

1. Shopifyの**Apps**で、**Tealium**アプリを選択します。
1. **Config**タブで、**Account**、**Profile**、**Environment**の情報を入力します。  
    Environmentの値は`prod`、`dev`、または`qa`です。
1. **Checkout Tracking**オプションを選択します。  
    * **Client Side Only**：Tag Managementのみを使用している場合は、このオプションを選択します。
    * **Client and Server Side**：Shopify Webhooksを使用してEvent Streamingにデータを送信する場合は、このオプションを選択します。
1. **Client and Server Side**を選択した場合は、以下を実行します。  
    1. Tealiumで、**Server-Side > Data Sources**に移動し、Shopify用に作成したデータソースを選択します。  
    1. 選択したデータソースの**Data Source Key**をコピーします。  
    1. Shopifyで、データソースキーを**Server Side Data Source ID**フィールドに貼り付けます。
1. 構成が完了したら、**Submit**をクリックします。Webhookは直ちに作成されます。

### Shopifyテーマを有効にする

以下の手順でShopifyテーマを有効にします。

1. Shopifyで、**Online Store > Themes > Customize**に移動します。
1. **App Embeds**をクリックし、Tealium拡張機能を有効にします。  
これにより、Tealiumライブラリ`utag.js`とShopifyイベント用の標準データレイヤーが読み込まれます。
1. **Tealium Settings**を`On`に構成します。
1. **Save**をクリックします。

### Checkout Pixelを構成する

Tealiumアプリは、カスタムCheckout Pixelを使用して、チェックアウトイベントデータをEvent Streamingに送信します。Event Streamingを有効にしていない場合、Checkout Pixelを構成する必要はありません。

以下の手順でCheckout Pixelを構成します。

1. **Shopify Admin**で、**Settings > Customer Events**に移動します。  
TealiumアプリによってインストールされたTealiumピクセルが表示されます。Checkout Pixelは手動で追加する必要があります。
1. **Add Custom Pixel**をクリックし、**Pixel Name**に`Tealium Checkout`と入力します。
1. **Customer Privacy**では、以下のオプションを推奨します。
    * **Permission**：**Analytics**を選択します。
    * **Data sale**：**Data collected does not qualify as data sale**を選択します。  
    Tealiumでストアが収集しているデータによっては、この構成を変更する必要があります。
1. **Code**ボックスに表示されているサンプルコードを削除します。
1. **Customer Events**タブからコピーしたコードを**Code**ボックスに貼り付けます。  
1. **Save**をクリックします。
1. **Connect**をクリックします。

## プライバシーと同意

Tealiumアプリは、[Shopify Customer Privacy API](https://shopify.dev/docs/api/customer-privacy)を利用する同意連携用のカスタムテンプレートを使用します。このセクションでは、Shopifyで推奨される同意管理とプライバシーの構成方法について説明します。

詳細については、[同意連携について]()を参照してください。

Tealium Shopifyアプリでは、Shopifyに組み込まれているCookieバナーとShopify Privacyプラットフォームを使用できます。サードパーティのバナーやその他の同意管理プラットフォームを構成するには、クライアントサイドの同意連携を使用します。

### クライアントサイドの同意連携を構成する

クライアントサイドの同意連携の構成は、以下の作業で構成されます。

* 目的グループと目的を作成する
* タグを目的にマッピングする
* Shopify用の同意連携を追加する

#### 目的グループと目的を作成する

Shopify用の同意連携を追加するには、目的グループと1つ以上の目的を作成します。作成する各目的には、名前とキーが必要です。名前は、Shopifyの同意カテゴリのいずれかに対応している必要があります。以下の表に、Shopifyの同意目的に使用するキーと名前を示します。

| キー | 名前 |
|----|----|
| `analytics` | `analytics` |
| `marketing` | `marketing` |
| `preferences` | `personalization/preferences` |
| `sale_of_data` | `sale_of_data` |

タグを各目的にマッピングする前に、適切なTag Managementの目的を割り当てます。各タグで、**Map**ドロップダウンメニューを選択し、そのタグに最も適した目的を割り当てます。

目的グループと目的の作成について詳しくは、[目的グループを追加する](https://docs.tealium.com/manage-consent-integrations/#add-a-purpose-group)を参照してください。

#### カスタム同意連携を追加する

Shopify用のカスタム連携を構成する際は、以下の構成を使用します。

| オプション | 値 |
|----|----|
| 名前 | `Shopify` |
| ベンダー | `Custom` |
| ベンダーID | `_tracking_consent` |
| 適用ルール | デフォルトを使用 |
| パブリッシュ先 | <ul><li>テストには`Dev`</li><li>テスト完了後は`Prod`</li></ul> |
| 目的グループ | Shopify用に作成した目的グループ。 |

カスタム同意連携の追加について詳しくは、[連携を追加する](https://docs.tealium.com/manage-consent-integrations/#add-an-integration)を参照してください。

## インストールを検証する

Shopify Custom PixelsはiFrameサンドボックス内で実行されるため、Tealium Universal Tag Debuggerを含むほとんどのタグ監視プラグインと互換性がありません。このセクションでは、デバッグモードを手動で実装する方法について説明します。

このデバッグモードを有効にするには、以下の手順を実行します。

1. テストするページに`tealium_debug`という名前のCookieを追加します。
1. Cookieの値を`dev`に構成します。  
これにより`utagdb=true`が自動的に構成され、詳細な出力が有効になり、Tealiumの`dev`環境バージョンが読み込まれます。
1. 追加の出力を確認するには、ブラウザコンソールを開きます。

デバッグモードはクライアントサイドにのみ適用されます。サーバーサイドのデータ収集の検証には使用できません。

WebhookおよびEvent Streamingに送信されたイベントは、Event StreamingのLive Eventsページを使用してデバッグできます。イベントを確認するには、テスト対象のページを再読み込みする必要があります。この方法は、チェックアウトを含むサイト全体で使用できます。詳細については、[Live Eventsについて]()を参照してください。

1. **Shopify Admin**で、**Online Store > Themes > Customize > App embeds**に移動します。
1. Tealium拡張機能の構成でデバッグを有効にし、**Save**をクリックします。
1. Webサイトを再読み込みし、ブラウザコンソールで詳細なデバッグ情報を確認します。

## サーバーイベントの管理

**Server Events**タブでは、サーバーサイドトラッキング用に登録するShopify Webhookを選択できます。トラッキング要件に応じて、個々のWebhookを有効または無効にします。

| Tealiumイベント | Shopify Webhook | 
|----------------|-----------------|
| cart_update | CARTS_UPDATE |
| cart_create | CARTS_CREATE |
| checkouts_create | CHECKOUTS_CREATE |
| purchase | ORDERS_CREATE |
| shopify_refund | REFUNDS_CREATE |
| Shopify New Customer | CUSTOMERS_CREATE |
| sms_consent_change | CUSTOMERS_MARKETING_CONSENT_CREATE |
| email_consent_change | CUSTOMERS_EMAIL_MARKETING_CONSENT_CREATE |

選択したWebhookはShopifyに自動的に登録され、Event Streamingにデータを送信するよう構成されます。

## Cookie分割モード

Cookie分割モードでは、単一の統合された`utag_main` Cookieの代わりに個別のCookieを書き込むことで、Cookieに関する透明性を高めます。`utag.js`バージョン4.50以降が検出された場合、Cookie分割構成を使用できます。

統合されたCookieを個別のCookieに分割するには、以下の手順を実行します。

1. **Detect utag.js Version**をクリックして、`utag.js`のバージョンを確認します。
1. **Enable split cookie mode**チェックボックスを選択します。
1. `utag_main` Cookieに保持するCookie値を選択します。選択しなかった値は、`utag_main_`プレフィックスが付いた個別のCookieとして書き込まれます。  
`ses_id`、`_st`、`_ss` Cookieは必須です。訪問数やセッション数の過大計上を防ぐため、赤いバッジが付いています。
1. **Save Cookie settings**をクリックします。
## Tealium Shopifyアプリをアンインストールする

ShopifyからTealiumアプリを削除するには、次の手順を実行します。

1. Shopifyで、**構成 > カスタムデータ**に移動します。
1. リストの下部付近にある**Tealium**をクリックします。  
Tealiumのメタデータフィールドが一覧表示されます。
1. フィールドのリストを下にスクロールし、**削除**をクリックします。